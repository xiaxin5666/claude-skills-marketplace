# Claude Code Skills Marketplace

A community-driven marketplace for [Claude Code](https://claude.ai/code) skills. Browse, install, and share reusable skills that extend Claude Code's capabilities.

## What is a Skill?

A skill is a reusable prompt packaged as a `SKILL.md` file that teaches Claude how to perform specialized tasks — from disk cleanup to PDF generation to API integrations. Skills can be invoked via `/skill-name` slash commands or triggered automatically by Claude when relevant.

## Quick Install

### Install a single skill

```bash
# Clone the marketplace
git clone https://github.com/xiaxin5666/claude-skills-marketplace.git
cd claude-skills-marketplace

# Copy the skill to your Claude Code skills directory
cp -r skills/disk-cleanup ~/.claude/skills/
```

### Or download just one skill directly

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/disk-cleanup

# Download the SKILL.md
curl -o ~/.claude/skills/disk-cleanup/SKILL.md \
  https://raw.githubusercontent.com/xiaxin5666/claude-skills-marketplace/main/skills/disk-cleanup/SKILL.md
```

### Install all marketplace skills

```bash
git clone https://github.com/xiaxin5666/claude-skills-marketplace.git
cp -r claude-skills-marketplace/skills/* ~/.claude/skills/
```

## Available Skills

| Skill | Description | Platforms |
|-------|-------------|-----------|
| [`disk-cleanup`](./skills/disk-cleanup/SKILL.md) | Analyze disk usage and clean up caches, temp files, app bloat, SDK leftovers, old restore points. Tiered safety levels. | Windows, macOS, Linux |

## Skill Format

Every skill lives in its own directory under `skills/` and contains a `SKILL.md` file:

```
skills/
└── my-skill/
    └── SKILL.md    # YAML frontmatter + Markdown instructions
```

The `SKILL.md` uses YAML frontmatter:

```yaml
---
name: my-skill
description: "What this skill does and when Claude should use it"
user-invocable: true
argument-hint: "[optional arguments]"
---
```

See [`skills/disk-cleanup/SKILL.md`](./skills/disk-cleanup/SKILL.md) for a full example.

## Contributing

Have a great skill? Share it with the community!

1. Fork this repository
2. Create your skill directory: `skills/<your-skill-name>/SKILL.md`
3. Follow the [skill format](#skill-format) above
4. Add your skill to the [registry](./registry.json) and this README
5. Submit a Pull Request

### Skill Guidelines

- **One skill per directory** — keep skills self-contained
- **Descriptive name** — use kebab-case, make it searchable
- **Clear description** — helps Claude decide when to auto-invoke
- **Cross-platform** when possible — document platform support
- **Safety levels** for destructive operations — let users control risk

## Registry

See [`registry.json`](./registry.json) for the machine-readable skill index.

---

🤖 Built for the [Claude Code](https://claude.ai/code) community.
