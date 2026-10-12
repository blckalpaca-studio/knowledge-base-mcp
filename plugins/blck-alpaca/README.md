# Blck Alpaca Agentic Audit

Plugin for Claude (chat, Cowork and Claude Code). It connects the Blck Alpaca MCP server at
`https://blckalpaca.at/mcp` and adds a skill that uses it.

## What it does

- **Website audit.** `audit_website` checks a public website the way AI agents see it and
  scores five weighted areas: access 30, understanding 25, discoverability 20, EU
  transparency and privacy signals 15, actionability 10. The result is a score out of 100,
  the evidence behind every check, the three fixes with the biggest impact (each with a
  Knowledge Base guide where one exists) and a link to the full report. Checks on young
  standards such as llms.txt only add bonus points; missing them costs nothing.
- **Knowledge Base.** 431 articles in German, English and Slovak on SEO and generative
  engine optimization (GEO), AI agents (including the Model Context Protocol, RAG and the EU
  AI Act) and social media. Answers cite the article with its link and the date of the last
  content change.
- **Skill `agentic-audit`.** Tells Claude which tool fits which request, how to report an
  audit (score, share per area, top three fixes with their guides, limits) and how to turn
  it into a roadmap along the A-L-P-A-C-A Framework.

## Try

- "Audit orf.at for AI-agent readiness and GEO. What are the three most important fixes?"
- "Audit orf.at and turn the findings into a prioritized 90-day implementation plan."
- "What does the Blck Alpaca Knowledge Base say about llms.txt?"
- "Was sagt die Blck Alpaca Knowledge Base zu GEO-Tools wie Profound und Peec AI?"

## Install in Claude Code

```bash
claude plugin marketplace add blckalpaca-studio/knowledge-base-mcp
claude plugin install blck-alpaca@blckalpaca
```

## Data and limits

The plugin sends tool calls to `https://blckalpaca.at/mcp` and nowhere else. No account,
key or sign-in. The audit only sends GET requests to the website you name; it never logs
in and never changes anything. An audit stores the audited address and its result for 90
days, never the conversation. Search terms are not stored. Limits: 240 requests per hour
per IP; `audit_website` at most 10 checks per website per hour and 60 in total. Not a
legal assessment: EU signals such as an imprint or a privacy notice are detected, not
certified.

- Privacy policy: https://blckalpaca.at/en/privacy
- Setup and troubleshooting: https://blckalpaca.at/en/developers#connect
- Method and every check: https://blckalpaca.at/en/agentic-check#methodik
- Contact: office@blckalpaca.at

## Changelog

### 1.0.0 (2026-10-12)

First release: skill `agentic-audit` and the Blck Alpaca MCP server (five read-only tools:
`audit_website`, `search_knowledge_base`, `get_knowledge_article`,
`list_knowledge_categories`, `list_knowledge_topic_articles`).

## License

MIT, see [LICENSE](./LICENSE). Blck Alpaca e.U., Vienna, Austria.
