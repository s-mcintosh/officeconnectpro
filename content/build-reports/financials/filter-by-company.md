---
title: "Filter Reports by Company in OfficeConnect (Financials)"
linkTitle: "Filter by Company"
weight: 6
description: >
  Scope an OfficeConnect Financials report to a specific legal entity, or build a multi-company view showing each entity in its own column.
tags: ["financials", "accounting", "reporting", "fp-and-a", "how-to"]
---

In the Financials data source, **Company** is the top-level org dimension — the equivalent of a legal entity or subsidiary in Workday Financial Management. Every Financials report must include at least one Company element to pull data. Here's how to use it effectively.

## Single-company report

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Click your column header cell (e.g., **B1**).

3. In the Reporting pane, expand **Company** and drag your target company into B1.

4. Add your version, time, and ledger account rows as usual.

5. Click **Refresh**. All data in column B is scoped to that company.

## Multi-company report (entities side by side)

To compare two or more companies:

1. Drag **Company A** into **B1** and **Company B** into **C1**.

2. Add version and time elements in B2:C2 (same values for both columns).

3. Add account rows in column A and copy data formulas across both columns.

4. Click **Refresh**. Each column shows actuals for its company, sharing the same accounts and time period.

## Consolidated view

To show a consolidated total across all companies:

1. In the Reporting pane, expand **Company** and look for a parent-level or consolidation company (often named **All Companies**, **Group**, or your parent entity name).

2. Drag the parent company into a column header. OfficeConnect returns consolidated data with intercompany eliminations applied if your Workday model is configured for consolidation.

> **Note:** Consolidated reporting requires that intercompany elimination rules are configured in Workday Financial Management. If the parent company value doesn't match your expected consolidated total, contact your Workday administrator.

## Related

- [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- [Report on Intercompany Eliminations](/build-reports/financials/intercompany-eliminations/)
- [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)
