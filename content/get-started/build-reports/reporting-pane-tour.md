---
title: "Interface Tour: The Reporting Pane"
linkTitle: "Reporting Pane Tour"
weight: 1
description: >
  A quick tour of the OfficeConnect interface in Excel — the ribbon tab and the Reporting pane.
tags: ["reporting", "adaptive-planning", "fpna", "reference"]
---

OfficeConnect adds two things to Excel: a **ribbon tab** and a **Reporting pane** that docks to the side of your worksheet.

## The OfficeConnect ribbon tab

The OfficeConnect tab appears between your standard Excel tabs. Key buttons include:

| Button | What it does |
|---|---|
| **Log In / Log Out** | Connect to or disconnect from your Workday tenant |
| **Refresh** | Pull the latest data from Adaptive Planning into all connected cells |
| **Show Reporting Pane** | Toggle the Reporting pane open or closed |
| **Workbook Properties** | Set rounding, data clearing, and filter defaults for the workbook |
| **User Settings** | Set your personal defaults (rounding, default instance, etc.) |
| **Find / Replace** | Find and replace elements across sheets |
| **Labels** | Add dynamic text labels (report date, level name, etc.) |
| **Help** | Access version info, documentation, and the troubleshooting tool |

{{< figure src="/images/screenshots/oc-ribbon-tab.png" alt="The OfficeConnect ribbon tab in Excel" caption="The OfficeConnect ribbon tab with Refresh, Show Reporting Pane, and other key buttons." >}}

## The Reporting pane

The Reporting pane docks to the right side of your worksheet by default. It has three tabs:

### Elements tab

Displays the full hierarchy of your Adaptive Planning instance:

- **Accounts** — GL accounts, custom accounts, metric accounts, modeled accounts
- **Time** — calendar years, quarters, months; also components and contexts
- **Level** — your organization's hierarchy (company, division, cost center, etc.)
- **Versions** — actuals and planning versions
- **Currencies** — if multi-currency is enabled
- **Custom Dimensions** — any additional dimensions in your model

Browse by expanding nodes in the tree. Drag elements into your worksheet, or right-click and select **Apply to Selection**.

{{< figure src="/images/screenshots/oc-elements-tab.png" alt="The Elements tab in the Reporting pane showing the Adaptive Planning hierarchy" caption="The Elements tab with Accounts, Time, Level, and Versions nodes expanded." >}}

### Filters tab

Apply worksheet-level or workbook-level filters. Use the **Enable Filters** toggle to activate or deactivate them without losing your selections.

{{< figure src="/images/screenshots/oc-filters-tab.png" alt="The Filters tab in the Reporting pane" caption="The Filters tab showing active worksheet-level filters with the Enable Filters toggle." >}}

### Review tab

Select a cell, row, or column and the Review tab shows exactly which elements are affecting that data point — broken down by Net, Row, Column, Worksheet filters, Workbook filters, and User Defaults.

{{< figure src="/images/screenshots/oc-review-tab.png" alt="The Review tab showing elements affecting a selected cell" caption="The Review tab with a cell selected, showing the breakdown of Row, Column, and Filter elements that determine its value." >}}

## Undocking the Reporting pane

Click the icon in the upper-right corner of the Reporting pane and select **Move** to undock it. Drag it anywhere, or hover at an edge of the worksheet to re-dock it.

If you lose a floating pane, click **Show Reporting Pane** in the OfficeConnect ribbon — it will reappear.

## Next steps

→ [Add Elements to Rows, Columns & Cells](/get-started/build-reports/add-elements/) to start building your first report
