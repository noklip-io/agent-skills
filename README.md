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

## Contributing

To add a new skill:

1. Create a folder in `skills/` with your skill name (kebab-case)
2. Add a `SKILL.md` with YAML frontmatter (name, description) and instructions
3. Optionally add `references/` for detailed documentation
4. Submit a pull request

## License

MIT License - See [LICENSE](LICENSE) for details.
