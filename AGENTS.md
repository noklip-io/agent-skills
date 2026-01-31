# Agent Skills Repository

This repository contains reusable skills for AI coding agents.

## Structure

```
agent-skills/
├── skills/
│   └── <skill-name>/
│       ├── SKILL.md          # Main skill file with frontmatter
│       ├── references/       # Optional detailed documentation
│       └── scripts/          # Optional helper scripts
├── README.md
├── LICENSE
└── CLAUDE.md
```

## Creating Skills

Each skill must have a `SKILL.md` file with YAML frontmatter:

```yaml
---
name: skill-name
description: |
  Description of when this skill should be triggered.
  Include specific phrases like "create X", "implement Y".
---

# Skill Content

Instructions and documentation here.
```

## Best Practices

- Keep `SKILL.md` focused (~2000 words max)
- Move detailed docs to `references/` for progressive loading
- Use specific trigger phrases in the description
- Include working code examples
