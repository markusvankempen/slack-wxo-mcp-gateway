# Publish — docs (public) · source (private / on request) · npm

**Author:** Markus van Kempen  
**Email:** [mvankempen@ca.ibm.com](mailto:mvankempen@ca.ibm.com) · [markus.van.kempen@gmail.com](mailto:markus.van.kempen@gmail.com)  
**Web:** [https://markusvankempen.github.io/](https://markusvankempen.github.io/) · [GitHub](https://github.com/markusvankempen)

| Surface | What’s published | URL |
|---------|------------------|-----|
| GitHub **public** | Docs + `package.json` / `server.json` metadata only | [slack-wxo-mcp-gateway](https://github.com/markusvankempen/slack-wxo-mcp-gateway) |
| GitHub **private** | Full application source + docs | [slack-wxo-mcp-gateway-dev](https://github.com/markusvankempen/slack-wxo-mcp-gateway-dev) |
| npm | Installable package (from private tree) | [`@markusvankempen/slack-wxo-mcp-gateway`](https://www.npmjs.com/package/@markusvankempen/slack-wxo-mcp-gateway) |
| MCP Registry | Manifest (`server.json`) | `io.github.markusvankempen/slack-wxo-mcp-gateway` |
| Site | Agentic AI Bridge | [https://markusvankempen.github.io/](https://markusvankempen.github.io/) |

**Source on request:** email the author — do not push Python / `bin/` / deploy app code to the public repo.

**Run modes A–D** (private tree): [`docs/PUBLISH-MODES.md`](docs/PUBLISH-MODES.md) · `./scripts/run.sh --mode http|podman|ce|ide`

---

## 1. Sync GitHub

```bash
gh auth switch --user markusvankempen

# Public: docs + metadata only (no app source)
./scripts/sync-public-repo.sh

# Private: full source + docs
./scripts/sync-private-repo.sh
```

Never push `.env`, `config.yaml`, `.run/`, `.mcpregistry*`, or secrets.

---

## 2. Publish npm + MCP Registry (from private / local full tree)

```bash
# From the private checkout or local slack_mcp_gateway tree
npm login
npm publish --access public --otp=XXXXXX
mcp-publisher login github
mcp-publisher publish
```

| Field | Value |
|-------|--------|
| `name` | `@markusvankempen/slack-wxo-mcp-gateway` |
| `mcpName` | `io.github.markusvankempen/slack-wxo-mcp-gateway` |
| `homepage` / `websiteUrl` | `https://markusvankempen.github.io/` |
| `repository` | public docs repo (metadata); source on request |

---

## 3. Consumers

| Client | How |
|--------|-----|
| watsonx Orchestrate | Toolkit URL `https://YOUR_HOST/mcp` (`streamable_http`) |
| Cursor / Claude | Remote `/mcp` or `npx -y mcp-remote …` |
| Local / IDE stdio | `npx -y @markusvankempen/slack-wxo-mcp-gateway --stdio` (after npm publish) |
