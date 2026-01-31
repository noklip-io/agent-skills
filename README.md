# Agent Skills

A collection of AI agent skills for Claude Code, Cursor, GitHub Copilot, and other AI coding assistants.

## Installation

### Install all skills

```bash
npx skills add noklip-io/agent-skills
```

### Install a specific skill

```bash
npx skills add noklip-io/agent-skills --skill three-js
```

## Available Skills

| Skill | Description |
|-------|-------------|
| [react-19](./skills/react-19) | React 19 patterns and breaking changes vs React 18 |
| [three-js](./skills/three-js) | Comprehensive Three.js reference for 3D web graphics |
| [nuqs](./skills/nuqs) | Type-safe URL query state management for React |
| [theatre-js](./skills/theatre-js) | Motion design editor and animation library for the web |
| [gsap](./skills/gsap) | Professional-grade JavaScript animation library |
| [payload](./skills/payload) | Payload CMS development (standalone version) |
| [shadcn-base](./skills/shadcn-base) | shadcn/ui Base UI edition: components, CLI, theming, and composition |

## Skill: react-19

Comprehensive React 19 skill covering 19.0 through 19.2+ with 10 reference documents:

- **New Hooks**: useActionState, useOptimistic, use(), useFormStatus, useEffectEvent (19.2)
- **New Components**: `<Activity>` for hide/show with state preservation (19.2)
- **Paradigm Shifts**: Server-first thinking, compiler-first optimization, declarative mutations
- **Anti-Patterns**: What to stop doing in React 19
- **Deprecations**: forwardRef, Context.Provider, removed APIs with migration guides
- **React Compiler**: Automatic memoization details and when manual is still useful
- **Server Components**: RSC, Server Actions, directives, streaming
- **TypeScript**: Type changes, codemods, new patterns
- **Migration**: Covers React 16/17/18 to 19 upgrade paths

```bash
npx skills add noklip-io/agent-skills --skill react-19
```

## Skill: nuqs

Best practices for nuqs - type-safe search params state management:

- Setup with adapters (Next.js, React, Remix, React Router)
- `useQueryState` and `useQueryStates` hooks
- Built-in parsers and custom parsers
- Server Components with `createSearchParamsCache`
- Testing with `withNuqsTestingAdapter`
- Common patterns and critical mistakes to avoid

```bash
npx skills add noklip-io/agent-skills --skill nuqs
```

## Skill: three-js

Complete Three.js reference with 18 documentation files covering:

- **Core**: Scene, Renderer, Object3D, cameras, math utilities
- **Visuals**: Materials, textures, lighting, shaders
- **Motion**: Animation, interaction, controls
- **Assets**: Loaders (GLTF, FBX, SVG, fonts, scientific formats)
- **Effects**: Post-processing, bloom, DOF, SSAO
- **Advanced**: WebGPU, TSL/node materials, physics, VR/XR

```bash
npx skills add noklip-io/agent-skills --skill three-js
```

## Skill: theatre-js

Motion design editor and animation library with visual timeline editor:

- **Core**: Project, Sheet, Object, Sequence architecture
- **Prop Types**: Number, compound, rgba, image, custom types
- **Studio**: Visual timeline editor, keyframe editing, export
- **React**: useVal, usePrism, Atom, Theatric
- **R3F**: editable components, SheetProvider, 3D animation
- **Production**: State export, assets, tree-shaking

```bash
npx skills add noklip-io/agent-skills --skill theatre-js
```

## Skill: gsap

Professional-grade JavaScript animation library with extensive plugin ecosystem:

- **Core**: gsap.to, from, fromTo, timelines, easing, callbacks
- **ScrollTrigger**: Scroll-based animations, pin, scrub, snap
- **ScrollSmoother**: Smooth scrolling, parallax effects
- **SplitText**: Text splitting and character animation
- **SVG**: DrawSVG, MorphSVG, MotionPath plugins
- **Flip**: Layout animations (FLIP technique)
- **React**: useGSAP hook, cleanup patterns
- **Utilities**: toArray, clamp, mapRange, interpolate

```bash
npx skills add noklip-io/agent-skills --skill gsap
```

## Skill: payload

Standalone Payload CMS skill for AI coding agents:

- **Collections**: Fields, hooks, access control, versioning, drafts
- **Fields**: All field types, validation, conditional fields, virtual fields
- **Queries**: Local API, REST, GraphQL, filtering, relationships
- **Hooks**: beforeChange, afterChange, beforeDelete, context management
- **Access Control**: Field-level, row-level security, complex queries
- **Plugins**: Plugin architecture, package structure, extending collections
- **Adapters**: Database adapters, storage adapters, transactions

> **Note:** Claude Code users should prefer the official [Payload Marketplace plugin](https://github.com/payloadcms/payload) which includes MCP tools. This standalone version is for other AI agents (Cursor, OpenCode, Copilot) or users who prefer not to install the full plugin.

```bash
npx skills add noklip-io/agent-skills --skill payload
```

## Skill: shadcn-base

Base UI edition of shadcn/ui with Base UI-only composition rules:

- **Docs map**: Base UI component index with conversion rule for `/components/base/*`
- **Composition**: render/useRender only; no Radix `asChild`
- **Setup**: CLI, installation, components.json, registries
- **Design**: theming, dark mode, CVA-based variants
- **Forms**: field patterns + form library integrations
- **Examples**: complex components and edge cases
- **Ops**: MCP guidance, changelog checks, issue links

```bash
npx skills add noklip-io/agent-skills --skill shadcn-base
```

## Contributing

To add a new skill:

1. Create a folder in `skills/` with your skill name (kebab-case)
2. Add a `SKILL.md` with YAML frontmatter (name, description) and instructions
3. Optionally add `references/` for detailed documentation
4. Submit a pull request

## License

MIT License - See [LICENSE](LICENSE) for details.
