# PowerPoint Charts That Update with the Period in Workday OfficeConnect

Build PowerPoint charts whose axes, titles, and data ranges update automatically when the reporting period rolls — no more re-creating the trend chart every month.


---


A static PowerPoint chart with the title "Revenue Trend: Jan 2026 - Mar 2026" is fine the first month. The next month, someone has to manually update the title to "Feb 2026 - Apr 2026" — and probably forgets the axis label. Multiply by every chart in a board pack, every month, and you've reinvented manual work.

This article walks through building **period-aware** PowerPoint charts: the axis range, title, and data all roll forward when you refresh.

If you're new to PowerPoint linking, start with [OfficeConnect for PowerPoint](/get-started/word-powerpoint/powerpoint/officeconnect-for-powerpoint/).

## What "period-aware" means

A period-aware chart has three things that update automatically when the source Excel workbook refreshes:

1. **Data** — the bars/lines reflect current periods
2. **X-axis labels** — show current period names (e.g., "Apr 2026", not "Mar 2026")
3. **Chart title** — reflects the current period range

The first one is free with any linked chart. The other two require a specific pattern in the source Excel.

## Step 1 — Use relative time elements, not absolute

The foundation of period-awareness is **relative** Time elements in OfficeConnect — like *Current Month*, *Prior 12 Months*, *YTD* — rather than hardcoded dates like *Mar 2026*.

{{< step n="1" title="Choose your chart's time scope" >}}
Common choices for a trend chart:
- *Trailing 12 Months* — rolling 12-month window, anchored to today
- *YTD* — January through current month
- *Current Quarter + Prior 3 Quarters* — quarterly bar chart with 4 columns
- *Current Period* — single-point chart (a KPI tile, basically)
{{< /step >}}

{{< step n="2" title="Use the relative Time element in the source workbook" >}}
In the Reporting pane, expand **Time** and find the relative version of your choice. Drag it into the header row of your chart's source range. See [Time and Contexts](/get-started/build-reports/time-and-contexts/) for the catalog of relative time elements.
{{< /step >}}

## Step 2 — Let Excel resolve the labels

When OfficeConnect refreshes a relative time element, the cell displays the resolved period name — e.g., "Apr 2026" when refreshed in May 2026.

{{< step n="3" title="Use the resolved cells as your X-axis labels" >}}
In your Excel chart source, the row above your data values holds the time elements (e.g., row 2: Mar 2026, Apr 2026, May 2026, ...). When you build your chart, point the **horizontal axis labels** to that row.

When the workbook refreshes next month, the cells re-resolve to (Apr 2026, May 2026, Jun 2026, ...). The chart's X-axis updates automatically.
{{< /step >}}

## Step 3 — Build a dynamic chart title

The chart title is the trickiest piece because PowerPoint chart titles aren't directly linkable — they're properties of the chart object.

{{< step n="4" title="Build the title string in Excel" >}}
In Excel, create a single cell that constructs the title from the resolved period elements. Example formula:

```
="Revenue Trend: " & TEXT(B2,"mmm yyyy") & " - " & TEXT(M2,"mmm yyyy")
```

Where B2 and M2 are the first and last time-element cells in your chart's source range.

Name this cell `Chart_Title_RevenueTrend` so you can find it later.
{{< /step >}}

{{< step n="5" title="Reference the cell as the chart title (Excel-side first)" >}}
In Excel, click the chart's title, then click in the formula bar and type `=Chart_Title_RevenueTrend`. The chart title becomes the value of that cell.

Now refresh — the chart's title updates dynamically as the periods roll.
{{< /step >}}

{{< step n="6" title="Link the chart into PowerPoint" >}}
With the dynamic title in place in Excel, link the chart into PowerPoint as normal. The chart object carries its dynamic-title behavior through the link. When you refresh in PowerPoint, the title updates.
{{< /step >}}

## Step 4 — Test across a period roll

The whole point is automatic period updates, so test it.

{{< step n="7" title="Simulate the next period in the source workbook" >}}
In Excel, manually advance the "current period" by changing the model's anchor date (or simply edit a single Time element to the next month) and refresh. Observe:

- Chart data shifts one column to the right
- X-axis labels update to the new period names
- Chart title reflects the new range
{{< /step >}}

{{< step n="8" title="Refresh in PowerPoint and verify" >}}
Open the deck, **Refresh Links**, and check the chart. All three elements (data, axis, title) should reflect the new period.
{{< /step >}}

## Patterns that don't work

| Pattern | Why it fails |
|---|---|
| Hardcoded period labels in PowerPoint text boxes | Need manual edit every month |
| Hardcoded titles in chart properties (typed directly, not linked) | Same — no auto-update |
| Absolute Time elements in Excel (e.g., *Mar 2026*) | Don't roll forward on refresh |
| Naming the chart range with absolute cell references | Works for data but breaks if rows insert/delete |

## Bonus: period-aware text in narrative slides

The same pattern works for narrative text. In Excel, build a cell:

```
="Revenue for " & TEXT(M2,"mmm yyyy") & " was " & TEXT(M5,"$#,##0M") & ", " & IF(M5>M4,"up","down") & " " & TEXT(ABS(M5-M4)/M4,"0.0%") & " from the prior month."
```

Name it `Narrative_Revenue_CurrentMonth`. Link the cell into a Word narrative or a PowerPoint text box. See [OfficeConnect for Word](/get-started/word-powerpoint/word/officeconnect-for-word/) — the qualitative-text refresh pattern is well-suited to this kind of period-aware narrative.

## Result

Your board-pack charts and titles roll forward automatically when the period changes. The monthly refresh cycle drops from "rebuild every chart" to "click Refresh Links, scan the deck."

## Next steps

- [Designing a Board Pack Template](/get-started/word-powerpoint/powerpoint/board-pack-template/) — the slide template that hosts these charts.
- [Refreshing All Slides Safely](/get-started/word-powerpoint/powerpoint/refresh-all-slides/) — the refresh discipline that surfaces the updates.
- [Time and Contexts](/get-started/build-reports/time-and-contexts/) — the catalog of relative time elements that drive period awareness.
