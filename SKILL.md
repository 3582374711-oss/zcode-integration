---
name: "zcode-integration"
description: "Connect OpenClaw to ZCode via CLI and MCP for bidirectional task execution."
---

# ZCode Integration

Bridge between OpenClaw and ZCode for executing prompts, reading state, and running plugins.

Supports ZCode v3.x (CLI v0.15+).

## Paths

- **CLI entry**: `/Applications/ZCode.app/Contents/Resources/glm/zcode.cjs`
- **Data dir**: `~/.zcode/`
- **Config**: `~/.zcode/v2/config.json`
- **Plugins**: `~/.zcode/cli/plugins/cache/`

## How It Works

ZCode ships as a self-contained 9MB Node.js bundle with `#!/usr/bin/env node` shebang. The OpenClaw skill discovers and invokes it on macOS.

On other platforms (Linux/Windows), adjust the CLI entry path to match your ZCode installation.

## Prerequisites

1. **ZCode** must be installed and running (check via `ps aux | grep -i zcode-cli`).
2. **Node.js** (the ZCode CLI is a Node bundle).

## CLI Commands

```bash
node /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs <subcommand>
```

| Command | Description |
|---|---|
| `--help` | Show all commands |
| `--version` | Show CLI version |
| `skills list` | List installed skills |
| `plugins list` | List and enable plugins |
| `login` | Sign in with Z.AI OAuth |
| `logout` | Remove Z.AI credentials |
| `doctor` | Inspect runtime/packaging |
| `commands` | List custom slash commands |
| `--prompt <text>` | Run a single prompt |
| `--attach <path>` | Attach file(s) to `--prompt` |
| `--mode <mode>` | Permission mode: yolo\|build\|edit\|plan |
| `--target <goal>` | Run with a session goal |
| `app-server` | Start MCP stdio server |

### macOS Quick Alias

```bash
ln -s /Applications/ZCode.app/Contents/Resources/glm/zcode.cjs /usr/local/bin/zcode-oc
# Then:
zcode-oc --version
zcode-oc skills list
```

## MCP Server Integration

ZCode exposes an stdio MCP server via `app-server`:

```bash
node /path/to/zcode.cjs app-server
```

Configure in OpenClaw's `openclaw.json` as an MCP tool provider.

## URL Scheme

ZCode registers `zcode://` — open via:
```bash
open "zcode://<handler>"
```

## Safety

- `~/.zcode/v2/config.json` may contain API keys — keep private.
- `--mode yolo` grants full permissions — use only for trusted prompts.
