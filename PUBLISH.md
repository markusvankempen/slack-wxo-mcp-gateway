# Publish — npm + MCP Registry + GitHub

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/) · [GitHub](https://github.com/markusvankempen)

| Surface | URL |
|---------|-----|
| npm | [`@markusvankempen/slack-wxo-mcp-gateway`](https://www.npmjs.com/package/@markusvankempen/slack-wxo-mcp-gateway) |
| MCP Registry | `io.github.markusvankempen/slack-wxo-mcp-gateway` |
| GitHub (public package) | [slack-wxo-mcp-gateway](https://github.com/markusvankempen/slack-wxo-mcp-gateway) |
| GitHub (private mirror) | [slack-wxo-mcp-gateway-dev](https://github.com/markusvankempen/slack-wxo-mcp-gateway-dev) |
| Site | [https://markusvankempen.github.io/](https://markusvankempen.github.io/) |

**Run modes A–D** (one package, switches):  
[`docs/PUBLISH-MODES.md`](docs/PUBLISH-MODES.md) · `./scripts/run.sh --mode http|podman|ce|ide`

---

## 1. Sync package to GitHub

Public repo = **full npm package** (Python source, `bin/`, docs, `server.json`).

```bash
gh auth switch --user markusvankempen
./scripts/sync-public-repo.sh    # public package
./scripts/sync-private-repo.sh   # private mirror (optional)
```

Never push `.env`, `config.yaml`, `.run/`, `.mcpregistry*`, or other secrets.

---

## 2. Publish to npm + MCP Registry

Order: **npm first**, then **mcp-publisher**.

```bash
cd /path/to/slack_mcp_gateway   # or clone the public repo

npm login
npm publish --access public --otp=XXXXXX
mcp-publisher login github       # or: -token "$(gh auth token)"
mcp-publisher publish            # reads server.json
```

| Field | Value |
|-------|--------|
| `name` | `@markusvankempen/slack-wxo-mcp-gateway` |
| `mcpName` | `io.github.markusvankempen/slack-wxo-mcp-gateway` |
| `bin` | `slack-wxo-mcp-gateway` → `bin/slack-wxo-mcp-gateway.js` |
| `homepage` / `websiteUrl` | `https://markusvankempen.github.io/` |
| `repository` | `https://github.com/markusvankempen/slack-wxo-mcp-gateway.git` |

---

## 3. Consumers

| Client | How |
|--------|-----|
| watsonx Orchestrate | `orchestrate toolkits add -k mcp … --url https://YOUR_HOST/mcp --transport streamable_http` |
| Cursor / Claude (remote) | `https://YOUR_HOST/mcp` or `npx -y mcp-remote https://YOUR_HOST/mcp` |
| Local / IDE stdio | `npx -y @markusvankempen/slack-wxo-mcp-gateway --stdio` |
