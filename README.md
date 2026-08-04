# Novence MCP

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for **Novence** — static site hosting for AI agents.

- **Endpoint:** `https://api.novence.ai/mcp` (streamable HTTP)
- **Auth:** `Authorization: Bearer nv_…`
- **Docs:** [novence.ai/mcp](https://novence.ai/mcp)
- **Privacy:** [novence.ai/privacy](https://novence.ai/privacy)

This repository is the **Claude Code plugin / install package** ([LincChad/novence-mcp](https://github.com/LincChad/novence-mcp)). The MCP server itself is hosted; there is nothing to run locally.

## Get an API key

```bash
curl -sS -X POST https://api.novence.ai/v1/bootstrap \
  -H 'Content-Type: application/json' \
  -d '{"email":"you@example.com"}'
```

Verify the emailed OTP when prompted to unlock full Free quotas.

## Claude Code (this plugin)

Claude stores the key via **plugin `userConfig`** (macOS Keychain / protected credentials) — prefer this over shell env.

```bash
claude plugin validate .
claude --plugin-dir .
```

Or install from a marketplace after this repo is listed in the Claude plugin directory.

1. Enable the plugin (you can leave the API key blank, bootstrap, then fill it in).
2. Set **Novence API key** in plugin settings, or pass `--config api_key='nv_…'` at install.
3. Confirm tools with `/mcp`.

The plugin’s `.mcp.json` sends `Authorization: Bearer ${user_config.api_key}`. See [SETUP.md](./SETUP.md).

## Cursor / shell

Use the environment variable pattern (not Claude plugin Keychain):

```bash
export NOVENCE_API_KEY='nv_…'
```

Add to `~/.cursor/mcp.json` (or project `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "novence": {
      "url": "https://api.novence.ai/mcp",
      "headers": {
        "Authorization": "Bearer ${env:NOVENCE_API_KEY}"
      }
    }
  }
}
```

One-click install (replace the key after install, or use env interpolation):

[Add to Cursor](https://novence.ai/mcp#connect)

## Generic MCP clients

```json
{
  "mcpServers": {
    "novence": {
      "url": "https://api.novence.ai/mcp",
      "headers": {
        "Authorization": "Bearer nv_…"
      }
    }
  }
}
```

## Official registry

Published as `io.github.LincChad/novence-mcp` on [registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io).

## License

MIT — see [LICENSE](./LICENSE).
