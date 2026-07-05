# ZCode Integration — OpenClaw Skill

Connect OpenClaw to [ZCode](https://dev.zcode.app) for bidirectional task execution, prompts, and MCP tool integration.

## Features

- Execute ZCode prompts from OpenClaw CLI
- List ZCode skills, plugins, and commands
- MCP server integration (app-server subcommand)
- Check ZCode process health
- Diagnose ZCode runtime via doctor command

## Prerequisites

- [ZCode](https://dev.zcode.app) v3.x installed and running
- Node.js (ZCode CLI is a Node.js bundle)

## Installation

### Via OpenClaw ClawHub (recommended)

```bash
# Coming soon
```

### Manual

1. Copy `SKILL.md` to `~/.openclaw/workspace/skills/zcode-integration/`
2. Restart OpenClaw Gateway or reload skills

## Usage

```bash
# Check version
node /path/to/zcode.cjs --version

# List skills
node /path/to/zcode.cjs skills list

# List plugins
node /path/to/zcode.cjs plugins list

# Run a prompt
node /path/to/zcode.cjs --prompt "your instruction" --mode yolo
```

On macOS, create a quick alias:

```bash
ln -s /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs /usr/local/bin/zcode-oc
zcode-oc --version
```

## Platform Notes

- **macOS**: ZCode typically installed at `/Applications/ZCode.app`
- **Linux/Windows**: Adjust the CLI entry path in SKILL.md

## License

MIT
