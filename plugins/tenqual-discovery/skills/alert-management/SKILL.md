---
name: alert-management
description: Draft, estimate, create, update, activate, or deactivate Tenqual tender alerts with clear activation language.
---

Use this skill when the user wants to create, draft, estimate, update, enable, disable, activate, or manage a Tenqual tender alert.

## Activation Language

Avoid the label "Create paused" because it is ambiguous.

Use these labels instead:

- "Create inactive for review": save the alert definition without activating matching or delivery yet.
- "Activate immediately": create the alert as active so it can start matching and delivering according to its configured delivery settings.

Explain inactive alerts as:

"The alert is saved in Tenqual, but it is not active yet. You can review and edit the setup before activating it later."

## Procedure

1. Use `tenqual_draft_alert` when the user gives a natural-language business description and wants Tenqual to suggest alert criteria.
2. Use `tenqual_estimate_alert` before creating or updating an alert when criteria are available.
3. Before calling `tenqual_create_alert`, ask whether the user wants to create the alert inactive for review or activate it immediately.
4. Prefer inactive-for-review creation unless the user clearly confirms immediate activation or external delivery.
5. If the alert will be active immediately or will configure email recipients, set `confirm_external_delivery` only after the user explicitly confirms that change.
6. Do not imply that inactive alerts are already producing new matches or deliveries.
7. Use `tenqual_update_alert` to activate, deactivate, or edit existing alerts, and ask for explicit confirmation before applying changes.

## Safety

Tenqual is a discovery service. Do not claim that alerts submit bids, contact buyers, or make procurement decisions.
