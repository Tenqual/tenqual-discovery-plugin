# Tenqual Claude Plugin

Tenqual connects Claude to source-backed public procurement and tender discovery workflows. It bundles the hosted Tenqual MCP connector with skills for tender search, opportunity review, bid/no-bid analysis, and compliance matrix preparation.

## What This Plugin Provides

- A hosted Tenqual MCP connector at `https://api.tenqual.com/mcp`
- OAuth-based workspace connection through Tenqual
- Skills that guide Claude through common procurement workflows
- Slash commands for common tender workflows
- Specialist agents for tender and compliance review
- Read-only tender and document review by default
- Explicit confirmation patterns for alert, delivery, webhook, and API-key changes

## Included Skills

- `tenqual-discovery:setup`
- `tenqual-discovery:alert-management`
- `tenqual-discovery:tender-search`
- `tenqual-discovery:tender-review`
- `tenqual-discovery:bid-no-bid`
- `tenqual-discovery:compliance-matrix`

## Included Commands

- `/tenqual-discovery:find-tenders`
- `/tenqual-discovery:review-tender`
- `/tenqual-discovery:assess-bid`
- `/tenqual-discovery:build-compliance-matrix`

## Included Agents

- `tenqual-discovery:tender-analyst`
- `tenqual-discovery:compliance-reviewer`

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
