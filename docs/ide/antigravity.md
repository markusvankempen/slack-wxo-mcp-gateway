# Google Antigravity — Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

Config: `~/.gemini/config/mcp_config.json`  
(Settings → Customizations → Open MCP Config)

Official: [Antigravity MCP](https://antigravity.google/docs/mcp)

---

## Option A — Remote (`serverUrl` or `mcp-remote`)

Native remote (if your Antigravity build accepts streamable HTTP):

```json
{
  "mcpServers": {
    "slack-wxo-gateway": {
      "serverUrl": "https://YOUR_HOST/mcp"
    }
  }
}
```

Bridge (most reliable):

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

Template: [`examples/mcp/antigravity-remote.json`](../../examples/mcp/antigravity-remote.json)

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

Template: [`examples/mcp/antigravity-local.json`](../../examples/mcp/antigravity-local.json)

Index: [README.md](./README.md)
