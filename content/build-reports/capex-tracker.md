---
title: "Build a Capital Expenditure Tracker"
linkTitle: "CapEx Tracker"
weight: 48
description: >
  Build a project-level CapEx tracker with planned spend, actual spend, forecast remaining, and budget variance — driven by a Project Code custom dimension.
tags: ["reporting", "adaptive-planning", "fpna", "recipe"]
---

Capital expenditure usually starts the year as a tidy plan and ends it as a sprawling list of in-flight projects and reforecasts. A good CapEx tracker keeps the picture coherent — project by project, plan vs. actual, with a clear view of remaining spend. This tutorial walks through building one in Workday OfficeConnect using a Project Code custom dimension in Adaptive Planning.

**What you'll build:** A project-level tracker with Planned, Actual YTD, Forecast Remaining, Total Forecast, and Variance to Plan columns — refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- A **Project Code** custom dimension in your model with each active CapEx project loaded
- CapEx accounts (Capital Expenditures or specific asset categories) dimensionalized by Project Code
- A Plan/Budget version and an Actuals version for the current year
- Familiarity with custom dimensions ([Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/))

---

## Step 1 — Set up the column headers

{{< step n="1" title="Add the column headers" >}}
On a blank sheet, in row 1 type: `Project Code`, `Planned (FY)`, `Actual YTD`, `Forecast Remaining`, `Total Forecast`, `Variance to Plan`, `% Spent`. These are the columns reviewers expect on a CapEx tracker.
{{< /step >}}

{{< step n="2" title="Add the version and time elements" >}}
Use a hidden helper area (for example, columns J:M, rows 1-3) to drop your Adaptive Planning context. In J1 drag the **Plan** version, in K1 drag **Actuals**, in L1 drag **Forecast**. In their respective rows below, drop **FY (Total Year)**, **Year-to-Date**, and **Remainder of Year** time elements.
{{< /step >}}

---

## Step 2 — Build the project row block

{{< step n="3" title="Add the first project row" >}}
Click A2 and drag a Project Code from the **Project Code** custom dimension (for example, `CAP-2025-001`). The dimension value populates column A.
{{< /step >}}

{{< step n="4" title="Populate the Planned column" >}}
In B2, drag the **Capital Expenditures** account, scoped to the Plan version and FY time. The cell resolves to that project's full-year planned spend.
{{< /step >}}

{{< step n="5" title="Populate Actual YTD" >}}
In C2, drag the same account scoped to the Actuals version and Year-to-Date time. The cell resolves to spend incurred so far this year on that project.
{{< /step >}}

{{< step n="6" title="Populate Forecast Remaining" >}}
In D2, drag the same account scoped to the Forecast version and the Remainder of Year time. This is the project owner's reforecast for what's still to come.
{{< /step >}}

---

## Step 3 — Add the calculated columns

{{< step n="7" title="Compute Total Forecast" >}}
In E2, write `=C2+D2`. This is Actual YTD plus Forecast Remaining — the project's expected full-year landing.
{{< /step >}}

{{< step n="8" title="Compute Variance to Plan" >}}
In F2, write `=E2-B2`. Positive values mean the project is forecasting over budget; negative values mean under.
{{< /step >}}

{{< step n="9" title="Compute % Spent" >}}
In G2, write `=C2/B2`. Format as percentage. This shows how much of the original plan has already been spent — useful for identifying projects that are 80% spent but only halfway through the year.
{{< /step >}}

{{< admin-note >}}
For projects renamed or restructured under a new Project Code mid-year, the dimension lookup will miss historical spend. Confirm with the project owner whether one code captures all activity or you need to sum across multiple codes.
{{< /admin-note >}}

---

## Step 4 — Scale across projects

{{< step n="10" title="Use repeating rows by Project Code" >}}
Rather than copying the row manually per project, configure row 2 as a repeating row scoped on the **Project Code** dimension. OfficeConnect generates one row per active project on refresh. The full pattern is covered in [Repeating Reports](/build-reports/repeating-reports/).
{{< /step >}}

{{< step n="11" title="Add a Total row" >}}
At the bottom, add a `Total` row that SUMs columns B through F across all projects. The program-level % Spent is `=SUM(C)/SUM(B)`.
{{< /step >}}

---

## Step 5 — Refresh and review

{{< step n="12" title="Refresh and flag the outliers" >}}
Click **Refresh**. Sort by Variance to Plan descending to surface projects at risk of overrun. Use conditional formatting to highlight any % Spent over 90% on projects whose Total Forecast is under plan — those are nearly done with budget to spare.
{{< /step >}}

---

## Result

You now have a project-by-project CapEx tracker that shows in one view which projects are tracking to plan, which are at risk, and which are coming in under budget. Each refresh updates the picture with the latest actuals and project owner reforecasts.

## Next steps

- Pair the tracker with a cash impact view — see [Cash Flow Statement](/build-reports/financials/cash-flow-statement/)
- Add a forecast accuracy view against the original plan — see [Build a Forecast Accuracy Report](/build-reports/forecast-accuracy/)
- Drill down into any project's underlying transactions — see [Cell Explorer Drill-Down](/build-reports/cell-explorer-drill-down/)
