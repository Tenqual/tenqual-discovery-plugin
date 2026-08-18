---
name: setup
description: Connect Tenqual to Claude and verify the workspace, OAuth scopes, and safe operating boundaries.
---

Use this skill when the user wants to set up, verify, or troubleshoot the Tenqual plugin connection.

## Procedure

1. Ask the user to complete the Tenqual OAuth sign-in if the connector is not connected.
2. Call `tenqual_get_connection` to verify the current workspace connection and available scopes.
3. Explain which workflows are available from the granted scopes:
   - `tenders:read`: tender search and tender details.
   - `documents:read`: matched tender document metadata and authenticated document resources.
   - `alerts:read`: alert list, match history, draft checks, and alert estimates.
   - `alerts:write`: alert drafts.
   - `alerts:manage`: creating, updating, and deleting alerts.
   - `integrations:read`: API key and webhook summaries.
   - `integrations:write`: API key handoffs, webhook handoffs, webhook disablement, and delivery changes.
   - `usage:read`: monthly evaluation usage.
   - `events:read`: integration event feed.
4. Never ask the user to paste Tenqual API keys, webhook signing secrets, OAuth tokens, passwords, or other durable credentials into Claude.
5. For credential creation, use only Tenqual handoff tools. The user must finish review and creation inside Tenqual's authenticated browser flow.
6. Remind the user that Tenqual is a discovery and review service. It does not submit bids and original procurement sources remain authoritative.
