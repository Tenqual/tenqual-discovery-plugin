---
name: compliance-matrix
description: Build a compliance matrix from Tenqual tender metadata and available tender documents.
---

Use this skill when the user wants a requirements table, response checklist, or compliance matrix for a tender.

## Procedure

1. Get the tender id from the user or prior search context.
2. Call `tenqual_get_tender` for notice metadata.
3. Call `tenqual_get_tender_documents` to identify available documents.
4. Use `tenqual_get_document_resource` for the specific documents that appear likely to contain requirements, instructions, evaluation criteria, terms, or forms.
5. If Tenqual cannot provide documents because the tender is not a workspace match, explain that compliance matrices require source documents and direct the user to the authoritative source link for manual download. Create only a preliminary matrix from notice metadata, and mark document-dependent rows as needs review.
6. Build a matrix with one row per requirement or deliverable.
7. For each row, include:
   - Requirement id or short label.
   - Requirement text.
   - Source document or source link.
   - Section, page, or location if available.
   - Response owner.
   - Evidence needed.
   - Status: open, answered, blocked, not applicable, or needs review.
   - Risk notes.
8. If the source does not provide enough detail, mark the row as needs review rather than filling gaps from assumption.
9. End with the highest-risk requirements and missing information.

## Output

Prefer a compact markdown table for short matrices. For large matrices, summarize the structure first and ask whether the user wants a file-ready version.
