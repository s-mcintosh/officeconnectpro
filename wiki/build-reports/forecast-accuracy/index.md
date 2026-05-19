---
title: "Build a Forecast Accuracy Report"
url: "https://officeconnectpro.com/wiki/build-reports/forecast-accuracy/"
description: "Build a report that compares a prior forecast version to actuals and calculates absolute error and MAPE by account and period.\n"
tags: ["reporting","adaptive-planning","fpna","performance","recipe"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Every FP&A team is asked the same question eventually: how accurate is the forecast? A forecast accuracy report answers that question with math, not anecdote. This tutorial walks through building one in Workday OfficeConnect — comparing a prior forecast version (for example, the forecast made three months ago) against actuals, then calculating absolute error and MAPE (Mean Absolute Percentage Error) by account and period.

**What you'll build:** A table with Forecast, Actual, Absolute Error, and Error % columns by account and month, plus a MAPE summary row.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/wiki/build-reports/build-first-report/))
- At least one snapshot forecast version (for example, `Forecast Q1` or `Forecast 3-Month-Ago`) preserved in Adaptive Planning
- Actuals loaded for the same period the forecast covered
- Familiarity with version selection ([Compare Planning Versions](/wiki/build-reports/compare-planning-versions/))

---

## Step 1 — Set up the comparison columns

{{< step n="1" title="Add the version headers" >}}
On a blank sheet, click **B1** and drag your prior forecast version (for example, **Forecast Q1 FY25**). Click **C1** and drag your **Actuals** version.
{{< /step >}}

{{< step n="2" title="Add the period context" >}}
Click **B2** and drag the time element the forecast was originally made for — typically the months the forecast covered. Copy B2 into C2. Both columns must share the same time context, or the comparison is meaningless.
{{< /step >}}

---

## Step 2 — Add account rows

{{< step n="3" title="List the accounts to score" >}}
In column A, list the accounts whose forecast accuracy matters — Revenue, COGS, Gross Profit, Operating Expenses, and any major OpEx subcategories. Drag the matching account into each row of column B; the formulas resolve against the forecast version.
{{< /step >}}

{{< step n="4" title="Copy across to Actuals" >}}
Select B3:B12 and copy into C3:C12. Column C now resolves the same accounts against Actuals for the same period.
{{< /step >}}

---

## Step 3 — Calculate error metrics

{{< step n="5" title="Add Absolute Error" >}}
In **D1** type `Abs Error`. In **D3** write:
```
=ABS(C3-B3)
```
Copy down for all account rows.
{{< /step >}}

{{< step n="6" title="Add Error %" >}}
In **E1** type `Error %`. In **E3** write:
```
=ABS(C3-B3)/ABS(C3)
```
Format column E as a percentage. Dividing by actuals (not forecast) is the convention for MAPE.
{{< /step >}}

{{< step n="7" title="Handle zero actuals" >}}
If any account has zero actuals, Error % returns `#DIV/0!`. Wrap the formula in `IFERROR(..., "")` to suppress the error, or exclude the row from the MAPE summary.
{{< /step >}}

---

## Step 4 — Add a MAPE summary

{{< step n="8" title="Compute MAPE across accounts" >}}
Below your last account row, add a row labeled `MAPE`. In the Error % column for that row, write:
```
=AVERAGE(E3:E12)
```
This is the Mean Absolute Percentage Error across all scored accounts. Format as percentage.
{{< /step >}}

{{< step n="9" title="Add a forecast-bias indicator" >}}
Optionally, add a column F titled `Signed Error` with `=C3-B3` (no absolute value). The average of this column tells you whether the forecast was systematically high (negative) or low (positive). A MAPE of 5% with a strong bias is a different problem than a MAPE of 5% that averages to zero.
{{< /step >}}

{{< admin-note >}}
For period-by-period accuracy, replicate the entire column set across multiple months. You can then compute MAPE per period and watch whether forecasting quality is improving or degrading over time.
{{< /admin-note >}}

---

## Step 5 — Refresh and interpret

{{< step n="10" title="Refresh and review" >}}
Click **Refresh**. The accuracy table populates. A MAPE under 5% on revenue is generally strong; over 15% suggests the forecast process needs revisiting. Look for which accounts consistently miss — those are the ones to dig into with the forecast owner.
{{< /step >}}

---

## Result

You now have an objective forecast accuracy scorecard. Each month or quarter, refresh the workbook and the report tells you exactly which accounts the prior forecast nailed and which it missed — and by how much. Over time, you can watch MAPE trend down as the forecasting process improves.

## Next steps

- Compare multiple forecast vintages side by side — see [Compare Planning Versions](/wiki/build-reports/compare-planning-versions/)
- Pair accuracy data with budget variance — see [Budget vs. Actuals Variance](/wiki/build-reports/budget-vs-actuals-variance/)
- Run accuracy across multiple scenarios — see [Scenario Comparison](/wiki/build-reports/scenario-comparison/)

