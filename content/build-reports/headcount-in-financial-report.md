---
title: "Add Headcount Data to a Financial Report"
linkTitle: "Headcount in Financial Reports"
weight: 24
description: >
  Mix workforce planning metrics (headcount, FTEs, salary cost) with financial accounts in a single OfficeConnect report.
tags: ["adaptive-planning", "reporting", "fp-and-a", "recipe"]
---

OfficeConnect doesn't separate financial and workforce accounts — they're all elements in your Adaptive Planning model. You can add headcount rows to any financial report by dragging the right accounts from the Reporting pane.

## Steps

1. Open your financial report in Excel and click the **OfficeConnect** tab.

2. Click an empty row below your financial accounts — for example, **A10** if your P&L ends at row 9.

3. In the Reporting pane, expand **Accounts** and look for your workforce accounts. Common names include:
   - **Headcount** (total employee count)
   - **FTEs** (full-time equivalents)
   - **Salaries & Benefits** (may already appear in your P&L)
   - **Open Positions**

4. Drag the headcount account into **A10**. OfficeConnect inserts a formula using the version and time context already set up in your report.

5. Copy the data formula from the row above (e.g., B9) into **B10** and across the row. Headcount resolves using the same version and time elements.

6. Click **Refresh**. The headcount row populates alongside your financial data.

> **Tip:** Headcount is often stored in a different account group than financial accounts (e.g., under a "Workforce" or "HR" section in the Accounts tree). If you don't see it, expand all groups in the Reporting pane or search by name.

## Keeping units clear

Headcount values are typically whole numbers while financial values are in thousands (or your model's default rounding). To avoid confusion:

- Format the headcount row with **no decimal places** and **no currency symbol** (Format Cells → Number → 0)
- Add a label in column A noting the unit: "Headcount (FTEs)"
- Use a thin border or shading to visually separate the headcount section from the financials above it

## Related

- [Workbook and Worksheet Properties](/build-reports/workbook-worksheet-properties/) — set default rounding for the whole workbook
- [Build a Department P&L Report](/build-reports/department-pl-report/) — organize by Level before adding headcount rows
