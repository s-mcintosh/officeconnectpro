# Build a Budget vs. Actuals Variance Report

Build an OfficeConnect report that shows budget, actuals, and variance side by side — the most common FP&A report in Adaptive Planning.


---


A budget vs. actuals variance report puts your plan and your reality in the same view. This tutorial walks through building one in OfficeConnect with a variance column that calculates automatically in Excel.

**What you'll build:** A report with monthly actuals and budget columns for each account, plus a variance column showing the difference — all refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
- An Adaptive Planning model with at least one Budget version and actuals loaded for the same period
- Basic familiarity with adding elements ([Add Elements](/get-started/build-reports/add-elements/))

---

## Step 1 — Set up your account rows

{{< step n="1" title="Open a workbook and activate OfficeConnect" >}}
Open Excel and click the **OfficeConnect** tab in the ribbon. Sign in if prompted. The Reporting pane opens on the right.
{{< /step >}}

{{< step n="2" title="Add your first account" >}}
Click cell **A3** — this will hold your first account label. In the Reporting pane, expand **Accounts** and drag **Revenue** (or your top-line account) into A3. OfficeConnect inserts a formula that resolves to the account name.
{{< /step >}}

{{< step n="3" title="Add remaining account rows" >}}
Click A4, A5, A6, and so on. Drag in each account you need: Cost of Goods Sold, Gross Profit, Operating Expenses, Net Income. Place each in its own row. For rollup accounts, OfficeConnect automatically aggregates child accounts.
{{< /step >}}

---

## Step 2 — Add Actuals and Budget version columns

{{< step n="4" title="Add an Actuals column header" >}}
Click cell **B1**. In the Reporting pane, expand **Versions** and drag your **Actuals** version into B1. OfficeConnect labels the cell with the version name.
{{< /step >}}

{{< step n="5" title="Add a Budget column header" >}}
Click cell **C1**. Drag your **Budget** version into C1.
{{< /step >}}

{{< step n="6" title="Add a time context" >}}
Click cell **B2**. In the Reporting pane, expand **Time** and drag the period you want to report on (for example, the current month or a full year) into B2. Copy B2 into C2 — both columns share the same time context.
{{< /step >}}

---

## Step 3 — Build the data cells and variance column

{{< step n="7" title="Populate the first data row" >}}
Click **B3**. OfficeConnect formulas reference the version in row 1 and the time in row 2, so B3 automatically resolves to Actuals for your chosen period. Copy B3 across to C3 — C3 resolves to Budget for the same period.
{{< /step >}}

{{< step n="8" title="Add a variance column header" >}}
Click **D1** and type `Variance`. Click **D2** and type `$` (or leave it blank — this cell doesn't need an OfficeConnect element).
{{< /step >}}

{{< step n="9" title="Write the variance formula" >}}
Click **D3** and enter:
```
=B3-C3
```
This is a plain Excel formula. OfficeConnect doesn't control column D — it just reads the live values from B3 and C3 after each refresh.
{{< /step >}}

{{< step n="10" title="Copy down for all account rows" >}}
Select B3:D3 and copy down to cover all your account rows. Each row picks up its own account from column A.
{{< /step >}}

---

## Step 4 — Refresh and verify

{{< step n="11" title="Click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon. Actuals and Budget columns populate from Adaptive Planning. The Variance column calculates automatically.
{{< /step >}}

{{< step n="12" title="Check for expected values" >}}
Spot-check a row against a known figure in Adaptive Planning (open the same account and period in a sheet). If a cell shows `#VALUE!` or `0`, the version or time element may not have data — confirm the period is loaded in your model.
{{< /step >}}

---

## Optional: Add a percentage variance column

Add column E with the header `Var %` and the formula `=(B3-C3)/ABS(C3)`. Format the column as percentage. This gives you both dollar and percentage variance side by side.

---

## Next steps

- Expand to multiple months by adding more time columns — see [Time and Contexts](/get-started/build-reports/time-and-contexts/)
- Add department rows using Level elements — see [Build a Department P&L Report](/get-started/build-reports/department-pl-report/)
- Share the finished report with your team — see [Share via Teams & SharePoint](/get-started/word-powerpoint/sharing/share-teams-sharepoint-onedrive/)
