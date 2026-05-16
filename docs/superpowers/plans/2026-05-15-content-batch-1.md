# Content Batch 1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish 16 new articles across FP&A (Adaptive Planning) and Accounting (Financials) audiences to make officeconnectpro.com the most comprehensive OfficeConnect resource online.

**Architecture:** All articles are Hugo Markdown files. FP&A articles extend the existing `content/build-reports/` section (weights 20–27). Accounting articles go into a new `content/build-reports/financials/` subsection (weights 1–8 within that section). Each tutorial uses the `step` shortcode (`{{< step n="N" title="Title" >}}content{{< /step >}}`). Admin-only steps use the `admin-note` shortcode (`{{< admin-note >}}content{{< /admin-note >}}`). How-to guides use plain numbered prose — no shortcodes.

**Tech Stack:** Hugo extended v0.161+, Docsy theme, GitHub Pages. Local dev: `hugo server` at `http://localhost:1313`.

---

## File Map

| File | Type |
|---|---|
| `content/build-reports/financials/_index.md` | New subsection index |
| `content/build-reports/budget-vs-actuals-variance.md` | Tutorial |
| `content/build-reports/department-pl-report.md` | Tutorial |
| `content/build-reports/year-over-year-trend.md` | Tutorial |
| `content/build-reports/compare-planning-versions.md` | How-to |
| `content/build-reports/headcount-in-financial-report.md` | How-to |
| `content/build-reports/lock-protect-reports.md` | How-to |
| `content/build-reports/scenario-comparison.md` | How-to |
| `content/build-reports/constant-currency-reporting.md` | How-to |
| `content/build-reports/financials/trial-balance-report.md` | Tutorial |
| `content/build-reports/financials/drill-through-journal-lines.md` | Tutorial |
| `content/build-reports/financials/actuals-trend-report.md` | Tutorial |
| `content/build-reports/financials/actuals-by-cost-center.md` | How-to |
| `content/build-reports/financials/effective-date-reporting.md` | How-to |
| `content/build-reports/financials/filter-by-company.md` | How-to |
| `content/build-reports/financials/intercompany-eliminations.md` | How-to |
| `content/build-reports/financials/multi-currency-financials.md` | How-to |

---

## Task 0: Create Financials Subsection

**Files:**
- Create: `content/build-reports/financials/_index.md`

- [ ] **Step 1: Create the subsection index**

Write the following to `content/build-reports/financials/_index.md`:

```markdown
---
title: "Financials Data Source"
linkTitle: "Financials"
weight: 20
type: docs
description: >
  Build OfficeConnect reports against Workday Financial Management (GL actuals) — for accounting teams reporting on posted transactions.
cascade:
  type: docs
---

This section covers OfficeConnect with the **Financials data source** — Workday Financial Management's general ledger actuals. If your organization uses Workday Financial Management alongside Adaptive Planning, accounting teams use this data source to report on posted journal entries, trial balances, and actuals by cost center.

Not sure which data source you're on? See [Adaptive Planning vs. Financials Data Source](/build-reports/financials-vs-adaptive-planning/) for a full comparison.
```

- [ ] **Step 2: Start the local server and verify the section appears**

```bash
hugo server
```

Open `http://localhost:1313/build-reports/financials/`. You should see a page titled "Financials Data Source" with the intro text and a link to the comparison page. The sidebar should show "Financials" under "Build Reports."

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/_index.md
git commit -m "feat: add Financials subsection for accounting content"
```

---

## Task 1: Budget vs. Actuals Variance Report (Tutorial)

**Files:**
- Create: `content/build-reports/budget-vs-actuals-variance.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/budget-vs-actuals-variance.md`:

```markdown
---
title: "Build a Budget vs. Actuals Variance Report"
linkTitle: "Budget vs. Actuals Variance"
weight: 20
description: >
  Build an OfficeConnect report that shows budget, actuals, and variance side by side — the most common FP&A report in Adaptive Planning.
---

A budget vs. actuals variance report puts your plan and your reality in the same view. This tutorial walks through building one in OfficeConnect with a variance column that calculates automatically in Excel.

**What you'll build:** A report with monthly actuals and budget columns for each account, plus a variance column showing the difference — all refreshable from Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
- An Adaptive Planning model with at least one Budget version and actuals loaded for the same period
- Basic familiarity with adding elements ([Add Elements](/build-reports/add-elements/))

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

