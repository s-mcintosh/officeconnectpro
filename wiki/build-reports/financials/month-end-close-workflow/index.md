---
title: "Month-End Close Workflow with OfficeConnect"
url: "https://officeconnectpro.com/wiki/build-reports/financials/month-end-close-workflow/"
description: "Use OfficeConnect to run a faster month-end close — verify trial balances, check journal completeness, and produce final financial statements directly from Workday Financial Management.\n"
tags: ["financials","accounting","reporting","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Month-end close in Workday Financial Management involves verifying journal completeness, reconciling account balances, and producing financial statements for management review. OfficeConnect lets your accounting team do all of this in Excel — pulling live data from Workday — without waiting for Report Writer outputs or PDF exports. This tutorial walks through a practical close workflow.

**What you'll build:** A close workbook with a trial balance check sheet, a journal completeness check, and a summary P&L — all refreshable as the close progresses.

**What you'll need:**
- OfficeConnect connected to the **Financials** data source
- Workday Financial Management with the current period in a close-in-progress state
- Familiarity with trial balance reports — see [Build a Trial Balance Report](/wiki/build-reports/financials/trial-balance-report/)

---

## Step 1 — Build a trial balance check sheet

{{< step n="1" title="Set up a Trial Balance tab" >}}
Open a new Excel workbook. Rename **Sheet1** to `Trial Balance`. Click the OfficeConnect tab and sign in. In the Trial Balance tab, build a quick trial balance:

- **B1**: Actuals version (drag from Reporting pane)
- **B2**: Current close period (drag the month being closed, e.g., April 2026)
- **A5 downward**: Drag all P&L and balance sheet rollup accounts from the Reporting pane — Revenue, COGS, Operating Expenses, Assets, Liabilities, Equity sections
- **B5 downward**: Copy the formula from B5 down for each account row
{{< /step >}}

{{< step n="2" title="Add a debit/credit balance check" >}}
In a blank cell below your accounts (for example, **B30**), enter:
```
=SUMIF(B5:B29,">0",B5:B29)+SUMIF(B5:B29,"<0",B5:B29)
```
This sums all account balances. A balanced trial balance produces **0** — debits equal credits. If the result is non-zero, a journal entry is missing or was posted in error.

In **A30**, type `Balance Check` and apply conditional formatting to **B30**: green fill if the value equals 0, red fill otherwise. This gives a clear at-a-glance indicator during close.
{{< /step >}}

{{< step n="3" title="Click Refresh to check current state" >}}
Click **Refresh** in the OfficeConnect ribbon. All account balances populate from Workday as of the current close period. Review the Balance Check cell. If it's red, work with your accounting team to identify the missing or incorrect journal entry before proceeding.
{{< /step >}}

---

## Step 2 — Check journal entry completeness

{{< step n="4" title="Add a Journal Completeness tab" >}}
Add a new sheet tab named `Journal Check`. In this tab, build a list of recurring journal entries you expect every month — things like depreciation, prepaid amortization, accruals for payroll, and rent. In column A, list the description of each expected journal. In column B, pull the relevant account balance using OfficeConnect to confirm it posted.

For example, if depreciation should be approximately $15,000/month: drag the Depreciation account into a cell and check that the current month balance is close to the expected amount. Format the cell with conditional formatting to flag if the balance is 0 (meaning depreciation likely didn't post).
{{< /step >}}

{{< step n="5" title="Add accrual verification rows" >}}
For each significant accrual, add a row with:
- Column A: Accrual description (e.g., "Payroll Accrual — April")
- Column B: OfficeConnect formula pulling the accrued liability account balance
- Column C: Expected amount (typed as a static value or pulled from a budget/prior-month reference)
- Column D: Variance formula `=B-C` with conditional formatting to flag large differences

Refresh this tab after each batch of journal entries posts to confirm completeness progressively.
{{< /step >}}

---

## Step 3 — Produce financial statements for review

{{< step n="6" title="Add a Summary P&L tab" >}}
Add a new sheet named `P&L Summary`. Build a concise income statement using rollup accounts — Revenue, COGS, Gross Profit, Operating Expenses, EBITDA, and Net Income. Use the same Actuals version and close period you set up in the Trial Balance tab.

This sheet is what you share with management for their review sign-off before the period is locked in Workday.
{{< /step >}}

{{< step n="7" title="Add a prior-period comparison column" >}}
In the P&L Summary, add column C with the prior month's period. Drag the same close period as column B but set to the prior month. Add a Variance column (D) with the formula `=B-C`. This shows month-over-month movement — significant swings often reveal missing journals or timing errors worth investigating before close is finalized.
{{< /step >}}

{{< step n="8" title="Final refresh and review" >}}
Once all journals are posted in Workday and the trial balance check shows 0, click **Refresh** on all sheets. Review the P&L Summary for reasonableness. When the accounting team approves the figures, export the P&L Summary as PDF for the management review record.
{{< /step >}}

---

## Step 4 — Lock the period in Workday

{{< step n="9" title="Lock the period after sign-off" >}}
Period locking happens in Workday Financial Management, not in OfficeConnect. Once management has signed off on the financial statements:

{{< admin-note >}}
Go to Workday → **Financial Accounting** → **Close Accounting Period** (or the equivalent task in your Workday tenant). Lock the period to prevent further journal entries. After locking, your OfficeConnect workbook continues to show the final locked balances on refresh — no changes are needed to the workbook itself.
{{< /admin-note >}}
{{< /step >}}

---

## Next steps

- Build a full balance sheet for the close package — see [Build a Balance Sheet](/wiki/build-reports/financials/balance-sheet-report/)
- Drill into specific journal lines to investigate variances — see [Drill Through to Workday Journal Lines](/wiki/build-reports/financials/drill-through-journal-lines/)
- Reconcile final figures to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/wiki/build-reports/financials/reconcile-to-workday/)

