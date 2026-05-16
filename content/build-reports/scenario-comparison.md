---
title: "Set Up Scenario Comparison in OfficeConnect"
linkTitle: "Scenario Comparison"
weight: 26
description: >
  Compare planning scenarios side by side in OfficeConnect — useful for showing upside, base case, and downside in the same report.
tags: ["adaptive-planning", "how-to", "reporting"]
---

Scenarios in Adaptive Planning are planning alternatives within a version — for example, a Base Case, Upside, and Downside within your annual Budget version. OfficeConnect can display multiple scenarios in the same report, making it easy to show a range of outcomes.

## Before you begin

Scenarios must be configured in your Adaptive Planning model before they appear in OfficeConnect. If you don't see scenarios in the Reporting pane, ask your Adaptive Planning administrator to confirm they are enabled and that you have read access.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Set up your account rows and time columns as usual — scenarios apply to the version layer, not the account or time layer.

3. Click your first version column header (e.g., **B1**). In the Reporting pane, expand **Versions** and locate your version. Expand it to see available scenarios. Drag the **Base Case** scenario into B1.

4. Click the next column header (**C1**). Drag the **Upside** scenario into C1.

5. Click **D1** and drag the **Downside** scenario into D1.

6. Add the same time element to B2, C2, and D2.

7. Copy your account formulas across rows for each scenario column.

8. Click **Refresh**. Each column populates with data from its respective scenario.

> **Note:** Scenarios that have no data entered in Adaptive Planning return blank or zero in OfficeConnect. If a scenario column is empty after refresh, confirm that data has been entered for that scenario in Adaptive Planning sheets.

## Adding a scenario variance

To show the difference between Upside and Base Case, add an Excel formula column:

- Column E header: `Upside vs. Base`
- E3 formula: `=C3-B3`

Copy down for all rows. This is a plain Excel formula — it updates automatically when you refresh.

## Related

- [Compare Two Planning Versions Side by Side](/build-reports/compare-planning-versions/)
- [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
