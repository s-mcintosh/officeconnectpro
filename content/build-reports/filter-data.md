---
title: "Filter Your Data"
linkTitle: "Filter Data"
weight: 4
description: >
  Apply worksheet and workbook filters to limit which data appears in your report.
---

Filters let you restrict report data by accounts, levels, versions, currencies, attributes, or custom dimensions — without adding those elements to rows or columns.

## Worksheet vs workbook filters

| Filter type | Scope | Precedence |
|---|---|---|
| **Worksheet filter** | Applies to one sheet only | Overrides workbook filters |
| **Workbook filter** | Applies to all sheets in the workbook | Lower precedence than worksheet filters |

## Apply a worksheet filter

{{< step n="1" title="Open the Filters tab in the Reporting pane" >}}
In the Reporting pane, click the **Filters** tab.
{{< /step >}}

{{< step n="2" title="Click Worksheet Filters" >}}
The Worksheet Filters dialog opens. It shows any previously selected filters.
{{< /step >}}

{{< step n="3" title="Search or browse for elements to filter by" >}}
Example: To filter by two specific levels, expand the Level hierarchy and select `Company A` and `Company B`.
{{< /step >}}

{{< step n="4" title="Click OK" >}}
Your selected elements appear in the Filters tab as a subset.
{{< /step >}}

{{< step n="5" title="Enable the filters" >}}
In the Filters tab, click **Enable Filters**, then check the specific elements you want active.
{{< /step >}}

{{< step n="6" title="Refresh" >}}
The report now shows data only for the filtered elements.
{{< /step >}}

## Turn filters off without losing selections

In the Filters tab, uncheck **Enable Filters**. Your filter selections are remembered — they're just inactive. Re-check **Enable Filters** to reapply them later.

## Multi-select filters

You can select multiple elements at once by right-clicking an element in the filter list and using the context menu. When a parent is in **Collapse All** state, selecting it selects all its descendants too.

## Review active filters

To verify which filters are active on a worksheet:
1. In the Reporting pane, click the **Review** tab
2. Expand **Worksheet** to see active worksheet filters
3. Expand **Workbook** to see active workbook filters

Applied filters are listed under **Elements** in each section.

## Next steps

→ [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/) to rearrange elements in your report