- Expand to multiple months by adding more time columns — see [Time and Contexts](/build-reports/time-and-contexts/)
- Add department rows using Level elements — see [Build a Department P&L Report](/build-reports/department-pl-report/)
- Share the finished report with your team — see [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
```

- [ ] **Step 2: Verify it renders**

With `hugo server` running, open `http://localhost:1313/build-reports/budget-vs-actuals-variance/`. Confirm: title appears, all 12 `step` blocks render with numbered circles, next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/budget-vs-actuals-variance.md
git commit -m "feat: add Budget vs Actuals Variance tutorial"
```

---

## Task 2: Department P&L Report (Tutorial)

**Files:**
- Create: `content/build-reports/department-pl-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/department-pl-report.md`:

```markdown
---
title: "Build a Department P&L Report in OfficeConnect"
linkTitle: "Department P&L Report"
weight: 21
description: >
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
- Publish to PowerPoint — see [OfficeConnect for PowerPoint](/share-publish/officeconnect-for-powerpoint/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/department-pl-report/`. Confirm step blocks render and next-steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/department-pl-report.md
git commit -m "feat: add Department P&L Report tutorial"
```

---

## Task 3: Year-over-Year Trend Report (Tutorial)

**Files:**
- Create: `content/build-reports/year-over-year-trend.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/year-over-year-trend.md`:

```markdown
---
title: "Build a Year-over-Year Trend Report"
linkTitle: "Year-over-Year Trend"
weight: 22
description: >
  Compare this year's actuals against the prior year month by month using fixed time elements in OfficeConnect.
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
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/year-over-year-trend/`. Confirm step blocks, tip callout, and all links render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/year-over-year-trend.md
git commit -m "feat: add Year-over-Year Trend tutorial"
```

---

## Task 4: Compare Two Planning Versions (How-to)

**Files:**
- Create: `content/build-reports/compare-planning-versions.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/compare-planning-versions.md`:

```markdown
---
title: "Compare Two Planning Versions Side by Side"
linkTitle: "Compare Planning Versions"
weight: 23
description: >
  Add a second version column to any OfficeConnect report to compare Budget vs. Forecast, two plan iterations, or any two Adaptive Planning versions.
---

Any OfficeConnect report can show multiple versions at once. Here's how to add a second version column alongside your existing data.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Click an empty column header cell (for example, **C1** if your existing data is in column B).

3. In the Reporting pane, expand **Versions** and drag the second version (e.g., Forecast) into C1.

4. Click **C2** and drag the same time element you used in B2 into C2. Both columns now share the same time period.

5. Click **C3** and copy your existing data formula from B3 into it. OfficeConnect resolves C3 using the version in C1 and the time in C2.

6. Copy C3 down for all account rows.

7. Click **Refresh**. Column C populates with the second version's data.

> **Note:** The version element must exist in your Adaptive Planning model. If a version doesn't appear in the Reporting pane, check that you have read access to it in Adaptive Planning under Administration > Users.

## Common version comparisons

| Scenario | Column 1 | Column 2 |
|---|---|---|
| Budget vs. Actuals | Actuals | Budget |
| Current forecast vs. prior forecast | Forecast v2 | Forecast v1 |
| Board case vs. management case | Board Plan | Mgmt Plan |
| Actuals vs. prior year actuals | Actuals (current year) | Actuals (prior year) |

For a full budget vs. actuals report with a variance column, see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/).
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/compare-planning-versions/`. Confirm the table and note render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/compare-planning-versions.md
git commit -m "feat: add Compare Planning Versions how-to"
```

---

## Task 5: Add Headcount Data to a Financial Report (How-to)

**Files:**
- Create: `content/build-reports/headcount-in-financial-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/headcount-in-financial-report.md`:

```markdown
---
title: "Add Headcount Data to a Financial Report"
linkTitle: "Headcount in Financial Reports"
weight: 24
description: >
  Mix workforce planning metrics (headcount, FTEs, salary cost) with financial accounts in a single OfficeConnect report.
---

OfficeConnect doesn't separate financial and workforce accounts — they're all elements in your Adaptive Planning model. You can add headcount rows to any financial report by dragging the right accounts from the Reporting pane.

## Steps

1. Open your financial report in Excel and click the **OfficeConnect** tab.

2. Click an empty row below your financial accounts — for example, **A10** if your P&L ends at row 9.

3. In the Reporting pane, expand **Accounts** and look for your workforce accounts. Common names include:
   - **Headcount** (total employee count)
   - **FTEs** (full-time equivalents)
   - **Salaries & Benefits** (may already appear in your P&L)
   - **Open Positions**

4. Drag the headcount account into **A10**. OfficeConnect inserts a formula using the version and time context already set up in your report.

5. Copy the data formula from the row above (e.g., B9) into **B10** and across the row. Headcount resolves using the same version and time elements.

6. Click **Refresh**. The headcount row populates alongside your financial data.

> **Tip:** Headcount is often stored in a different account group than financial accounts (e.g., under a "Workforce" or "HR" section in the Accounts tree). If you don't see it, expand all groups in the Reporting pane or search by name.

## Keeping units clear

Headcount values are typically whole numbers while financial values are in thousands (or your model's default rounding). To avoid confusion:

- Format the headcount row with **no decimal places** and **no currency symbol** (Format Cells → Number → 0)
- Add a label in column A noting the unit: "Headcount (FTEs)"
- Use a thin border or shading to visually separate the headcount section from the financials above it

## Related

- [Workbook and Worksheet Properties](/build-reports/workbook-worksheet-properties/) — set default rounding for the whole workbook
- [Build a Department P&L Report](/build-reports/department-pl-report/) — organize by Level before adding headcount rows
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/headcount-in-financial-report/`. Confirm tips and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/headcount-in-financial-report.md
git commit -m "feat: add Headcount in Financial Reports how-to"
```

---

## Task 6: Lock and Protect Reports for Distribution (How-to)

**Files:**
- Create: `content/build-reports/lock-protect-reports.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/lock-protect-reports.md`:

```markdown
---
title: "Lock and Protect Reports for Distribution"
linkTitle: "Lock and Protect Reports"
weight: 25
description: >
  Protect an OfficeConnect workbook for distribution so recipients can't accidentally break formulas — while keeping Refresh working.
---

When you share an OfficeConnect report with people who shouldn't edit it, Excel's sheet protection prevents accidental changes. The catch: you must leave OfficeConnect formula cells unlocked, or Refresh will fail with a "sheet is protected" error.

## How OfficeConnect cells work with protection

OfficeConnect stores data in formula cells. When you click Refresh, OfficeConnect writes new values into those cells. If the sheet is protected and those cells are locked, Refresh fails. The solution: unlock the OfficeConnect cells before protecting the sheet.

## Steps

1. Open your OfficeConnect workbook and click **Refresh** once to make sure all OfficeConnect cells are populated.

2. Select all cells: **Ctrl+A** (or **Cmd+A** on Mac).

3. Open Format Cells: **Ctrl+1** (or right-click → Format Cells). Go to the **Protection** tab. Check **Locked**. Click OK. This locks every cell by default.

4. Now select only the OfficeConnect cells — the cells containing element formulas (they typically look like `=OC(...)` or similar). You can identify them by clicking each cell and checking the formula bar for an OfficeConnect formula.

   > **Tip:** Use **Ctrl+G → Special → Formulas** to select all formula cells at once. This selects both OfficeConnect formulas and any Excel formulas you've added (like variance calculations). Deselect the Excel-only formula cells if you want those locked.

5. With the OfficeConnect cells selected, open Format Cells again → Protection → **uncheck Locked** → OK.

6. Go to **Review → Protect Sheet**. Set a password if desired. Under "Allow all users of this worksheet to:", leave the defaults (select locked cells, select unlocked cells). Click OK.

7. Click **Refresh** to confirm it still works. If you see a protection error, repeat steps 4–5 — some OfficeConnect cells were missed.

## What recipients can and can't do

| Action | Allowed |
|---|---|
| Click Refresh | Yes (OfficeConnect cells are unlocked) |
| Read data | Yes |
| Edit OfficeConnect formulas | No |
| Edit your Excel labels and headers | No (unless you unlocked them) |
| Add rows or columns | No |

## Related

- [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/) — distribute the protected workbook
- [Secure Workbooks](/connect/secure-workbooks/) — additional security options at the tenant level
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/lock-protect-reports/`. Confirm the table and tip callout render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/lock-protect-reports.md
git commit -m "feat: add Lock and Protect Reports how-to"
```

---

## Task 7: Set Up Scenario Comparison (How-to)

**Files:**
- Create: `content/build-reports/scenario-comparison.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/scenario-comparison.md`:

```markdown
---
title: "Set Up Scenario Comparison in OfficeConnect"
linkTitle: "Scenario Comparison"
weight: 26
description: >
  Compare planning scenarios side by side in OfficeConnect — useful for showing upside, base case, and downside in the same report.
---

Scenarios in Adaptive Planning are planning alternatives within a version — for example, a Base Case, Upside, and Downside within your annual Budget version. OfficeConnect can display multiple scenarios in the same report, making it easy to show a range of outcomes.

## Before you begin

Scenarios must be configured in your Adaptive Planning model before they appear in OfficeConnect. If you don't see scenarios in the Reporting pane, ask your Adaptive Planning administrator to confirm they are enabled and that you have read access.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Set up your account rows and time columns as usual — scenarios apply to the version layer, not the account or time layer.

3. Click your first version column header (e.g., **B1**). In the Reporting pane, expand **Versions** and locate your version. Expand it to see available scenarios. Drag the **Base Case** scenario into B1.

4. Click the next column header (**C1**). Drag the **Upside** scenario into C1.

5. Click **D1** and drag the **Downside** scenario into D1.

6. Add the same time element to B2, C2, and D2.

7. Copy your account formulas across rows for each scenario column.

8. Click **Refresh**. Each column populates with data from its respective scenario.

> **Note:** Scenarios that have no data entered in Adaptive Planning return blank or zero in OfficeConnect. If a scenario column is empty after refresh, confirm that data has been entered for that scenario in Adaptive Planning sheets.

## Adding a scenario variance

To show the difference between Upside and Base Case, add an Excel formula column:

- Column E header: `Upside vs. Base`
- E3 formula: `=C3-B3`

Copy down for all rows. This is a plain Excel formula — it updates automatically when you refresh.

## Related

- [Compare Two Planning Versions Side by Side](/build-reports/compare-planning-versions/)
- [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/scenario-comparison/`. Confirm note callout and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/scenario-comparison.md
git commit -m "feat: add Scenario Comparison how-to"
```

---

## Task 8: Constant Currency Reporting (How-to)

**Files:**
- Create: `content/build-reports/constant-currency-reporting.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/constant-currency-reporting.md`:

```markdown
---
title: "Report in Constant Currency in OfficeConnect"
linkTitle: "Constant Currency Reporting"
weight: 27
description: >
  Use a constant currency version in Adaptive Planning to remove FX impact from OfficeConnect reports — useful for multinational teams comparing performance across periods.
---

Constant currency reporting holds foreign exchange rates fixed at a baseline period so you can see underlying business performance without FX noise. In Adaptive Planning, this is done through a dedicated constant currency version. OfficeConnect surfaces that version like any other — you just need to know which one to select.

## How constant currency works in Adaptive Planning

Your Adaptive Planning administrator sets up a constant currency version by configuring currency conversion rules that use a fixed rate (for example, the prior-year average rate or a budget rate). When you report against this version, all values are translated at that fixed rate regardless of the reporting period.

This is different from reporting in a single currency (e.g., USD only) — constant currency still shows values in your chosen currency but removes the variability caused by rate fluctuations between periods.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Identify your constant currency version — common names include **Constant Currency**, **CC Actuals**, **FX Neutral**, or **Budget Rate Actuals**. If you're unsure, ask your Adaptive Planning administrator which version uses fixed rates.

3. Set up your report as usual with account rows and time columns.

4. In your version column header (e.g., **B1**), drag the constant currency version from the Reporting pane into the cell instead of your standard Actuals version.

5. To compare constant currency actuals against reported actuals, add a second column (**C1**) with the standard Actuals version.

6. Add an Excel variance column (**D**) with the formula `=B3-C3` to show the FX impact.

7. Click **Refresh**. Column B shows performance at fixed rates; column C shows performance at actual rates; column D shows the FX impact.

> **Note:** If your model does not have a constant currency version, OfficeConnect cannot create one — this must be configured in Adaptive Planning. See your Workday administrator to set up currency conversion rules.

## Labeling your report clearly

Constant currency reports can confuse readers who don't know which rates were used. Add a text cell near the top of your workbook noting the base period rate — for example: *"Values in column B translated at FY2025 average rates."*

## Related

- [Compare Two Planning Versions Side by Side](/build-reports/compare-planning-versions/)
- [Multi-Currency Reporting with the Financials Data Source](/build-reports/financials/multi-currency-financials/) — currency options for accounting teams on the Financials data source
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/constant-currency-reporting/`. Confirm note callout and cross-links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/constant-currency-reporting.md
git commit -m "feat: add Constant Currency Reporting how-to"
```

---

## Task 9: Trial Balance Report — Financials (Tutorial)

**Files:**
- Create: `content/build-reports/financials/trial-balance-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/trial-balance-report.md`:

```markdown
---
title: "Build a Trial Balance Report with OfficeConnect (Financials)"
linkTitle: "Trial Balance Report"
weight: 1
description: >
  Build a live trial balance in Excel using OfficeConnect's Financials data source — pulling posted GL actuals directly from Workday Financial Management.
---

A trial balance lists every ledger account with its debit or credit balance for a given period. With OfficeConnect's Financials data source, you can build one that refreshes directly from Workday Financial Management — no export, no copy-paste.

**What you'll build:** A trial balance report showing all ledger accounts grouped by type (Assets, Liabilities, Equity, Revenue, Expenses) for a selected company and period.

**What you'll need:**
- OfficeConnect installed and connected to a tenant configured for the **Financials data source** (not Adaptive Planning)
- Access to at least one company with posted journal entries in Workday Financial Management
- The [Financials vs. Adaptive Planning](/build-reports/financials-vs-adaptive-planning/) page explains the difference if you're unsure which data source you have

---

## Step 1 — Confirm your data source

{{< step n="1" title="Check your data source" >}}
Click the **OfficeConnect** tab in Excel and sign in. In the Reporting pane, look at the top of the element tree. If you see **Ledger Accounts** and **Company**, you're on the Financials data source. If you see **Accounts** and **Levels**, you're on Adaptive Planning. This tutorial requires the Financials data source.
{{< /step >}}

---

## Step 2 — Add Company and Period context

{{< step n="2" title="Add your Company element" >}}
Click **B1**. In the Reporting pane, expand **Company** and drag your company (legal entity) into B1. If you have multiple companies, start with one — you can add more later.
{{< /step >}}

{{< step n="3" title="Add your Version" >}}
Click **B2**. In the Reporting pane, expand **Versions** and drag **Actuals** into B2.
{{< /step >}}

{{< step n="4" title="Add your Period" >}}
Click **B3**. In the Reporting pane, expand **Time** and drag the period you want (e.g., December 2025) into B3. For a year-end trial balance, use the last period of your fiscal year.
{{< /step >}}

---

## Step 3 — Add ledger account rows

{{< step n="5" title="Add an Assets section header" >}}
Click **A5** and type `ASSETS`. Bold it. This is a plain Excel label — not an OfficeConnect element.
{{< /step >}}

{{< step n="6" title="Add asset ledger accounts" >}}
Click **A6**. In the Reporting pane, expand **Ledger Accounts → Assets** (or the equivalent group in your chart of accounts). Drag your first asset account (e.g., Cash) into A6. Continue adding asset accounts in A7, A8, etc.
{{< /step >}}

{{< step n="7" title="Add the data formula for assets" >}}
Click **B6**. The OfficeConnect formula references the company in B1, the version in B2, and the period in B3. Copy B6 down for all asset account rows.
{{< /step >}}

{{< step n="8" title="Repeat for Liabilities, Equity, Revenue, Expenses" >}}
Add section headers and ledger account rows for each account type. Copy the data formula from column B into each new row — OfficeConnect picks up the ledger account from column A automatically.
{{< /step >}}

---

## Step 4 — Add subtotals

{{< step n="9" title="Add SUM rows for each section" >}}
Below each account group, add an Excel SUM row. For example, if your asset accounts are in B6:B12, add `=SUM(B6:B12)` in B13 with the label **Total Assets** in A13. Repeat for each section.
{{< /step >}}

{{< step n="10" title="Add a balance check" >}}
At the bottom of the report, add a row labeled **Out of Balance** with the formula:
```
=TotalAssets - (TotalLiabilities + TotalEquity)
```
This should equal zero for a balanced trial balance. If it doesn't, there are unposted or missing journals in Workday for this period.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Refresh the report" >}}
Click **Refresh** in the OfficeConnect ribbon. All ledger account rows populate with balances from Workday Financial Management.
{{< /step >}}

{{< step n="12" title="Verify the balance check" >}}
Confirm the Out of Balance cell shows zero (or near-zero for rounding). If it's non-zero, check that all ledger accounts are included and that your period is fully closed in Workday.
{{< /step >}}

---

## Next steps

- Drill into any balance to see the contributing journal lines — see [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/)
- Add prior-period columns for comparison — see [Build an Actuals Trend Report](/build-reports/financials/actuals-trend-report/)
- Filter to a specific cost center — see [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/trial-balance-report/`. Confirm step blocks render, all internal links resolve, and the page appears in the Financials sidebar section.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/trial-balance-report.md
git commit -m "feat: add Trial Balance Report tutorial (Financials)"
```

---

## Task 10: Drill Through to Workday Journal Lines (Tutorial)

**Files:**
- Create: `content/build-reports/financials/drill-through-journal-lines.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/drill-through-journal-lines.md`:

```markdown
---
title: "Drill Through to Workday Journal Lines from OfficeConnect"
linkTitle: "Drill Through to Journal Lines"
weight: 2
description: >
  Use OfficeConnect's Show Details feature to see the individual journal lines behind any GL balance — and drill through to the source transaction in Workday.
---

When a number in your OfficeConnect report doesn't look right, you don't need to leave Excel. OfficeConnect's **Show Details** feature opens a panel showing every journal line contributing to that cell's balance. From there, you can drill through directly to the transaction in Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to a **Financials data source** tenant
- A report with at least one populated cell (actuals data for a ledger account, company, and period)

---

## Step 1 — Build or open a Financials report

{{< step n="1" title="Open a report with Financials data" >}}
Open any OfficeConnect workbook using the Financials data source and click **Refresh** to ensure cells are populated. If you need to build one from scratch, follow [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/) first.
{{< /step >}}

---

## Step 2 — Open Show Details

{{< step n="2" title="Right-click a populated cell" >}}
Right-click any cell containing an OfficeConnect Financials value (a cell with a balance, not a header or label cell).
{{< /step >}}

{{< step n="3" title="Select Show Details" >}}
In the context menu, click **Show Details**. A detail pane opens below or beside your report (depending on your OfficeConnect layout settings). This pane lists every journal line that contributed to the cell's balance.
{{< /step >}}

{{< step n="4" title="Review the journal lines" >}}
The Show Details pane shows each journal line with columns including:
- **Journal Source** — where the entry originated (e.g., Accounts Payable, Payroll)
- **Journal Date** — the accounting date of the entry
- **Ledger Account** — the account charged
- **Amount** — the debit or credit amount
- **Memo** — the journal line description if one was entered
{{< /step >}}

---

## Step 3 — Drill through to Workday

{{< step n="5" title="Click a journal line to drill through" >}}
Click any row in the Show Details pane. OfficeConnect opens the corresponding transaction in Workday Financial Management in your default browser — logged in as your current Workday user.
{{< /step >}}

{{< step n="6" title="Review the source transaction" >}}
In Workday, you'll see the full accounting journal: all lines, the journal source, the preparer, any attachments, and the approval chain. This is the authoritative source of the posted entry.
{{< /step >}}

---

> **Note:** Drill-through requires that your Workday user account has access to view journals in Workday Financial Management. If the Workday page shows an error or access denied message, contact your Workday Security Administrator to verify your security role includes journal viewing permissions.

---

## What Show Details vs. Explore Cell means

If you're switching between Adaptive Planning and Financials tenants, note that the right-click menu is different:

| Data Source | Right-click option | What it shows |
|---|---|---|
| Financials | Show Details | Contributing journal lines, with drill-through to Workday |
| Adaptive Planning | Explore Cell | Contributing dimension splits within the Adaptive Planning model |

See [Adaptive Planning vs. Financials Data Source](/build-reports/financials-vs-adaptive-planning/) for a full comparison.

---

## Next steps

- Build a trial balance to have a full set of balances to drill into — see [Trial Balance Report](/build-reports/financials/trial-balance-report/)
- Build an actuals trend to find the period where a variance appears — see [Actuals Trend Report](/build-reports/financials/actuals-trend-report/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/drill-through-journal-lines/`. Confirm step blocks, comparison table, and note render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/drill-through-journal-lines.md
git commit -m "feat: add Drill Through to Journal Lines tutorial (Financials)"
```

---

## Task 11: Actuals Trend Report (Tutorial — Financials)

**Files:**
- Create: `content/build-reports/financials/actuals-trend-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/actuals-trend-report.md`:

```markdown
---
title: "Build an Actuals Trend Report in OfficeConnect (Financials)"
linkTitle: "Actuals Trend Report"
weight: 3
description: >
  Build a 12-month GL actuals trend report in minutes — the same report that takes hours to configure in Workday's native report writer.
---

Trending actuals across 12 months in Workday's native report writer means configuring a matrix report, setting up time period prompts, managing column layouts, and wrestling with formatting. In OfficeConnect, the same report takes about five minutes.

This tutorial shows you how — and explains why the difference matters for accounting teams who need monthly trend data on demand.

**What you'll build:** A 12-month actuals trend report showing GL account balances by period for a selected company, fully refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to a **Financials data source** tenant
- A company with at least several months of posted actuals in Workday Financial Management

---

## Why OfficeConnect vs. the Workday Report Writer

The Workday report writer is powerful but complex for time-series reporting. To build a 12-month trend report natively, you typically need to:

1. Create a matrix report with custom column definitions for each period
2. Configure time period prompts or hard-code the periods
3. Map the report to the correct financial data source
4. Run, export, and reformat in Excel

In OfficeConnect, you drag 12 time elements into a row and click Refresh. The data is live, the format is Excel, and there's no export step.

---

## Step 1 — Set up your context row

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel and click the **OfficeConnect** tab. Sign in and confirm you're on a Financials data source tenant (you'll see Ledger Accounts and Company in the Reporting pane).
{{< /step >}}

{{< step n="2" title="Add your Company" >}}
Click **B1**. In the Reporting pane, expand **Company** and drag your company into B1.
{{< /step >}}

{{< step n="3" title="Add your Version" >}}
Click **B2**. Drag **Actuals** from the Reporting pane into B2.
{{< /step >}}

---

## Step 2 — Add 12 monthly time columns

{{< step n="4" title="Add January" >}}
Click **B3**. In the Reporting pane, expand **Time → Months** and drag the first month of your trend period (e.g., Jan 2025) into B3.
{{< /step >}}

{{< step n="5" title="Add the remaining 11 months" >}}
Click **C3** through **M3** in turn, dragging each successive month (Feb 2025 through Dec 2025) into the cells. You now have a 12-month time header row.
{{< /step >}}

---

## Step 3 — Add ledger account rows

{{< step n="6" title="Add your first account" >}}
Click **A4**. In the Reporting pane, expand **Ledger Accounts** and drag your first account (e.g., Revenue or a specific expense account) into A4.
{{< /step >}}

{{< step n="7" title="Populate the data row" >}}
Click **B4**. OfficeConnect formulas reference the company in B1, the version in B2, and the time in B3, so B4 returns the Jan 2025 actuals for your account. Copy **B4** across to **M4** — each cell picks up its month from row 3 automatically.
{{< /step >}}

{{< step n="8" title="Add remaining account rows" >}}
Copy row 4 down for each additional ledger account. Add each new account to column A by dragging from the Reporting pane.
{{< /step >}}

---

## Step 4 — Add totals and formatting

{{< step n="9" title="Add a monthly total row" >}}
Below your last account row, add an Excel SUM row: `=SUM(B4:B[last row])` in column B, copied across to column M. Label it **Total** in column A.
{{< /step >}}

{{< step n="10" title="Format the header row" >}}
OfficeConnect time labels can be long. Select row 3 and apply a custom number format (`mmm-yy`) to display months as "Jan-25", "Feb-25", etc. — or type short labels in a separate row above row 3.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon. All 12 months populate with posted actuals from Workday Financial Management.
{{< /step >}}

{{< step n="12" title="Spot-check a value" >}}
Pick one account and one month. Compare the value in your report against the same account/period in a Workday report or the trial balance for that month. They should match exactly — OfficeConnect reads the same posted data.
{{< /step >}}

---

## Next steps

- Drill into any cell to see contributing journal lines — see [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/)
- Add a prior-year comparison column — see [Compare Two Planning Versions Side by Side](/build-reports/compare-planning-versions/)
- Filter by cost center — see [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/actuals-trend-report/`. Confirm the value-prop intro, step blocks, and all links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/actuals-trend-report.md
git commit -m "feat: add Actuals Trend Report tutorial (Financials)"
```

---

## Task 12: Report on Actuals by Cost Center (How-to)

**Files:**
- Create: `content/build-reports/financials/actuals-by-cost-center.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/actuals-by-cost-center.md`:

```markdown
---
title: "Report on Actuals by Cost Center"
linkTitle: "Actuals by Cost Center"
weight: 4
description: >
  Filter an OfficeConnect Financials report to a specific cost center or worktag to see GL actuals for a single department or team.
---

OfficeConnect's Financials data source supports Workday worktags — including Cost Center — as dimension filters. Adding a cost center to your report scopes all data to that organizational unit.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Set up your report with company, version, time, and ledger account rows as usual. If you need to start from scratch, see [Build an Actuals Trend Report](/build-reports/financials/actuals-trend-report/).

3. Click an empty row or column header where you want to add the cost center filter. A common layout puts the cost center in the same header area as the company, stacked in adjacent cells.

4. In the Reporting pane, expand **Dimensions → Cost Center** (or the equivalent worktag in your Workday model). Drag the specific cost center into the header cell.

5. Click **Refresh**. All account values now reflect actuals for that cost center only, within the selected company and period.

> **Tip:** To build a report comparing multiple cost centers side by side, put each cost center in its own column header. Each column pulls data for its cost center, while sharing the same company, version, and time context from the rows above.

## Multiple worktag filters

You can stack multiple worktag dimensions in the header area. For example:
- Company → Cost Center → Project → Period

Each additional dimension narrows the data further. OfficeConnect resolves the intersection of all dimension elements in your report.

> **Note:** The available dimensions depend on how your Workday Financial Management instance is configured. If Cost Center doesn't appear in the Reporting pane, your administrator may need to enable it in the Workday financial reporting data model.

## Related

- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Build an Actuals Trend Report](/build-reports/financials/actuals-trend-report/)
- [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/actuals-by-cost-center/`. Confirm tips, notes, and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/actuals-by-cost-center.md
git commit -m "feat: add Actuals by Cost Center how-to (Financials)"
```

---

## Task 13: Effective Date Reporting (How-to)

**Files:**
- Create: `content/build-reports/financials/effective-date-reporting.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/effective-date-reporting.md`:

```markdown
---
title: "Use Effective Date Reporting After a Reorganization"
linkTitle: "Effective Date Reporting"
weight: 5
description: >
  Use OfficeConnect's effective date setting to report against your organization's structure as it existed on a specific date — essential after a reorganization.
---

When your organization restructures mid-year, historical reports can show cost centers, companies, or hierarchies that no longer exist — or omit ones that didn't exist yet. OfficeConnect's Financials data source supports **effective date reporting**, which lets you select the org structure as it existed on a specific date.

> **Note:** Effective date reporting requires configuration in Workday's financial reporting data model. If the effective date option isn't available in your tenant, contact your Workday Security Administrator.

## When to use effective date reporting

- **After a reorganization:** Report Q1 actuals under the pre-reorg structure to compare apples to apples
- **For historical audits:** View the org hierarchy as it was at a specific point in time
- **For restatements:** Show actuals under the structure that was in place when the transactions were posted

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. In the Reporting pane, look for the **Effective Date** setting. It typically appears near the top of the pane or in a data source settings panel. (If you don't see it, effective date is not enabled on your tenant — see the note above.)

3. Click the effective date field and enter the date you want to report as of — for example, `03/31/2025` to see the org structure as it was at end of Q1 2025.

4. Build or refresh your report as usual. OfficeConnect applies the effective date to all dimension hierarchies — cost centers, companies, and any other org elements resolve to their structure as of that date.

5. To return to the current structure, clear the effective date field and refresh again.

## What changes with an effective date

| Element | Without effective date | With effective date |
|---|---|---|
| Cost centers | Current hierarchy | Hierarchy as of selected date |
| Companies | Current structure | Structure as of selected date |
| Dimension rollups | Current | As of selected date |
| Transaction amounts | Unchanged | Unchanged (only the org structure changes) |

## Related

- [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Adaptive Planning vs. Financials Data Source](/build-reports/financials-vs-adaptive-planning/) — effective date is a Financials-only feature
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/effective-date-reporting/`. Confirm note callout, table, and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/effective-date-reporting.md
git commit -m "feat: add Effective Date Reporting how-to (Financials)"
```

---

## Task 14: Filter Reports by Company (How-to)

**Files:**
- Create: `content/build-reports/financials/filter-by-company.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/filter-by-company.md`:

```markdown
---
title: "Filter Reports by Company in OfficeConnect (Financials)"
linkTitle: "Filter by Company"
weight: 6
description: >
  Scope an OfficeConnect Financials report to a specific legal entity, or build a multi-company view showing each entity in its own column.
---

In the Financials data source, **Company** is the top-level org dimension — the equivalent of a legal entity or subsidiary in Workday Financial Management. Every Financials report must include at least one Company element to pull data. Here's how to use it effectively.

## Single-company report

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Click your column header cell (e.g., **B1**).

3. In the Reporting pane, expand **Company** and drag your target company into B1.

4. Add your version, time, and ledger account rows as usual.

5. Click **Refresh**. All data in column B is scoped to that company.

## Multi-company report (entities side by side)

To compare two or more companies:

1. Drag **Company A** into **B1** and **Company B** into **C1**.

2. Add version and time elements in B2:C2 (same values for both columns).

3. Add account rows in column A and copy data formulas across both columns.

4. Click **Refresh**. Each column shows actuals for its company, sharing the same accounts and time period.

## Consolidated view

To show a consolidated total across all companies:

1. In the Reporting pane, expand **Company** and look for a parent-level or consolidation company (often named **All Companies**, **Group**, or your parent entity name).

2. Drag the parent company into a column header. OfficeConnect returns consolidated data with intercompany eliminations applied if your Workday model is configured for consolidation.

> **Note:** Consolidated reporting requires that intercompany elimination rules are configured in Workday Financial Management. If the parent company value doesn't match your expected consolidated total, contact your Workday administrator.

## Related

- [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- [Report on Intercompany Eliminations](/build-reports/financials/intercompany-eliminations/)
- [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/filter-by-company/`. Confirm note callout and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/filter-by-company.md
git commit -m "feat: add Filter by Company how-to (Financials)"
```

---

## Task 15: Intercompany Eliminations (How-to)

**Files:**
- Create: `content/build-reports/financials/intercompany-eliminations.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/intercompany-eliminations.md`:

```markdown
---
title: "Report on Intercompany Eliminations in OfficeConnect"
linkTitle: "Intercompany Eliminations"
weight: 7
description: >
  Use OfficeConnect's Financials data source to report on intercompany transactions and eliminations — with options to include or exclude eliminations from consolidated views.
---

Intercompany eliminations remove transactions between entities in a consolidated group — preventing double-counting of intercompany revenue and expenses. OfficeConnect's Financials data source surfaces these as data you can include or exclude in your reports.

## How eliminations appear in OfficeConnect

When you report against a parent company (consolidated entity) in OfficeConnect, the data you see depends on your Workday Financial Management configuration:

- If **elimination journals are posted** in Workday, they are included in consolidated totals automatically
- The **Exclude Elimination** option (available in Financials data source reports) lets you toggle whether elimination entries are included in your totals

> **Note:** The Exclude Elimination option is a Financials-only feature — it is not available in Adaptive Planning reports. See [Adaptive Planning vs. Financials Data Source](/build-reports/financials-vs-adaptive-planning/).

## View intercompany eliminations separately

To see elimination amounts on their own:

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Add a column for the **elimination company** — in Workday Financial Management, eliminations are typically posted to a dedicated elimination entity (often named **Eliminations**, **Elim**, or prefixed with **E_**). Drag this entity from the Company dimension in the Reporting pane.

3. Add your ledger account rows and refresh. The elimination column shows only the elimination journal entries for each account.

## Exclude eliminations from a consolidated report

1. In your consolidated report (with a parent company element), look for the **Exclude Elimination** checkbox in the Reporting pane or report settings.

2. Check **Exclude Elimination** to see gross consolidated data without eliminations applied. This is useful for understanding the total volume of intercompany activity.

3. Uncheck it to return to standard consolidated totals with eliminations included.

## Common intercompany reporting layouts

| Column A (Accounts) | Column B | Column C | Column D |
|---|---|---|---|
| Revenue | Company A | Company B | Eliminations |
| Intercompany Revenue | Company A IC | Company B IC | Elim entry |
| Consolidated Revenue | Sum of B+C+D | | |

Building this layout in OfficeConnect requires one column per entity plus one for the elimination company, with Excel SUM formulas for consolidated totals.

## Related

- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)
- [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/) — verify elimination journal entries
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/intercompany-eliminations/`. Confirm note callout, table, and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/intercompany-eliminations.md
git commit -m "feat: add Intercompany Eliminations how-to (Financials)"
```

---

## Task 16: Multi-Currency Reporting — Financials (How-to)

**Files:**
- Create: `content/build-reports/financials/multi-currency-financials.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/multi-currency-financials.md`:

```markdown
---
title: "Multi-Currency Reporting with the Financials Data Source"
linkTitle: "Multi-Currency Reporting"
weight: 8
description: >
  Report in your chosen currency using Workday Financial Management's currency conversion — select transaction currency, company currency, or a converted reporting currency in OfficeConnect.
---

Workday Financial Management supports multicurrency transactions — journals can be posted in a transaction currency and converted to a company (ledger) currency automatically. OfficeConnect surfaces these currency layers so you can choose which currency your report shows.

## Currency options in the Financials data source

| Currency type | What it shows |
|---|---|
| **Transaction currency** | The original currency of the posted journal (e.g., GBP for a UK invoice) |
| **Company currency** | The ledger currency of the reporting company (e.g., USD for a US parent) |
| **Converted reporting currency** | A second converted amount if alternate ledger currency is configured in Workday |

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. In the Reporting pane, look for the **Currency** selector. It typically appears near the top of the pane or in report settings alongside the effective date option.

3. Select the currency option you want:
   - **Company currency** — most common for consolidated reporting; all amounts appear in your company's ledger currency
   - **Transaction currency** — useful for auditing specific foreign-currency transactions; amounts appear in the currency they were originally posted in
   - A specific converted currency — if your Workday model has alternate ledger currency configured, additional currency options may appear here

4. Build or refresh your report. All account values resolve in the selected currency.

> **Note:** Transaction currency reporting returns one row per currency if multiple currencies exist for the same account and period — your report may show separate rows for USD, GBP, and EUR entries rather than a single combined total. This is expected behavior for auditing purposes.

## Rate types and conversion

Workday Financial Management uses **rate types** to convert foreign currency transactions to the company currency. Common rate types include:

- **Average rate** — monthly average FX rate (typical for P&L accounts)
- **Spot rate** — rate at the date of the transaction
- **Budget rate** — fixed planning rate (used for constant currency comparisons)

The rate type applied to your OfficeConnect data is determined by your Workday configuration — OfficeConnect reports the converted amount, it does not select or override the rate type.

## Related

- [Report in Constant Currency in OfficeConnect](/build-reports/constant-currency-reporting/) — constant currency for Adaptive Planning users
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Effective Date Reporting](/build-reports/financials/effective-date-reporting/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/multi-currency-financials/`. Confirm tables, note callout, and related links render.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/multi-currency-financials.md
git commit -m "feat: add Multi-Currency Reporting how-to (Financials)"
```

---

## Final Step: Push to main and verify live site

- [ ] **Push all commits**

```bash
git push origin main
```

- [ ] **Verify deployment**

GitHub Actions deploys automatically on push. Monitor the Actions tab on GitHub. Once complete, open `https://officeconnectpro.com/build-reports/` and `https://officeconnectpro.com/build-reports/financials/` and confirm:

- All 16 articles appear in the sidebar
- The Financials subsection is clearly separated
- No broken links in next-steps sections
- Step blocks render with numbered circles on all tutorial pages
