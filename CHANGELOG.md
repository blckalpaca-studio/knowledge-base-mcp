# Changelog

Versions follow the manifest in [`server.json`](./server.json). A published version in the
official MCP Registry is immutable — any change to description, endpoint or icon needs a
new version number.

## 1.0.1 — 2026-10-12

Metadata only, same endpoint.

- Title "Blck Alpaca Agentic Audit & Knowledge Base"; the description names the website
  audit (`audit_website`), which the server has offered since October 2026
- `websiteUrl` points to the English developer page

## Repository — 2026-10-12

Not a server version; `server.json` stays at 1.0.0.

- Claude plugin `blck-alpaca` 1.0.0 under [`plugins/blck-alpaca`](./plugins/blck-alpaca), with
  the marketplace manifest at `.claude-plugin/marketplace.json`. Its own changelog is in the
  plugin README.
- README lists `audit_website`, the fifth tool the server has offered since October 2026,
  and its limits.

## 1.0.0 — 2026-08-28

First public release.

- Four read-only tools: `search_knowledge_base`, `list_knowledge_categories`,
  `list_knowledge_topic_articles`, `get_knowledge_article`
- German, English and Slovak content; untranslated articles are omitted, not substituted
- Streamable HTTP at `https://blckalpaca.at/mcp`, no authentication, no session
- Protocol `2026-07-28`, with a handshake branch for `2025-11-25`, `2025-06-18` and
  `2025-03-26` on the same URL
- Rate limit 240 requests per hour and IP, advertised on every response
- Published as `at.blckalpaca/knowledge-base` in the official MCP Registry (DNS namespace)
  and on Smithery
