# Anthropic submission materials

Submit both the remote connector and this public plugin after the production MCP revision is live.
The connector provides broad Claude access; the plugin packages the connector for Cowork and Claude
Code. Community publication does not guarantee Anthropic Verified status.

## Connector Directory packet

- Name: `Tenqual Discovery`
- Tagline: `Find and monitor qualified public tenders`
- Description: `Search source-backed public tender notices, review Low, Medium, and High matches for your Tenqual workspace, manage tender alerts, inspect usage and delivery events, and retrieve clean documents for matched tenders. Tenqual Discovery does not write or submit bids.`
- Categories: `Productivity`, `Search`, `Business Intelligence`
- Documentation: `https://github.com/Tenqual/tenqual-discovery-plugin#readme`
- Privacy: `https://tenqual.com/privacy`
- Support: `support@tenqual.com` and `https://tenqual.com/contact`
- Company: `Tenqual Software AS`, `https://tenqual.com`
- Server: universal Streamable HTTP at `https://api.tenqual.com/mcp`
- Authentication: OAuth 2.1 authorization code with PKCE and dynamic client registration
- Account prerequisite: active Tenqual workspace membership; owner or administrator for writes
- Access classification: reads and writes Tenqual Discovery data
- API ownership: first-party Tenqual API; source procurement records remain attributable to their
  public sources
- Sensitive categories: no personal health data and no sponsored content
- Allowed browser-link origin: `https://tenqual.com`
- Screenshots: none; this remote connector has no MCP App UI

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

## Test and launch

Use the same `Tenqual Plugin Review` fixture defined in `review/openai-submission.md`. Connect the
production server as a custom Claude connector, run every tool through MCP Inspector and through a
custom Claude, and record pass/fail, arguments, result shape, and timestamp in a private release
artifact. Creation handoffs must be completed only with the signed-in synthetic reviewer account;
webhooks must point only to a Tenqual-owned review sink. Revoke the reviewer session, MCP grants,
created credentials, and webhook after review.

Submit the remote connector through the Claude.ai Connector Directory portal. Submit this public
repository separately through the Claude.ai or Console Plugin Directory form. Run
`claude plugin validate . --strict` immediately before the plugin submission.
