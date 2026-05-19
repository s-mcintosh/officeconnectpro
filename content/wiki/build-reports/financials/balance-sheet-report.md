---
title: "Build a Balance Sheet with OfficeConnect (Financials)"
linkTitle: "Balance Sheet"
weight: 9
description: >
  Build a formatted balance sheet in Excel using OfficeConnect's Financials data source — assets, liabilities, and equity drawn live from Workday Financial Management.
tags: ["financials", "accounting", "reporting", "fpna", "tutorial"]
---

A balance sheet in OfficeConnect pulls directly from Workday Financial Management's general ledger, so your assets, liabilities, and equity balances are always current without manual copy-paste from Workday Report Writer. This tutorial walks through building a structured balance sheet with the three standard sections.

**What you'll build:** A balance sheet workbook with Current Assets, Non-Current Assets, Current Liabilities, Non-Current Liabilities, and Equity sections — all refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect installed and connected to the **Financials** data source (not Adaptive Planning) ([Get Started](/wiki/))
- Workday Financial Management with balance sheet accounts (Assets, Liabilities, Equity) loaded with actuals
- Basic familiarity with the Financials data source — see [Build a Trial Balance Report](/wiki/build-reports/financials/trial-balance-report/)

---

## Step 1 — Set up the version and time context

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel, click the **OfficeConnect** tab, and sign in. Confirm the Reporting pane shows the **Financials** data source — you should see account types (Assets, Liabilities, Equity) rather than Adaptive Planning versions and levels.
{{< /step >}}

{{< step n="2" title="Add the version and period" >}}
Click cell **B1**. In the Reporting pane, expand **Versions** and drag **Actuals** into B1. Click **B2** and drag your reporting period (for example, the end of the current quarter) into it. Balance sheets are point-in-time, so choose a specific period end date rather than a range.
{{< /step >}}

---

## Step 2 — Build the Assets section

{{< step n="3" title="Add a section header for Current Assets" >}}
Click **A4** and type `CURRENT ASSETS`. Bold and apply an underline to make it a visual section header.
{{< /step >}}

{{< step n="4" title="Add Current Asset accounts" >}}
Click **A5**. In the Reporting pane, expand **Accounts → Assets → Current Assets**. Drag **Cash and Cash Equivalents** into A5. Continue in A6–A8 with **Accounts Receivable**, **Prepaid Expenses**, and **Other Current Assets**. In **A9**, drag the **Total Current Assets** rollup account.
{{< /step >}}

{{< step n="5" title="Add a section header for Non-Current Assets" >}}
Click **A11** and type `NON-CURRENT ASSETS`. Bold and underline.
{{< /step >}}

{{< step n="6" title="Add Non-Current Asset accounts" >}}
In A12–A14, drag **Property Plant and Equipment (Net)**, **Intangible Assets**, and **Other Non-Current Assets** from the Reporting pane. In **A15**, drag **Total Non-Current Assets**. In **A17**, drag **Total Assets** — the top-level rollup.
{{< /step >}}

{{< step n="7" title="Populate data cells for Assets" >}}
Click **B5**. OfficeConnect creates a formula for Actuals (B1), the period (B2), and Cash and Cash Equivalents (A5). Copy **B5** down through **B17**, skipping the section header rows (B4, B10, B11, B16). Each row resolves to the correct account balance.
{{< /step >}}

---

## Step 3 — Build the Liabilities section

{{< step n="8" title="Add Current Liabilities" >}}
Starting in **A20**, type `CURRENT LIABILITIES` (bold, underlined). In A21–A23, drag **Accounts Payable**, **Accrued Liabilities**, and **Other Current Liabilities**. In **A24**, drag **Total Current Liabilities**.
{{< /step >}}

{{< step n="9" title="Add Non-Current Liabilities" >}}
In **A26**, type `NON-CURRENT LIABILITIES`. In A27–A28, drag **Long-Term Debt** and **Other Non-Current Liabilities**. In **A29**, drag **Total Non-Current Liabilities**. In **A31**, drag **Total Liabilities**.
{{< /step >}}

{{< step n="10" title="Populate data cells for Liabilities" >}}
Click **B21** and copy the formula structure down through **B31**, matching the account rows you've built. Skip the header and spacer rows.
{{< /step >}}

---

## Step 4 — Build the Equity section

{{< step n="11" title="Add Equity accounts" >}}
In **A34**, type `EQUITY`. In A35–A37, drag **Common Stock**, **Retained Earnings**, and **Other Comprehensive Income (Loss)**. In **A38**, drag **Total Equity**.
{{< /step >}}

{{< step n="12" title="Add Total Liabilities and Equity" >}}
In **A40**, drag **Total Liabilities and Equity** — the top-level balance sheet rollup account. In **B40**, copy the formula structure from the rows above. This should equal Total Assets (B17) — the balance check.
{{< /step >}}

---

## Step 5 — Verify and format

{{< step n="13" title="Refresh and check the balance" >}}
Click **Refresh** in the OfficeConnect ribbon. All accounts populate. Verify that **B17** (Total Assets) equals **B40** (Total Liabilities and Equity). If they don't match, check that you've used the correct rollup accounts — the discrepancy usually means a leaf account is missing from one section.
{{< /step >}}

{{< step n="14" title="Format as a balance sheet" >}}
Format the number columns with Accounting format (no decimals). Bold the rollup rows (Total Current Assets, Total Non-Current Assets, Total Assets, Total Current Liabilities, Total Non-Current Liabilities, Total Liabilities, Total Equity, Total Liabilities and Equity). Add a double underline below Total Assets and Total Liabilities and Equity to follow standard balance sheet presentation.
{{< /step >}}

---

## Next steps

- Build a cash flow statement — see [Build a Cash Flow Statement](/wiki/build-reports/financials/cash-flow-statement/)
- Add prior-period comparison columns — see [Report on Actuals by Cost Center](/wiki/build-reports/financials/actuals-by-cost-center/)
- Reconcile balances to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/wiki/build-reports/financials/reconcile-to-workday/)
