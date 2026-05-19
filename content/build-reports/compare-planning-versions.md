---
title: "Compare Two Planning Versions Side by Side"
linkTitle: "Compare Planning Versions"
weight: 23
description: >
  Add a second version column to any OfficeConnect report to compare Budget vs. Forecast, two plan iterations, or any two Adaptive Planning versions.
tags: ["adaptive-planning", "reporting", "fp-and-a", "how-to"]
---

Any OfficeConnect report can show multiple versions at once. Here's how to add a second version column alongside your existing data.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Click an empty column header cell (for example, **C1** if your existing data is in column B).

3. In the Reporting pane, expand **Versions** and drag the second version (e.g., Forecast) into C1.

4. Click **C2** and drag the same time element you used in B2 into C2. Both columns now share the same time period.

5. Click **C3** and copy your existing data formula from B3 into it. OfficeConnect resolves C3 using the version in C1 and the time in C2.

6. Copy C3 down for all account rows.

7. Click **Refresh**. Column C populates with the second version's data.

> **Note:** The version element must exist in your Adaptive Planning model. If a version doesn't appear in the Reporting pane, check that you have read access to it in Adaptive Planning under Administration > Users.

## Common version comparisons

| Scenario | Column 1 | Column 2 |
|---|---|---|
| Budget vs. Actuals | Actuals | Budget |
| Current forecast vs. prior forecast | Forecast v2 | Forecast v1 |
| Board case vs. management case | Board Plan | Mgmt Plan |
| Actuals vs. prior year actuals | Actuals (current year) | Actuals (prior year) |

For a full budget vs. actuals report with a variance column, see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/).
