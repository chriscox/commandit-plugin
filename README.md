# CommandIt MCP Plugin

[CommandIt](https://commandit.ai) is a native macOS command palette for developers. This plugin exposes CommandIt's MCP server to any compatible AI coding assistant, giving it direct access to your snippet library.

## Prerequisites

1. **CommandIt app** installed on macOS ([download](https://commandit.ai))
2. **CommandIt CLI** installed and on PATH (Settings > Developer Tools > Install CLI in the app)

Verify the CLI is available:

```bash
commandit version
```

## Install

### Claude Code

**Option A — Plugin (recommended)**

```bash
claude plugin add chriscox/commandit-plugin
```

**Option B — Manual registration**

```bash
claude mcp add --scope user commandit -- $(which commandit) mcp
```

### Cursor / Windsurf

Add to your config file (`~/.cursor/mcp.json` or `~/.windsurf/mcp.json`):

```json
{
  "mcpServers": {
    "commandit": {
      "command": "commandit",
      "args": ["mcp"]
    }
  }
}
```

Or use the CLI to write the config automatically:

```bash
commandit install-mcp --cursor    # or --windsurf
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "commandit": {
      "type": "stdio",
      "command": "commandit",
      "args": ["mcp"]
    }
  }
}
```

### Codex / Gemini CLI

```bash
codex mcp add commandit -- commandit mcp
gemini mcp add commandit -- commandit mcp
```

### Claude Desktop

```bash
commandit install-mcp --claude
```

## Examples

Once connected, your AI assistant can work with your snippet library through natural conversation:

**Search and use snippets:**
> "Deploy to staging" → AI finds your K8s Deploy snippet, fills env=staging, returns the rendered command

**Create snippets from conversation:**
> "Save that docker compose command as a snippet" → AI detects args, generates description, suggests category and tags

**Explain unfamiliar commands:**
> "Explain `find . -name '*.log' -mtime +30 -delete`" → AI returns flag-by-flag breakdown with safety warnings

**Fill arguments from context:**
> "Run my Docker snippet with port 8080 and image nginx" → AI renders `docker run -p 8080 --name app nginx:latest`

**Browse your library:**
> "What categories do I have?" → AI lists all categories with snippet counts

**Generate commands from natural language:**
> "Compress all PNG files recursively" → AI generates `find . -name '*.png' -exec pngquant --force --ext .png {} \;`

## Available Tools

### Free Tier

| Tool | Description |
|------|-------------|
| `commandit_search` | Search snippets by query |
| `commandit_describe` | Get a snippet's schema and arguments |
| `commandit_list_categories` | List categories with snippet counts |
| `commandit_detect_args` | Parse arguments from a command template |
| `commandit_describe_command` | AI-generated description for a command |
| `commandit_categorize` | AI-suggested category for a snippet |

### Plus Tier

| Tool | Description |
|------|-------------|
| `commandit_render` | Render a template with argument values |
| `commandit_create` | Create a new snippet |
| `commandit_paste` | Render a snippet and paste into the active app |
| `commandit_generate` | Generate a command from natural language |
| `commandit_explain` | Explain what a command does |
| `commandit_enhance` | Enhance snippet metadata (description, tags) |
| `commandit_improve` | Improve a command template |
| `commandit_suggest_tags` | AI-suggested tags for a snippet |

## Troubleshooting

### "commandit: command not found"

The CLI isn't on your PATH. Open CommandIt > Settings > Developer Tools and click "Install Command Line Tool". Make sure `~/.local/bin` is in your PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"  # add to ~/.zshrc
```

### Tools not appearing

1. Verify the CLI works: `commandit version`
2. Verify the MCP server starts: `commandit mcp` (should wait for JSON-RPC input on stdin)
3. Restart your editor after changing MCP config

### MCP server not connecting

Make sure `commandit` is on your PATH (`which commandit`). If not, restart your terminal — the installer adds `~/.local/bin` to your shell profile automatically. For maximum reliability, use `install-mcp` which writes the absolute path:

```bash
commandit install-mcp --cursor  # writes absolute path to config
```

## Links

- [CommandIt](https://commandit.ai) — product homepage
- [commandit-swift](https://github.com/chriscox/commandit-swift) — source code
- [Agent Integration docs](https://commandit.ai/help/agent-integration) — full integration guide

## License

MIT
