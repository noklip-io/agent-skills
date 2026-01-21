---
name: nuqs
description: Use when implementing URL query state in React, managing search params, syncing state with URL, building filterable/sortable lists, pagination with URL state, or using nuqs/useQueryState/useQueryStates hooks in Next.js, Remix, React Router, or plain React.
---

# nuqs Best Practices

Type-safe URL query state management for React. Like `useState`, but stored in the URL.

## Setup (Required First)

Wrap your app with the appropriate adapter:

```tsx
// Next.js App Router - app/layout.tsx
import { NuqsAdapter } from 'nuqs/adapters/next/app'

export default function RootLayout({ children }) {
  return <NuqsAdapter>{children}</NuqsAdapter>
}

// Next.js Pages Router - pages/_app.tsx
import { NuqsAdapter } from 'nuqs/adapters/next/pages'

// React SPA (Vite/CRA)
import { NuqsAdapter } from 'nuqs/adapters/react'

// Remix - app/root.tsx
import { NuqsAdapter } from 'nuqs/adapters/remix'

// React Router v6/v7
import { NuqsAdapter } from 'nuqs/adapters/react-router'
```

## Core API

### Single Parameter

```tsx
'use client'
import { useQueryState, parseAsInteger } from 'nuqs'

// String (default)
const [search, setSearch] = useQueryState('q')  // null | string

// With parser + default (recommended)
const [page, setPage] = useQueryState('page', parseAsInteger.withDefault(1))

// Update
setSearch('hello')      // ?q=hello
setSearch(null)         // removes param
setPage(p => p + 1)     // functional update
```

### Multiple Parameters

```tsx
import { useQueryStates, parseAsInteger, parseAsString } from 'nuqs'

const [filters, setFilters] = useQueryStates({
  q: parseAsString.withDefault(''),
  page: parseAsInteger.withDefault(1),
  sort: parseAsString.withDefault('date')
})

// Update multiple at once
setFilters({ page: 1, sort: 'name' })  // partial updates allowed
```

## Built-in Parsers

| Parser | Type | Example |
|--------|------|---------|
| `parseAsString` | `string` | `?q=hello` |
| `parseAsInteger` | `number` | `?page=1` |
| `parseAsFloat` | `number` | `?price=9.99` |
| `parseAsBoolean` | `boolean` | `?active=true` |
| `parseAsIsoDateTime` | `Date` | `?date=2024-01-15` |
| `parseAsArrayOf(parser)` | `T[]` | `?tags=a,b,c` |
| `parseAsJson<T>()` | `T` | `?data={...}` |
| `parseAsStringEnum(values)` | `enum` | `?status=active` |

**Always use `.withDefault()` to avoid null handling:**

```tsx
// ❌ Returns null when param missing
const [page] = useQueryState('page', parseAsInteger)

// ✅ Returns 1 when param missing
const [page] = useQueryState('page', parseAsInteger.withDefault(1))
```

## Options

```tsx
useQueryState('key', parseAsString.withOptions({
  history: 'push',      // 'push' | 'replace' (default: replace)
  shallow: false,       // true (default) = client only, false = notify server
  scroll: false,        // scroll to top on change
  throttleMs: 500,      // throttle URL updates
  clearOnDefault: true, // remove param when value equals default (default: true)
}))
```

## Server Components (Next.js)

```tsx
// searchParams.ts
import { createSearchParamsCache, parseAsInteger, parseAsString } from 'nuqs/server'

export const searchParamsCache = createSearchParamsCache({
  q: parseAsString.withDefault(''),
  page: parseAsInteger.withDefault(1)
})

// page.tsx (Server Component)
import { searchParamsCache } from './searchParams'
import type { SearchParams } from 'nuqs/server'

type Props = { searchParams: Promise<SearchParams> }

export default async function Page({ searchParams }: Props) {
  const { q, page } = await searchParamsCache.parse(searchParams)
  return <Results query={q} page={page} />
}

// Nested server component - access without props
function NestedComponent() {
  const page = searchParamsCache.get('page')  // type-safe!
  return <span>Page {page}</span>
}
```

