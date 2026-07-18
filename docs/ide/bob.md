# IBM Bob — Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

Config file: `~/.bob/settings/mcp_settings.json`

---

## Option A — Remote via `mcp-remote` (recommended)

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

Template: [`examples/mcp/bob-remote.json`](../../examples/mcp/bob-remote.json)

---

## Option B — Local stdio

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
        "WXO_API_KEY": "…"
      }
    }
  }
}
```

Template: [`examples/mcp/bob-local.json`](../../examples/mcp/bob-local.json)

Restart Bob after editing. Confirm tools appear under MCP / agent tool lists.

Index: [README.md](./README.md)
