---
title: "Build a Cohort Revenue Retention Report"
linkTitle: "Cohort Revenue Retention"
weight: 47
description: >
  Build a SaaS cohort retention report — revenue by signup cohort, retained revenue by month, and net revenue retention percentage — using repeating rows.
tags: ["reporting", "adaptive-planning", "fp-and-a", "recipe"]
---

For SaaS and subscription businesses, cohort retention is the most important diagnostic in the model — it answers whether customers are staying and expanding. This tutorial walks through building a Workday OfficeConnect cohort revenue retention report with one row per signup cohort, retained revenue across each subsequent month, and a net revenue retention (NRR) percentage at the right edge.

**What you'll build:** A triangular cohort matrix showing each signup cohort's starting revenue across its starting month and every subsequent month, with NRR computed at the 12-month mark.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- A model with a **Signup Cohort** custom dimension (for example, monthly cohorts: `2024-01`, `2024-02`, etc.)
- A subscription revenue account dimensionalized by cohort
- Familiarity with custom dimensions ([Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/)) and repeating rows ([Repeating Reports](/build-reports/repeating-reports/))

---

## Step 1 — Lay out the cohort grid

{{< step n="1" title="Add the period columns" >}}
On a blank sheet, label B1 `M0`, C1 `M1`, D1 `M2`, and so on through `M12`. These represent months since the cohort started — not calendar months. They're the column dimension of the cohort triangle.
{{< /step >}}

{{< step n="2" title="Add cohort labels in column A" >}}
In column A, list each cohort by its start month: `2024-01`, `2024-02`, `2024-03`, etc. Each row is one signup cohort.
{{< /step >}}

---

## Step 2 — Populate the M0 column

{{< step n="3" title="Drag the cohort dimension into a row" >}}
Click B2 (the M0 cell for the first cohort). In the Reporting pane, drag the **Subscription Revenue** account in, then filter it on the **Signup Cohort = 2024-01** dimension value and the time context set to that cohort's start month (January 2024).
{{< /step >}}

{{< step n="4" title="Repeat for every cohort" >}}
For B3, B4, B5, etc., do the same — each cohort row filters on its own cohort and resolves against its own start month for M0. This is the starting revenue baseline for each cohort.
{{< /step >}}

---

## Step 3 — Build the retention columns

{{< step n="5" title="Add M1 for each cohort" >}}
In C2 (M1 for the 2024-01 cohort), drag the same Subscription Revenue account, filter on **Signup Cohort = 2024-01**, but advance the time context one month (February 2024). This is revenue from the 2024-01 cohort one month after signup.
{{< /step >}}

{{< step n="6" title="Use repeating rows to scale" >}}
Rather than building this matrix cohort by cohort manually, configure the row block as a repeating row scoped on the **Signup Cohort** dimension, with each column resolving to *cohort start month + N*. OfficeConnect generates one row per cohort on refresh. The full pattern is covered in [Repeating Reports](/build-reports/repeating-reports/).
{{< /step >}}

{{< admin-note >}}
The cohort grid is triangular — recent cohorts only have a few months of history. Use conditional formatting to color empty future cells light gray so reviewers can tell at a glance which zeros are simply "not yet."
{{< /admin-note >}}

---

## Step 4 — Compute retention percentages

{{< step n="7" title="Add a second cohort block as percentages" >}}
Below the dollar matrix, repeat the same cohort structure but in each cell write `=B2/$B2` (the cohort's M-N revenue divided by its M0 revenue). Format as percentage. This is the retention curve — typically starting at 100% for M0 and trending up (expansion) or down (churn) over time.
{{< /step >}}

{{< step n="8" title="Add the NRR column" >}}
In a column labeled `NRR @ M12`, write `=M2/$B2` for each cohort (M12 revenue divided by M0 revenue). Above 100% is net expansion; below 100% is net contraction. Healthy SaaS businesses target 110%+ NRR.
{{< /step >}}

---

## Step 5 — Refresh and analyze

{{< step n="9" title="Refresh and read the diagonals" >}}
Click **Refresh**. The matrix populates. The diagonals show how cohorts of similar maturity compare — if recent cohorts have steeper drop-offs than older ones, retention is deteriorating.
{{< /step >}}

{{< step n="10" title="Add an average row" >}}
Below the matrix, add an `Average` row that computes a weighted average retention percentage per month-since-signup across all cohorts. This is the summary retention curve for the business.
{{< /step >}}

---

## Result

You now have a cohort retention report that surfaces subscription health in one view. Investors get the NRR percentage they ask for, the board gets the retention curve, and FP&A spots churn or expansion patterns months before top-line revenue reveals them.

## Next steps

- Build a top-line subscription revenue trend to pair with this — see [Year-over-Year Trend Report](/build-reports/year-over-year-trend/)
- Add scenario overlays for retention assumptions — see [Scenario Comparison](/build-reports/scenario-comparison/)
- Use repeating rows for other multi-dimension reports — see [Repeating Reports](/build-reports/repeating-reports/)
