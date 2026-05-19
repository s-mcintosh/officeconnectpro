---
title: "Build a Multi-Entity Consolidations Report"
linkTitle: "Multi-Entity Consolidations"
weight: 46
description: >
  Build a consolidated P&L across legal entities with intercompany eliminations called out as a separate column.
tags: ["financials", "reporting", "adaptive-planning", "fp-and-a", "recipe"]
---

Multi-entity consolidation is one of the harder reporting problems in finance — you need to roll up several legal entities, eliminate intercompany activity, and produce a view that ties to the consolidated P&L. This tutorial walks through building a consolidations report in Workday OfficeConnect that lays out each entity in its own column, calls out intercompany eliminations explicitly, and totals to a consolidated view.

**What you'll build:** A P&L report with one column per legal entity, a dedicated Eliminations column, and a Consolidated total column — all refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- A model with multiple legal entity Levels (for example, US Inc., UK Ltd., APAC Pte.)
- An Eliminations entity or Level configured in your model — see [Intercompany Eliminations](/build-reports/financials/intercompany-eliminations/)
- Familiarity with selecting Levels in the Reporting pane ([Add Elements](/build-reports/add-elements/))

---

## Step 1 — Set up the entity columns

{{< step n="1" title="Add a version and time" >}}
On a blank sheet, click **A1** and drag your **Actuals** version. Click **A2** and drag the time element you want to report on — typically the closing month or quarter.
{{< /step >}}

{{< step n="2" title="Add one column per entity" >}}
Click **B1** and drag your first legal entity Level (for example, **US Inc.**). Repeat across C1, D1, etc. for each additional entity (UK Ltd., APAC Pte., etc.). Each Level scopes the column beneath it to that entity's data.
{{< /step >}}

{{< step n="3" title="Add the Eliminations column" >}}
In the next column, drag the **Eliminations** Level or entity. This is the dedicated bucket that holds intercompany offsets — sales from US Inc. to UK Ltd. and the matching reductions that net to zero across the group.
{{< /step >}}

{{< step n="4" title="Add the Consolidated column" >}}
In the final column, drag the **Total Company** (or top-level rollup) Level. This column will show the consolidated result, which by definition equals the sum of entities plus eliminations.
{{< /step >}}

---

## Step 2 — Add account rows

{{< step n="5" title="List the P&L accounts" >}}
In column A, list the standard P&L lines: Revenue, Intercompany Revenue, COGS, Intercompany COGS, Gross Profit, Operating Expenses, EBITDA, Net Income.
{{< /step >}}

{{< step n="6" title="Drag the accounts into the first entity column" >}}
Click B3 and drag the Revenue account in. Repeat down for each P&L line. Then copy column B across to each entity column, the Eliminations column, and the Consolidated column. Every column shares the same row definitions and the same time, but resolves against a different Level.
{{< /step >}}

{{< admin-note >}}
Calling out Intercompany Revenue and Intercompany COGS on their own rows — separate from third-party Revenue and COGS — makes the eliminations column intuitive. Reviewers can see at a glance that the intercompany sales in the entity columns reverse out in Eliminations and net to zero in Consolidated.
{{< /admin-note >}}

---

## Step 3 — Verify the consolidation ties

{{< step n="7" title="Add a tie-out row" >}}
Below the Net Income row, add a row called `Tie Check`. Write a formula like `=SUM(B[entities])+B[Eliminations]-B[Consolidated]`. This should resolve to zero in every account. If it doesn't, an entity Level isn't included in the rollup, or an elimination is missing.
{{< /step >}}

{{< step n="8" title="Format eliminations distinctly" >}}
Apply a light gray fill to the Eliminations column so reviewers immediately recognize it as a non-operational adjustment. Italicize the intercompany row labels in column A.
{{< /step >}}

---

## Step 4 — Refresh and document

{{< step n="9" title="Refresh and validate" >}}
Click **Refresh**. Every entity column populates from Adaptive Planning. Spot-check the Consolidated Net Income against the official consolidated trial balance — see [Trial Balance Report](/build-reports/financials/trial-balance-report/) for the supporting view.
{{< /step >}}

{{< step n="10" title="Add a commentary column" >}}
Add a final column titled `Commentary` for explaining any unusual eliminations or one-time adjustments. Leave this column unprotected when you lock the sheet.
{{< /step >}}

---

## Result

You now have a consolidated P&L that any finance reviewer can read — entity by entity, with eliminations on their own line, totaling cleanly to the group result. The report refreshes with one click and ties to your consolidated trial balance, so close reviews stop turning into investigations of where a $50K intercompany variance came from.

## Next steps

- Dig into the elimination logic itself — see [Intercompany Eliminations](/build-reports/financials/intercompany-eliminations/)
- Pair this with a cash flow view — see [Cash Flow Statement](/build-reports/financials/cash-flow-statement/)
- Report in a single reporting currency across entities — see [Constant Currency Reporting](/build-reports/constant-currency-reporting/)
