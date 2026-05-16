---
title: "Multi-Currency Reporting with the Financials Data Source"
linkTitle: "Multi-Currency Reporting"
weight: 8
description: >
  Report in your chosen currency using Workday Financial Management's currency conversion — select transaction currency, company currency, or a converted reporting currency in OfficeConnect.
---

Workday Financial Management supports multicurrency transactions — journals can be posted in a transaction currency and converted to a company (ledger) currency automatically. OfficeConnect surfaces these currency layers so you can choose which currency your report shows.

## Currency options in the Financials data source

| Currency type | What it shows |
|---|---|
| **Transaction currency** | The original currency of the posted journal (e.g., GBP for a UK invoice) |
| **Company currency** | The ledger currency of the reporting company (e.g., USD for a US parent) |
| **Converted reporting currency** | A second converted amount if alternate ledger currency is configured in Workday |

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. In the Reporting pane, look for the **Currency** selector. It typically appears near the top of the pane or in report settings alongside the effective date option.

3. Select the currency option you want:
   - **Company currency** — most common for consolidated reporting; all amounts appear in your company's ledger currency
   - **Transaction currency** — useful for auditing specific foreign-currency transactions; amounts appear in the currency they were originally posted in
   - A specific converted currency — if your Workday model has alternate ledger currency configured, additional currency options may appear here

4. Build or refresh your report. All account values resolve in the selected currency.

> **Note:** Transaction currency reporting returns one row per currency if multiple currencies exist for the same account and period — your report may show separate rows for USD, GBP, and EUR entries rather than a single combined total. This is expected behavior for auditing purposes.

## Rate types and conversion

Workday Financial Management uses **rate types** to convert foreign currency transactions to the company currency. Common rate types include:

- **Average rate** — monthly average FX rate (typical for P&L accounts)
- **Spot rate** — rate at the date of the transaction
- **Budget rate** — fixed planning rate (used for constant currency comparisons)

The rate type applied to your OfficeConnect data is determined by your Workday configuration — OfficeConnect reports the converted amount, it does not select or override the rate type.

## Related

- [Report in Constant Currency in OfficeConnect](/build-reports/constant-currency-reporting/) — constant currency for Adaptive Planning users
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Effective Date Reporting](/build-reports/financials/effective-date-reporting/)
