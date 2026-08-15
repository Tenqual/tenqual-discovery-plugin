# Tenqual Setup

1. Install or enable the Tenqual plugin in Claude.
2. Connect the Tenqual MCP connector when Claude prompts for authentication.
3. Sign in to Tenqual and choose the intended workspace.
4. Confirm the granted scopes match the workflow you want Claude to perform.
5. Ask Claude to check the connection with `tenqual_get_connection`.

For most review workflows, the default read scopes are enough. Alert management and integration administration require additional Tenqual authorization and explicit user confirmation before changes.
