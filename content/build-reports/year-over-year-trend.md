---
title: "Build a Year-over-Year Trend Report"
linkTitle: "Year-over-Year Trend"
weight: 22
description: >
  Compare this year's actuals against the prior year month by month using fixed time elements in OfficeConnect.
tags: ["adaptive-planning", "tutorial", "reporting"]
---

A year-over-year trend report shows how each month compares to the same month last year — useful for spotting seasonal patterns and measuring real growth. OfficeConnect's time elements let you pin both years in the same report.

**What you'll build:** A report with 12 months of current-year actuals alongside 12 months of prior-year actuals, plus a YoY variance row.

**What you'll need:**
- OfficeConnect connected to an Adaptive Planning tenant with at least two full years of actuals
- Familiarity with adding elements ([Add Elements](/build-reports/add-elements/)) and time contexts ([Time and Contexts](/build-reports/time-and-contexts/))

---

## Step 1 — Set up current-year monthly columns

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel and click the **OfficeConnect** tab. Sign in if prompted.
{{< /step >}}

{{< step n="2" title="Add your Actuals version" >}}
Click **B1**. In the Reporting pane, expand **Versions** and drag your **Actuals** version into B1. This version applies to all columns that share row 1.
{{< /step >}}

{{< step n="3" title="Add current-year monthly time elements" >}}
Click **B2**. In the Reporting pane, expand **Time → Months** and find January of the current year (e.g., Jan 2026). Drag it into B2. Continue across row 2 — C2 through M2 — adding Feb 2026 through Dec 2026. You should have 12 monthly time elements across row 2.
{{< /step >}}

---

## Step 2 — Set up prior-year monthly columns

{{< step n="4" title="Add prior-year Actuals version" >}}
Click **N1**. Drag your **Actuals** version into N1. (It's the same version — the time elements in row 2 control which year's data loads.)
{{< /step >}}

{{< step n="5" title="Add prior-year monthly time elements" >}}
Click **N2**. Drag Jan 2025 into N2. Continue across — O2 through Y2 — adding Feb 2025 through Dec 2025.
{{< /step >}}

---

## Step 3 — Add account rows

{{< step n="6" title="Add your primary account" >}}
Click **A3**. In the Reporting pane, expand **Accounts** and drag your key account (e.g., Revenue) into A3.
{{< /step >}}

{{< step n="7" title="Populate the data row" >}}
Click **B3**. OfficeConnect formulas reference the version in row 1 and the time in row 2, so B3 returns Jan 2026 Actuals for Revenue. Copy B3 across to Y3 — each cell picks up the correct month and year from its column.
{{< /step >}}

{{< step n="8" title="Add remaining account rows" >}}
Copy row 3 down for each additional account. Add more accounts to column A as needed.
{{< /step >}}

---

## Step 4 — Add YoY variance

{{< step n="9" title="Add a variance section header" >}}
In column Z row 1, type `YoY Variance`. Leave Z2 empty.
{{< /step >}}

{{< step n="10" title="Add monthly variance formulas" >}}
In **B4** (one row below your last account row, or in a dedicated variance row), enter:
```
=B3-N3
```
This subtracts the prior-year January value from the current-year January value. Copy across to M4. Each cell compares the same calendar month between the two years.
{{< /step >}}

{{< step n="11" title="Add a percentage YoY row" >}}
In row 5, enter `=B3/N3-1` in B5 and copy across to M5. Format this row as percentage. This gives you the YoY growth rate for each month.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="12" title="Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon. Both years of data populate. Check that December 2025 (your last prior-year column) and December 2026 (your last current-year column) show the expected values.
{{< /step >}}

---

> **Tip:** To make column headers show as "Jan 26 / Jan 25" instead of the full OfficeConnect element name, add a row above row 2 with custom Excel text labels. OfficeConnect doesn't require headers to be in row 1 — the element formula just needs to be in a cell the data rows reference.

---

## Next steps

- Add a rolling 12-month view alongside fixed years — see [Create a Rolling 12-Month Report](/tutorials/rolling-12-month-report/)
- Compare budget and actuals for the same period — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- Share the finished report — see [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
