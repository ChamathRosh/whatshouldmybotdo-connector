# WhatShouldMyBotDo MCP connector

A free, read-only remote MCP server that helps small-business owners pick their first AI agent. It uses the same planner and use-case library as https://whatshouldmybotdo.com/?utm_source=github&utm_campaign=chanlab&utm_content=c98.

- Server URL: `https://whatshouldmybotdo.com/api/mcp` (Streamable HTTP, no sign-in, no API key)
- Docs: https://whatshouldmybotdo.com/connector
- Privacy: https://whatshouldmybotdo.com/about#privacy

## Tools (all read-only)
| Tool | Input | Returns |
|---|---|---|
| `plan_first_agent` | The planner's 5 answers: `business_type`, `time_drains` (1–2), `apps` (0–12), `ai_tool` (grok, chatgpt, claude, n8n), `first_goal` | First agent + next 3 jobs, why each fits, estimated hours a week (estimates), schedule, guide links, link to the full plan |
| `search_use_cases` | `query` (2–100 characters) | Up to 8 matching use cases with slug, summary, schedule and guide link |
| `get_template` | `slug`, optional `ai_tool` | The copy-paste, drafts-first routine for that use case |

## Use it
Cursor: install this plugin, or add to `.cursor/mcp.json`:
```json
{ "mcpServers": { "whatshouldmybotdo": { "url": "https://whatshouldmybotdo.com/api/mcp" } } }
```
Grok Bot: tell your bot `Add this MCP server: https://whatshouldmybotdo.com/api/mcp`

Try: "Use WhatShouldMyBotDo to plan my first AI agent. Ask me the 5 questions first."

## Data and limits
No account. Tool inputs are not stored or logged; only per-tool call counts are. Rate limiting is best-effort and in memory (about 30 requests a minute per caller on each server instance; a salted hash of the caller IP is held in memory for about a minute and never written to disk). Requests are capped at 8 KB.

## License
MIT (see LICENSE).
