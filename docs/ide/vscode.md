# VS Code — Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

Config (Copilot MCP):

- macOS: `~/Library/Application Support/Code/User/mcp.json`
- Or workspace: `.vscode/mcp.json`

---

## Option A — Remote HTTP (native)

```json
{
  "servers": {
    "slack-wxo-gateway": {
      "type": "http",
      "url": "https://YOUR_HOST/mcp"
    }
  }
}
```

Template: [`examples/mcp/vscode-remote.json`](../../examples/mcp/vscode-remote.json)

---

## Option B — Local stdio

```json
{
  "servers": {
    "slack-wxo-gateway": {
      "type": "stdio",
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

Template: [`examples/mcp/vscode-local.json`](../../examples/mcp/vscode-local.json)

---

## Verify

Command Palette → **MCP: List Servers** → tools for `slack-wxo-gateway`.  
Chat: “Run get_gateway_status on the Slack WxO gateway.”

Index: [README.md](./README.md)
