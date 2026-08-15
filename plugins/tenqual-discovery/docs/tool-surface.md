# Tenqual MCP Tool Surface

The Tenqual plugin declares one hosted MCP server:

```json
{
  "type": "http",
  "url": "https://api.tenqual.com/mcp"
}
```

The hosted MCP server owns OAuth, tool schemas, tool annotations, and workspace authorization. The plugin package does not include local executables, hooks, telemetry, bundled credentials, or alternate network destinations.

## Default Read Scopes

The hosted MCP OAuth default grant is read-oriented:

- `openid`
- `email`
- `events:read`
- `tenders:read`
- `documents:read`
- `alerts:read`
- `usage:read`

## Elevated Scopes

These scopes require additional authorization:

- `alerts:write`
- `alerts:manage`
- `integrations:read`
- `integrations:write`

## Read Tools

- `tenqual_get_connection`
- `tenqual_search_tenders`
- `tenqual_get_tender`
- `tenqual_list_matches`
- `tenqual_list_alerts`
- `tenqual_get_usage`
- `tenqual_get_tender_documents`
- `tenqual_list_delivery_events`
- `tenqual_get_alert_draft`
- `tenqual_estimate_alert`
- `tenqual_get_document_resource`
- `tenqual_list_api_keys`
- `tenqual_list_webhooks`

## Write Or Management Tools

- `tenqual_draft_alert`
- `tenqual_create_alert`
- `tenqual_update_alert`
- `tenqual_delete_alert`
- `tenqual_prepare_api_key_creation`
- `tenqual_revoke_api_key`
- `tenqual_prepare_webhook_creation`
- `tenqual_disable_webhook`
- `tenqual_set_alert_integration_delivery`

## Credential Boundary

Credential-creation tools prepare authenticated Tenqual browser handoffs only. They must not create or return durable credentials in Claude. The user must complete credential creation in Tenqual.

## Document Boundary

Documents are exposed through authenticated `tenqual://` MCP resources. The connector must not return signed storage URLs or durable bearer credentials.

## Source Boundary

Tenqual provides normalized and source-backed discovery context. Original procurement-source notices and documents remain authoritative.
