# OpenAI Agents SDK + Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

`tags:` `openai-agents` · `openai` · `mcp` · `agents-sdk`

Run agents with the **OpenAI Agents SDK** (or any OpenAI-tool loop); keep Slack/WxO on this MCP server.

---

## Remote HTTP

```text
https://YOUR_HOST/mcp
```

If the SDK supports MCP servers natively, register a server entry with that URL (streamable HTTP).  
If not, bridge with:

```bash
npx -y mcp-remote https://YOUR_HOST/mcp
```

and attach the stdio bridge as an MCP server in the Agents SDK config (same shape as Claude Desktop remote).

---

## Local stdio

```json
{
  "command": "npx",
  "args": ["-y", "@markusvankempen/slack-wxo-mcp-gateway", "--stdio"],
  "env": {
    "GATEWAY_TRANSPORT": "stdio",
    "SLACK_BOT_TOKEN": "xoxb-…",
    "WXO_INSTANCE_URL": "https://…",
    "WXO_API_KEY": "…"
  }
}
```

Wire that block into the Agents SDK MCP server list (see current OpenAI Agents MCP documentation for the exact field names).

---

## Smoke

Ask the agent: “Call get_gateway_status and summarize bindings.”  
Expect tool calls against this gateway, not invented Slack APIs.

Index: [README.md](./README.md) · IDE templates: [`../../examples/mcp/`](../../examples/mcp/)
