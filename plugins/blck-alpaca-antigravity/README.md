# Blck Alpaca Agentic Audit for Antigravity

Plugin for Google Antigravity (CLI `agy`, IDE and Antigravity 2.0). It connects the Blck
Alpaca MCP server at `https://blckalpaca.at/mcp` and adds the skill `agentic-audit`.

- **Website audit.** `audit_website` checks a public website the way AI agents see it:
  a score out of 100 across five weighted areas, the evidence behind every check, the
  three fixes with the biggest impact (each with a Knowledge Base guide where one exists)
  and a link to the full report.
- **Knowledge Base.** 431 articles in German, English and Slovak on SEO and generative
  engine optimization (GEO), AI agents and social media, cited with link and date.

## Install

```bash
agy plugin install https://github.com/blckalpaca-studio/knowledge-base-mcp/tree/main/plugins/blck-alpaca-antigravity
```

Without the plugin, the server alone goes into `~/.gemini/config/mcp_config.json`:

```json
{ "mcpServers": { "blckalpaca": { "serverUrl": "https://blckalpaca.at/mcp" } } }
```

Antigravity reads remote servers only from `serverUrl`; `url` and `httpUrl` are not
supported.

## Data and limits

Tool calls go to `https://blckalpaca.at/mcp` and nowhere else. No account, key or sign-in.
The audit only sends GET requests to the website you name. An audit stores the audited
address and its result for 90 days, never the conversation. Limits: 240 requests per hour
per IP; `audit_website` at most 10 checks per website per hour and 60 in total. Not a legal
assessment.

- Privacy policy: https://blckalpaca.at/en/privacy
- Setup and troubleshooting: https://blckalpaca.at/en/developers#connect
- Contact: office@blckalpaca.at

The skill is the same as in the Claude plugin (`plugins/blck-alpaca`); change both together.

## License

MIT, see [LICENSE](./LICENSE). Blck Alpaca e.U., Vienna, Austria.