## Testing

```tsx
import { withNuqsTestingAdapter } from 'nuqs/adapters/testing'
import { render, screen } from '@testing-library/react'

it('updates URL on click', async () => {
  const onUrlUpdate = vi.fn()

  render(<MyComponent />, {
    wrapper: withNuqsTestingAdapter({
      searchParams: '?count=1',
      onUrlUpdate
    })
  })

  await userEvent.click(screen.getByRole('button'))

  expect(onUrlUpdate).toHaveBeenCalledWith(
    expect.objectContaining({ queryString: '?count=2' })
  )
})
```

## Common Patterns

### Reusable Parser Definitions

```tsx
// lib/searchParams.ts
export const paginationParsers = {
  page: parseAsInteger.withDefault(1),
  limit: parseAsInteger.withDefault(20)
}

// Component
const [pagination, setPagination] = useQueryStates(paginationParsers)
```

### URL Key Mapping

```tsx
const [coords, setCoords] = useQueryStates(
  {
    latitude: parseAsFloat.withDefault(0),
    longitude: parseAsFloat.withDefault(0)
  },
  {
    urlKeys: { latitude: 'lat', longitude: 'lng' }  // ?lat=0&lng=0
  }
)
```

### Custom Parser

```tsx
const parseAsDate = {
  parse: (value: string) => new Date(value),
  serialize: (date: Date) => date.toISOString().split('T')[0]
}

const [date, setDate] = useQueryState('date', parseAsDate)
```

## Critical Mistakes to Avoid

### 1. Missing Adapter
```tsx
// ❌ Error: nuqs requires an adapter
useQueryState('q')

// ✅ Wrap app in NuqsAdapter first
```

### 2. Wrong Adapter
```tsx
// ❌ Using app router adapter in pages router
import { NuqsAdapter } from 'nuqs/adapters/next/app'  // Wrong!

// ✅ Match adapter to your router
import { NuqsAdapter } from 'nuqs/adapters/next/pages'
```

### 3. Missing Suspense (Next.js App Router)
```tsx
// ❌ Hydration error: Missing Suspense boundary
export default function Page() {
  const [q] = useQueryState('q')
  return <div>{q}</div>
}

// ✅ Wrap client components in Suspense
export default function Page() {
  return (
    <Suspense fallback={<Loading />}>
      <SearchClient />
    </Suspense>
  )
}
```

### 4. Same Key, Different Parsers
```tsx
// ❌ Conflicts - last update wins with wrong type
const [intVal] = useQueryState('foo', parseAsInteger)
const [floatVal] = useQueryState('foo', parseAsFloat)

// ✅ One parser per key, share via custom hook
function useFoo() {
  const [val, setVal] = useQueryState('foo', parseAsFloat)
  return { float: val, int: Math.floor(val ?? 0), setVal }
}
```

### 5. Forgetting to Parse on Server
```tsx
// ❌ Returns cache object, not values
const values = searchParamsCache  // Wrong!

// ✅ Call parse() with searchParams prop
const values = await searchParamsCache.parse(searchParams)
```

### 6. Server Component with Client Hook
```tsx
// ❌ useQueryState only works in client components
export default function Page() {  // Server component
  const [q] = useQueryState('q')  // Error!
}

// ✅ Use createSearchParamsCache for server, useQueryState for client
```

## Quick Reference

| Task | Solution |
|------|----------|
| Single param | `useQueryState('key', parser.withDefault(val))` |
| Multiple params | `useQueryStates({ key: parser })` |
| Server access | `createSearchParamsCache` + `.parse()` |
| Notify server | `{ shallow: false }` |
| History entry | `{ history: 'push' }` |
| Test component | `withNuqsTestingAdapter({ searchParams: '?...' })` |
