---
title: "Designing a Board Pack Template in Workday OfficeConnect"
url: "https://officeconnectpro.com/wiki/word-powerpoint/powerpoint/board-pack-template/"
description: "A reusable PowerPoint board-pack template built on Workday OfficeConnect — slide structure, named-range conventions, refresh discipline, and the design choices that keep it maintainable.\n"
tags: ["sharing","reporting","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


The monthly board pack is the most visible artifact your FP&A team ships. Done well, the entire deck refreshes from the OfficeConnect Excel workbook in five minutes; done poorly, a junior analyst spends two days re-pasting tables. This article walks through a reusable template design that's biased toward the five-minute version.

**What you'll build:** A 14-slide PowerPoint board pack template with linked tables and charts pulling from one OfficeConnect Excel workbook. Refresh discipline is built in.

**What you'll need:**
- Workday OfficeConnect installed in both Excel and PowerPoint — see [Install for End Users](/wiki/install-end-user/)
- A working OfficeConnect Excel workbook with the data you want to surface (P&L, KPIs, cash, headcount)
- PowerPoint with the OfficeConnect tab visible — see [OfficeConnect for PowerPoint](/wiki/word-powerpoint/powerpoint/officeconnect-for-powerpoint/)
- 60 minutes for the first build; subsequent months take under 10

---

## Step 1 — Design the slide structure first, data second

{{< step n="1" title="Sketch the deck on paper" >}}
Don't open PowerPoint yet. List the 12-15 slides the board actually reads: cover, agenda, financial highlights, P&L summary, revenue by segment, gross margin, OpEx trend, headcount, cash and runway, KPI dashboard, variance vs plan, risks, appendix.

Trim ruthlessly. The temptation is always to add slides. The board reads 10 of them.
{{< /step >}}

{{< step n="2" title="Decide what's a table vs a chart vs a number tile" >}}
- **Tables** — full P&L, variance bridges, KPI metrics across periods
- **Charts** — trend lines, waterfalls, mix breakdowns
- **Number tiles** — single-cell hero numbers (revenue, EBITDA, runway months)

This determines what you'll name in Excel.
{{< /step >}}

## Step 2 — Build named ranges in Excel

Every PowerPoint linkable element comes from an Excel **named range**. Establish a naming convention now or regret it forever.

{{< step n="3" title="Adopt a naming convention" >}}
Recommended pattern: `BP_<SlideName>_<Element>` — for example:

- `BP_PL_Summary_Table` — the P&L table on the P&L summary slide
- `BP_Cash_Runway_Tile` — the single-cell runway number
- `BP_OpEx_Trend_Chart` — the OpEx trend chart range

The `BP_` prefix groups all board-pack ranges so they sort together in Excel's Name Manager.
{{< /step >}}

{{< step n="4" title="Create the ranges" >}}
For each slide element, select the cells in Excel, click the **Name Box**, type the name, press Enter. See [OfficeConnect for PowerPoint](/wiki/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) for the named-range mechanics.
{{< /step >}}

## Step 3 — Build the PowerPoint template

{{< step n="5" title="Start with master slides, not content" >}}
In PowerPoint, customize the slide master once: header, footer, page numbers, brand colors, fonts. Every slide inherits — fix once, fixed everywhere.
{{< /step >}}

{{< step n="6" title="Build each slide and link the named range" >}}
For each slide:
1. Place the title and any commentary text
2. **OfficeConnect tab → Link from Excel** → browse to the workbook
3. Select the appropriate named range (e.g., `BP_PL_Summary_Table`)
4. Position and size the inserted table or chart

The linked element is now live — it'll refresh when the underlying Excel data changes.
{{< /step >}}

{{< step n="7" title="Add narrative text in PowerPoint, not Excel" >}}
Commentary like *"Revenue grew 8% vs plan driven by..."* lives in PowerPoint text boxes, not in linked cells. This keeps the analyst's qualitative work separate from the auto-updating numbers.
{{< /step >}}

## Step 4 — Establish refresh discipline

{{< step n="8" title="Refresh order matters" >}}
Always refresh **Excel first**, then PowerPoint. Doing it in the other order pulls stale data.
{{< /step >}}

{{< step n="9" title="Refresh-all-or-refresh-none" >}}
Refresh every linked element in the deck, not a subset. Partial refreshes produce decks where some numbers are from this month and some are from last — the worst possible state. See [Refreshing All Slides Safely](/wiki/word-powerpoint/powerpoint/refresh-all-slides/).
{{< /step >}}

{{< warning >}}
Don't save and send the deck without doing a full visual scan. A broken link or stale chart silently undermines trust in every number on the page. Build the visual scan into your monthly checklist.
{{< /warning >}}

## Step 5 — Version the template

Each board cycle, save a date-stamped copy: `BoardPack_2026Q2.pptx`. Keep a clean master template (`BoardPack_Template.pptx`) you never edit directly.

For the next period:

{{< step n="10" title="Copy the master template to a new dated file" >}}
Duplicate `BoardPack_Template.pptx` and name it for the new period (e.g., `BoardPack_2026Q3.pptx`).
{{< /step >}}

{{< step n="11" title="Update the linked Excel workbook for the new period" >}}
Change time elements or refresh against a new version in the source workbook.
{{< /step >}}

{{< step n="12" title="Open the new deck, refresh links, scan, and save" >}}
Open the dated deck, click **Refresh Links** in the OfficeConnect tab, do a visual scan of every slide, then save.
{{< /step >}}

Total time once the template exists: 10-15 minutes.

## Result

You have a board-pack template that refreshes in minutes, follows a consistent naming convention, and survives staff transitions because the conventions are documented in the named ranges themselves.

## Next steps

- [Refreshing All Slides Safely](/wiki/word-powerpoint/powerpoint/refresh-all-slides/) — the discipline that prevents broken decks.
- [Recovering Broken Links](/wiki/word-powerpoint/powerpoint/recovering-broken-links/) — when a refresh doesn't go smoothly.
- [Quarterly Board Pack](/wiki/build-reports/quarterly-board-pack/) — the source-workbook side of the same workflow.

