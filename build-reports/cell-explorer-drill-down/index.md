# Cell Explorer & Drill-Down

Explore the data behind any cell to understand what's driving the numbers.


---


When a number in your report looks unexpected, **Explore Cell** lets you drill into the contributing details to find the source.

## What Explore Cell shows

For any cell with data, Explore Cell reveals:

| Detail | Description |
|---|---|
| **Contributing rows** | The specific data intersections driving the value |
| **Account details** | Rollup values and links to child accounts |
| **Level details** | Rollup values and links to child levels |
| **Time details** | Breakdown by time period |
| **Audit trail** | Change history (if Audit Trail is enabled in Adaptive Planning) |
| **Other sheets** | Links to other sheets that show the same value |
| **Source drills** | Drill into Transactions, Workday objects, or NetSuite (if configured) |

> **Note:** Explore Cell applies to the **Adaptive Planning** data source. For the **Financials** data source, use **Show Details** instead, which shows contributing journal line and plan line details.

## Steps

{{< step n="1" title="Select the cell you want to investigate" >}}
Click on any cell in your OfficeConnect report that contains data.
{{< /step >}}

{{< step n="2" title="Right-click and select Explore Cell" >}}
Or use the **Explore Cell** button in the OfficeConnect ribbon.
{{< /step >}}

{{< step n="3" title="Review the contributing details" >}}
Explore Cell opens showing the breakdown. Expand sections to drill deeper — you can open nested Explore Cell views to follow the data chain.
{{< /step >}}

## Zeros and blanks in Explore Cell

Explore Cell automatically suppresses rows with all zeros or blanks by default — only rows that actually contribute to the value are shown. To see zero rows:
1. Clear the **Suppress Rows if all Zeros or Blanks** setting on the Explore Cell page

Note: This setting resets each time you launch Explore Cell.

## Show Details (Financials data source)

For Financials data source users, **Show Details** is the equivalent feature:
1. Right-click any report cell with data
2. Select **Show Details**
3. A new Excel worksheet opens showing contributing journal lines and plan lines
4. From there you can drill through to Workday to view related journals and transactions

> For large worksheets, Show Details performs better with 64-bit Excel.
