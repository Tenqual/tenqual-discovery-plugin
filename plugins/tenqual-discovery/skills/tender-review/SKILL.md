---
name: tender-review
description: Review one tender notice and its available Tenqual documents for deadlines, requirements, risks, and next actions.
---

Use this skill when the user wants a structured review of a specific tender or opportunity.

## Procedure

1. Get the tender id from the user or from a prior Tenqual search result.
2. Call `tenqual_get_tender` for normalized tender metadata and the authoritative source link.
3. Call `tenqual_get_tender_documents` to inspect document availability when the tender is matched to the workspace.
4. Use `tenqual_get_document_resource` only when the user needs document content and the listed document is small enough for MCP transfer.
5. If Tenqual cannot provide documents because the tender is not a workspace match, explain that Tenqual retrieves documents for qualified workspace matches only. Use the tender's authoritative source link as the next step for manual document download, and mark document-dependent facts as unknown until the user provides the files or source text.
6. Extract and separate:
   - Buyer and procurement source.
   - Scope of work.
   - Submission deadline and important dates.
   - Eligibility, qualification, and compliance requirements.
   - Deliverables and response format.
   - Commercial or legal risks.
   - Open questions.
7. If a fact is not present in Tenqual or the authoritative source, say that it is not available.
8. Do not claim Tenqual or Claude can submit the bid.

## Output

Provide:

- Executive summary.
- Must-know facts.
- Requirements and risks.
- Recommended next actions.
- Source links and document references where available.
- A clear manual-download instruction when Tenqual documents are unavailable.
