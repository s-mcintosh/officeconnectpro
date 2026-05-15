---
title: "Work with Time & Contexts"
linkTitle: "Time & Contexts"
weight: 3
description: >
  Add time periods to your report and use contexts like YTD, QTD, and Beginning Balance.
---

Time elements define which periods display in your report. Contexts add a calculation lens to those periods — like showing the year-to-date total instead of a single month's value.

## Time element types

| Type | Description | Example |
|---|---|---|
| **Absolute time** | A fixed, named period | `FY 2025`, `Q1 2025`, `Jan 2025` |
| **Relative time** | A period relative to today's date | `Current Month`, `Prior Year` |
| **Components** | Year/quarter/month components that combine at their intersection | Apply `FY 2025` to a row and `Q3` to a column → resolves to Q3 of FY 2025 |

## Add a time element

{{< step n="1" title="Select a column (or row)" >}}
Time is most commonly applied to columns so each column shows a different period.
{{< /step >}}

{{< step n="2" title="In the Elements tab, expand Time" >}}
Expand the calendar hierarchy to find the period you want: Year → Quarter → Month.
{{< /step >}}

{{< step n="3" title="Drag the time element to your selection" >}}
Drop it onto the selected column. Click **Refresh**.
{{< /step >}}

## Add a context

Contexts layer a calculation on top of a time element. You apply a context in the same location as the time element, or as a worksheet/workbook filter.

{{< step n="1" title="In the Elements tab, expand Time → Contexts" >}}
Available contexts depend on your calendar configuration.
{{< /step >}}

{{< step n="2" title="Drag the context to the same column, row, or cell as your time element" >}}
Or apply it to a cell within the time element's column or row.
{{< /step >}}

{{< step n="3" title="Refresh" >}}
The column now shows the context calculation for that time period.
{{< /step >}}

## Common contexts explained

| Context | What it shows |
|---|---|
| **Beginning Balance** | The balance at the start of the time period (= end of prior period) |
| **YTD** | Year-to-date: sum from the start of the fiscal year to the end of this period |
| **YTD Balance** | The balance as of the last month of the prior fiscal year |
| **QTD** | Quarter-to-date: sum from the start of the quarter to the end of this period |
| **QTD Balance** | The balance as of the last month of the prior quarter |

> **Best practice:** For period-to-date contexts, use time elements *smaller* than the context period. Use QTD or YTD with monthly time elements. Using Month-to-Date with a quarter element doesn't make logical sense and OfficeConnect will correct it.

## Relative time

Relative time elements automatically advance as time passes. For example, **Current Month** always shows the current calendar month when you refresh — no manual updates needed for rolling reports.

To lock a relative date (make it absolute), right-click the time element in the **Review** pane and select **Switch to Absolute**.

## Next steps

→ [Filter Your Data](/build-reports/filter-data/) to limit report data by level, version, or custom dimension
