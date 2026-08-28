# Blck Alpaca Knowledge Base MCP

Public MCP server for the Blck Alpaca knowledge base: SEO, GEO (generative engine
optimization), AI agents and marketing automation. Read-only, no authentication,
German, English and Slovak.

Listed in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=at.blckalpaca/knowledge-base)
as `at.blckalpaca/knowledge-base`.

This repository holds metadata only. The server runs as part of blckalpaca.at and its
source is not published here.

## Endpoint

```
POST https://blckalpaca.at/mcp
```

Transport: Streamable HTTP. No session is created — there is no `Mcp-Session-Id` and no
GET stream. Every call is a single POST.

## Install

Claude Code:

```bash
claude mcp add --transport http blckalpaca-knowledge-base https://blckalpaca.at/mcp
```

Any client that reads a config file:

```json
{
  "mcpServers": {
    "blckalpaca-knowledge-base": {
      "type": "http",
      "url": "https://blckalpaca.at/mcp"
    }
  }
}
```

## Protocol revisions

The same URL serves two generations, so clients built on older SDKs keep working.

| Revision | Client entry point | Required headers |
|---|---|---|
| `2026-07-28` | `server/discover`, `tools/list`, `tools/call` directly | `MCP-Protocol-Version`, `Mcp-Method`; on `tools/call` also `Mcp-Name` |
| `2025-11-25`, `2025-06-18`, `2025-03-26` | `initialize`, then `notifications/initialized` | none |

An unknown version gets JSON-RPC error `-32022` with the full list under `data.supported`.

## Tools

| Tool | Purpose | Required | Optional |
|---|---|---|---|
| `search_knowledge_base` | Full-text search over article title, short definition and main keyword. Returns URL plus a path triple for the full text. | `query` (string, min 2 chars) | `locale` (`de`\|`en`\|`sk`, default `de`), `limit` (integer 1–25, default 8) |
| `list_knowledge_categories` | Structure of the knowledge base: all categories with their topics, each with slug and URL. Entry point when no search term is known. | — | `locale` |
| `list_knowledge_topic_articles` | All published articles of one topic. | `categorySlug`, `topicSlug` | `locale` |
| `get_knowledge_article` | Full article as Markdown, plus short definition, key takeaways, sourced statistics and FAQ. | `categorySlug`, `topicSlug`, `articleSlug` | `locale` |

Slugs are localized. Category and topic slug must come from the same locale as the
request; if they do not match, the response says why. Content that is not translated into
the requested language is omitted rather than silently replaced with German.

The path triple returned by `search_knowledge_base` and `list_knowledge_topic_articles`
can be passed straight into `get_knowledge_article`.

## Rate limit

240 requests per hour and IP. Every response carries `RateLimit` and `RateLimit-Policy`
(IETF draft) plus the legacy `RateLimit-Limit` / `-Remaining` / `-Reset` triple. Over the
limit the server answers HTTP 429 and JSON-RPC
`-32603` with `data.retryAfterSeconds`, plus a `Retry-After` header.

## Using the content

Articles may be quoted and summarized with attribution to Blck Alpaca and a link to the
article URL returned by the tool.

## Links

- Developer documentation: [DE](https://blckalpaca.at/de/entwickler) · [EN](https://blckalpaca.at/en/developers) · [SK](https://blckalpaca.at/sk/vyvojari)
- OpenAPI spec of the surrounding REST API: https://blckalpaca.at/openapi.json
- Server card: https://blckalpaca.at/.well-known/mcp/server-card.json
- Smithery: https://smithery.ai/server/blckalpaca/knowledge-base
- Manifest: [`server.json`](./server.json)

## Contact

office@blckalpaca.at — Blck Alpaca OG, Vienna, Austria
