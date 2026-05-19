---
title: "Report on Intercompany Eliminations in OfficeConnect"
url: "https://officeconnectpro.com/get-started/build-reports/financials/intercompany-eliminations/"
description: "Use OfficeConnect's Financials data source to report on intercompany transactions and eliminations — with options to include or exclude eliminations from consolidated views.\n"
tags: ["financials","accounting","reporting","fpna","recipe"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Intercompany eliminations remove transactions between entities in a consolidated group — preventing double-counting of intercompany revenue and expenses. OfficeConnect's Financials data source surfaces these as data you can include or exclude in your reports.

## How eliminations appear in OfficeConnect

When you report against a parent company (consolidated entity) in OfficeConnect, the data you see depends on your Workday Financial Management configuration:

- If **elimination journals are posted** in Workday, they are included in consolidated totals automatically
- The **Exclude Elimination** option (available in Financials data source reports) lets you toggle whether elimination entries are included in your totals

> **Note:** The Exclude Elimination option is a Financials-only feature — it is not available in Adaptive Planning reports. See [Adaptive Planning vs. Financials Data Source](/get-started/migration-comparison/financials-vs-adaptive-planning/).

## View intercompany eliminations separately

To see elimination amounts on their own:

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Add a column for the **elimination company** — in Workday Financial Management, eliminations are typically posted to a dedicated elimination entity (often named **Eliminations**, **Elim**, or prefixed with **E_**). Drag this entity from the Company dimension in the Reporting pane.

3. Add your ledger account rows and refresh. The elimination column shows only the elimination journal entries for each account.

## Exclude eliminations from a consolidated report

1. In your consolidated report (with a parent company element), look for the **Exclude Elimination** checkbox in the Reporting pane or report settings.

2. Check **Exclude Elimination** to see gross consolidated data without eliminations applied. This is useful for understanding the total volume of intercompany activity.

3. Uncheck it to return to standard consolidated totals with eliminations included.

## Common intercompany reporting layouts

| Column A (Accounts) | Column B | Column C | Column D |
|---|---|---|---|
| Revenue | Company A | Company B | Eliminations |
| Intercompany Revenue | Company A IC | Company B IC | Elim entry |
| Consolidated Revenue | Sum of B+C+D | | |

Building this layout in OfficeConnect requires one column per entity plus one for the elimination company, with Excel SUM formulas for consolidated totals.

## Related

- [Filter Reports by Company](/get-started/build-reports/financials/filter-by-company/)
- [Build a Trial Balance Report](/get-started/build-reports/financials/trial-balance-report/)
- [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/) — verify elimination journal entries

