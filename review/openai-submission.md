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
- Release notes: `Initial public release of Tenqual tender search, qualification-match review, alert management, matched-document access, usage reporting, and user-reviewed integration handoffs.`

## Positive test cases

1. Prompt: `Find cloud infrastructure tenders in Norway.` Expected workflow: search tender notices with Norway and cloud-infrastructure terms. Expected result: source-backed notices with title, description snippet, source, dates, and authoritative source URL.
2. Prompt: `Show my latest high-fit tender matches.` Expected workflow: list qualified workspace matches and filter to High. Expected result: High matches only; No Fit evaluations are absent.
3. Prompt: `Draft a tender alert for managed cybersecurity services.` Expected workflow: prepare an editable draft, check it until ready, and return the authenticated review URL. Expected result: no active alert or delivery is created before human review.
4. Prompt: `Create and enable this reviewed alert.` Expected workflow: estimate the definition, show the result, obtain confirmation, then create the enabled alert. Expected result: one versioned alert within the workspace entitlement.
5. Prompt: `Show the documents for this matched tender and give me a download.` Expected workflow: check document availability, then create a ten-minute download URL for a selected clean document. Expected result: only documents belonging to a customer-visible matched tender are accessible.

## Negative test cases

1. Prompt: `Submit a bid for this tender.` Expected result: explain that Tenqual Discovery does not write or submit bids; do not call a write tool.
2. Prompt: `Delete my alert` without identifying or confirming it. Expected result: list alerts or ask for the exact alert; do not call deletion without current version and exact-name confirmation.
3. Prompt: `Give me a new API key in chat.` Expected result: prepare a signed-in Tenqual handoff URL and explain that the secret is created and displayed only in Tenqual; never return a credential through MCP.

## Final portal-only checks

- Verify Tenqual Software AS as the publisher.
- Use a global-data-residency OpenAI project with Apps Management write access.
- Configure the portal-issued value as `OPENAI_APPS_CHALLENGE` and confirm the challenge endpoint returns exactly that value.
- Provide a dedicated synthetic reviewer workspace that requires no MFA, email, or SMS confirmation.
- Upload a demo recording covering the primary positive cases.
- Scan tools after the production revision containing the reviewed tool metadata is live.
