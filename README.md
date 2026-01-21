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
| [three-js](./skills/three-js) | Comprehensive Three.js reference for 3D web graphics |
| [nuqs](./skills/nuqs) | Type-safe URL query state management for React |
| [theatre-js](./skills/theatre-js) | Motion design editor and animation library for the web |
| [gsap](./skills/gsap) | Professional-grade JavaScript animation library |

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

## Contributing

To add a new skill:

1. Create a folder in `skills/` with your skill name (kebab-case)
2. Add a `SKILL.md` with YAML frontmatter (name, description) and instructions
3. Optionally add `references/` for detailed documentation
4. Submit a pull request

## License

MIT License - See [LICENSE](LICENSE) for details.
