# Summit53 MCP Server

**48 revenue intelligence tools for AI assistants.**

Summit53 MCP server connects your AI assistant to your CRM — search deals, forecast revenue, analyze pipeline risk, run qualification frameworks, manage outreach sequences, and track value delivery using natural language.

[![npm version](https://img.shields.io/npm/v/@summit53/mcp-server)](https://www.npmjs.com/package/@summit53/mcp-server)
[![MCP Compatible](https://img.shields.io/badge/MCP-compatible-brightgreen)](https://modelcontextprotocol.io)
[![License](https://img.shields.io/badge/license-Proprietary-blue)](https://summit53.io/terms)

## Quick Start

All connections use **OAuth 2.0 authentication** — no API keys to manage. You sign in with your Summit53 account and scoped tokens are issued automatically.

### Claude.ai (Web)

1. Go to **Settings > Connectors**
2. Click **Add custom connector**
3. Enter Name: `Summit53` and URL: `https://api.summit53.io/mcp`
4. Click Save, then **Configure**
5. Complete OAuth sign-in with your Summit53 credentials

### Claude Desktop / Claude Code

Uses `mcp-remote` to bridge stdio to the hosted OAuth server:

```json
{
  "mcpServers": {
    "summit53": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.summit53.io/mcp/"
      ]
    }
  }
}
```

On first run, a browser window opens for OAuth sign-in. Tokens are cached locally and refresh automatically.

**Config file locations:**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/Claude/claude_desktop_config.json`

### ChatGPT

1. Go to **Settings > Apps**
2. Click **Add app** and search for Summit53
3. Enter server URL: `https://api.summit53.io/mcp`
4. Authorize via OAuth with your Summit53 account

### Cursor / Windsurf

Use the same `mcp-remote` proxy command in your client's MCP configuration:

```json
{
  "mcpServers": {
    "summit53": {
      "command": "npx",
      "args": ["mcp-remote", "https://api.summit53.io/mcp/"]
    }
  }
}
```

## What Can You Do?

Ask your AI assistant questions like:

| Category | Example Prompts |
|----------|----------------|
| **Search** | "Show me all deals over $50k" · "Find accounts in the technology industry" |
| **Pipeline Risk** | "What deals are at risk?" · "Show me the risk heatmap" |
| **Forecasting** | "What's our forecast confidence this quarter?" · "What's our current ARR?" |
| **Qualification** | "Run MEDDPIC analysis on deal 15" · "What's the BANT score for opportunity 7?" |
| **Activity** | "Which accounts haven't been touched in 30 days?" · "What's my weekly action plan?" |
| **Outreach** | "Show me outreach leads for Globex" · "Enroll leads 11 and 12 in sequence 7" |
| **Value Tracking** | "How is Acme Corp tracking on value delivery?" · "Show the value contract for deal 15" |
| **Team** | "How is my team doing on their weekly plans?" · "Show team activities for last week" |

## All 48 Tools

### Search (3 tools)
- `get_opportunity` — Full deal details by ID
- `search_opportunities` — Filter deals by name, stage, account, value
- `search_accounts` — Filter accounts by name, industry, owner, revenue

### Account Intelligence (3 tools)
- `account_intelligence_summary` — Health scores, risk accounts, expansion candidates
- `account_execution_health` — Execution health score for a specific account
- `opportunity_framework_summary` — MEDDPIC/BANT/SPICED qualification scores

### Pipeline & Risk (4 tools)
- `pipeline_risk_summary` — Risk analysis with confidence metrics
- `risk_heatmap` — Deal-level risk heatmap with scores and factors
- `deal_drag_summary` — Stalled deals, waste scores, risk distribution
- `deal_drag_dashboard` — Paginated deal drag with filters

### Forecasting (4 tools)
- `forecast_confidence` — Confidence scores, rep performance, velocity, quota coverage
- `arr_growth_analytics` — ARR, NRR, growth stage classification, trends
- `arr_growth_narrative` — AI-generated ARR narrative with recommendations
- `unified_forecast_summary` — Executive forecast: pipeline coverage, revenue at risk

### Activity (3 tools)
- `activity_gaps` — Accounts not touched in N days
- `weekly_action_plan` — Prioritized weekly tasks with risk summaries
- `team_action_plan` — Team-wide completion rates and flagged deals

### Research (1 tool)
- `external_account_research` — Queue async web/news research for an account

### Notes & Activities (5 tools)
- `get_opportunity_notes_summary` — AI-generated notes summary
- `rebuild_opportunity_notes_summary` — Regenerate notes summary
- `get_opportunity_activities` — All activities (calls, emails, meetings, notes)
- `get_opportunity_notes` — All notes on a deal
- `create_opportunity_note` — Add a note (triggers async summary update)

### Outreach (13 tools)
- `search_outreach_leads` — Filter leads by query, status, owner, list
- `list_outreach_sequences` — All sequences with metadata
- `get_outreach_sequence` — Sequence details including steps
- `enroll_outreach_leads_in_sequence` — Enroll leads into sequences
- `process_outreach_due_steps` — Trigger due-step processing
- `resolve_outreach_manual_step` — Complete/skip manual steps
- `convert_outreach_lead` — Convert lead to CRM account/contact/opportunity
- `list_outreach_starter_templates` — Predefined sequence templates
- `get_outreach_lead` — Full lead details
- `update_outreach_lead` — Update lead fields
- `list_outreach_lead_lists` — Lead lists with counts
- `bulk_upsert_outreach_leads` — Create/update up to 200 leads with dedup
- `outreach_funnel_summary` — Funnel breakdown by status, stage, fit, engagement

### Value Impact (11 tools)
- `get_value_impact_card` — Fulfillment score, expansion readiness, evidence confidence
- `get_value_contract` — Promised outcomes for an opportunity
- `list_impact_entries` — Post-sale impact evidence for a contract
- `list_account_contracts` — All contracts with dates, ARR, status
- `create_impact_entry` — Add manual impact evidence
- `update_impact_entry` — Update impact entry fields
- `delete_impact_entry` — Remove an impact entry
- `update_account_contract` — Update contract dates, ARR, term
- `set_primary_contract` — Set primary contract for an account
- `generate_value_contract` — AI-generate value contract from deal notes
- `run_value_impact_pipeline` — Full pipeline: contracts, generation, evidence extraction

### Discovery (1 tool)
- `list_available_tools` — Discover all tools, optionally filtered by category

## Authentication

Summit53 uses **OAuth 2.0** for all MCP connections. No API keys to generate or rotate.

- Sign in with your Summit53 account credentials during setup
- Scoped tokens are issued automatically (`crm:read`, `pipeline:read`, `revenue:read`, `actions:read`)
- Tokens expire after 1 year and can be revoked from your admin panel at `/admin/integrations/mcp`
- OAuth discovery: `https://api.summit53.io/.well-known/oauth-authorization-server`

For stdio-based clients (Claude Desktop, Cursor, Windsurf), the `mcp-remote` package handles the OAuth flow — a browser window opens on first run, and tokens are cached locally.

## Architecture

- **Transport**: Streamable HTTP (Cloud Run compatible, no WebSocket required)
- **Rate Limiting**: 100 calls/min global, 30/min per tool (Redis-backed sliding window)
- **Caching**: Redis-backed with per-tool TTLs (5-15 minutes)
- **Metrics**: Built-in usage tracking per tool, per org
- **Hosting**: Google Cloud Run (stateless, auto-scaling)

## Getting Started

1. Sign up at [summit53.io](https://summit53.io)
2. Add Summit53 to your MCP client (see Quick Start above)
3. Authenticate via OAuth when prompted
4. Start asking your AI assistant about your pipeline

## Support

- Documentation: [summit53.com/docs](https://www.summit53.com/docs)
- Email: support@summit53.io
- Issues: [github.com/summit53/mcp-server/issues](https://github.com/summit53/mcp-server/issues)

## License

Proprietary. See [summit53.io/terms](https://summit53.io/terms) for details.
