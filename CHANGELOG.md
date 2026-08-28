# Changelog

Versions follow the manifest in [`server.json`](./server.json). A published version in the
official MCP Registry is immutable — any change to description, endpoint or icon needs a
new version number.

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
