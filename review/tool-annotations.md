# MCP tool annotation rationale

The production MCP server is authoritative. Re-scan it before every submission or version update.

| Tools | Read only | Destructive | Open world | Rationale |
| --- | --- | --- | --- | --- |
| Connection, tender search/detail, matches, alerts, usage, document availability, delivery events, alert-draft status, estimates, API-key listings, webhook listings | Yes | No | No | Retrieve workspace-scoped data without changing external state. |
| Create document download | Yes | No | No | Creates no persistent record; returns a ten-minute URL for an already-authorized clean document. |
| Draft alert | No | No | Yes | Persists a draft and may inspect the explicitly supplied company website; it cannot activate delivery. |
| Create or update alert | No | No | Yes | Changes a workspace alert and may activate future email or webhook delivery. |
| Delete alert | No | Yes | No | Soft-deletes the named alert and cancels pending deliveries after exact-name and version confirmation. |
| Prepare API-key or webhook creation | Yes | No | No | Returns an authenticated Tenqual review URL only; it creates no credential and returns no secret. |
| Revoke API key or disable webhook | No | Yes | No | Immediately removes credential or delivery capability after exact-name confirmation. |
| Set alert integration delivery | No | No | Yes | Changes whether future match and document-ready events are sent to subscribed external endpoints. |

Identifiers and cursors returned by the tools are limited to values required for a follow-up operation, pagination, deduplication, or retrieval. Dates are returned only when needed to interpret publication deadlines, alert freshness, delivery order, credential status, or quota periods.
