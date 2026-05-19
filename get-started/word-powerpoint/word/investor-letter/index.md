---
title: "Build an Investor Letter Template with Workday OfficeConnect for Word"
url: "https://officeconnectpro.com/get-started/word-powerpoint/word/investor-letter/"
description: "A reusable Word investor-letter template where opening numbers, segment results, and forward guidance update from Workday OfficeConnect on each cycle.\n"
tags: ["sharing","reporting","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


The CEO's quarterly investor letter is part narrative, part numbers. The narrative changes; the numbers are the same fields every quarter — revenue, growth, margin, cash, headcount, segment results. Templating it once means subsequent quarters take an hour instead of a day, and the numbers can't go out wrong.

This guide walks through building a reusable investor-letter Word template with Workday OfficeConnect-linked cells. It builds on the same pattern as [MD&A Automated Draft](/get-started/word-powerpoint/word/mda-automated-draft/); the difference is voice and structure.

**What you'll build:** A reusable Word investor-letter template with 15-20 linked phrases covering opening, segment results, balance-sheet snapshot, and forward guidance — refreshes from Excel each quarter.

**What you'll need:**
- Workday OfficeConnect installed in Excel and Word
- An OfficeConnect Excel workbook with quarterly P&L, segment P&L, balance sheet, and headcount
- Last quarter's investor letter as a starting point
- 2 hours for the first build; subsequent quarters take under an hour

---

## Step 1 — Identify the standard structure

A typical investor letter has 4-6 sections that appear every quarter:

| Section | Linkable content |
|---|---|
| **Opening** | Total revenue, growth rate, gross/operating margin |
| **Segment results** | Revenue and growth by reportable segment |
| **Balance sheet** | Cash, debt, working capital snapshot |
| **Operational highlights** | Headcount, customer count, key KPIs |
| **Forward guidance** | Next-quarter revenue range, full-year outlook |
| **Cash & capital** | Buybacks, dividends, capex |

Templatize each. The CEO writes the narrative *between* the sections; the section heads and quantitative phrases are linked.

## Step 2 — Build the linked-cell library in Excel

Adopt a naming convention from the start: `IL_<Section>_<Variant>`.

{{< step n="1" title="Build opening-paragraph cells" >}}
- `IL_Opening_Revenue` — current quarter total revenue
- `IL_Opening_RevenueGrowth` — YoY growth %
- `IL_Opening_GrossMargin` — current quarter gross margin %
- `IL_Opening_GrowthDirection` — IF-based "grew/declined/held flat"
- `IL_Opening_Phrase` — concatenated narrative phrase

The concatenated phrase looks like:

```
="revenue " & IL_Opening_GrowthDirection & " " & TEXT(ABS(IL_Opening_RevenueGrowth),"0.0%") & " to " & TEXT(IL_Opening_Revenue,"$#,##0M")
```

Result: *"revenue grew 12.3% to $156M"*.
{{< /step >}}

{{< step n="2" title="Build segment-result cells" >}}
For each reportable segment:

- `IL_Segment_SaaS_Revenue` — current segment revenue
- `IL_Segment_SaaS_Growth` — YoY %
- `IL_Segment_SaaS_Phrase` — narrative ("SaaS revenue grew 18.4% to $98M, driven by strong renewals")

The "driven by" tail is hand-written (qualitative); the numbers come from cells.
{{< /step >}}

{{< step n="3" title="Build balance-sheet snapshot cells" >}}
- `IL_Cash_EOQ` — cash and equivalents at end of quarter
- `IL_Debt_EOQ` — total debt at end of quarter
- `IL_NetCash_EOQ` — formula: `IL_Cash_EOQ - IL_Debt_EOQ`
- `IL_Cash_Phrase` — *"We ended the quarter with [IL_Cash_EOQ] in cash and [IL_Debt_EOQ] in debt, for net cash of [IL_NetCash_EOQ]."*
{{< /step >}}

{{< step n="4" title="Build operational-highlight cells" >}}
- `IL_Headcount_EOQ` — employees at end of quarter
- `IL_Headcount_Change` — change from prior quarter
- `IL_Customers_EOQ` — customer count
- `IL_KPI_NRR` — net revenue retention or similar headline KPI
{{< /step >}}

{{< step n="5" title="Build forward-guidance cells" >}}
- `IL_Guidance_NextQ_Low` — low end of next-quarter revenue range
- `IL_Guidance_NextQ_High` — high end
- `IL_Guidance_FY_Revenue` — full-year revenue guidance
- `IL_Guidance_Phrase` — *"For the next quarter, we expect revenue of [IL_Guidance_NextQ_Low] to [IL_Guidance_NextQ_High]."*

Guidance comes from your latest forecast version in Adaptive Planning. See [Compare Planning Versions](/get-started/build-reports/compare-planning-versions/) if you maintain multiple forecast versions.
{{< /step >}}

## Step 3 — Build the Word template

{{< step n="6" title="Create the template structure" >}}
Start a new Word document with the section headings. Leave the narrative paragraphs as placeholder text — they'll be hand-written each quarter.
{{< /step >}}

{{< step n="7" title="Link the cells into the template" >}}
For each section, use the OfficeConnect Word links pane to insert the named cells in place. See [OfficeConnect for Word](/get-started/word-powerpoint/word/officeconnect-for-word/) for the linking mechanics.

Example linked sentence in the opening paragraph:

> "In the third quarter, [IL_Opening_Phrase], with gross margin of [IL_Opening_GrossMargin]."

After refresh:

> "In the third quarter, revenue grew 12.3% to $156M, with gross margin of 78.2%."
{{< /step >}}

{{< step n="8" title="Save as a template (.dotx)" >}}
Save the file as `Investor_Letter_Template.dotx`. Each quarter, open the template to create a new dated copy.
{{< /step >}}

## Step 4 — Cycle through a quarter close

{{< step n="9" title="Open the template and save as a dated copy" >}}
File → New → from `Investor_Letter_Template.dotx`. Save the new file as `Investor_Letter_2026Q3.docx`.
{{< /step >}}

{{< step n="10" title="Refresh Excel first, then Word" >}}
Refresh the OfficeConnect source workbook for the new quarter. Save. Then in Word, OfficeConnect tab → **Refresh**. Every linked phrase updates to the new quarter's data.
{{< /step >}}

{{< step n="11" title="Hand to the CEO for narrative" >}}
The CEO writes the qualitative narrative around the now-current numbers: what drove the quarter, what to expect, what's new strategically.
{{< /step >}}

{{< step n="12" title="Final review and disconnection" >}}
Once the CEO has finalized the narrative, you can optionally break the links to lock the file as a static historical record. See [Recovering Broken Links](/get-started/word-powerpoint/powerpoint/recovering-broken-links/) (the PowerPoint guide; the Word break-link procedure is similar via **Manage Links → Break Link**).
{{< /step >}}

{{< warning >}}
Once an investor letter ships, archive a static copy with links broken. If anyone later refreshes the live-linked version, the historical document changes — a serious problem if regulators or investors ask for a copy of the document as filed.
{{< /warning >}}

## Style considerations

- **Round consistently.** Format your linked dollar amounts the same way every quarter ($M rounded to one decimal, or whole millions — pick one).
- **Use the same tense and voice each quarter.** The cells provide numbers; the writer provides voice. A drift in style is jarring; the linked numbers are the anchor.
- **Refresh the template seldom.** Once you've built it, leave it alone except for adding/removing sections. Tinkering between quarters introduces bugs.

## Result

Each quarter the investor letter takes an hour of CEO time plus 30 minutes of refresh-and-review, instead of a day of typing and proofreading. The numbers are right by construction.

## Next steps

- [MD&A Automated Draft](/get-started/word-powerpoint/word/mda-automated-draft/) — the related management-discussion document.
- [OfficeConnect for Word](/get-started/word-powerpoint/word/officeconnect-for-word/) — the underlying linking mechanics.
- [Charts That Update with the Period](/get-started/word-powerpoint/powerpoint/period-aware-charts/) — period-aware chart patterns for the accompanying deck.

