# AI Analytics Agent

An AI agent for analytics and reporting — turning any enriched or scraped dataset into a client-facing report or dashboard spec — backed by real analytics APIs.

Part of [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os), an open ecosystem of specialized AI agents for real business work.

## Related Projects

- [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os) — the central catalog this repo is part of.
- [ai-seo-agent](https://github.com/SamurAIGPT/ai-seo-agent) — one of the data sources this repo can turn into a report or dashboard.
- [ai-ecommerce-agent](https://github.com/SamurAIGPT/ai-ecommerce-agent) — another data source this repo can report on.
- [ai-competitor-intelligence-agent](https://github.com/SamurAIGPT/ai-competitor-intelligence-agent) — shares this repo's cross-umbrella data-aggregation role.
- [MuAPI MCP docs](https://muapi.ai/docs/mcp) — connect this repo's `SKILL.md` files via MCP.
- [MuAPI Agent Skills](https://muapi.ai/docs/agent-skills) — background on the `SKILL.md` pattern this repo uses.
- [MuAPI access keys](https://muapi.ai/access-keys) — create the API key this agent needs.

## What this covers

This repo is the umbrella for turning raw numbers into something a client can actually read: a written report with takeaways, or a dashboard spec a BI tool can be built from. It's a cross-cutting umbrella — it doesn't collect its own data, it consumes datasets produced by other Agency Agents OS umbrellas (`ai-sales-agent`, `ai-social-agent`, `ai-ecommerce-agent`, `ai-ads-agent`, and others) and turns them into deliverables.

## Sub-agents

| Agent | Does | Status |
|---|---|---|
| [Report Generation](agents/report-generation/SKILL.md) | Turns a raw dataset into a structured, client-facing written report with key takeaways | Coming Soon |
| [Dashboard Builder](agents/dashboard-builder/SKILL.md) | Turns a raw dataset into a structured dashboard spec (metrics, chart types, layout) | Coming Soon |

## Required Muapi APIs

- `analytics.ga4_report` — pull a structured analytics report for a given property/date range.
- `analytics.aggregate_dataset` — aggregate and summarize an arbitrary dataset (rows/columns from another umbrella's output) into report- or dashboard-ready metrics.

See each sub-agent's `SKILL.md` for the specific capabilities it uses.

## Setup

1. Create a Muapi account and API key at [muapi.ai](https://muapi.ai).
2. Review the [Muapi API quickstart](https://muapi.ai) and [OpenAPI schema](https://api.muapi.ai/openapi.json) for the analytics endpoints.
3. Load the `SKILL.md` for the sub-agent you need into your agent runtime (hosted agent, MCP client, or custom LLM app), or follow it manually.


## Using with an AI agent

Every sub-agent's `SKILL.md` is model- and runtime-agnostic — it's plain Markdown, so it works with any LLM agent, not just Claude. Two integration paths:

**As an MCP connection (the agent gets live Muapi tools):**

Muapi runs an MCP server at `https://api.muapi.ai/mcp` that any MCP-compatible client can connect to — Cursor, Windsurf, Claude, or your own custom agent.

- **Cursor / Windsurf / other clients with a header field:** connect to `https://api.muapi.ai/mcp` with an `Authorization: Bearer YOUR_MUAPI_KEY` header.
- **claude.ai / Claude Cowork / other connector UIs with no header field:** use the URL-embedded key form instead, `https://api.muapi.ai/mcp/YOUR_MUAPI_KEY`, via Settings → Connectors → Add custom connector.
- **Claude Code / Claude Desktop:** `claude mcp add muapi -e MUAPI_API_KEY=YOUR_MUAPI_KEY -- muapi mcp serve` (uses the muapi CLI's stdio transport — Claude Code's HTTP MCP client doesn't reliably inject tools).

Full setup details for every client: [muapi.ai/docs/mcp](https://muapi.ai/docs/mcp).

**As agent instructions (any LLM follows the workflow directly):**

Drop a sub-agent's `SKILL.md` into a Claude Code project's `.claude/skills/` directory, paste it into a custom-GPT/Project's system instructions, hand it to an autonomous agent framework as a tool spec, or attach it directly in a chat conversation — then ask the agent to follow it.

## Read-only vs. write actions

Both sub-agents are `read-only`/`draft-only`: they read a dataset and produce a report or dashboard spec, never a live publish. Handing a dashboard spec to an actual BI tool, or a report to a client-facing channel, is a separate, explicitly approved step outside this repo.

## Status and limitations

Both sub-agents are Coming Soon. They depend on analytics and reporting capabilities (`analytics.ga4_report`, `analytics.aggregate_dataset`) that aren't yet live on Muapi. Until then, treat the `SKILL.md` files as blueprints, not working integrations.

## Contributing

See [Agency Agents OS CONTRIBUTING.md](https://github.com/Anil-matcha/agency-agents-os/blob/main/CONTRIBUTING.md).

## License

[MIT](LICENSE)
