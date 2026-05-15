---
title: "Suppress & Hide Zeros and Blanks"
linkTitle: "Hide Zeros & Blanks"
weight: 5
description: >
  How to hide rows with all zeros or blank values in your OfficeConnect workbook.
---

Zero suppression in OfficeConnect is a two-part system: **Workbook Properties** controls the *default state*, and the **Hide Zeros & Blanks** ribbon button is a *toggle* on top of that default.

## How it works

| Workbook property | Effect |
|---|---|
| **Hide rows with all zeroes** is **checked** | Zero suppression is enabled by default. The **Hide Zeros & Blanks** button on the ribbon toggles it on/off. |
| **Hide rows with all zeroes** is **unchecked** | Zero suppression is disabled. The **Hide Zeros & Blanks** button will not work after refresh. |

## Enable zero suppression

{{< step n="1" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**.
{{< /step >}}

{{< step n="2" title="Check 'Hide rows with all zeroes'" >}}
In the **Row Display** section, check the **Hide rows with all zeroes** option.
{{< /step >}}

{{< step n="3" title="Click Refresh" >}}
After refreshing, click **Hide Zeros & Blanks** in the OfficeConnect ribbon to activate suppression.
{{< /step >}}

## Per-row overrides

With the workbook default set, you can configure individual rows to behave differently:
1. Select the row
2. Right-click → **OfficeConnect → Row Properties**
3. Set a different zero suppression behavior for that specific row

This lets some rows follow the workbook default while others always show (or always hide) zeros.

## Zero suppression and Excel's Hide Rows

Within OfficeConnect-linked data ranges, you can also use Excel's native **Hide** capability on rows and columns. These behave independently from OfficeConnect's zero suppression.
