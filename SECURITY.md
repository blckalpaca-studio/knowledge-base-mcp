# Security Policy

## Scope

This repository contains metadata only. Reports concerning the live MCP server at
`https://blckalpaca.at/mcp` and the surrounding blckalpaca.at API belong here as well.

## Reporting

Send findings to **office@blckalpaca.at**. Include the request, the response and the time
of the observation. We confirm receipt within three working days.

Please do not open a public issue for anything that exposes data or allows unauthorized
writes.

## What the server does

- Read-only. The tools return published knowledge base content; there is no write path.
- No authentication and no user data. Requests are not tied to an account, and no personal
  data is required or stored beyond what is needed for rate limiting and standard access
  logs.
- No session state. There is no `Mcp-Session-Id` and no GET stream, so there is nothing to
  hijack between calls.
- Rate limited to 240 requests per hour and IP. The remaining quota is on every response
  in `RateLimit` and `RateLimit-Policy`.
- Arguments are validated against the declared input schemas. Unknown properties are
  rejected, and out-of-range values (for example `limit` outside 1–25) are refused with an
  `-32602` listing the offending fields rather than silently corrected.

## Out of scope

- Volumetric denial of service and automated scanner output without a reproducible finding
- Missing hardening headers with no exploitable consequence
- Content of the knowledge base articles themselves
