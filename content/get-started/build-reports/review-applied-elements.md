---
title: "Review & Verify Applied Elements"
linkTitle: "Review Applied Elements"
weight: 6
description: >
  Use the Review tab to see exactly which elements are affecting any cell, row, or column.
tags: ["reporting", "adaptive-planning", "fpna", "how-to"]
---

The **Review tab** in the Workday OfficeConnect Reporting pane shows you a complete picture of what's driving data in your report. Use it to verify elements are applied correctly before sharing or distributing a report — especially after you've used [Add Elements](/get-started/build-reports/add-elements/) to assemble rows and columns.

## What the Review tab shows

Select a cell, row, or column, then click the **Review** tab. The sections you see depend on your selection:

| Section | Shown when | What it displays |
|---|---|---|
| **Net** | Cell selected | All elements *actively affecting* that cell's data — the combined result of all applied elements |
| **Rows** | Cell or row selected | All elements applied to that row |
| **Columns** | Cell or column selected | All elements applied to that column |
| **Worksheet** | Cell selected | Active worksheet filters |
| **Workbook** | Cell selected | Active workbook filters |
| **User Defaults** | Cell selected | Default elements from your User Settings |

> **Note:** The Net section only appears for single-cell selections. It's the most useful for diagnosing unexpected data — it shows what's *actually* driving the number.

## Basic steps

{{< step n="1" title="Click Refresh" >}}
Make sure the data is current before reviewing.
{{< /step >}}

{{< step n="2" title="Select a single cell, row, or column" >}}
The Review tab only shows useful information for a single selection — don't select multiple cells.
{{< /step >}}

{{< step n="3" title="Click the Review tab" >}}
In the Reporting pane, click **Review**.
{{< /step >}}

{{< step n="4" title="Expand sections to investigate" >}}
Click any section header (Net, Rows, Columns, etc.) to expand it and see the elements listed.
{{< /step >}}

## Review element sources

If the Net section shows an unexpected element, expand **Rows** and **Columns** to see where it was added. Expanding **Worksheet** and **Workbook** shows if a filter is contributing.

## Switch time elements between relative and absolute

From the Review tab, you can also change how time elements behave:

{{< step n="5" title="Right-click the time element metadata line" >}}
In the Review tab, right-click the time element you want to change.
{{< /step >}}

{{< step n="6" title="Select Switch to Absolute or Switch to Relative" >}}
Choose **Switch to Absolute** to lock the element to a fixed date, or **Switch to Relative** to make it roll with the current period.
{{< /step >}}

{{< step n="7" title="Refresh to see the effect" >}}
Click **Refresh** to apply the change and see the updated data.
{{< /step >}}

## Identify element groups

If a row or column is part of an expansion (element group), the Review tab shows an expansion `[+]` icon next to the element.

## Next steps

- [Cell Explorer & Drill-Down](/get-started/build-reports/cell-explorer-drill-down/) to inspect the data behind a specific cell
- [Filter Your Data](/get-started/build-reports/filter-data/) when Review shows an unexpected workbook or worksheet filter
- [Fix Data Discrepancies Between OfficeConnect and Workday](/reference/troubleshoot/data-discrepancies/) if Review confirms the right elements but figures still look wrong
