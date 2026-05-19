---
title: "Create Fixed Date Columns"
linkTitle: "Fixed Date Columns"
weight: 9
description: >
  How to prevent date columns from rolling forward when using relative time elements.
tags: ["reporting", "adaptive-planning", "fpna", "system-admin", "troubleshoot"]
---

**Problem:** You've set up a report with relative time elements (like "Current Month," "Prior Month") so it always shows recent data. But you want certain columns to stay fixed at a specific historical date — not roll forward with time.

## Why relative dates roll

When you create a report using relative time elements, OfficeConnect automatically advances them when you refresh — "Current Month" always shows the current month. This is great for rolling reports but not for fixed comparisons.

## Fix: Switch the time element to Absolute

{{< step n="1" title="In the report, select the column with the date you want to fix" >}}
{{< /step >}}

{{< step n="2" title="In the Reporting pane, click the Review tab" >}}
{{< /step >}}

{{< step n="3" title="Find the time element in the left pane" >}}
Right-click on the calendar element listed under that column.
{{< /step >}}

{{< step n="4" title="Select View/Edit" >}}
{{< /step >}}

{{< step n="5" title="Uncheck 'Make Date Relative to Book'" >}}
{{< /step >}}

{{< step n="6" title="Click OK and refresh" >}}
The column now shows a fixed date that won't advance when you refresh.
{{< /step >}}

## Using Component Dates for fixed period combinations

Component dates let you create combinations like "Q4 of FY 2024" without locking a single absolute date:

{{< step n="7" title="Apply a year element to a row" >}}
Drag a **year** element (e.g., `FY 2024`) from the Reporting pane onto a row.
{{< /step >}}

{{< step n="8" title="Apply a quarter component to a column" >}}
Drag a **quarter component** (e.g., `Q4`) from the Reporting pane onto a column.
{{< /step >}}

{{< step n="9" title="Refresh to resolve the intersection" >}}
The intersection resolves to Q4 2024 specifically. Click **Refresh** to populate the data.
{{< /step >}}

See the **Components** section under Time in the Elements tab. Components are listed under `Time → Components` in the Reporting pane.
