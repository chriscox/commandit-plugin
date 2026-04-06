# CommandIt Plugin for Claude Code

[CommandIt](https://commandit.ai) is a native macOS command palette for developers. This plugin exposes CommandIt's MCP server to Claude Code, giving your AI assistant direct access to your snippet library.

## Prerequisites

1. **CommandIt app** installed on macOS ([download](https://commandit.ai))
2. **CommandIt CLI** installed and on PATH (Settings > Developer Tools > Install CLI in the app)

Verify the CLI is available:

```bash
commandit version
```

## Install

**Option A — CLI command (recommended)**

The CLI writes the absolute binary path, which is the most reliable method:

```bash
commandit install-mcp --claude
```

**Option B — Plugin marketplace**

```bash
# Add the marketplace
claude plugin marketplace add chriscox/commandit-plugin

# Install the plugin
claude plugin install commandit@commandit-plugin
```

**Option C — Manual registration**

```bash
claude mcp add --scope user commandit -- /Users/you/.local/bin/commandit mcp
```

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

## Local Testing

To test the plugin locally before installing from the marketplace:

```bash
claude --plugin-dir ./commandit-plugin
```

## Troubleshooting

### "commandit: command not found"

The CLI isn't on your PATH. Open CommandIt > Settings > Developer Tools and click "Install Command Line Tool".

### Tools not appearing

1. Verify the CLI works: `commandit version`
2. Verify the MCP server starts: `commandit mcp` (should wait for JSON-RPC input on stdin)
3. Restart Claude Code after installing the plugin

### Plugin not updating

Run `claude plugin update` to pull the latest version.

## Links

- [CommandIt](https://commandit.ai) — product homepage
- [commandit-swift](https://github.com/chriscox/commandit-swift) — source code
- [Agent Integration docs](https://commandit.ai/help/agent-integration) — full integration guide

## License

MIT
