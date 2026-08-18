---
name: tender-search
description: Find relevant public procurement opportunities with Tenqual and summarize source-backed tender matches.
---

Use this skill when the user wants to search for tenders, discover opportunities, or inspect Tenqual matches.

## Procedure

1. If needed, call `tenqual_get_connection` to confirm the Tenqual workspace and scopes.
2. Translate the user's need into focused search terms. Prefer separate phrases in `terms` over punctuation-heavy query strings.
3. Call `tenqual_search_tenders` with the relevant query, terms, countries, sources, dates, and a modest limit.
4. If the user asks for workspace-qualified matches, call `tenqual_list_matches` instead of general search.
5. Present a short ranked list with title, buyer, country, source, deadline when available, fit rationale, and source link.
6. When a tender looks promising, call `tenqual_get_tender` before making substantive claims.
7. Treat original procurement sources as authoritative. Do not invent missing deadlines, requirements, budgets, or eligibility constraints.

## Output

Keep the first answer scannable:

- Best opportunities first.
- Separate known facts from interpretation.
- Mention uncertainty when the notice lacks detail.
- Offer to review one selected tender in depth.
