# LangGraph / LangChain + Slack ↔ WxO MCP Gateway

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/)

`tags:` `langgraph` · `langchain` · `langchain-mcp-adapters` · `mcp` · `stdio` · `streamable-http`

Use LangGraph/LangChain as the **agent runtime**; this gateway stays the **Slack/WxO edge**.

---

## Option A — Remote HTTP (gateway already on CE / ngrok)

Point your MCP client at:

```text
https://YOUR_HOST/mcp
```

Transport: **streamable HTTP** (same URL WxO uses).

With [`langchain-mcp-adapters`](https://pypi.org/project/langchain-mcp-adapters/) (API names evolve — check the package docs):

```python
# Illustrative — verify import paths for your adapter version
from langchain_mcp_adapters.client import MultiServerMCPClient

client = MultiServerMCPClient(
    {
        "slack-wxo-gateway": {
            "url": "https://YOUR_HOST/mcp",
            "transport": "streamable_http",
        }
    }
)
tools = await client.get_tools()
# bind tools into your LangGraph / create_react_agent graph
```

---

## Option B — Local stdio

```bash
# terminal: ensure .env has SLACK_* and WXO_*
export GATEWAY_TRANSPORT=stdio
```

```python
from langchain_mcp_adapters.client import MultiServerMCPClient

client = MultiServerMCPClient(
    {
        "slack-wxo-gateway": {
            "command": "npx",
            "args": ["-y", "@markusvankempen/slack-wxo-mcp-gateway", "--stdio"],
            "transport": "stdio",
            "env": {
                "GATEWAY_TRANSPORT": "stdio",
                "SLACK_BOT_TOKEN": "...",
                "WXO_INSTANCE_URL": "...",
                "WXO_API_KEY": "...",
            },
        }
    }
)
tools = await client.get_tools()
```

From a private checkout before npm publish:

```text
command: python3
args: ["-m", "slack_mcp_gateway", "--stdio"]
env: PYTHONPATH=<parent-of-package>, GATEWAY_TRANSPORT=stdio, …
```

---

## Smoke test

1. List tools — expect `list_bindings`, `get_gateway_status`, `post_thread_reply`, …  
2. Invoke `get_gateway_status`  
3. Invoke `list_bindings`  

Do **not** enable the Slack poller in stdio mode unless you intentionally want a second poller (`GATEWAY_ENABLE_POLLER=1`).

Index: [README.md](./README.md) · Why: [../WHY-THIS-MCP.md](../WHY-THIS-MCP.md)
