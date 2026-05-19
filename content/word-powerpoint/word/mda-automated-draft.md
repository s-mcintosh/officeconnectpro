---
title: "Automated MD&A Draft with Workday OfficeConnect for Word"
linkTitle: "MD&A Automated Draft"
weight: 30
description: >
  Build a Word document where the numbers in your MD&A narrative — revenue, growth percentages, margin changes — update automatically from the Workday OfficeConnect Excel source.
tags: ["sharing", "reporting", "fp-and-a", "tutorial"]
---

The Management Discussion & Analysis (MD&A) narrative is the financial story that accompanies the numbers. Done well, it explains the period's results in plain language. Done manually, every quarter someone types numbers from a closed P&L into Word and prays they get every comma right.

This article walks through building an MD&A Word template where every quantitative phrase pulls live from the Workday OfficeConnect Excel workbook. The CFO still writes the narrative; OfficeConnect handles the numbers.

If you're new to Word linking, start with [OfficeConnect for Word](/word-powerpoint/word/officeconnect-for-word/).

**What you'll build:** A reusable Word MD&A template where revenue figures, growth percentages, margin changes, and directional words ("increased", "declined") refresh from the source Excel workbook with one click.

**What you'll need:**
- Workday OfficeConnect installed in both Excel and Word
- A working OfficeConnect Excel workbook with a current P&L for the reporting period
- A baseline MD&A draft to template-ize (use last quarter's if you have it)
- 90 minutes for the first build

---

## Step 1 — Identify the linkable phrases

{{< step n="1" title="Pull up last period's MD&A and mark every number" >}}
Read through last quarter's MD&A. Highlight every quantitative phrase: revenue figures, percentage changes, margin levels, headcount numbers, dollar deltas.
{{< /step >}}

{{< step n="2" title="Also mark the directional words" >}}
Words like *"increased"*, *"declined"*, *"flat"*, *"favorable"*, *"unfavorable"* are quantitative claims dressed up as words. They should update when the numbers update.
{{< /step >}}

A typical MD&A paragraph might have 8-12 linkable phrases. After identification, the rest is mechanical.

## Step 2 — Build the linkable cells in Excel

For each marked phrase, you need a single cell in the source workbook that resolves to the correct text or number.

{{< step n="3" title="Build hero number cells" >}}
For straight numbers like total revenue, create a single OfficeConnect cell with the right intersection (current period + total revenue account). Name it descriptively: `MDA_Revenue_Current`.
{{< /step >}}

{{< step n="4" title="Build delta cells" >}}
For phrases like *"up 8% vs prior period"*, build the delta in Excel:

```
=(MDA_Revenue_Current - MDA_Revenue_Prior) / MDA_Revenue_Prior
```

Format the cell as a percentage. Name it `MDA_Revenue_GrowthPct`.
{{< /step >}}

{{< step n="5" title="Build directional-word cells" >}}
For words like "increased" / "declined", use IF in Excel:

```
=IF(MDA_Revenue_GrowthPct>0,"increased",IF(MDA_Revenue_GrowthPct<0,"declined","held flat"))
```

Name it `MDA_Revenue_Direction`. This cell now contains a word that updates automatically.
{{< /step >}}

{{< step n="6" title="Build narrative-fragment cells (optional, powerful)" >}}
For longer phrases, combine pieces:

```
="revenue " & MDA_Revenue_Direction & " " & TEXT(ABS(MDA_Revenue_GrowthPct),"0.0%") & " to " & TEXT(MDA_Revenue_Current,"$#,##0M")
```

Returns something like *"revenue increased 8.2% to $124M"*. Name it `MDA_Revenue_Phrase`.
{{< /step >}}

Continue for every linkable phrase: gross margin, OpEx, EBITDA, headcount, cash. Use a naming convention (`MDA_<Topic>_<Variant>`) so the cells are easy to find.

## Step 3 — Link cells into Word

{{< step n="7" title="Open the MD&A draft in Word" >}}
Click the **OfficeConnect** tab. Click **Link to Workbook** and select your source workbook.

The OfficeConnect links pane appears with your named cells under **Single Links** (and any tables under **Table Links**).
{{< /step >}}

{{< step n="8" title="Replace each marked phrase with a link" >}}
For each phrase you marked in Step 1-2:

1. Delete the existing text in Word
2. Place your cursor where the text was
3. In the links pane, right-click the appropriate named cell (e.g., `MDA_Revenue_Phrase`) and choose **Apply to Selection**

The linked cell content replaces the placeholder. Repeat for every linkable phrase.
{{< /step >}}

{{< tip >}}
For the first pass, paste the named cell links in **bracketed** form, like *"[MDA_Revenue_Phrase]"*, before replacing the brackets. This makes it easy to visually confirm every placeholder has been linked.
{{< /tip >}}

## Step 4 — Test across a period roll

{{< step n="9" title="Refresh source data for the new period" >}}
In Excel, update the time elements to the new period and refresh. Save.
{{< /step >}}

{{< step n="10" title="Refresh in Word" >}}
In Word, OfficeConnect tab → **Refresh**. All linked phrases update with the new period's numbers and directional words.
{{< /step >}}

{{< step n="11" title="Read the draft end-to-end" >}}
Read through the MD&A as if you were the audience. Confirm:

- Numbers match expectations
- Directional words make grammatical sense (no awkward "increased -3%")
- Sentence structure flows now that variable phrases have replaced fixed text
{{< /step >}}

## Step 5 — Refine the qualitative narrative

The CFO still writes the qualitative parts — *why* revenue increased, what risks emerged, what to expect next quarter. Those paragraphs go between the linked phrases and remain hand-written each cycle.

The discipline: keep the quantitative phrases linked and the qualitative narrative human. Don't try to template the analysis; that's what the CFO is for.

## Patterns to avoid

- **Don't hardcode any number that could be linked.** Even "the company has 1,247 employees" should be a link to `MDA_Headcount_Current`.
- **Don't link a number twice.** If revenue appears in three paragraphs, use one named cell linked three times — not three named cells.
- **Don't bury the source workbook in a personal folder.** Store it where every author of the MD&A can reach it.

## Result

The MD&A draft refreshes from the source workbook in minutes. The CFO works on the narrative; the numbers are no longer a source of typos.

## Next steps

- [OfficeConnect for Word](/word-powerpoint/word/officeconnect-for-word/) — the underlying Word linking mechanics.
- [Investor Letter Template](/word-powerpoint/word/investor-letter/) — the same pattern applied to investor communications.
- [Charts That Update with the Period](/word-powerpoint/powerpoint/period-aware-charts/) — period-aware text and narrative for PowerPoint.
