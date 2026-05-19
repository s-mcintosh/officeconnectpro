---
title: "Build an Actuals Trend Report in OfficeConnect (Financials)"
linkTitle: "Actuals Trend Report"
weight: 3
description: >
  Build a 12-month GL actuals trend report in minutes — the same report that takes hours to configure in Workday's native report writer.
tags: ["financials", "accounting", "reporting", "fpna", "tutorial"]
---

Trending actuals across 12 months in Workday's native report writer means configuring a matrix report, setting up time period prompts, managing column layouts, and wrestling with formatting. In OfficeConnect, the same report takes about five minutes.

This tutorial shows you how — and explains why the difference matters for accounting teams who need monthly trend data on demand.

**What you'll build:** A 12-month actuals trend report showing GL account balances by period for a selected company, fully refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to a **Financials data source** tenant
- A company with at least several months of posted actuals in Workday Financial Management

---

## Why OfficeConnect vs. the Workday Report Writer

The Workday report writer is powerful but complex for time-series reporting. To build a 12-month trend report natively, you typically need to:

1. Create a matrix report with custom column definitions for each period
2. Configure time period prompts or hard-code the periods
3. Map the report to the correct financial data source
4. Run, export, and reformat in Excel

In OfficeConnect, you drag 12 time elements into a row and click Refresh. The data is live, the format is Excel, and there's no export step.

---

## Step 1 — Set up your context row

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel and click the **OfficeConnect** tab. Sign in and confirm you're on a Financials data source tenant (you'll see Ledger Accounts and Company in the Reporting pane).
{{< /step >}}

{{< step n="2" title="Add your Company" >}}
Click **B1**. In the Reporting pane, expand **Company** and drag your company into B1.
{{< /step >}}

{{< step n="3" title="Add your Version" >}}
Click **B2**. Drag **Actuals** from the Reporting pane into B2.
{{< /step >}}

---

## Step 2 — Add 12 monthly time columns

{{< step n="4" title="Add January" >}}
Click **B3**. In the Reporting pane, expand **Time → Months** and drag the first month of your trend period (e.g., Jan 2025) into B3.
{{< /step >}}

{{< step n="5" title="Add the remaining 11 months" >}}
Click **C3** through **M3** in turn, dragging each successive month (Feb 2025 through Dec 2025) into the cells. You now have a 12-month time header row.
{{< /step >}}

---

## Step 3 — Add ledger account rows

{{< step n="6" title="Add your first account" >}}
Click **A4**. In the Reporting pane, expand **Ledger Accounts** and drag your first account (e.g., Revenue or a specific expense account) into A4.
{{< /step >}}

{{< step n="7" title="Populate the data row" >}}
Click **B4**. OfficeConnect formulas reference the company in B1, the version in B2, and the time in B3, so B4 returns the Jan 2025 actuals for your account. Copy **B4** across to **M4** — each cell picks up its month from row 3 automatically.
{{< /step >}}

{{< step n="8" title="Add remaining account rows" >}}
Copy row 4 down for each additional ledger account. Add each new account to column A by dragging from the Reporting pane.
{{< /step >}}

---

## Step 4 — Add totals and formatting

{{< step n="9" title="Add a monthly total row" >}}
Below your last account row, add an Excel SUM row: `=SUM(B4:B[last row])` in column B, copied across to column M. Label it **Total** in column A.
{{< /step >}}

{{< step n="10" title="Format the header row" >}}
OfficeConnect time labels can be long. Select row 3 and apply a custom number format (`mmm-yy`) to display months as "Jan-25", "Feb-25", etc. — or type short labels in a separate row above row 3.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon. All 12 months populate with posted actuals from Workday Financial Management.
{{< /step >}}

{{< step n="12" title="Spot-check a value" >}}
Pick one account and one month. Compare the value in your report against the same account/period in a Workday report or the trial balance for that month. They should match exactly — OfficeConnect reads the same posted data.
{{< /step >}}

---

## Next steps

- Drill into any cell to see contributing journal lines — see [Drill Through to Workday Journal Lines](/wiki/build-reports/financials/drill-through-journal-lines/)
- Add a prior-year comparison column — see [Compare Two Planning Versions Side by Side](/wiki/build-reports/compare-planning-versions/)
- Filter by cost center — see [Report on Actuals by Cost Center](/wiki/build-reports/financials/actuals-by-cost-center/)
