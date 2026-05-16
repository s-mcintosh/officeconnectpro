# Content Plan — Batch 2

**Date:** 2026-05-16
**Goal:** Extend officeconnectpro.com with 16 additional high-value articles covering data entry, financial statements, month-end close, automation, and an expanded troubleshoot section.

---

## Strategy

Same approach as Batch 1: use-case led, targeting specific search queries. Two audiences (FP&A on Adaptive Planning, Accounting on Financials), mix of tutorials and how-tos.

New in Batch 2:
- **Data entry / writeback** — entering data back to Adaptive Planning from OfficeConnect (underserved, high value)
- **Financial statements** — balance sheet and cash flow for accounting teams
- **Month-end close workflow** — practical, time-sensitive use case
- **Automation** — Power Automate integration for scheduled refresh
- **Troubleshoot expansion** — the four most-searched OfficeConnect error scenarios

---

## Content Structure

### FP&A — Adaptive Planning (6 articles)
Articles live under `content/build-reports/` (existing section). Weights continue from Batch 1 (which ended at 27); Batch 2 starts at 28.

| Type | Title | Slug | Weight |
|---|---|---|---|
| Tutorial | Enter Budget Data in Excel with OfficeConnect | `enter-budget-data` | 28 |
| Tutorial | Build a Formatted Executive Report for Distribution | `formatted-executive-report` | 29 |
| How-to | Refresh Reports Automatically with Power Automate | `refresh-with-power-automate` | 30 |
| How-to | Work with Custom Dimensions and Attributes | `custom-dimensions-attributes` | 31 |
| How-to | Optimize Performance for Large Models | `optimize-performance` | 32 |
| How-to | Use OfficeConnect on Mac | `officeconnect-on-mac` | 33 |

### Accounting — Financials (6 articles)
Articles live under `content/build-reports/financials/`. Weights continue from Batch 1 (which ended at 8); Batch 2 starts at 9.

| Type | Title | Slug | Weight |
|---|---|---|---|
| Tutorial | Build a Balance Sheet with OfficeConnect (Financials) | `balance-sheet-report` | 9 |
| Tutorial | Build a Cash Flow Statement with OfficeConnect (Financials) | `cash-flow-statement` | 10 |
| Tutorial | Month-End Close Workflow with OfficeConnect | `month-end-close-workflow` | 11 |
| How-to | Variance Analysis by Journal Source | `variance-by-journal-source` | 12 |
| How-to | Report on Worktag Combinations | `worktag-combinations` | 13 |
| How-to | Reconcile OfficeConnect Values to Workday Reports | `reconcile-to-workday` | 14 |

### Troubleshoot expansion (4 articles)
Articles live under `content/troubleshoot/`. Existing articles use weights 1–12 (approx); new articles start at 20.

| Type | Title | Slug | Weight |
|---|---|---|---|
| How-to | Fix OfficeConnect Not Refreshing | `not-refreshing` | 20 |
| How-to | Fix Authentication and Token Errors | `authentication-token-errors` | 21 |
| How-to | Fix Slow Performance in Large Reports | `slow-performance` | 22 |
| How-to | Fix Data Discrepancies Between OfficeConnect and Workday | `data-discrepancies` | 23 |

---

## Article Standards

Same as Batch 1:

### Tutorials
- Front matter: `title`, `linkTitle`, `weight`, `description` (SEO meta)
- "What you'll build" intro sentence
- "What you'll need" prerequisites block
- Numbered steps using `{{< step n="N" title="Title" >}}` shortcode
- Next steps section with 2–3 links

### How-to guides
- Front matter: same as tutorials
- Plain numbered prose (no `step` shortcode)
- One note or tip callout where relevant
- Related links at the end

### Troubleshoot articles
- Front matter: title written as the exact symptom (e.g., "Fix OfficeConnect Not Refreshing") for SEO
- "Symptom" section — what the user sees
- "Causes" section — common root causes
- Numbered fix steps for each cause
- "If none of these work" escalation path (contact Workday support / check version)

---

## Existing Troubleshoot Weights

Check `content/troubleshoot/` weights before writing to confirm 20+ is safe and doesn't conflict. Existing articles are at weights 1–12 range.

---

## Source Material

- **FP&A articles:** Workday Adaptive Planning Documentation PDF (locally available at `~/Downloads/Workday-Adaptive-Planning-Documentation.pdf`)
- **Financials articles:** Admin Guide Financial Management PDF (locally available at `~/Downloads/Admin-Guide--Financial-Management.pdf`)
- **Troubleshoot articles:** Source from existing troubleshoot patterns on the site + Workday documentation

---

## Success Criteria

- All 16 articles published and reachable from the sidebar
- Troubleshoot articles use symptom-first titles for SEO
- No duplication with Batch 1 or existing content
- Each tutorial includes next-steps linking to at least 2 related articles
- Every article has a populated `description:` field
