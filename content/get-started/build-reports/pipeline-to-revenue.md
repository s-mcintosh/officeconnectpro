---
title: "Build a Sales Pipeline-to-Revenue Forecast"
linkTitle: "Pipeline-to-Revenue Forecast"
weight: 45
description: >
  Build a probability-weighted revenue forecast from pipeline data — stages, probabilities, and expected close dates — using a Pipeline custom dimension in Adaptive Planning.
tags: ["reporting", "adaptive-planning", "fpna", "recipe"]
---

Pipeline-to-revenue forecasting bridges the gap between the CRM and the financial model. Instead of treating bookings as a single top-down number, this approach builds the forecast bottom-up from deal stages and probabilities. This tutorial walks through assembling a probability-weighted revenue forecast in Workday OfficeConnect, assuming your pipeline data is already loaded into Adaptive Planning through a custom dimension.

**What you'll build:** A report that lists pipeline by stage, applies a stage-weighted probability, and projects expected revenue by month for the next two quarters.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- A **Pipeline Stage** custom dimension in Adaptive Planning (Prospect, Qualified, Proposal, Negotiation, Closed Won)
- A **Pipeline Amount** account loaded with deal values dimensionalized by stage and expected close month
- Familiarity with custom dimensions ([Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/))

---

## Step 1 — Set up the stage rows

{{< step n="1" title="Add the time headers" >}}
On a blank sheet, click **B1** and drag the first forecast month (for example, **Current Month +1**). Repeat across C1:G1 for the next five months. This gives you a six-month forward view.
{{< /step >}}

{{< step n="2" title="Add stage rows from the custom dimension" >}}
In column A, list the pipeline stages: `Prospect`, `Qualified`, `Proposal`, `Negotiation`, `Closed Won`. In B2 drag the **Pipeline Amount** account and filter it on the **Pipeline Stage = Prospect** dimension value using the Reporting pane. Repeat for B3:B6, filtering on each stage.
{{< /step >}}

{{< step n="3" title="Copy across the months" >}}
Select B2:B6 and copy into C2:G6. Each cell now resolves to the pipeline amount for that stage and that month.
{{< /step >}}

---

## Step 2 — Apply stage probabilities

{{< step n="4" title="Add a probability column" >}}
In column H, type the stage probability next to each row: 10% for Prospect, 25% for Qualified, 50% for Proposal, 75% for Negotiation, 100% for Closed Won. These are static values you can tune to match your historical win rates.
{{< /step >}}

{{< step n="5" title="Compute weighted pipeline per stage per month" >}}
In a second block below the raw pipeline table (rows 10-14), repeat the stage labels in column A, then in B10 write `=B2*$H2` and copy across and down. This block shows the probability-weighted contribution from each stage by month.
{{< /step >}}

---

## Step 3 — Build the forecast row

{{< step n="6" title="Total the weighted contributions" >}}
In row 16, label A16 `Expected Revenue`. In B16 write `=SUM(B10:B14)` and copy across to G16. This is the bottom-up pipeline-weighted forecast for each month.
{{< /step >}}

{{< step n="7" title="Compare to plan" >}}
Below the forecast row, add a row labeled `Plan` and drag the **Budget** version of your Revenue account into each month. Add a third row labeled `Gap` with `=B16-B17` to show where pipeline coverage is short.
{{< /step >}}

{{< admin-note >}}
Many teams define a *coverage ratio* — total unweighted pipeline divided by the revenue target. A coverage ratio of 3x is healthy in most B2B SaaS contexts; below 2x is a leading indicator of a miss.
{{< /admin-note >}}

---

## Step 4 — Refresh and review

{{< step n="8" title="Refresh and validate" >}}
Click **Refresh**. The raw pipeline rows populate from the custom dimension. Weighted rows and totals recalculate automatically. Spot-check the Closed Won row — it should match closed-won bookings already in your CRM for those months.
{{< /step >}}

{{< step n="9" title="Add stage drilldown" >}}
For any cell that looks off, use [Cell Explorer Drill-Down](/build-reports/cell-explorer-drill-down/) to see exactly which deals contribute to the value.
{{< /step >}}

---

## Result

You now have a probability-weighted revenue forecast driven directly by your pipeline data. Each refresh pulls the latest deal stages and amounts from Adaptive Planning, applies your tuned conversion rates, and shows month-by-month expected revenue against plan. Sales leadership sees pipeline coverage; FP&A sees a forecast they can defend with deal-level math.

## Next steps

- Add additional pipeline cuts by region or product — see [Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/)
- Compare this bottom-up forecast against the top-down plan — see [Compare Planning Versions](/build-reports/compare-planning-versions/)
- Score the forecast against actuals after the quarter closes — see [Build a Forecast Accuracy Report](/build-reports/forecast-accuracy/)
