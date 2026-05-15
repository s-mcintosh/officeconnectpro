---
title: "Display Percentage Values Correctly"
linkTitle: "Percentage Values"
weight: 8
description: >
  How to prevent rounding from distorting percentage values in OfficeConnect.
---

**Problem:** Percentage values from Adaptive Planning appear as tiny decimals in OfficeConnect. For example, `25.25%` shows as `0.0002525` when workbook rounding is set to Thousands.

This happens because OfficeConnect stores percentages as decimals (`0.2525`) and then applies the workbook's rounding setting on top — Thousands rounding divides by 1,000, making it `0.0002525`.

## Fix option 1: Set rounding to No Rounding (whole workbook)

{{< step n="1" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**.
{{< /step >}}

{{< step n="2" title="On the Format tab, set Round to No Rounding" >}}
{{< /step >}}

{{< step n="3" title="Format the percentage cells in Excel" >}}
Select the cells and use Excel's **Format Cells → Percentage** to display them correctly.
{{< /step >}}

{{< step n="4" title="Refresh" >}}
{{< /step >}}

**Trade-off:** This removes rounding from the entire workbook. All other numbers will display without rounding too.

## Fix option 2: Suppress rounding on specific cells only

{{< step n="1" title="Select the cells that contain percentages" >}}
{{< /step >}}

{{< step n="2" title="In the OfficeConnect ribbon, open Row/Column/Cell Properties" >}}
Right-click → **OfficeConnect → Cell Properties** (or Row/Column Properties for a full row/column).
{{< /step >}}

{{< step n="3" title="Enable Suppress Rounding (Do Not Round Amounts)" >}}
{{< /step >}}

{{< step n="4" title="Format those cells as percentages using Excel" >}}
Select the cells → **Home tab → Number format → Percentage** (or use the `%` button).
{{< /step >}}

{{< step n="5" title="Refresh" >}}
{{< /step >}}

**Advantage:** The rest of the workbook keeps its rounding. Only the percentage cells display without rounding.
