---
name: bid-no-bid
description: Run a bid/no-bid assessment from Tenqual tender facts, documents, fit signals, risks, and required next decisions.
---

Use this skill when the user asks whether to pursue a tender or wants a procurement qualification assessment.

## Procedure

1. Identify the tender id and the user's company context. If company context is missing, ask for the minimum needed context: capabilities, geography, references, certifications, capacity, and deal-size preference.
2. Call `tenqual_get_tender` and, when available, `tenqual_get_tender_documents`.
3. Call `tenqual_list_matches` if the user wants the workspace's qualified Tenqual matches.
4. If Tenqual cannot provide documents because the tender is not a workspace match, explain the limitation in product terms: Tenqual retrieves documents for qualified workspace matches, while searchable non-matches should be checked through the authoritative source link. Do not treat this as a plugin failure.
5. Review available document content only when needed for evidence.
6. Score the opportunity across:
   - Strategic fit.
   - Technical fit.
   - Eligibility and compliance.
   - Delivery capacity.
   - Competitive position.
   - Commercial attractiveness.
   - Deadline feasibility.
   - Risk level.
7. Mark each score as evidence-backed, inferred, or unknown.
8. Produce a recommendation: Bid, Bid with conditions, No bid, or More information needed.
9. Include blocking questions that must be answered before a final decision.
10. When eligibility, requirements, pricing, contract terms, or submission instructions depend on unavailable documents, guide the user to download the documents from the authoritative source link and return with the files or extracted text.

## Safety

Do not treat inferred fit as proven. Do not override explicit procurement requirements. Original procurement-source documents remain authoritative.
