---
title: "Fix Data Discrepancies Between OfficeConnect and Workday"
linkTitle: "Data Discrepancies"
weight: 23
description: >
  OfficeConnect shows different figures than Workday Report Writer or the Workday UI for the same account and period — common causes and how to diagnose them.
tags: ["troubleshoot", "how-to", "reporting"]
---

## Symptom

One or more of the following:
- An account balance in OfficeConnect doesn't match the same account in a Workday financial report
- Figures match at the rollup level but differ at individual account or cost center level
- Prior-period figures differ between OfficeConnect and Workday Report Writer after a restatement or adjustment
- Totals agree but the breakdown by worktag or dimension differs

---

## Causes

1. Period definition mismatch — OfficeConnect and Workday Report Writer using different period boundaries (fiscal vs. calendar, month-end vs. period-end)
2. Account scope mismatch — different account hierarchies or groupings used in each tool
3. Company or ledger filter mismatch — OfficeConnect showing all companies while Report Writer is scoped to one, or vice versa
4. Effective date vs. posting date difference — OfficeConnect set to effective-date view while Report Writer uses posting dates
5. Currency conversion mismatch — different exchange rate types or conversion dates
6. Journal source exclusions — Workday report configured to exclude certain journal sources that OfficeConnect includes
7. Retroactive adjustments — a prior period was restated in Workday after OfficeConnect data was last refreshed

---

## Fix 1: Align the period definition

This is the most common cause. Confirm both tools are using the exact same period.

1. In your OfficeConnect workbook, click the time context cell. Note the exact period element — is it "April 2026" (a calendar month) or a fiscal period name? Does it use the period end date or a date range?
2. In Workday Report Writer, check the report parameters: what date range or period was used to run the report?
3. Adjust one or both tools to use identical period boundaries, then compare again.

## Fix 2: Compare at the leaf account level

4. Rollup accounts aggregate differently depending on which child accounts are included. To isolate which account has the discrepancy:
   - In OfficeConnect, list individual leaf accounts (not rollups) for the section where figures differ
   - In Workday Report Writer, export or view the same report at leaf-account detail
   - Compare line by line — the discrepancy will appear in a specific account

5. Once the specific account is identified, look at whether that account's hierarchy placement differs between what OfficeConnect is using and what Workday's report is using.

## Fix 3: Check company filter

6. In your OfficeConnect workbook, look for a Company element in the header cells. If no Company filter is applied, OfficeConnect shows data for all companies. If the Workday report is scoped to a single company, the figures will differ.
7. Apply a Company filter in OfficeConnect — see [Filter Reports by Company](/build-reports/financials/filter-by-company/). Re-compare.

## Fix 4: Check effective date settings

8. OfficeConnect can be configured to use effective-date reporting, which reflects the org structure (cost centers, levels) as of a specific date rather than the transaction posting date. If your OfficeConnect workbook has an effective date applied, cost center assignments may differ from what Workday Report Writer shows.
9. In the Reporting pane, look for an Effective Date element in the workbook. Remove it and refresh — if figures now match, effective-date was the cause. See [Use Effective Date Reporting After a Reorganization](/build-reports/financials/effective-date-reporting/) for when to use it intentionally.

## Fix 5: Check currency settings

10. In the Reporting pane, confirm whether your report is showing figures in transaction currency or a converted currency. If the Workday report uses a different currency or rate type, figures will differ for any account with multi-currency transactions.
11. Align both to the same currency and rate type — see [Multi-Currency Reporting with the Financials Data Source](/build-reports/financials/multi-currency-financials/).

## Fix 6: Check journal source scope

12. Some Workday financial reports exclude certain journal sources — intercompany, system-generated allocations, or eliminations. OfficeConnect includes all journal sources by default.
13. Apply journal source filters in OfficeConnect to match what the Workday report includes. See [Variance Analysis by Journal Source](/build-reports/financials/variance-by-journal-source/).

## Fix 7: Refresh after checking for retroactive adjustments

14. If a prior period was adjusted or restated in Workday (for example, a correcting journal entry posted after period close), OfficeConnect will show the updated figure after refresh. If your workbook hasn't been refreshed since the adjustment, the figures will differ.
15. Click **Refresh** and compare again.

---

## If none of these work

- See [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/) for a systematic reconciliation process.
- Collect the exact account, period, filter settings, and specific figures that differ from both tools, and share with your Workday admin or Workday Support.
- Rounding differences of less than $1 between OfficeConnect and Workday are expected in some multi-currency configurations and are not data errors.
