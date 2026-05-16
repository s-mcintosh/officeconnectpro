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

## Tags

All articles (Batch 2 new articles AND all 16 Batch 1 articles retroactively) get 2–4 tags in front matter:

```yaml
tags: ["adaptive-planning", "tutorial", "reporting"]
```

Hugo generates `/tags/<tag>/` index pages automatically. Docsy's offline search indexes them.

### Tag definitions

| Tag | When to use |
|---|---|
| `adaptive-planning` | Any FP&A / Adaptive Planning article |
| `financials` | Any Workday Financial Management / GL article |
| `tutorial` | End-to-end walkthrough articles |
| `how-to` | Task-focused shorter articles |
| `troubleshoot` | Troubleshoot section articles |
| `data-entry` | Articles covering writeback / input |
| `currency` | Multi-currency, constant currency articles |
| `reporting` | General reporting articles |
| `sharing` | Distribution, Teams, SharePoint articles |
| `administration` | IT admin / setup articles |

### Tag assignments — Batch 1 (retroactive)

| Article | Tags |
|---|---|
| budget-vs-actuals-variance | `adaptive-planning`, `tutorial`, `reporting` |
| department-pl-report | `adaptive-planning`, `tutorial`, `reporting` |
| year-over-year-trend | `adaptive-planning`, `tutorial`, `reporting` |
| compare-planning-versions | `adaptive-planning`, `how-to`, `reporting` |
| headcount-in-financial-report | `adaptive-planning`, `how-to`, `reporting` |
| lock-protect-reports | `adaptive-planning`, `how-to`, `sharing` |
| scenario-comparison | `adaptive-planning`, `how-to`, `reporting` |
| constant-currency-reporting | `adaptive-planning`, `how-to`, `currency` |
| financials/trial-balance-report | `financials`, `tutorial`, `reporting` |
| financials/drill-through-journal-lines | `financials`, `tutorial`, `reporting` |
| financials/actuals-trend-report | `financials`, `tutorial`, `reporting` |
| financials/actuals-by-cost-center | `financials`, `how-to`, `reporting` |
| financials/effective-date-reporting | `financials`, `how-to`, `reporting` |
| financials/filter-by-company | `financials`, `how-to`, `reporting` |
| financials/intercompany-eliminations | `financials`, `how-to`, `reporting` |
| financials/multi-currency-financials | `financials`, `how-to`, `currency` |

### Tag assignments — Batch 2 (new articles)

| Article | Tags |
|---|---|
| enter-budget-data | `adaptive-planning`, `tutorial`, `data-entry` |
| formatted-executive-report | `adaptive-planning`, `tutorial`, `reporting`, `sharing` |
| refresh-with-power-automate | `adaptive-planning`, `how-to`, `reporting` |
| custom-dimensions-attributes | `adaptive-planning`, `how-to`, `reporting` |
| optimize-performance | `adaptive-planning`, `how-to`, `reporting` |
| officeconnect-on-mac | `adaptive-planning`, `how-to` |
| financials/balance-sheet-report | `financials`, `tutorial`, `reporting` |
| financials/cash-flow-statement | `financials`, `tutorial`, `reporting` |
| financials/month-end-close-workflow | `financials`, `tutorial`, `reporting` |
| financials/variance-by-journal-source | `financials`, `how-to`, `reporting` |
| financials/worktag-combinations | `financials`, `how-to`, `reporting` |
| financials/reconcile-to-workday | `financials`, `how-to`, `reporting` |
| troubleshoot/not-refreshing | `troubleshoot`, `how-to` |
| troubleshoot/authentication-token-errors | `troubleshoot`, `how-to`, `administration` |
| troubleshoot/slow-performance | `troubleshoot`, `how-to` |
| troubleshoot/data-discrepancies | `troubleshoot`, `how-to`, `reporting` |

---

## Article Standards

Same as Batch 1 plus tags in every front matter block:

### Tutorials
- Front matter: `title`, `linkTitle`, `weight`, `description`, `tags`
- "What you'll build" intro sentence
- "What you'll need" prerequisites block
- Numbered steps using `{{< step n="N" title="Title" >}}` shortcode
- Next steps section with 2–3 links

### How-to guides
- Front matter: `title`, `linkTitle`, `weight`, `description`, `tags`
- Plain numbered prose (no `step` shortcode)
- One note or tip callout where relevant
- Related links at the end

### Troubleshoot articles
- Front matter: title written as the exact symptom (e.g., "Fix OfficeConnect Not Refreshing") for SEO, plus `tags`
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

- All 16 Batch 1 articles retroactively tagged
- All 16 Batch 2 articles published with tags, reachable from sidebar
- Tag index pages auto-generated by Hugo at `/tags/<tag>/`
- Troubleshoot articles use symptom-first titles for SEO
- No duplication with Batch 1 or existing content
- Each tutorial includes next-steps linking to at least 2 related articles
- Every article has a populated `description:` field
