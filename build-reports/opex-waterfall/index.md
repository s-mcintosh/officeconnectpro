# Build an Operating Expense Waterfall

Build a month-over-month OpEx walk showing prior period, adds, reductions, and current period — visualized as an Excel waterfall chart driven by OfficeConnect data.


---


A waterfall walk is how finance teams explain *why* a number moved. Instead of just showing OpEx went from $4.2M to $4.6M, a waterfall breaks the $400K change into its components — new hires, marketing program, software renewal, T&E reduction. This tutorial walks through building one in Workday OfficeConnect using a native Excel waterfall chart with live Adaptive Planning data.

**What you'll build:** A two-column table of OpEx changes by account category, paired with an Excel waterfall chart that shows prior month, the adds and reductions in between, and the current month total.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/build-reports/build-first-report/))
- Actuals loaded for the current and prior month
- An OpEx account hierarchy in your model (Salaries, Marketing, Software, T&E, Other)
- Excel 2016 or later (for the built-in waterfall chart)

---

## Step 1 — Build the bridge data table

{{< step n="1" title="Lay out the row labels" >}}
On a blank sheet, in column A, type the bridge rows in order: `Prior Month Total`, then one row per OpEx category (`Salaries`, `Marketing`, `Software`, `T&E`, `Facilities`, `Other`), and finally `Current Month Total`. Leave column B for the value.
{{< /step >}}

{{< step n="2" title="Add helper columns for prior and current" >}}
In columns D and E (hide them later), add the prior-month and current-month OpEx values for each category. In D1 drag your **Actuals** version. In D2 drag **Current Month -1**. In E2 drag **Current Month**. In D3:D8, drag each category account; copy across to E3:E8.
{{< /step >}}

---

## Step 2 — Compute the bridge values

{{< step n="3" title="Set the anchor rows" >}}
In **B3** (Prior Month Total), write `=SUM(D3:D8)`. In the last row (Current Month Total), write `=SUM(E3:E8)`. These two cells are the bookends of the waterfall.
{{< /step >}}

{{< step n="4" title="Compute the deltas" >}}
For each category row, write `=E3-D3` in column B. A positive value is an add; a negative value is a reduction. The signs tell Excel's waterfall chart which direction the bar goes.
{{< /step >}}

{{< step n="5" title="Sanity check" >}}
Confirm that `Prior Month Total + SUM(deltas) = Current Month Total`. If it doesn't, an account category is missing or double-counted. The full hierarchy should roll up cleanly.
{{< /step >}}

---

## Step 3 — Insert the waterfall chart

{{< step n="6" title="Select the chart range" >}}
Highlight the A:B range covering Prior Month Total, all category rows, and Current Month Total. Go to **Insert → Charts → Waterfall**.
{{< /step >}}

{{< step n="7" title="Mark the totals" >}}
By default Excel treats every bar as a change. Right-click the *Prior Month Total* bar and choose **Set as Total**. Do the same for *Current Month Total*. The two ends now anchor to the axis baseline.
{{< /step >}}

{{< step n="8" title="Polish the chart" >}}
Use distinct colors for increases (positive deltas), decreases (negative), and totals. Add data labels showing the dollar value of each bar. Title the chart `Operating Expense Walk — Prior Month to Current Month`.
{{< /step >}}

---

## Step 4 — Refresh and reuse

{{< step n="9" title="Refresh and verify" >}}
Click **Refresh** on the OfficeConnect ribbon. The helper columns repopulate, the bridge column recalculates, and the waterfall chart redraws automatically.
{{< /step >}}

{{< step n="10" title="Hide the helper columns" >}}
Hide columns D and E so only the bridge table and chart are visible. Save as a template — next month, change only the time context if you used fixed periods, or rely on relative periods to roll forward automatically.
{{< /step >}}

{{< admin-note >}}
For a quarter-over-quarter or year-over-year walk, swap **Current Month** and **Current Month -1** for the relevant quarterly or annual contexts. The bridge math is identical.
{{< /admin-note >}}

---

## Result

You now have a self-refreshing OpEx waterfall that explains the month's movement at a glance. Executives stop asking "why did OpEx go up?" because the chart already shows them — $180K from new hires, $90K from a marketing program, offset by $40K less travel. The same template works for any month, quarter, or year.

## Next steps

- Apply the same pattern to revenue or gross margin walks — see [Year-over-Year Trend Report](/build-reports/year-over-year-trend/)
- Pair the waterfall with budget variance context — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- Use rolling periods so the walk always shows the latest month — see [Rolling 12-Month Report](/build-reports/rolling-12-month-report/)
