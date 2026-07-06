# ZCode Integration — OpenClaw Skill

Bridge OpenClaw to [ZCode](https://dev.zcode.app) (macOS local AI coding agent).  
OpenClaw delegates tasks to ZCode via CLI — ZCode generates code/scripts, returns results.

## What it does

- OpenClaw calls `zcode.cjs --prompt "..."` with your request
- ZCode's AI (configured with bighub.cn/deepseek-v4-flash) generates the answer
- Output comes back to OpenClaw as text/code

## Quick start

1. Install [ZCode](https://dev.zcode.app) on macOS
2. Install this skill for OpenClaw (see [Installation](#installation))
3. Tell OpenClaw: "用 zcode 写个 XXX"

## Installation

### Manual

```bash
git clone https://github.com/3582374711-oss/zcode-integration.git
mkdir -p ~/.openclaw/workspace/skills/zcode-integration
cp zcode-integration/SKILL.md ~/.openclaw/workspace/skills/zcode-integration/
```

Restart OpenClaw Gateway and the skill is active.

## Platform

- **macOS only** — ZCode.app is macOS-native
- CLI path: `/Applications/ZCode.app/Contents/Resources/glm/zcode.cjs`

## Learn more

Read [SKILL.md](./SKILL.md) for full command reference and safety notes.

## License

MIT
