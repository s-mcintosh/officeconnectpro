---
title: "Report on Actuals by Cost Center"
linkTitle: "Actuals by Cost Center"
weight: 4
description: >
  Filter an OfficeConnect Financials report to a specific cost center or worktag to see GL actuals for a single department or team.
tags: ["financials", "accounting", "reporting", "fpna", "recipe"]
---

OfficeConnect's Financials data source supports Workday worktags — including Cost Center — as dimension filters. Adding a cost center to your report scopes all data to that organizational unit.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Set up your report with company, version, time, and ledger account rows as usual. If you need to start from scratch, see [Build an Actuals Trend Report](/get-started/build-reports/financials/actuals-trend-report/).

3. Click an empty row or column header where you want to add the cost center filter. A common layout puts the cost center in the same header area as the company, stacked in adjacent cells.

4. In the Reporting pane, expand **Dimensions → Cost Center** (or the equivalent worktag in your Workday model). Drag the specific cost center into the header cell.

5. Click **Refresh**. All account values now reflect actuals for that cost center only, within the selected company and period.

> **Tip:** To build a report comparing multiple cost centers side by side, put each cost center in its own column header. Each column pulls data for its cost center, while sharing the same company, version, and time context from the rows above.

## Multiple worktag filters

You can stack multiple worktag dimensions in the header area. For example:
- Company → Cost Center → Project → Period

Each additional dimension narrows the data further. OfficeConnect resolves the intersection of all dimension elements in your report.

> **Note:** The available dimensions depend on how your Workday Financial Management instance is configured. If Cost Center doesn't appear in the Reporting pane, your administrator may need to enable it in the Workday financial reporting data model.

## Related

- [Filter Reports by Company](/get-started/build-reports/financials/filter-by-company/)
- [Build an Actuals Trend Report](/get-started/build-reports/financials/actuals-trend-report/)
- [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/)
