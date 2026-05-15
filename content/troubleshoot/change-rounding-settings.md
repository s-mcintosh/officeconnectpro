---
title: "Change Rounding Settings"
linkTitle: "Rounding Settings"
weight: 7
description: >
  How to change how numbers are rounded in OfficeConnect reports.
---

OfficeConnect defaults to **Thousands** rounding for Adaptive Planning data sources — so `100,000` displays as `100` and `1,000` displays as `1`. You can change this at three levels.

## Rounding levels (highest to lowest precedence)

1. **Selection Properties** — for a specific row, column, or cell
2. **Workbook Properties** — for the current workbook
3. **User Settings** — your personal default for all new workbooks

## Change rounding in User Settings (affects new workbooks)

{{< step n="1" title="Click User Settings in the OfficeConnect ribbon" >}}
{{< /step >}}

{{< step n="2" title="In the Round to drop-down, select the rounding level" >}}
Options: Hundreds, Thousands (default), Ten Thousands, Hundred Thousands, Millions, Ten Millions, Hundred Millions, Billions, No Rounding.
{{< /step >}}

{{< step n="3" title="Click OK" >}}
This applies to all new workbooks. The current open workbook is not affected.
{{< /step >}}

## Change rounding for the current workbook

{{< step n="1" title="Click Workbook Properties in the OfficeConnect ribbon" >}}
{{< /step >}}

{{< step n="2" title="On the Format tab, change the Round to setting" >}}
{{< /step >}}

{{< step n="3" title="Click OK, then Refresh → All Sheets" >}}
The new rounding applies to the entire workbook across all worksheets.
{{< /step >}}

## Change rounding for a specific row, column, or cell

{{< step n="1" title="Select the row, column, or cell" >}}
{{< /step >}}

{{< step n="2" title="Right-click → OfficeConnect → Row/Column/Cell Properties" >}}
{{< /step >}}

{{< step n="3" title="Change the Round to setting and click OK" >}}
This overrides the workbook setting for this specific selection only.
{{< /step >}}

## Rounding and percentage values

If your report includes percentages, rounding to Thousands will distort them — `25.25%` becomes `0.0002525`. See [Display Percentage Values](/troubleshoot/display-percentage-values/) for the fix.
