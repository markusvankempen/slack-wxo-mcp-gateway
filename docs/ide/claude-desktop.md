# Claude Desktop — Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

Config (macOS): `~/Library/Application Support/Claude/claude_desktop_config.json`

---

## Local stdio

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

## Remote via `mcp-remote`

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

Templates: [`examples/mcp/claude-desktop-local.json`](../../examples/mcp/claude-desktop-local.json) · [`claude-desktop-remote.json`](../../examples/mcp/claude-desktop-remote.json)

Restart Claude Desktop after saving.

Index: [README.md](./README.md)
