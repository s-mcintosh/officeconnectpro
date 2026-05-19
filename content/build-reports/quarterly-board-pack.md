---
title: "Build a Quarterly Board Pack"
linkTitle: "Quarterly Board Pack"
weight: 40
description: >
  Build a multi-sheet OfficeConnect workbook — P&L summary, KPI page, variance commentary, cash snapshot — designed to feed directly into a PowerPoint board deck.
tags: ["reporting", "adaptive-planning", "fpna", "recipe"]
---

A board pack is the quarterly artifact every finance team produces and the one most prone to last-minute spreadsheet panic. This tutorial walks through building a structured, multi-sheet Workday OfficeConnect workbook that acts as the single source for your quarterly board deck — P&L summary, KPI page, variance commentary, and cash snapshot — with each tab designed to link directly into PowerPoint.

**What you'll build:** A four-tab Excel workbook (P&L, KPIs, Variance, Cash) with consistent formatting, refreshable from Adaptive Planning, and ready to link to slides.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- Actuals loaded for the closing quarter plus a Budget or Forecast version
- A blank workbook with four named tabs: `PL`, `KPIs`, `Variance`, `Cash`
- The [OfficeConnect for PowerPoint](/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) add-in installed for downstream linking

---

## Step 1 — Build the P&L summary tab

{{< step n="1" title="Set the period header" >}}
On the `PL` tab, click **B1** and drag your **Actuals** version. In **C1**, drag your **Budget** version. In **B2** and **C2**, drag a time element for the closing quarter (for example, **Q4 FY25**).
{{< /step >}}

{{< step n="2" title="Add quarter-summary rows" >}}
In column A, list the standard P&L lines: Revenue, COGS, Gross Profit, Operating Expenses, EBITDA, Net Income. Drag the corresponding accounts into B3:B8. Copy B3:B8 across to C3:C8 to pick up the Budget column.
{{< /step >}}

{{< step n="3" title="Add a variance column" >}}
In **D1** type `Variance`. In **D3** write `=B3-C3` and copy down. This mirrors the pattern from [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/).
{{< /step >}}

---

## Step 2 — Build the KPI tab

{{< step n="4" title="Place six KPI tiles" >}}
On the `KPIs` tab, lay out six merged-cell tiles for the metrics the board reviews quarter to quarter — Revenue Growth %, Gross Margin %, OpEx Ratio, EBITDA Margin, Ending Headcount, Cash Balance.
{{< /step >}}

{{< step n="5" title="Populate each tile" >}}
For each tile, drop a single OfficeConnect cell that resolves to the metric for the closing quarter, and a small comparison cell underneath for the prior quarter. The full mechanics are covered in [Build a KPI Dashboard](/build-reports/kpi-dashboard/).
{{< /step >}}

---

## Step 3 — Build the variance commentary tab

{{< step n="6" title="Add account rows with variance columns" >}}
On the `Variance` tab, list the OpEx accounts your board scrutinizes — Salaries, Marketing, Software, Travel, Facilities, Professional Services. Add Actuals, Budget, $ Variance, and % Variance columns using the same pattern from the P&L tab.
{{< /step >}}

{{< step n="7" title="Add a commentary column" >}}
Add a wide column F titled `Commentary`. This is plain Excel text — finance owners type explanations here for each material variance. The column persists across refreshes.
{{< /step >}}

{{< admin-note >}}
Lock all OfficeConnect cells but leave the Commentary column unlocked so reviewers can edit explanations without breaking the structure. See [Lock and Protect Reports](/build-reports/lock-protect-reports/).
{{< /admin-note >}}

---

## Step 4 — Build the cash snapshot tab

{{< step n="8" title="Pull cash balances" >}}
On the `Cash` tab, build a small four-quarter trend of ending cash plus operating cash flow. Use **Current Quarter -3** through **Current Quarter** as the time headers, then drop Cash and Net Cash from Operations accounts into the data rows.
{{< /step >}}

{{< step n="9" title="Add an Excel chart" >}}
Insert a line chart over the cash trend cells. The chart updates automatically each time OfficeConnect refreshes.
{{< /step >}}

---

## Step 5 — Refresh and link to PowerPoint

{{< step n="10" title="Refresh the whole workbook" >}}
Click **Refresh** once — all four tabs update together.
{{< /step >}}

{{< step n="11" title="Link tables and charts into the deck" >}}
Open your board deck in PowerPoint. Use [Publish to PowerPoint](/build-reports/publish-to-powerpoint/) or paste-as-linked-object so each refresh of the workbook flows directly into the slides. The [OfficeConnect for PowerPoint](/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) add-in supports an end-to-end refresh from the slide side.
{{< /step >}}

---

## Result

You now have a structured, four-tab board pack workbook whose every number is sourced from Adaptive Planning and whose every chart and table can flow straight into the quarterly deck. The next time the board calendar lands on your inbox, the pack assembles itself in minutes — not days.

## Next steps

- Polish the look of each tab — see [Formatted Executive Report](/build-reports/formatted-executive-report/)
- Add scenario overlays for the forward outlook — see [Scenario Comparison](/build-reports/scenario-comparison/)
- Push the final tables and KPIs into slides — see [Publish to PowerPoint](/build-reports/publish-to-powerpoint/)
