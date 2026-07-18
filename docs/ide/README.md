# IDE setup — Cursor · VS Code · IBM Bob · Antigravity · Claude

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/) · [GitHub](https://github.com/markusvankempen)

Connect the Slack ↔ WxO MCP gateway to any MCP-capable IDE.

---

## Choose your path

| Path | When | How |
|------|------|-----|
| **Remote HTTP** (recommended) | Gateway already on [Code Engine](../code-engine/) or [ngrok](../local-ngrok/) | Point the IDE at `https://YOUR_HOST/mcp` (or bridge with `mcp-remote`) |
| **Local stdio** | Tools in the IDE without a public URL | `npx` / Python with `GATEWAY_TRANSPORT=stdio` |

JSON templates: [`examples/mcp/`](../../examples/mcp/)

---

## Quick pick by IDE

| IDE | Config file | Guide |
|-----|-------------|--------|
| **Cursor** | `~/.cursor/mcp.json` | [cursor.md](./cursor.md) |
| **VS Code** (Copilot MCP) | `User/mcp.json` or `.vscode/mcp.json` | [vscode.md](./vscode.md) |
| **IBM Bob** | `~/.bob/settings/mcp_settings.json` | [bob.md](./bob.md) |
| **Google Antigravity** | `~/.gemini/config/mcp_config.json` | [antigravity.md](./antigravity.md) |
| **Claude Desktop** | `claude_desktop_config.json` | [claude-desktop.md](./claude-desktop.md) |

---

## Transports

| Transport | Endpoint / mode | Clients |
|-----------|-----------------|---------|
| **streamable-http** (default) | `https://HOST/mcp` | WxO toolkits, VS Code `type: http`, Cursor URL / `mcp-remote` |
| **stdio** | `GATEWAY_TRANSPORT=stdio` or `--stdio` | Cursor, VS Code, Bob, Antigravity, Claude (local) |
| **sse** (optional) | `GATEWAY_TRANSPORT=sse` → `/sse` | Older SSE-only clients |

WxO remote toolkits must use `--transport streamable_http` against `/mcp`.

---

## See also

- [Local + ngrok](../local-ngrok/) · [Code Engine](../code-engine/)
- [SETUP.md](../../SETUP.md) — Slack scopes & agents
