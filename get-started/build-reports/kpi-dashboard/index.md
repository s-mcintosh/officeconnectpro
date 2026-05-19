---
title: "Build a KPI Dashboard"
url: "https://officeconnectpro.com/get-started/build-reports/kpi-dashboard/"
description: "Build a single-sheet executive dashboard with six to eight KPI tiles, each pulled live from Adaptive Planning and shown with a prior-period comparison.\n"
tags: ["reporting","adaptive-planning","fpna","recipe"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


A KPI dashboard is the one page an executive will actually read. This tutorial walks through building a single-sheet Workday OfficeConnect dashboard with six to eight large-format tiles — Revenue, OpEx, Headcount, EBITDA margin, and so on — each refreshable from your Adaptive Planning model and each showing how the current period compares to the prior one.

**What you'll build:** A formatted Excel sheet with KPI tiles, each containing a current-period value, a prior-period value, and a delta — all driven by single OfficeConnect cells.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/get-started/build-reports/build-first-report/))
- A model with Actuals loaded for the current and prior period
- Comfort dragging Account, Version, and Time elements ([Add Elements](/get-started/build-reports/add-elements/))
- A blank workbook to start fresh

---

## Step 1 — Sketch the tile grid

{{< step n="1" title="Lay out a 4x2 grid of tiles" >}}
On a blank sheet, merge cells to form eight tiles — for example, B2:E6, F2:I6, J2:M6, N2:Q6 for the top row, and the same range one row down for the bottom row. Leave a row of whitespace between rows. Each merged block is one KPI tile.
{{< /step >}}

{{< step n="2" title="Label each tile" >}}
In the top-left of each tile, type the KPI name in a small font: *Revenue*, *Operating Expenses*, *Headcount*, *EBITDA Margin*, *Gross Margin %*, *Bookings*, *Cash*, *DSO*. These labels are static text — no OfficeConnect element needed.
{{< /step >}}

---

## Step 2 — Place the current-period value cells

{{< step n="3" title="Pick the value cell inside each tile" >}}
Choose one cell inside each tile to hold the big number — for example, the center cell of the merged block. Format it as 28pt bold and centered.
{{< /step >}}

{{< step n="4" title="Drop the Account, Version, and Time" >}}
Click into the value cell for the Revenue tile. In the Reporting pane, drag the **Revenue** account into the cell. OfficeConnect will need a version and a time context — add them in a hidden helper row (for example, row 30) using **Actuals** as the version and **Current Month** as the time. Repeat for each tile, pointing each at its own account.
{{< /step >}}

{{< admin-note >}}
You can also build each KPI as a fully self-contained cell formula by combining account, version, and time directly. Hidden helper rows are easier to maintain when you swap reporting periods.
{{< /admin-note >}}

---

## Step 3 — Add prior-period comparisons

{{< step n="5" title="Add a prior-period helper cell" >}}
Below the big number in each tile (still inside the merged block, or in a smaller cell beneath), add a second OfficeConnect cell pointing at the same Account and Version but with **Current Month -1** as the time context. Format it small and gray — this is the comparison value.
{{< /step >}}

{{< step n="6" title="Add the delta and arrow" >}}
In a third cell, write a plain Excel formula: `=(current - prior) / ABS(prior)`. Format as a percentage. Use Excel conditional formatting to color positive deltas green and negative red, and use a custom number format like `▲ 0.0%;▼ 0.0%` to add directional arrows.
{{< /step >}}

---

## Step 4 — Refresh, format, and lock

{{< step n="7" title="Refresh and spot-check" >}}
Click **Refresh** on the OfficeConnect ribbon. Every tile populates. Spot-check the Revenue tile against your P&L for the same month. If a tile shows `#VALUE!`, the account, version, or time element is likely missing from its helper row.
{{< /step >}}

{{< step n="8" title="Apply a consistent visual style" >}}
Use a single fill color per tile, white text for labels, and a subtle border. Hide gridlines (View → Gridlines off) for a cleaner look. Hide the helper rows.
{{< /step >}}

{{< step n="9" title="Lock the layout" >}}
Once you're happy with the layout, protect the sheet so executives can't accidentally drag a tile out of place — see [Lock and Protect Reports](/get-started/build-reports/lock-protect-reports/).
{{< /step >}}

---

## Result

You now have an executive-ready single-sheet dashboard with eight live KPI tiles. Each value pulls directly from Adaptive Planning, each comparison updates automatically against the prior period, and the whole sheet refreshes with one click. It's the report executives will open first and the one FP&A teams stop rebuilding from scratch each month.

## Next steps

- Apply executive-grade formatting across the rest of your reporting pack — see [Formatted Executive Report](/get-started/build-reports/formatted-executive-report/)
- Push the dashboard into a slide deck — see [Publish to PowerPoint](/get-started/build-reports/publish-to-powerpoint/)
- Add a current vs. prior-year layer — see [Year-over-Year Trend Report](/get-started/build-reports/year-over-year-trend/)

