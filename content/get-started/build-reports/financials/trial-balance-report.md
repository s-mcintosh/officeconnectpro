---
title: "Build a Trial Balance Report with OfficeConnect (Financials)"
linkTitle: "Trial Balance Report"
weight: 1
description: >
  Build a live trial balance in Excel using OfficeConnect's Financials data source — pulling posted GL actuals directly from Workday Financial Management.
tags: ["financials", "accounting", "reporting", "fpna", "tutorial"]
---

A trial balance lists every ledger account with its debit or credit balance for a given period. With OfficeConnect's Financials data source, you can build one that refreshes directly from Workday Financial Management — no export, no copy-paste.

**What you'll build:** A trial balance report showing all ledger accounts grouped by type (Assets, Liabilities, Equity, Revenue, Expenses) for a selected company and period.

**What you'll need:**
- OfficeConnect installed and connected to a tenant configured for the **Financials data source** (not Adaptive Planning)
- Access to at least one company with posted journal entries in Workday Financial Management
- The [Financials vs. Adaptive Planning](/get-started/migration-comparison/financials-vs-adaptive-planning/) page explains the difference if you're unsure which data source you have

---

## Step 1 — Confirm your data source

{{< step n="1" title="Check your data source" >}}
Click the **OfficeConnect** tab in Excel and sign in. In the Reporting pane, look at the top of the element tree. If you see **Ledger Accounts** and **Company**, you're on the Financials data source. If you see **Accounts** and **Levels**, you're on Adaptive Planning. This tutorial requires the Financials data source.
{{< /step >}}

---

## Step 2 — Add Company and Period context

{{< step n="2" title="Add your Company element" >}}
Click **B1**. In the Reporting pane, expand **Company** and drag your company (legal entity) into B1. If you have multiple companies, start with one — you can add more later.
{{< /step >}}

{{< step n="3" title="Add your Version" >}}
Click **B2**. In the Reporting pane, expand **Versions** and drag **Actuals** into B2.
{{< /step >}}

{{< step n="4" title="Add your Period" >}}
Click **B3**. In the Reporting pane, expand **Time** and drag the period you want (e.g., December 2025) into B3. For a year-end trial balance, use the last period of your fiscal year.
{{< /step >}}

---

## Step 3 — Add ledger account rows

{{< step n="5" title="Add an Assets section header" >}}
Click **A5** and type `ASSETS`. Bold it. This is a plain Excel label — not an OfficeConnect element.
{{< /step >}}

{{< step n="6" title="Add asset ledger accounts" >}}
Click **A6**. In the Reporting pane, expand **Ledger Accounts → Assets** (or the equivalent group in your chart of accounts). Drag your first asset account (e.g., Cash) into A6. Continue adding asset accounts in A7, A8, etc.
{{< /step >}}

{{< step n="7" title="Add the data formula for assets" >}}
Click **B6**. The OfficeConnect formula references the company in B1, the version in B2, and the period in B3. Copy B6 down for all asset account rows.
{{< /step >}}

{{< step n="8" title="Repeat for Liabilities, Equity, Revenue, Expenses" >}}
Add section headers and ledger account rows for each account type. Copy the data formula from column B into each new row — OfficeConnect picks up the ledger account from column A automatically.
{{< /step >}}

---

## Step 4 — Add subtotals

{{< step n="9" title="Add SUM rows for each section" >}}
Below each account group, add an Excel SUM row. For example, if your asset accounts are in B6:B12, add `=SUM(B6:B12)` in B13 with the label **Total Assets** in A13. Repeat for each section.
{{< /step >}}

{{< step n="10" title="Add a balance check" >}}
At the bottom of the report, add a row labeled **Out of Balance** with the formula:
```
=TotalAssets - (TotalLiabilities + TotalEquity)
```
This should equal zero for a balanced trial balance. If it doesn't, there are unposted or missing journals in Workday for this period.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Refresh the report" >}}
Click **Refresh** in the OfficeConnect ribbon. All ledger account rows populate with balances from Workday Financial Management.
{{< /step >}}

{{< step n="12" title="Verify the balance check" >}}
Confirm the Out of Balance cell shows zero (or near-zero for rounding). If it's non-zero, check that all ledger accounts are included and that your period is fully closed in Workday.
{{< /step >}}

---

## Next steps

- Drill into any balance to see the contributing journal lines — see [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/)
- Add prior-period columns for comparison — see [Build an Actuals Trend Report](/get-started/build-reports/financials/actuals-trend-report/)
- Filter to a specific cost center — see [Report on Actuals by Cost Center](/get-started/build-reports/financials/actuals-by-cost-center/)
