---
title: "Remove Elements"
linkTitle: "Remove Elements"
weight: 6
description: >
  How to clear OfficeConnect elements from cells, rows, or columns.
tags: ["reporting", "fpna", "system-admin", "troubleshoot"]
---

When you clear cells in a Workday OfficeConnect report with Excel's normal delete, the element metadata can linger and confuse later refreshes — so use OfficeConnect's own clear command instead. For the related move and copy workflows, see [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/).

**Question:** How do I remove OfficeConnect elements from a range of cells?

## Steps

{{< step n="1" title="Select the row, column, or cell" >}}
Select the area where the element is applied. For best results, select the entire row or column (not just individual cells within it).
{{< /step >}}

{{< step n="2" title="Right-click and choose Clear Design Elements" >}}
From the right-click context menu, select **OfficeConnect → Clear Design Elements**.
{{< /step >}}

## What gets cleared

- The OfficeConnect element metadata is removed from the selection
- The cells become plain Excel cells — no longer linked to Adaptive Planning
- **Labels** you added remain in place (they're plain text, not elements)
- The visual contents of the cells remain until you delete them manually or the next refresh would have populated them

## Remove elements from multiple locations

To remove elements from several rows or columns at once:
1. Hold **Ctrl** and click each row number or column letter
2. Right-click any of the selected rows/columns
3. Select **OfficeConnect → Clear Design Elements**

## Find all instances of an element first

If you want to find everywhere a specific element is used before removing it:
1. From the OfficeConnect ribbon, click **Find** (in the Find drop-down)
2. Search for the element
3. Use **Find All** to see all instances across the workbook

Then clear each one individually or use **Replace** to swap it with a different element.

## Next steps

- [Review & Verify Applied Elements](/build-reports/review-applied-elements/) to confirm the right elements were cleared
- [Add Elements to Rows, Columns & Cells](/build-reports/add-elements/) to re-apply elements after a clean-up
- [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/) for relocating rather than removing elements
