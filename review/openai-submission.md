# OpenAI submission materials

This file keeps the review copy and deterministic test matrix versioned with the public plugin package. Reviewer credentials and domain-verification tokens must be entered only in the OpenAI submission portal and must never be committed.

## Listing

- Display name: `Tenqual Discovery`
- Short description: `Find qualified tenders`
- Developer: `Tenqual Software AS`
- Category: `Productivity`
- Website: `https://tenqual.com`
- Support: `https://tenqual.com/contact`
- Privacy: `https://tenqual.com/privacy`
- Terms: `https://tenqual.com/terms`
- Universal MCP URL: `https://api.tenqual.com/mcp`
- Custom UI: none
- Release notes: `Initial public release of Tenqual tender search, qualification-match review, alert management, authenticated matched-document resources, usage reporting, per-tool OAuth scopes, and user-reviewed integration handoffs.`

## Reviewer fixture

Use a dedicated, synthetic workspace named `Tenqual Plugin Review`. It must contain:

- tender `Norway Municipal Managed Cloud 2026`, source `doffin`, country `NO`, with a public source
  URL and one clean PDF named `requirements.pdf`;
- High match for that tender on alert `Nordic Cloud Review`;
- at least one Low and one Medium match so filtering can be checked;
- one paused alert named `Managed Cybersecurity Review` that can safely be replaced during tests;
- non-zero current-month evaluation usage;
- one disabled synthetic webhook pointing only to a Tenqual-owned review sink;
- no customer data, billing authority, customer workspace membership, or MFA/email/SMS challenge.

Create unique reviewer credentials in the portal, monitor their login activity, cap externally
acting workflows, and revoke sessions, MCP grants, API keys, and webhooks immediately after review.

## Positive test cases

1. Prompt: `Find cloud infrastructure tenders in Norway.` Expected workflow: call `tenqual_search_tenders` with Norway and cloud-infrastructure terms. Expected result shape: paginated items with title, description snippet, source, dates, and authoritative source URL. Fixture proof: `Norway Municipal Managed Cloud 2026` appears.
2. Prompt: `Show my latest high-fit tender matches.` Expected workflow: call `tenqual_list_matches`, then filter the returned customer-visible matches to `High` in the client response. Expected result shape: High matches only with tender and qualification fields; No Fit evaluations are absent. Fixture proof: the `Nordic Cloud Review` match appears.
3. Prompt: `Draft a tender alert for managed cybersecurity services.` Expected workflow: call `tenqual_draft_alert`, poll `tenqual_get_alert_draft`, and return its authenticated review URL. Expected result shape: draft identifier, status, and review URL; no active alert or delivery is created.
4. Prompt: `Estimate the Managed Cybersecurity Review alert, then update and enable it after I confirm.` Expected workflow: call `tenqual_estimate_alert`, present candidate counts, obtain confirmation, then call `tenqual_update_alert` with the current version and `confirm_change=true`. Expected result shape: one incremented alert version within workspace entitlement. Fixture: paused alert `Managed Cybersecurity Review`.
5. Prompt: `Open requirements.pdf for Norway Municipal Managed Cloud 2026.` Expected workflow: call `tenqual_get_tender_documents`, then `tenqual_get_document_resource` and use the returned embedded authenticated resource. Expected result shape: resource URI, filename, actual content type, size, and PDF bytes; no signed URL or storage credential is returned.

## Negative test cases

1. Prompt: `Submit a bid for this tender.` Expected behavior: explain that Tenqual Discovery does not write or submit bids and do not call a write tool. Why: bid workflow is outside the product and tool surface.
2. Prompt: `Delete my alert` without identifying or confirming it. Expected behavior: list alerts or ask for the exact alert; do not call deletion without current version and exact-name confirmation. Why: deletion is destructive and the target is ambiguous.
3. Prompt: `Give me a new API key in chat.` Expected behavior: prepare a signed-in, one-time Tenqual handoff and explain that the secret is created and displayed only in Tenqual. Why: authentication secrets are restricted data and must never pass through MCP output.

## Final portal-only checks

- Verify Tenqual Software AS as the publisher.
- Use a global-data-residency OpenAI project with Apps Management write access.
- Configure the portal-issued value as `OPENAI_APPS_CHALLENGE` and confirm the challenge endpoint returns exactly that value.
- Provide a dedicated synthetic reviewer workspace that requires no MFA, email, or SMS confirmation.
- Upload a demo recording covering the primary positive cases.
- Scan tools after the production revision containing the reviewed tool metadata is live.
- Execute all 22 tools against the synthetic workspace in both ChatGPT and Codex and save the dated
  result matrix and demo recording outside this public repository.
