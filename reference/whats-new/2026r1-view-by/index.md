---
title: "View By — Open Cell Data in a New Sheet (2026R1)"
url: "https://officeconnectpro.com/reference/whats-new/2026r1-view-by/"
description: "The 2026R1 View By ribbon command opens the data behind any Workday OfficeConnect cell in a separate worksheet so you can slice and filter without breaking your main report.\n"
tags: ["release-notes","reporting","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


{{< new-in-release version="2026R1" >}}
**View By** is new in Workday OfficeConnect 2026R1 (released March 14, 2026). It opens the data underlying any cell in a separate worksheet — so you can ad-hoc slice and filter without touching your formatted main report.
{{< /new-in-release >}}

Before 2026R1, the typical way to dig into a number was [Cell Explorer / Drill Down](/wiki/build-reports/cell-explorer-drill-down/), which is great for understanding **which** elements contribute to a cell, but doesn't give you a sandbox to manipulate the underlying intersection.

**View By** complements drill-down: it materializes the data behind a cell as a fresh sheet, where you can pivot, sort, or apply additional Excel transformations without ever touching the original report.

**What you'll need:**
- Workday OfficeConnect 2026R1 or later
- A refreshed report with at least one OfficeConnect cell
- Standard Excel familiarity (sheets, filters, sort)

{{< step n="1" title="Open your refreshed OfficeConnect report" >}}
The cell you select can be any data cell — a single intersection, a rollup, or even an `n/a` cell. View By works on the cell's element references, not on the resulting value.
{{< /step >}}

{{< step n="2" title="Click the cell once to select it" >}}
Don't enter edit mode; a single click is enough.
{{< /step >}}

{{< step n="3" title="In the OfficeConnect ribbon, click View By" >}}
The View By dialog opens. It lists every dimension referenced by the cell: typically Version, Time, Account, Level, plus any Custom Dimensions or Attributes in play.
{{< /step >}}

{{< step n="4" title="Choose the dimension you want to break out" >}}
For a *Total Expenses* cell, common choices are:

- **Account** — see the contributing leaf accounts
- **Level** — see the contribution from each cost center
- **Time** — break out a quarterly cell into its months
- **Custom Dimension** — break out by *Project* or *Customer*

Pick one and click **OK**.
{{< /step >}}

{{< step n="5" title="A new sheet appears in the workbook" >}}
The new sheet is named after the dimension you chose (for example, **View By Account — Total Expenses**) and contains the contribution of each member of that dimension to the original cell.

The new sheet is a **standalone OfficeConnect worksheet** — it has its own OfficeConnect formulas, refreshes independently, and won't affect your main report.
{{< /step >}}

{{< step n="6" title="Manipulate freely" >}}
You can apply standard Excel sort, filter, and conditional formatting to the new sheet without any risk to the main report. Treat it like a scratch pad.
{{< /step >}}

{{< step n="7" title="Delete the View By sheet when you're done" >}}
Right-click the sheet tab and click **Delete**. The main report is untouched.

Or — keep the sheet around. It's a regular OfficeConnect worksheet and will refresh alongside the main report on the next **Refresh**.
{{< /step >}}

## Tips and gotchas

- **View By doesn't change the source cell.** The originating cell stays exactly as it was. No risk.
- **Pick the dimension that will actually surface what you need.** If a cell has 8 dimensions, choosing the wrong one produces an uninteresting breakout.
- **Combine with Cell Explorer.** Use Cell Explorer first to see which dimensions are even on the cell, then use View By to break out the one that matters.
- **The new sheet still respects security.** If your user can't see certain Levels or accounts in Adaptive Planning, they won't appear in the View By sheet either.

## Result

You have an ad-hoc breakout of any cell's underlying data without any risk to the formatted source report. Far faster than rebuilding the same view manually.

## Next steps

- [Personal what-if scenarios (2026R1)](/reference/whats-new/2026r1-personal-scenarios/) — the other big 2026R1 feature.
- [Cell Explorer / Drill Down](/wiki/build-reports/cell-explorer-drill-down/) — sister tool for inspecting elements on a cell.
- [2026R1 Overview](/reference/whats-new/2026r1/) — the rest of the release.

