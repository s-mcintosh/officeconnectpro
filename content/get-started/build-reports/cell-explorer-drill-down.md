---
title: "Cell Explorer & Drill-Down"
linkTitle: "Cell Explorer"
weight: 10
description: >
  Explore the data behind any cell to understand what's driving the numbers.
tags: ["reporting", "adaptive-planning", "fpna", "how-to"]
---

When a number in your Workday OfficeConnect report looks unexpected, **Explore Cell** lets you drill into the contributing details to find the source. It pairs naturally with [Review & Verify Applied Elements](/get-started/build-reports/review-applied-elements/) — Review shows which elements drive a cell, while Explore Cell shows the underlying data behind the result.

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

{{< step n="4" title="Clear the Suppress Rows if all Zeros or Blanks setting" >}}
In the Explore Cell page, uncheck the **Suppress Rows if all Zeros or Blanks** option to show all rows including zero-value contributors.
{{< /step >}}

Note: This setting resets each time you launch Explore Cell.

## Show Details (Financials data source)

For Financials data source users, **Show Details** is the equivalent feature:

{{< step n="1" title="Right-click any report cell with data" >}}
Click to select the cell, then right-click to open the context menu.
{{< /step >}}

{{< step n="2" title="Select Show Details" >}}
Choose **Show Details** from the context menu.
{{< /step >}}

{{< step n="3" title="Review the contributing journal lines in the new worksheet" >}}
A new Excel worksheet opens showing contributing journal lines and plan lines.
{{< /step >}}

{{< step n="4" title="Drill through to Workday" >}}
From the new worksheet, you can drill through to Workday to view related journals and transactions.
{{< /step >}}

> For large worksheets, Show Details performs better with 64-bit Excel.

## Next steps

- [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/) for the Financials-data-source equivalent
- [Review & Verify Applied Elements](/get-started/build-reports/review-applied-elements/) to confirm the elements driving a cell
- [Fix Data Discrepancies Between OfficeConnect and Workday](/reference/troubleshoot/data-discrepancies/) when the drill-down reveals an unexpected variance
