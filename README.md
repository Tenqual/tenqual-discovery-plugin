# Tenqual Discovery plugin

Tenqual Discovery connects Codex, ChatGPT, and Claude to Tenqual's production Model Context Protocol server. It lets a signed-in customer search source-backed tender notices, review qualified matches, manage tender alerts, inspect evaluation usage, and retrieve available documents for tenders matched to their workspace.

The plugin contains configuration and documentation only. It does not bundle Tenqual's application source code, execute local scripts, register lifecycle hooks, collect conversation history, or send telemetry. All product actions go directly to `https://api.tenqual.com/mcp` over HTTPS.

## Requirements

- A Tenqual account and workspace.
- A client that supports remote HTTP MCP servers and OAuth 2.0 with PKCE.
- Workspace owner or administrator access for integration-management permissions.

## Authentication and permissions

The client opens Tenqual in the browser for sign-in, workspace selection, and explicit scope approval. Tenqual issues a short-lived workspace-scoped access token and supports refresh and revocation. Durable Tenqual API keys are not used to authenticate the plugin.

Credential creation uses a human handoff. The MCP server can open a prefilled Tenqual page, but API keys and webhook signing secrets are created and displayed only in the signed-in Tenqual interface. They are never returned to Codex, ChatGPT, or Claude.

## Example requests

- "Find cloud infrastructure tenders in Norway."
- "Show my latest high-fit tender matches."
- "Draft a tender alert for managed cybersecurity services."
- "Show the available documents for this matched tender."
- "Pause my Nordic cloud alert."

Tenqual Discovery does not write or submit bids. Original procurement sources remain authoritative.

## Data and privacy

The plugin sends only explicit tool inputs to Tenqual. It does not request full conversations, local files, browser data, precise location, or credentials. Tool results are scoped to the workspace approved during OAuth.

See Tenqual's [Privacy Policy](https://tenqual.com/privacy) and [Terms of Service](https://tenqual.com/terms).

## Support and security

For product, privacy, or security questions, contact [support@tenqual.com](mailto:support@tenqual.com) or visit [tenqual.com/contact](https://tenqual.com/contact).

Security reports are handled according to [SECURITY.md](SECURITY.md).

## Development validation

Validate the Codex package with OpenAI's plugin validator and the Claude package with:

```bash
claude plugin validate . --strict
```

The public package intentionally contains no hooks, executable code, package-install commands, or additional network destinations.
