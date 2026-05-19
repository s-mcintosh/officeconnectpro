# Build a Department P&L Report in OfficeConnect

Build a profit and loss report broken down by department or cost center using OfficeConnect's Level dimension.


---


A department P&L shows revenue, expenses, and net income for each business unit in the same workbook. OfficeConnect's Level dimension makes this straightforward — one row set per department, all pulling live data from the same Adaptive Planning model.

**What you'll build:** A P&L report with accounts as rows and departments as column groups, refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect connected to an Adaptive Planning tenant with Levels configured for your org structure
- An Adaptive Planning model with P&L accounts (Revenue, COGS, OpEx, Net Income)

---

## Step 1 — Set up your P&L account rows

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel, click the **OfficeConnect** tab, and sign in. The Reporting pane opens on the right.
{{< /step >}}

{{< step n="2" title="Add your P&L account hierarchy" >}}
Click cell **A3**. In the Reporting pane, expand **Accounts** and drag **Revenue** into A3. Continue in rows A4–A7 with: **Cost of Goods Sold**, **Gross Profit**, **Operating Expenses**, and **Net Income**. Gross Profit and Net Income are typically rollup accounts — OfficeConnect aggregates their child accounts automatically.
{{< /step >}}

---

## Step 2 — Add department (Level) columns

{{< step n="3" title="Add your version and time context" >}}
Click **B1** and drag your version (e.g., Actuals) from the Reporting pane into it. Click **B2** and drag your time period (e.g., full year or current month) into it.
{{< /step >}}

{{< step n="4" title="Add the first department Level element" >}}
Click **B3**. In the Reporting pane, expand **Levels** and find your first department (e.g., Sales). Drag it into **B3**. OfficeConnect creates a formula that pulls data for the Actuals version, the time in B2, and the Sales level.
{{< /step >}}

{{< step n="5" title="Copy B3 down for all account rows" >}}
Copy **B3** down to **B4:B7**. Each row picks up its own account from column A while sharing the Level in B3's formula structure.
{{< /step >}}

{{< step n="6" title="Add remaining departments" >}}
Repeat Step 4–5 for each department, placing each in its own column (C, D, E, etc.). Add column headers in row 1 with the department name — you can type these as labels or drag the Level element into row 1 and OfficeConnect will label it automatically.
{{< /step >}}

---

## Step 3 — Add a company total column

{{< step n="7" title="Add a Total column" >}}
In the rightmost column header row, drag your **top-level Level** (the parent of all departments) from the Reporting pane. This gives you a company-wide total column that rolls up all departments. Alternatively, use an Excel SUM formula across the department columns.
{{< /step >}}

---

## Step 4 — Refresh and verify

{{< step n="8" title="Refresh the report" >}}
Click **Refresh** in the OfficeConnect ribbon. All department columns populate from Adaptive Planning.
{{< /step >}}

{{< step n="9" title="Spot-check totals" >}}
Confirm that each department's Gross Profit = Revenue − COGS, and that Net Income = Gross Profit − Operating Expenses. If rollup accounts are showing unexpected values, check that the account hierarchy in your Adaptive Planning model is configured correctly.
{{< /step >}}

---

## Next steps

- Add a budget or prior-year comparison column — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- Protect the report for distribution — see [Lock and Protect Reports](/build-reports/lock-protect-reports/)
- Publish to PowerPoint — see [OfficeConnect for PowerPoint](/build-reports/officeconnect-for-powerpoint/)
