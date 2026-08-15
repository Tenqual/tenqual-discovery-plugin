# Tenqual Discovery plugin and connector

Tenqual Discovery connects Codex, ChatGPT, Claude, Cursor, and VS Code to Tenqual's production Model Context Protocol server. It lets a signed-in customer search source-backed tender notices, review qualified matches, manage tender alerts, inspect evaluation usage, and retrieve available documents for tenders matched to their workspace.

The plugin contains configuration and documentation only. It does not bundle Tenqual's application source code, execute local scripts, register lifecycle hooks, collect conversation history, or send telemetry. All product actions go directly to `https://api.tenqual.com/mcp` over HTTPS.

## Repository layout

This repository is the public umbrella package for Tenqual AI client integrations.

- `plugin.json`, `mcp.json`, and `.codex-plugin/plugin.json` keep the portable and Codex/OpenAI-facing package metadata.
- `.claude-plugin/marketplace.json` exposes the Claude marketplace catalog.
- `plugins/tenqual-discovery/` contains the dedicated Claude plugin package with its own `.claude-plugin/plugin.json`, MCP declaration, skills, commands, agents, and setup documentation.

Keeping the Claude package in a subdirectory lets Claude install a clean plugin while preserving the existing cross-client connector files at the repository root.

## Requirements

- A Tenqual account and workspace.
- A client that supports remote Streamable HTTP MCP servers and OAuth 2.1 with PKCE.
- Workspace owner or administrator access for integration-management permissions.

Ordinary workspace members can connect with read-only permissions. Creating or changing alerts,
API keys, webhooks, and integration delivery requires an owner or administrator grant.

## Install and connect

When the directory listings are live, install **Tenqual Discovery** from the OpenAI Plugins
Directory or Anthropic Plugin Directory and follow the OAuth prompt. Claude users can also add
`https://api.tenqual.com/mcp` as a custom remote connector. Cursor and VS Code can install this
repository as an Agent Plugins 1.0 package; the portable entry points are `plugin.json` and
`mcp.json` at the repository root. During review or local package testing:

1. Validate this repository with the current Codex plugin validator and
   `claude plugin validate . --strict`.
2. Configure the package or custom connector with the fixed MCP URL in `.mcp.json` or `mcp.json`,
   depending on the client format.
3. Sign in to Tenqual in the browser, select the intended workspace, and approve the displayed
   scopes.
4. Start with `Check my Tenqual connection and show the permissions you have.`

The default grant is read-only and includes identity scopes used to confirm the verified Tenqual
email shown during consent. A tool that needs a privileged scope returns a transport-level OAuth
challenge so a compatible client can ask the user to reconnect and approve that scope without
dropping already approved permissions.

## Authentication and permissions

The client opens Tenqual in the browser for sign-in, workspace selection, and explicit scope approval. Tenqual issues a short-lived workspace-scoped access token and supports refresh and revocation. Durable Tenqual API keys are not used to authenticate the plugin.

Credential creation uses a human handoff. The MCP server can open a prefilled Tenqual page, but API keys and webhook signing secrets are created and displayed only in the signed-in Tenqual interface. They are never returned to Codex, ChatGPT, or Claude.

Document content is delivered as an authenticated MCP resource. The server does not place a signed
storage URL or other bearer credential in model-visible tool output.

## Example requests

- "Find cloud infrastructure tenders in Norway."
- "Show my latest high-fit tender matches."
- "Draft a tender alert for managed cybersecurity services."
- "Show the available documents for this matched tender."
- "Pause my Nordic cloud alert."

Tenqual Discovery does not write or submit bids. Original procurement sources remain authoritative.

## Privacy Policy

Tenqual receives OAuth client metadata, the workspace and scopes the user approves, connection and
last-use times, and the explicit inputs sent to a Tenqual tool. It does not request full
conversations, unrelated local files, browser data, precise location, or client credentials. Tool
results and MCP resources are scoped to the workspace approved during OAuth.

See Tenqual's [Privacy Policy](https://tenqual.com/privacy) and [Terms of Service](https://tenqual.com/terms).

## Support and security

For product, privacy, or security questions, contact [support@tenqual.com](mailto:support@tenqual.com) or visit [tenqual.com/contact](https://tenqual.com/contact).

Security reports are handled according to [SECURITY.md](SECURITY.md).

## Troubleshooting

- **Sign-in repeats or returns to the wrong account:** sign out of Tenqual in the browser, reconnect
  the plugin, and complete OAuth with the intended verified Tenqual account.
- **No eligible workspace:** read-only grants require an active workspace membership. Alert or
  integration write scopes require an active owner or administrator membership.
- **Insufficient scope:** reconnect when the client shows the Tenqual authorization prompt and
  approve the requested scope. The server will not silently broaden an existing grant.
- **401 or disconnected:** reconnect the plugin. Access tokens expire after one hour and a workspace
  administrator can revoke a connection immediately.
- **403:** confirm the user still has an active membership and the role required by the requested
  write operation.
- **Document unavailable:** only clean documents for customer-visible matched tenders are exposed.
  Retrieval or malware-scanning failure does not block the tender alert itself; try again later or
  use the authoritative source URL.
- **Creation link expired:** API-key and webhook handoffs expire after 10 minutes and work once. Ask
  the agent to prepare a new handoff.
- **Unexpected server error:** retry once, then send the time, workflow, and returned correlation ID
  to [support@tenqual.com](mailto:support@tenqual.com). Never send a token, signing secret, or live
  customer document in a support request.

## Development validation

Validate the Codex package with OpenAI's plugin validator. Validate the Claude marketplace and nested Claude plugin package with:

```bash
claude plugin validate . --strict
claude plugin validate plugins/tenqual-discovery --strict
```

The public package intentionally contains no hooks, executable code, package-install commands, or additional network destinations.
