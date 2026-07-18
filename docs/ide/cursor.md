# Cursor — Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

Config file: `~/.cursor/mcp.json` (or project `.cursor/mcp.json`)

---

## Option A — Remote gateway (Code Engine / ngrok) via `mcp-remote`

Best when the poller + admin UI already run on a host.

```json
{
  "mcpServers": {
    "slack-wxo-gateway": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://YOUR_HOST/mcp"]
    }
  }
}
```

Template: [`examples/mcp/cursor-remote.json`](../../examples/mcp/cursor-remote.json)

If bare `"url"` times out, use `uvx mcp-proxy` against the same `/mcp` URL (or enable `GATEWAY_TRANSPORT=sse` on the host and proxy `/sse`).

---

## Option B — Local stdio (`npx`)

```json
{
  "mcpServers": {
    "slack-wxo-gateway": {
      "command": "npx",
      "args": ["-y", "@markusvankempen/slack-wxo-mcp-gateway", "--stdio"],
      "env": {
        "GATEWAY_TRANSPORT": "stdio",
        "SLACK_BOT_TOKEN": "xoxb-…",
        "WXO_INSTANCE_URL": "https://…",
        "WXO_API_KEY": "…",
        "WXO_AGENT_ID": "…"
      }
    }
  }
}
```

Template: [`examples/mcp/cursor-local.json`](../../examples/mcp/cursor-local.json)

From a private checkout (before npm publish):

```json
{
  "mcpServers": {
    "slack-wxo-gateway": {
      "command": "python3",
      "args": ["-m", "slack_mcp_gateway", "--stdio"],
      "cwd": "/path/to/wxo-slack-middleware",
      "env": {
        "GATEWAY_TRANSPORT": "stdio",
        "PYTHONPATH": "/path/to/wxo-slack-middleware",
        "SLACK_BOT_TOKEN": "xoxb-…",
        "WXO_INSTANCE_URL": "https://…",
        "WXO_API_KEY": "…"
      }
    }
  }
}
```

---

## Verify

1. Cursor → Settings → MCP → slack-wxo-gateway should show green / tools listed  
2. Ask: “List Slack↔WxO gateway bindings”  
3. Expect `list_bindings` (and other tools) to run  

Docs index: [README.md](./README.md)
