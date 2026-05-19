---
title: "Build a 13-Week Cash Forecast"
linkTitle: "13-Week Cash Forecast"
weight: 49
description: >
  Build a rolling 13-week cash forecast — weekly receipts, disbursements, and ending balance — in the treasury-standard format used for liquidity planning.
tags: ["reporting", "adaptive-planning", "fpna", "recipe"]
---

The 13-week cash forecast is the treasury team's most-used artifact. It projects weekly cash inflows and outflows over a rolling window so leadership can see liquidity coming weeks before it arrives — or fails to. This tutorial walks through building one in Workday OfficeConnect against a model with weekly cash forecasting enabled.

**What you'll build:** A treasury-format report with 13 weekly columns showing Beginning Balance, Receipts (by category), Disbursements (by category), Net Cash Flow, and Ending Balance — refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- A model configured with weekly time granularity for cash accounts
- Cash flow accounts broken into Receipts (AR collections, other inflows) and Disbursements (Payroll, AP, Tax, Debt Service, CapEx, Other)
- An opening cash balance loaded for the first week
- Familiarity with time contexts ([Time and Contexts](/build-reports/time-and-contexts/))

---

## Step 1 — Set up the weekly columns

{{< step n="1" title="Add the week headers" >}}
On a blank sheet, click **B1** and drag **Current Week** from the **Time → Relative Periods** group. Continue across C1:N1 for **Current Week +1** through **Current Week +12**. You should now have 13 column headers spanning the rolling 13-week window.
{{< /step >}}

{{< step n="2" title="Apply a short date format" >}}
Format B1:N1 with a custom format like `WE mm/dd` so the columns read as the week-ending dates. This is the treasury convention.
{{< /step >}}

---

## Step 2 — Build the cash flow row structure

{{< step n="3" title="Lay out the row labels" >}}
In column A, type the structure: `Beginning Balance`, a `Receipts:` header, `AR Collections`, `Other Receipts`, `Total Receipts`, a `Disbursements:` header, `Payroll`, `AP Payments`, `Tax`, `Debt Service`, `CapEx`, `Other Disbursements`, `Total Disbursements`, `Net Cash Flow`, and `Ending Balance`.
{{< /step >}}

{{< step n="4" title="Pull the opening cash balance" >}}
In the Beginning Balance row at column B (the first week), drag the **Cash** balance account scoped to the period just before the current week. This is the starting point of the forecast.
{{< /step >}}

---

## Step 3 — Populate receipts and disbursements

{{< step n="5" title="Map accounts to receipt rows" >}}
In the AR Collections row, drag the **AR Collections** account into column B and copy across B:N. Repeat for Other Receipts. Each cell resolves to the forecasted amount for that week.
{{< /step >}}

{{< step n="6" title="Total receipts" >}}
In the Total Receipts row, write `=SUM(B[AR Collections]:B[Other Receipts])` and copy across. This is the weekly cash inflow total.
{{< /step >}}

{{< step n="7" title="Map and total disbursements" >}}
Drag the matching account into each disbursement row (Payroll, AP, Tax, Debt Service, CapEx, Other) and copy each across B:N. In Total Disbursements, write `=SUM(B[Payroll]:B[Other Disbursements])` and copy across. Disbursements are stored as positive values in the model and subtracted later in Net Cash Flow.
{{< /step >}}

---

## Step 4 — Compute Net Cash Flow and Ending Balance

{{< step n="8" title="Net Cash Flow" >}}
In Net Cash Flow, write `=B[Total Receipts] - B[Total Disbursements]` and copy across. This is the weekly change in cash.
{{< /step >}}

{{< step n="9" title="Ending Balance" >}}
In Ending Balance at column B, write `=B[Beginning Balance] + B[Net Cash Flow]`. From C onward, last week's ending becomes this week's beginning — write `=B[Ending Balance] + C[Net Cash Flow]` and copy across C:N. Optionally, link the Beginning Balance row from week 2 forward to the prior week's ending.
{{< /step >}}

{{< admin-note >}}
Treasury teams often add `Minimum Cash` and `Headroom` rows under Ending Balance to show the cushion above a covenant or operating minimum. CFOs read the Headroom row first — the gap to the floor matters more than the absolute level.
{{< /admin-note >}}

---

## Step 5 — Refresh, format, and stress-test

{{< step n="10" title="Refresh and validate" >}}
Click **Refresh**. The 13-week grid populates. Spot-check week 1's Ending Balance against your bank reconciliation — if it ties at week 1, the rest is arithmetic.
{{< /step >}}

{{< step n="11" title="Stress-test with a scenario" >}}
Drop a second copy of the report on another tab and swap the version to a downside scenario (collections delayed 30 days, for example). Compare Ending Balances side by side. Cross-version comparisons are covered in [Scenario Comparison](/build-reports/scenario-comparison/).
{{< /step >}}

---

## Result

You now have a rolling 13-week cash forecast that updates automatically each Monday. Treasury sees the runway week by week; the CFO sees whether the next covenant test is comfortable or tight. The report holds its shape week after week — only the data refreshes.

## Next steps

- Pair the cash forecast with the period close cash flow statement — see [Cash Flow Statement](/build-reports/financials/cash-flow-statement/)
- Make the rolling-period mechanic do the same job for monthly views — see [Rolling 12-Month Report](/build-reports/rolling-12-month-report/)
- Run downside scenarios alongside the base case — see [Scenario Comparison](/build-reports/scenario-comparison/)
