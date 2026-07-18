# Agent frameworks — use this MCP (don’t embed them)

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/) · [GitHub](https://github.com/markusvankempen)

`tags:` `langchain` · `langgraph` · `llamaindex` · `openai-agents` · `mcp` · `bring-your-own-agent`

This gateway is an **MCP server**. Popular LLM frameworks should **connect to it** — we do not ship LangChain/CrewAI inside the process.

```text
Your agent (LangGraph / LlamaIndex / OpenAI Agents / WxO / …)
        │  MCP client
        ▼
  slack-wxo-mcp-gateway   (/mcp or stdio)
        │
        ▼
  Slack bindings + WxO Runs API
```

---

## Choose a guide

| Framework | Guide | Typical transport |
|-----------|--------|-------------------|
| watsonx Orchestrate | [../code-engine/](../code-engine/) · [../local-ngrok/](../local-ngrok/) | `streamable_http` → `/mcp` |
| IDEs (Cursor, VS Code, Bob, …) | [../ide/](../ide/) | stdio or `mcp-remote` |
| **LangGraph / LangChain** | [langgraph.md](./langgraph.md) | stdio or HTTP |
| **LlamaIndex** | [llamaindex.md](./llamaindex.md) | stdio or HTTP |
| **OpenAI Agents SDK** | [openai-agents.md](./openai-agents.md) | stdio or HTTP |

Same **14 tools** for every client — no per-framework tool surface.

---

## What you need (checklist)

1. Gateway reachable: local `--stdio` **or** `https://YOUR_HOST/mcp`  
2. Framework MCP client / adapter package  
3. Call `list_bindings` / `get_gateway_status` as a smoke test  
4. Keep Slack/WxO secrets in env — not in the agent prompt  

Why this exists: [../WHY-THIS-MCP.md](../WHY-THIS-MCP.md)
