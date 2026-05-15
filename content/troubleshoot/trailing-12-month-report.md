---
title: "Create a Trailing 12-Month Report"
linkTitle: "Trailing 12-Month Report"
weight: 10
description: >
  How to build a report that always shows the most recent 12 months of data.
---

A trailing 12-month (T12M) report shows the 12 most recent calendar months and advances automatically each month. This is a common layout for rolling actuals analysis.

## How to build it

The key is using **relative time elements** for each of the 12 columns — each column is defined as "N months ago" relative to today.

{{< step n="1" title="Set up your rows with account elements" >}}
Apply your account elements (e.g., Revenue, COGS, Gross Profit) to rows as usual.
{{< /step >}}

{{< step n="2" title="For the first column, apply 'Current Month - 11'" >}}
In the Elements tab, expand **Time → Relative**. Find the relative time element for 11 months prior (the oldest month in your T12M window) and apply it to column C.
{{< /step >}}

{{< step n="3" title="For each subsequent column, apply the next relative month" >}}
Continue applying relative months across columns:
- Column C: `Current Month - 11`
- Column D: `Current Month - 10`
- Column E: `Current Month - 9`
- …
- Column N: `Current Month` (most recent)
{{< /step >}}

{{< step n="4" title="Refresh" >}}
The report shows 12 months of data. Each month you refresh, the window advances by one month automatically.
{{< /step >}}

## Add a YTD column

After the 12 monthly columns, add a YTD column:
1. Select the column after your last month
2. Apply `Current Month` as the time element
3. Apply `YTD` as a context element in the same column
4. Refresh — this column shows the year-to-date sum as of the current month

## Formatting tip

Use Excel's column headers to show friendly month names using an OfficeConnect label:
1. Select the header cell above a monthly column
2. In the OfficeConnect ribbon, click **Labels**
3. Select **Time** as the Label Type and the appropriate format for the Label Type Value
4. Refresh — the header automatically shows the correct month name
