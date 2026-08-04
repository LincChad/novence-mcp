# Novence MCP

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for **Novence** — static site hosting for AI agents.

- **Endpoint:** `https://api.novence.ai/mcp` (streamable HTTP)
- **Auth:** `Authorization: Bearer nv_…`
- **Docs:** [novence.ai/mcp](https://novence.ai/mcp)
- **Privacy:** [novence.ai/privacy](https://novence.ai/privacy)

This repository is the **Claude Code plugin / install package**. The MCP server itself is hosted; there is nothing to run locally.

## Get an API key

```bash
curl -sS -X POST https://api.novence.ai/v1/bootstrap \
  -H 'Content-Type: application/json' \
  -d '{"email":"you@example.com"}'
```

Export the returned key:

```bash
export NOVENCE_API_KEY='nv_…'
```

Verify the emailed OTP when prompted to unlock full Free quotas.

## Claude Code (this plugin)

```bash
claude plugin validate .
claude --plugin-dir .
```

Or install from a marketplace after this repo is listed in the Claude plugin directory.

Set `NOVENCE_API_KEY` in your environment before using tools. See [SETUP.md](./SETUP.md).

## Cursor

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

Published as `ai.novence/mcp` on [registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io).

## License

MIT — see [LICENSE](./LICENSE).
