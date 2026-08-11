# MCP tool annotation rationale

The production MCP server is authoritative. Re-scan it before every submission or version update.
Each row is intentionally independent so it can be copied into marketplace review fields.

| Tool | Read only | Destructive | Open world | OAuth scope | Rationale |
| --- | --- | --- | --- | --- | --- |
| `tenqual_get_connection` | Yes | No | No | connected grant | Reads connection and scope status only. |
| `tenqual_search_tenders` | Yes | No | No | `tenders:read` | Searches source-backed notices without changing data. |
| `tenqual_get_tender` | Yes | No | No | `tenders:read` | Retrieves one source-backed notice. |
| `tenqual_list_matches` | Yes | No | No | `alerts:read` | Lists customer-visible Low, Medium, and High matches. |
| `tenqual_list_alerts` | Yes | No | No | `alerts:read` | Lists current workspace alert definitions. |
| `tenqual_get_usage` | Yes | No | No | `usage:read` | Reads current evaluation entitlement and consumption. |
| `tenqual_get_tender_documents` | Yes | No | No | `documents:read` | Lists clean document metadata for a visible matched tender. |
| `tenqual_list_delivery_events` | Yes | No | No | `events:read` | Reads paginated delivery events without redelivery. |
| `tenqual_draft_alert` | No | No | No | `alerts:write` | Persists and queues a private draft without activating delivery or changing public state; when provided, the company website may be retrieved for context. |
| `tenqual_get_alert_draft` | Yes | No | No | `alerts:read` | Reads the state and result of one existing draft. |
| `tenqual_estimate_alert` | Yes | No | No | `alerts:read` | Computes bounded candidate counts without reserving quota or changing configuration. |
| `tenqual_create_alert` | No | Yes | Yes | `alerts:manage` | Creates an alert and can enable future external email or webhook delivery. |
| `tenqual_update_alert` | No | Yes | Yes | `alerts:manage` | Overwrites a versioned alert definition and can change future external delivery. |
| `tenqual_delete_alert` | No | Yes | No | `alerts:manage` | Soft-deletes the exact named/versioned alert and cancels pending delivery. |
| `tenqual_get_document_resource` | Yes | No | No | `documents:read` | Returns an authenticated embedded MCP resource for an already-authorized clean document. |
| `tenqual_list_api_keys` | Yes | No | No | `integrations:read` | Reads non-secret API-key metadata. |
| `tenqual_prepare_api_key_creation` | No | No | No | `integrations:write` | Creates a short-lived, single-use private browser handoff; no credential is created or returned yet. |
| `tenqual_revoke_api_key` | No | Yes | No | `integrations:write` | Immediately revokes the exact named key after confirmation. |
| `tenqual_list_webhooks` | Yes | No | No | `integrations:read` | Reads non-secret webhook configuration and health. |
| `tenqual_prepare_webhook_creation` | No | No | No | `integrations:write` | Creates a short-lived, single-use private browser handoff; no signing secret is returned. |
| `tenqual_disable_webhook` | No | Yes | No | `integrations:write` | Immediately disables the exact named webhook after confirmation. |
| `tenqual_set_alert_integration_delivery` | No | Yes | Yes | `integrations:write` | Overwrites future API/webhook delivery routing for one alert after explicit confirmation. |

Identifiers and cursors returned by the tools are limited to values needed for a follow-up
operation, pagination, or retrieval. Dates are returned only when needed to interpret
publication deadlines, alert freshness, delivery order, credential status, or quota periods.
