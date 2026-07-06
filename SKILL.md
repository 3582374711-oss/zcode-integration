---
name: "zcode-integration"
description: "Run ZCode CLI commands from OpenClaw. Use --prompt to delegate tasks to ZCode, or list/doctor for diagnostics. ZCode CLI is already configured with bighub.cn/deepseek-v4-flash."
---

# ZCode Integration

Use this skill when OpenClaw needs to interact with ZCode via its CLI.

ZCode is a local AI coding agent (macOS app at `/Applications/ZCode.app`).  
This skill bridges OpenClaw to ZCode — OpenClaw calls the ZCode CLI, passes a prompt, and gets the generated output back.

## How to install this skill for OpenClaw

### Manual install

```bash
git clone https://github.com/3582374711-oss/zcode-integration.git
mkdir -p ~/.openclaw/workspace/skills/zcode-integration
cp zcode-integration/SKILL.md ~/.openclaw/workspace/skills/zcode-integration/
```

OpenClaw picks it up automatically — no config needed.

### Via ClawHub (once published)

```bash
openclaw skills install zcode-integration
```

## How this skill works

When someone says "用 zcode 写 XX" or "走 zcode", OpenClaw will:

1. Run `node /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs doctor` to verify ZCode is available
2. Use `--prompt` to pass the user's request to ZCode's AI
3. Capture the output and return it to the user

## Prerequisites

- **macOS only** — ZCode.app is a macOS application
- ZCode.app must be installed at `/Applications/ZCode.app`
- Node.js is included with ZCode.app

## CLI Commands reference

All commands run as:

```bash
node /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs <subcommand> [options]
```

### Read-only commands (safe to run anytime)

| Command | Description |
|---|---|
| `doctor` | Inspect ZCode runtime and packaging |
| `--version` | Print CLI version |
| `skills list` | List installed ZCode skills |
| `plugins list` | List installed plugins |
| `commands` | List custom slash commands |

### Action commands (may need confirmation)

| Command | Description |
|---|---|
| `--prompt <text>` | Run a single prompt through ZCode's AI |
| `--mode yolo` | Full permission mode for prompts |
| `--json` | Get JSON output (always use with `--prompt`) |
| `login` | Sign in with Z.AI OAuth |
| `logout` | Remove Z.AI login credentials |

## Typical workflow

### Check ZCode is running
```bash
node /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs doctor
```

### Write something with ZCode
```bash
node /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs --prompt "Write an RPG Maker MV/MZ plugin script that..." --mode yolo --json
```

The response comes back in JSON with a `response` field containing the generated output.

## Platform notes

- **macOS**: ZCode.app at `/Applications/ZCode.app` — works out of the box
- **Linux/Windows**: ZCode is not available; this skill won't work. Adjust the CLI path if ZCode is installed elsewhere.

## Safety

- `~/.zcode/` may contain API keys — do not expose in responses.
- `--mode yolo` grants full permissions — use only for trusted prompts.
- ZCode CLI config: `~/.zcode/cli/config.json`
- ZCode v2 config: `~/.zcode/v2/config.json` — contains Z.AI credentials, keep private.
