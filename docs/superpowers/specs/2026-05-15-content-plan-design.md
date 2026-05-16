# Content Plan — Batch 1

**Date:** 2026-05-15
**Goal:** Establish officeconnectpro.com as the best resource on the internet for Workday OfficeConnect by publishing 16 high-value articles targeting real FP&A and Accounting use cases.

---

## Strategy

**Approach:** Use-case led. Each article targets a specific task a user would search for. Titles map directly to search queries. Every article is standalone and shareable.

**Audiences:**
- **FP&A teams** using OfficeConnect with the Adaptive Planning data source (budget, forecast, variance, headcount)
- **Accounting teams** using OfficeConnect with the Financials data source (GL actuals, drill-through, month-end close)

**Content mix:** Tutorials (end-to-end walkthroughs, 800–1500 words) and how-to guides (task-focused, 300–500 words). Tutorials target high-value scenarios; how-tos cover supporting tasks around them.

---

## Content Structure

### FP&A — Adaptive Planning data source
Articles live under `content/build-reports/` (existing section).

| Type | Title | Slug |
|---|---|---|
| Tutorial | Build a Budget vs. Actuals Variance Report | `budget-vs-actuals-variance` |
| Tutorial | Build a Department P&L Report in OfficeConnect | `department-pl-report` |
| Tutorial | Build a Year-over-Year Trend Report | `year-over-year-trend` |
| How-to | Compare Two Planning Versions Side by Side | `compare-planning-versions` |
| How-to | Add Headcount Data to a Financial Report | `headcount-in-financial-report` |
| How-to | Lock and Protect Reports for Distribution | `lock-protect-reports` |
| How-to | Set Up Scenario Comparison in OfficeConnect | `scenario-comparison` |
| How-to | Report in Constant Currency in OfficeConnect | `constant-currency-reporting` |

### Accounting — Financials data source
Articles live under a new `content/build-reports/financials/` subsection to keep the two audiences clearly separated in the sidebar.

| Type | Title | Slug |
|---|---|---|
| Tutorial | Build a Trial Balance Report with OfficeConnect (Financials) | `trial-balance-report` |
| Tutorial | Drill Through to Workday Journal Lines from OfficeConnect | `drill-through-journal-lines` |
| Tutorial | Build an Actuals Trend Report (vs. Workday Report Writer) | `actuals-trend-report` |
| How-to | Report on Actuals by Cost Center | `actuals-by-cost-center` |
| How-to | Use Effective Date Reporting After a Reorganization | `effective-date-reporting` |
| How-to | Filter Reports by Company | `filter-by-company` |
| How-to | Report on Intercompany Eliminations | `intercompany-eliminations` |
| How-to | Multi-Currency Reporting with the Financials Data Source | `multi-currency-financials` |

---

## Article Standards

### Tutorials
- **Front matter:** `title`, `linkTitle`, `weight`, `description` (for SEO meta)
- **Intro:** "What you'll build" — one sentence describing the finished output
- **Prerequisites:** What-you'll-need block using existing `admin-note` shortcode where admin access is required
- **Video placeholder:** Comment block for future YouTube embed
- **Steps:** Numbered using the existing `step` shortcode
- **Next steps:** 2–3 links to related articles at the end

### How-to guides
- **Front matter:** same as tutorials
- **No video placeholder** — these are short enough that text suffices
- **Steps:** Numbered prose, no `step` shortcode (keeps them lightweight)
- **One "Note" or "Tip" callout** where a common mistake or non-obvious behavior warrants it

### SEO
- Page `description:` field populated on every article (Docsy uses it as the meta description)
- Titles written as the search query a user would type, not a product-manual heading
- Exact error messages or UI label names used verbatim where relevant

---

## New Sidebar Section: Financials

Create `content/build-reports/financials/_index.md` with:
- `title: "Financials Data Source"`
- `description`: one-sentence explanation that this section covers OfficeConnect with the Workday Financials (GL actuals) data source, distinct from Adaptive Planning
- Link to the existing [Financials vs. Adaptive Planning](/build-reports/financials-vs-adaptive-planning/) comparison page

---

## Source Material

- **Adaptive Planning articles:** Source from `Workday-Adaptive-Planning-Documentation.pdf` (locally available)
- **Financials articles:** Source from `Admin-Guide--Financial-Management.pdf` (locally available)
- **Both:** Cross-reference existing site content to avoid duplication and link to related pages

---

## Success Criteria

- All 16 articles published and reachable from the sidebar
- Every article has a populated `description:` for SEO
- Financials subsection is clearly separated in the sidebar
- No duplication with existing content (rolling 12-month, data source comparison page, SSO guide)
- Each tutorial includes a next-steps block linking to at least 2 related articles
