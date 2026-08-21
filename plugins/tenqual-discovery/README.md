# Tenqual Claude Plugin

Tenqual connects Claude to source-backed public procurement and tender discovery workflows. It bundles the hosted Tenqual MCP connector with skills for tender search, match review, alert management, and retrieval of available documents.

## What This Plugin Provides

- A hosted Tenqual MCP connector at `https://api.tenqual.com/mcp`
- OAuth-based workspace connection through Tenqual
- Skills that guide Claude through tender discovery workflows
- A specialist agent for source-backed tender review
- Read-only tender and document review by default
- Explicit confirmation patterns for alert, delivery, webhook, and API-key changes

## Included Skills

- `tenqual-discovery:setup`
- `tenqual-discovery:alert-management`
- `tenqual-discovery:tender-search`
- `tenqual-discovery:tender-review`

## Included Agents

- `tenqual-discovery:tender-analyst`

## Documentation

- [Tool surface](docs/tool-surface.md)
- [Local verification](docs/local-verification.md)

## Safety Boundaries

Tenqual is a discovery and review service. It does not submit bids, replace original procurement sources, or create credentials in conversation. Original buyer and procurement-source records remain authoritative.

Credential creation must finish inside Tenqual's authenticated browser flow. Claude must not request, store, or return durable credentials such as API keys, webhook signing secrets, passwords, or bearer tokens.

## Local Validation

From this plugin directory, run:

```bash
claude plugin validate . --strict
```

If `claude` is not installed, install Claude Code and sign in with a supported Claude account before validating.
