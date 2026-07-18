# LlamaIndex + Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

`tags:` `llamaindex` · `llama-index` · `mcp` · `rag` · `tool-calling`

LlamaIndex owns RAG / agents; this gateway exposes Slack + WxO as **MCP tools**.

---

## Remote (recommended when gateway is hosted)

```text
https://YOUR_HOST/mcp   # streamable HTTP
```

Use LlamaIndex’s MCP client utilities (package names vary by version — see current LlamaIndex MCP docs) to load tools from that URL, then attach them to a `FunctionAgent` / workflow.

Illustrative pattern:

```python
# Pseudo-API — confirm against your llama-index version
# from llama_index.tools.mcp import BasicMCPClient, McpToolSpec
#
# client = BasicMCPClient("https://YOUR_HOST/mcp")
# tools = await McpToolSpec(client=client).to_tool_list_async()
# agent = FunctionAgent(tools=tools, llm=...)
```

---

## Local stdio

```bash
npx -y @markusvankempen/slack-wxo-mcp-gateway --stdio
# env: GATEWAY_TRANSPORT=stdio, SLACK_BOT_TOKEN, WXO_*
```

Configure the LlamaIndex MCP client with `command` / `args` / `env` the same way as Cursor local stdio ([`../ide/cursor.md`](../ide/cursor.md)).

---

## Good first tools

| Tool | Why |
|------|-----|
| `get_gateway_status` | Connectivity |
| `list_bindings` | See channel → agent map |
| `list_recent_messages` | Ground RAG / agent in Slack context |
| `post_thread_reply` | Write back (use carefully) |

Index: [README.md](./README.md)
