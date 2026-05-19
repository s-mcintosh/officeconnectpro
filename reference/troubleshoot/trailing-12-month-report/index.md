# Create a Trailing 12-Month Report

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

{{< step n="5" title="Select the column after your last month" >}}
Click the column letter immediately to the right of your final monthly column.
{{< /step >}}

{{< step n="6" title="Apply Current Month as the time element" >}}
Drag `Current Month` from the Reporting pane into the header cell of this column.
{{< /step >}}

{{< step n="7" title="Apply YTD as a context element" >}}
In the same column, drag `YTD` as a context element alongside the time element.
{{< /step >}}

{{< step n="8" title="Refresh" >}}
Click **Refresh** — this column shows the year-to-date sum as of the current month.
{{< /step >}}

## Formatting tip

Use Excel's column headers to show friendly month names using an OfficeConnect label:

{{< step n="1" title="Select the header cell above a monthly column" >}}
Click the header cell (the cell directly above a monthly data column).
{{< /step >}}

{{< step n="2" title="Click Labels in the OfficeConnect ribbon" >}}
In the OfficeConnect ribbon, click **Labels**.
{{< /step >}}

{{< step n="3" title="Set the Label Type and format" >}}
Select **Time** as the Label Type and the appropriate format for the Label Type Value.
{{< /step >}}

{{< step n="4" title="Refresh" >}}
Click **Refresh** — the header automatically shows the correct month name.
{{< /step >}}
