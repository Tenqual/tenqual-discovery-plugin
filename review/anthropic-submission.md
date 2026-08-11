# Anthropic submission materials

Submit this package to Anthropic's community marketplace after the production MCP revision is live. Anthropic's official marketplace is separately curated and has no standard application process.

## Core examples

1. `Find cloud infrastructure tenders in Norway.`
2. `Show my latest high-fit tender matches.`
3. `Draft a tender alert for managed cybersecurity services.`

## Review notes

- The plugin connects only to `https://api.tenqual.com/mcp`.
- It contains no hooks, local executables, telemetry, package installers, hidden instructions, or credential readers.
- OAuth is completed directly with Tenqual. The plugin does not read browser, operating-system, Claude, or third-party credentials.
- API keys and webhook signing secrets are displayed only in Tenqual's authenticated interface, never in MCP output.
- The submitted testing account must contain synthetic alerts, qualified matches, available documents, delivery events, and evaluation usage.
- Support, privacy, terms, troubleshooting, and intended behavior are documented in the repository.
