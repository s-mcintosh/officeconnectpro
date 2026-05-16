# Content Batch 2 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish 16 new articles (FP&A data entry, financial statements, month-end close, automation, Mac, troubleshoot) and retroactively tag all 16 Batch 1 articles so Hugo auto-generates `/tags/<tag>/` index pages.

**Architecture:** Same as Batch 1: Hugo Markdown files in `content/`. New articles follow existing weight sequences — FP&A at weights 28–33 under `content/build-reports/`, Financials at weights 9–14 under `content/build-reports/financials/`, Troubleshoot at weights 20–23 under `content/troubleshoot/`. Tags are a standard Hugo taxonomy — adding `tags:` to front matter is all that is needed; no config changes required (taxonomy is already defined in Docsy). Tutorials use the `step` shortcode; how-tos use plain numbered prose. Troubleshoot articles follow Symptom → Causes → Fix steps per cause → Escalation structure.

**Tech Stack:** Hugo extended v0.161+, Docsy theme, GitHub Pages. Local dev: `hugo server` at `http://localhost:1313`.

---

## File Map

| File | Action | Type |
|---|---|---|
| `content/build-reports/budget-vs-actuals-variance.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/department-pl-report.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/year-over-year-trend.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/compare-planning-versions.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/headcount-in-financial-report.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/lock-protect-reports.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/scenario-comparison.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/constant-currency-reporting.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/trial-balance-report.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/drill-through-journal-lines.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/actuals-trend-report.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/actuals-by-cost-center.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/effective-date-reporting.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/filter-by-company.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/intercompany-eliminations.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/financials/multi-currency-financials.md` | Modify — add tags | Batch 1 retroactive |
| `content/build-reports/enter-budget-data.md` | Create | Tutorial |
| `content/build-reports/formatted-executive-report.md` | Create | Tutorial |
| `content/build-reports/refresh-with-power-automate.md` | Create | How-to |
| `content/build-reports/custom-dimensions-attributes.md` | Create | How-to |
| `content/build-reports/optimize-performance.md` | Create | How-to |
| `content/build-reports/officeconnect-on-mac.md` | Create | How-to |
| `content/build-reports/financials/balance-sheet-report.md` | Create | Tutorial |
| `content/build-reports/financials/cash-flow-statement.md` | Create | Tutorial |
| `content/build-reports/financials/month-end-close-workflow.md` | Create | Tutorial |
| `content/build-reports/financials/variance-by-journal-source.md` | Create | How-to |
| `content/build-reports/financials/worktag-combinations.md` | Create | How-to |
| `content/build-reports/financials/reconcile-to-workday.md` | Create | How-to |
| `content/troubleshoot/not-refreshing.md` | Create | Troubleshoot |
| `content/troubleshoot/authentication-token-errors.md` | Create | Troubleshoot |
| `content/troubleshoot/slow-performance.md` | Create | Troubleshoot |
| `content/troubleshoot/data-discrepancies.md` | Create | Troubleshoot |

---

## Task 0: Retroactive Tagging — All 16 Batch 1 Articles

Add `tags:` to the front matter of each existing Batch 1 article. The `tags:` line goes directly after the `description:` block (after the closing `>` line or after the inline description value). Do not change any other front matter or content.

**Files:**
- Modify: `content/build-reports/budget-vs-actuals-variance.md`
- Modify: `content/build-reports/department-pl-report.md`
- Modify: `content/build-reports/year-over-year-trend.md`
- Modify: `content/build-reports/compare-planning-versions.md`
- Modify: `content/build-reports/headcount-in-financial-report.md`
- Modify: `content/build-reports/lock-protect-reports.md`
- Modify: `content/build-reports/scenario-comparison.md`
- Modify: `content/build-reports/constant-currency-reporting.md`
- Modify: `content/build-reports/financials/trial-balance-report.md`
- Modify: `content/build-reports/financials/drill-through-journal-lines.md`
- Modify: `content/build-reports/financials/actuals-trend-report.md`
- Modify: `content/build-reports/financials/actuals-by-cost-center.md`
- Modify: `content/build-reports/financials/effective-date-reporting.md`
- Modify: `content/build-reports/financials/filter-by-company.md`
- Modify: `content/build-reports/financials/intercompany-eliminations.md`
- Modify: `content/build-reports/financials/multi-currency-financials.md`

- [ ] **Step 1: Add tags to each Batch 1 article**

For each file below, read the file and add the specified `tags:` line to its front matter, immediately before the closing `---`. The front matter currently ends with the `description:` field. Place `tags:` after that field.

**`content/build-reports/budget-vs-actuals-variance.md`** — add:
```yaml
tags: ["adaptive-planning", "tutorial", "reporting"]
```

**`content/build-reports/department-pl-report.md`** — add:
```yaml
tags: ["adaptive-planning", "tutorial", "reporting"]
```

**`content/build-reports/year-over-year-trend.md`** — add:
```yaml
tags: ["adaptive-planning", "tutorial", "reporting"]
```

**`content/build-reports/compare-planning-versions.md`** — add:
```yaml
tags: ["adaptive-planning", "how-to", "reporting"]
```

**`content/build-reports/headcount-in-financial-report.md`** — add:
```yaml
tags: ["adaptive-planning", "how-to", "reporting"]
```

**`content/build-reports/lock-protect-reports.md`** — add:
```yaml
tags: ["adaptive-planning", "how-to", "sharing"]
```

**`content/build-reports/scenario-comparison.md`** — add:
```yaml
tags: ["adaptive-planning", "how-to", "reporting"]
```

**`content/build-reports/constant-currency-reporting.md`** — add:
```yaml
tags: ["adaptive-planning", "how-to", "currency"]
```

**`content/build-reports/financials/trial-balance-report.md`** — add:
```yaml
tags: ["financials", "tutorial", "reporting"]
```

**`content/build-reports/financials/drill-through-journal-lines.md`** — add:
```yaml
tags: ["financials", "tutorial", "reporting"]
```

**`content/build-reports/financials/actuals-trend-report.md`** — add:
```yaml
tags: ["financials", "tutorial", "reporting"]
```

**`content/build-reports/financials/actuals-by-cost-center.md`** — add:
```yaml
tags: ["financials", "how-to", "reporting"]
```

**`content/build-reports/financials/effective-date-reporting.md`** — add:
```yaml
tags: ["financials", "how-to", "reporting"]
```

**`content/build-reports/financials/filter-by-company.md`** — add:
```yaml
tags: ["financials", "how-to", "reporting"]
```

**`content/build-reports/financials/intercompany-eliminations.md`** — add:
```yaml
tags: ["financials", "how-to", "reporting"]
```

**`content/build-reports/financials/multi-currency-financials.md`** — add:
```yaml
tags: ["financials", "how-to", "currency"]
```

- [ ] **Step 2: Verify tag pages are generated**

With `hugo server` running, open the following URLs and confirm each returns a non-404 index page listing the relevant articles:

- `http://localhost:1313/tags/adaptive-planning/` — should list 8 articles
- `http://localhost:1313/tags/financials/` — should list 8 articles
- `http://localhost:1313/tags/tutorial/` — should list 6 articles
- `http://localhost:1313/tags/how-to/` — should list 10 articles
- `http://localhost:1313/tags/reporting/` — should list articles tagged reporting
- `http://localhost:1313/tags/currency/` — should list 2 articles
- `http://localhost:1313/tags/sharing/` — should list 1 article

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/budget-vs-actuals-variance.md \
        content/build-reports/department-pl-report.md \
        content/build-reports/year-over-year-trend.md \
        content/build-reports/compare-planning-versions.md \
        content/build-reports/headcount-in-financial-report.md \
        content/build-reports/lock-protect-reports.md \
        content/build-reports/scenario-comparison.md \
        content/build-reports/constant-currency-reporting.md \
        content/build-reports/financials/trial-balance-report.md \
        content/build-reports/financials/drill-through-journal-lines.md \
        content/build-reports/financials/actuals-trend-report.md \
        content/build-reports/financials/actuals-by-cost-center.md \
        content/build-reports/financials/effective-date-reporting.md \
        content/build-reports/financials/filter-by-company.md \
        content/build-reports/financials/intercompany-eliminations.md \
        content/build-reports/financials/multi-currency-financials.md
git commit -m "feat: retroactively add tags to all Batch 1 articles"
```

---

## Task 1: Enter Budget Data in Excel with OfficeConnect (Tutorial)

**Files:**
- Create: `content/build-reports/enter-budget-data.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/enter-budget-data.md`:

```markdown
---
title: "Enter Budget Data in Excel with OfficeConnect"
linkTitle: "Enter Budget Data"
weight: 28
description: >
  Use OfficeConnect's data entry mode to write budget figures directly from Excel into Adaptive Planning — no need to log in to the Adaptive Planning web interface.
tags: ["adaptive-planning", "tutorial", "data-entry"]
---

OfficeConnect isn't just for reading data from Adaptive Planning — it can write data back. This tutorial walks through setting up a data entry workbook that lets planners enter budget figures in Excel and submit them directly to an Adaptive Planning version.

**What you'll build:** A data entry workbook with account rows and period columns where planners type figures and click Submit to push them into a Budget version in Adaptive Planning.

**What you'll need:**
- OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
- A Budget (or other input) version in Adaptive Planning configured to accept input at your level
- Write access to the version — your Adaptive Planning role must include Input permission

{{< admin-note >}}
Data entry requires the target version to be open for input in Adaptive Planning. If the version is locked, planners will receive a write error. Confirm with your Adaptive Planning admin that the Budget version is in an editable state before distributing the workbook.
{{< /admin-note >}}

---

## Step 1 — Enable data entry in the workbook

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel and click the **OfficeConnect** tab in the ribbon. Sign in if prompted. The Reporting pane opens on the right.
{{< /step >}}

{{< step n="2" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**. In the dialog, find the **Data Entry** section and set **Allow Data Entry** to **Yes**. Click **OK**.

This enables the Submit button in the ribbon and allows OfficeConnect formulas to be overwritten with typed values.
{{< /step >}}

---

## Step 2 — Build the account and period structure

{{< step n="3" title="Add account rows" >}}
Click cell **A3**. In the Reporting pane, expand **Accounts** and drag your first input account (for example, **Salaries**) into A3. Continue in A4, A5, A6 with additional accounts: **Benefits**, **Travel**, **Other Operating Expenses**. Each row holds one account element.
{{< /step >}}

{{< step n="4" title="Add a version header" >}}
Click **B1**. In the Reporting pane, expand **Versions** and drag your **Budget** version into B1. This tells OfficeConnect that data entered in this column belongs to the Budget version.
{{< /step >}}

{{< step n="5" title="Add period columns" >}}
Click **B2** and drag **January** from the Time section of the Reporting pane into it. Repeat for **C2** through **M2**, placing February through December in each subsequent column. You should now have 12 month columns across row 2.
{{< /step >}}

{{< step n="6" title="Populate the data area" >}}
Click **B3**. OfficeConnect creates a formula referencing the Budget version (B1), January (B2), and Salaries (A3). Copy **B3** across to **M3**, then copy that range down to cover all your account rows. Each cell resolves to the existing budget figure in Adaptive Planning (if any).
{{< /step >}}

---

## Step 3 — Enter and submit data

{{< step n="7" title="Refresh to load current values" >}}
Click **Refresh** in the OfficeConnect ribbon. All cells populate with whatever figures currently exist in the Budget version for each account and month. If a cell is blank, no value exists yet for that combination.
{{< /step >}}

{{< step n="8" title="Type new budget figures" >}}
Click any data cell — for example, **B3** (Salaries, January) — and type a number directly over the formula. OfficeConnect replaces the formula with your typed value and highlights the cell to indicate it contains a pending input.

Repeat for all cells you want to update. You can move through cells normally with Tab and Enter.
{{< /step >}}

{{< step n="9" title="Click Submit" >}}
When you have finished entering figures, click **Submit** in the OfficeConnect ribbon. OfficeConnect pushes all highlighted (pending) cells to the Budget version in Adaptive Planning.

A confirmation message appears when the submission completes. The cells restore their OfficeConnect formulas, and the values now reflect what you entered.
{{< /step >}}

---

## Step 4 — Verify the submission

{{< step n="10" title="Refresh and spot-check" >}}
Click **Refresh** again. The cells should show the figures you just submitted. If a cell reverts to a different value, the submission may have been overridden by a formula or allocation rule in Adaptive Planning — check with your model administrator.
{{< /step >}}

---

## Tips for distributing data entry workbooks

- **Lock non-input cells** before sharing. Protect the sheet in Excel with a password and unlock only the data entry cells (B3:M6 in this example) so planners cannot accidentally overwrite account or period headers.
- **One version per workbook.** Avoid mixing multiple input versions in the same workbook — it is easy for planners to accidentally submit to the wrong version.
- **Set a clear period.** Add a note at the top of the sheet indicating which budget cycle and deadline this workbook covers.

---

## Next steps

- Protect the workbook before sharing — see [Lock and Protect Reports](/build-reports/lock-protect-reports/)
- Compare submitted budget to actuals — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- Distribute the workbook via SharePoint — see [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
```

- [ ] **Step 2: Verify it renders**

With `hugo server` running, open `http://localhost:1313/build-reports/enter-budget-data/`. Confirm: title appears, all step blocks render with numbered circles, admin-note callout renders, next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/enter-budget-data.md
git commit -m "feat: add Enter Budget Data tutorial"
```

---

## Task 2: Build a Formatted Executive Report for Distribution (Tutorial)

**Files:**
- Create: `content/build-reports/formatted-executive-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/formatted-executive-report.md`:

```markdown
---
title: "Build a Formatted Executive Report for Distribution"
linkTitle: "Formatted Executive Report"
weight: 29
description: >
  Build a polished, print-ready executive summary report in OfficeConnect with custom formatting, logos, and page layout — ready to share as PDF or Excel.
tags: ["adaptive-planning", "tutorial", "reporting", "sharing"]
---

A raw OfficeConnect report shows the right numbers, but an executive report needs to look the part. This tutorial walks through building a formatted P&L summary with branding, clean layout, and print-ready page setup — the kind of report you can share as a PDF without touching it in PowerPoint first.

**What you'll build:** A one-page executive P&L summary with a header, logo, formatted number columns, and page layout configured for PDF export.

**What you'll need:**
- OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
- An Adaptive Planning model with P&L accounts, actuals, and budget loaded
- Basic familiarity with building variance reports — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)

---

## Step 1 — Build the data structure

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open a new Excel workbook and click the **OfficeConnect** tab. Sign in if prompted. The Reporting pane opens on the right.
{{< /step >}}

{{< step n="2" title="Add account rows" >}}
Starting in **A5** (leaving rows 1–4 for the header), add your P&L summary accounts. Click A5 and drag **Revenue** from the Reporting pane. Add **Cost of Goods Sold** in A6, **Gross Profit** in A7, **Operating Expenses** in A8, and **Net Income** in A9. Use rollup accounts so OfficeConnect aggregates child accounts automatically.
{{< /step >}}

{{< step n="3" title="Add version and time columns" >}}
Click **B3** and drag your **Actuals** version in. Click **C3** and drag **Budget**. Click **D3** and type `Variance` (this will be a plain Excel formula column, not an OfficeConnect element).

Click **B4** and drag the reporting period into it (for example, the current quarter or full year). Copy B4 into C4 — both version columns share the same time context.
{{< /step >}}

{{< step n="4" title="Populate data cells and variance formula" >}}
Click **B5** — OfficeConnect creates a formula for Actuals, the period in B4, and the account in A5. Copy B5 down to B9, then copy B5:B9 across to C5:C9 for Budget.

In **D5**, enter `=B5-C5`. Copy D5 down to D9. Format column D to show positive variances as favorable (green) and negative as unfavorable (red) using Excel's conditional formatting.
{{< /step >}}

---

## Step 2 — Build the header

{{< step n="5" title="Add a report title" >}}
Click **A1** and type your report title, for example: `Executive Summary — Q2 2026`. Merge cells A1:D1 (Home ribbon → Merge & Center). Set font to **16pt Bold**.
{{< /step >}}

{{< step n="6" title="Add a subtitle with the refresh date" >}}
Click **A2** and enter a formula to show today's date dynamically:
```
="As of "&TEXT(TODAY(),"MMMM D, YYYY")
```
Merge A2:D2 and set to 10pt italic gray. This updates automatically each time the workbook is opened.
{{< /step >}}

{{< step n="7" title="Insert a logo" >}}
Click **Insert** in the Excel ribbon, then **Pictures → This Device**. Select your company logo file. Resize and position it in the upper-right area (around D1:D2). Right-click the image and choose **Format Picture → Properties → Move and size with cells** — this keeps it in place when rows reflow.
{{< /step >}}

---

## Step 3 — Apply formatting

{{< step n="8" title="Format number columns" >}}
Select **B5:D9**. Apply the Accounting number format with no decimal places (`Home → Number → Accounting`, set decimal places to 0). For column D (variance), apply a custom format: `[Green]#,##0;[Red]-#,##0` to color-code favorable and unfavorable variances automatically.
{{< /step >}}

{{< step n="9" title="Add column headers and borders" >}}
In **B3:D3**, type the column headers: `Actuals`, `Budget`, `Variance`. Bold and center them. Add a thick bottom border under row 3 (the header row) and a thin top border above row 9 (the Net Income row) to create a visual subtotal separator.
{{< /step >}}

{{< step n="10" title="Add alternating row shading" >}}
Select A5:D8 (the data rows, excluding Net Income). Apply a light gray fill (`#F2F2F2`) to every other row — A5:D5 and A7:D7 — so the report is easy to scan. Leave A6:D6 and A8:D8 with no fill.
{{< /step >}}

---

## Step 4 — Configure page layout for PDF export

{{< step n="11" title="Set page orientation and margins" >}}
Click the **Page Layout** tab in Excel. Set **Orientation** to Landscape. Set **Margins** to Narrow. Set **Fit to** 1 page wide by 1 page tall — this ensures the report prints as a single page regardless of zoom.
{{< /step >}}

{{< step n="12" title="Add a footer with page number and company name" >}}
Go to **Insert → Header & Footer**. Click in the footer area and add: left section — company name; center section — `Confidential`; right section — `&P of &N` (page number). Click outside the header/footer area to exit.
{{< /step >}}

{{< step n="13" title="Refresh and export as PDF" >}}
Click **Refresh** in the OfficeConnect ribbon to populate the latest figures. Then go to **File → Export → Create PDF/XPS** and save the PDF. Open it to confirm the layout is clean, the logo appears, and numbers are formatted correctly.
{{< /step >}}

---

## Next steps

- Share the PDF automatically — see [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
- Schedule the refresh automatically — see [Refresh Reports Automatically with Power Automate](/build-reports/refresh-with-power-automate/)
- Add it to a PowerPoint deck — see [OfficeConnect for PowerPoint](/share-publish/officeconnect-for-powerpoint/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/formatted-executive-report/`. Confirm all step blocks render and next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/formatted-executive-report.md
git commit -m "feat: add Formatted Executive Report tutorial"
```

---

## Task 3: Refresh Reports Automatically with Power Automate (How-to)

**Files:**
- Create: `content/build-reports/refresh-with-power-automate.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/refresh-with-power-automate.md`:

```markdown
---
title: "Refresh Reports Automatically with Power Automate"
linkTitle: "Refresh with Power Automate"
weight: 30
description: >
  Use Power Automate Desktop to schedule OfficeConnect report refreshes automatically — keep distributed Excel reports up to date without manual intervention.
tags: ["adaptive-planning", "how-to", "reporting"]
---

OfficeConnect doesn't have a built-in scheduler, but you can automate report refresh using **Power Automate Desktop** — Microsoft's desktop automation tool included with Windows 10/11 and Microsoft 365. This how-to sets up a scheduled desktop flow that opens your report workbook, refreshes OfficeConnect data, saves, and closes — on any schedule you set.

**What you'll need:**
- Windows 10 or 11 with Power Automate Desktop installed ([download from Microsoft](https://powerautomate.microsoft.com/en-us/desktop/))
- Microsoft 365 subscription (Power Automate Desktop is included)
- Your OfficeConnect report workbook saved to a local path or a network/SharePoint location accessible from the machine

> **Note:** The machine running the flow must be on and signed in for the scheduled flow to run. This approach works best on a server or shared workstation that stays online. For cloud-only approaches, consider saving the refreshed file to SharePoint so downstream users always see the latest version.

---

## 1. Create the desktop flow

1. Open **Power Automate Desktop** from the Start menu.
2. Click **+ New flow**, give it a name like `Refresh OfficeConnect Monthly Report`, and click **Create**.
3. The flow designer opens. You will build the flow by adding actions from the left panel.

## 2. Add actions to open, refresh, save, and close the workbook

4. In the **Actions** panel, search for **Launch Excel** and drag it into the flow. Set:
   - **Launch Excel**: With a blank document — change to **Open the following document**
   - **Document path**: Enter the full path to your workbook, e.g. `C:\Reports\Monthly-PL.xlsx`
   - Leave **Make instance visible** checked so you can see the automation in progress during testing

5. Add a **Wait** action after the Launch step. Set it to wait **10 seconds** — this gives Excel time to fully load and activate the OfficeConnect add-in before the next action runs.

6. Add a **Send keys** action. Set **Send keys to**: the Excel window (select it from the dropdown). In the **Text to send** field, enter the keyboard shortcut to trigger OfficeConnect Refresh. OfficeConnect does not have a default keyboard shortcut, so you have two options:

   **Option A — Use a macro:** Record a macro in Excel that calls `Application.Run "OfficeConnect.Refresh"` and assign it a keyboard shortcut (e.g., `Ctrl+Shift+R`). Then use **Send keys** to send `^+R` (Ctrl+Shift+R).

   **Option B — Use Office Scripts (Microsoft 365 E3/E5):** Write an Office Script that calls the OfficeConnect COM object. This is more reliable but requires an Office Scripts-enabled license.

   For most setups, Option A is simpler. Create the macro once in the workbook and save the workbook with macros (`.xlsm` format).

7. Add another **Wait** action — wait **30 seconds** to allow the refresh to complete. Adjust this value based on your model size; large models may need 60–90 seconds.

8. Add a **Send keys** action to save: send `^s` (Ctrl+S). Add another **Wait** of 5 seconds.

9. Add a **Close Excel** action. Set **Before closing Excel**: **Save document**.

## 3. Test the flow manually

10. Click **Run** in the Power Automate Desktop toolbar. Watch the automation open Excel, wait, trigger refresh, save, and close. Verify the workbook's data is updated after the flow completes.

## 4. Schedule the flow

11. In the Power Automate Desktop home screen, the flow you created appears in your list. To schedule it, go to the **Power Automate web portal** (flow.microsoft.com) and create a **Scheduled cloud flow** that triggers on your desired schedule (daily, weekly, monthly).

12. In the cloud flow, add an action: **Power Automate Desktop → Run a flow built with Power Automate Desktop**. Select your desktop flow. This cloud flow triggers the desktop flow on schedule.

> **Note:** The desktop machine must be running and signed in for the cloud-triggered desktop flow to execute. Configure the machine to auto-login on startup if it needs to run unattended overnight.

---

## Related links

- [Build a Formatted Executive Report for Distribution](/build-reports/formatted-executive-report/)
- [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
- [Lock and Protect Reports](/build-reports/lock-protect-reports/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/refresh-with-power-automate/`. Confirm the note callout renders, numbered steps display correctly, and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/refresh-with-power-automate.md
git commit -m "feat: add Refresh with Power Automate how-to"
```

---

## Task 4: Work with Custom Dimensions and Attributes (How-to)

**Files:**
- Create: `content/build-reports/custom-dimensions-attributes.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/custom-dimensions-attributes.md`:

```markdown
---
title: "Work with Custom Dimensions and Attributes in OfficeConnect"
linkTitle: "Custom Dimensions and Attributes"
weight: 31
description: >
  Report on custom dimensions and attributes defined in your Adaptive Planning model — filter by product line, region, project, or any other custom segment your team uses.
tags: ["adaptive-planning", "how-to", "reporting"]
---

Adaptive Planning models often include custom dimensions beyond the standard account and level hierarchy — things like Product Line, Region, Project Code, or Customer Segment. OfficeConnect exposes these as **Custom Dimensions** in the Reporting pane, letting you filter and report on any segment your model defines.

**What you'll need:**
- OfficeConnect connected to an Adaptive Planning model that includes custom dimensions
- Familiarity with building basic reports — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)

---

## 1. Find your custom dimensions in the Reporting pane

1. Open the OfficeConnect Reporting pane. Scroll down past Accounts, Versions, Time, and Levels to find the **Custom Dimensions** section (it may also appear as **Dimensions** depending on your OfficeConnect version).
2. Expand **Custom Dimensions** to see the dimensions your model administrator has defined. Each dimension has members — for example, a "Region" dimension might have members: North America, EMEA, APAC.

> **Note:** Custom dimensions are model-specific. If you don't see a **Custom Dimensions** section, your model may not have any configured. Contact your Adaptive Planning model administrator to confirm.

## 2. Add a custom dimension filter to a report

3. Build a basic report with account rows, a version header, and a time context — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/) for a walkthrough.
4. To filter the entire report by a single dimension member (for example, show only North America figures): In the Reporting pane, expand **Custom Dimensions → Region** and drag the **North America** member into any blank cell in the header area of your report (for example, E1). OfficeConnect adds a filter element — this restricts all formulas in the workbook to that member of the dimension.
5. Click **Refresh**. All data cells update to show values scoped to North America only.

## 3. Build a multi-column report across dimension members

6. To compare multiple dimension members side by side — one column per region, for example — place each member in a separate column header:
   - Drag **North America** into **B1**
   - Drag **EMEA** into **C1**
   - Drag **APAC** into **D1**
7. Add the version in a row above (or incorporate it directly into the formula by keeping a version element in the workbook). Add a time context in row 2.
8. In **B3**, OfficeConnect creates a formula referencing the account in A3, the version, the time in B2, and the North America member in B1. Copy across to C3 and D3 — each resolves to the correct region automatically.
9. Click **Refresh** to populate all columns.

## 4. Use attributes to filter within a dimension

10. Some Adaptive Planning models use **Attributes** — metadata attached to dimension members (for example, attaching a "Business Unit" attribute to each Region member). In the Reporting pane, look for an **Attributes** section under the relevant dimension.
11. Drag an attribute value into your report header to filter by it. This works the same way as a dimension member — OfficeConnect includes all members that have that attribute value.

## 5. Remove a dimension filter

12. To remove a filter, click the cell containing the dimension element and press **Delete**. Click **Refresh** — the report reverts to returning values across all members of that dimension (unfiltered).

---

## Related links

- [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- [Set Up Scenario Comparison](/build-reports/scenario-comparison/)
- [Build a Department P&L Report](/build-reports/department-pl-report/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/custom-dimensions-attributes/`. Confirm the note callout renders and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/custom-dimensions-attributes.md
git commit -m "feat: add Custom Dimensions and Attributes how-to"
```

---

## Task 5: Optimize Performance for Large Models (How-to)

**Files:**
- Create: `content/build-reports/optimize-performance.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/optimize-performance.md`:

```markdown
---
title: "Optimize Performance for Large Models in OfficeConnect"
linkTitle: "Optimize Performance"
weight: 32
description: >
  Speed up OfficeConnect reports that are slow to refresh — reduce formula count, use efficient time contexts, and configure workbook settings for large Adaptive Planning models.
tags: ["adaptive-planning", "how-to", "reporting"]
---

OfficeConnect reports can slow down significantly when workbooks contain hundreds of formulas pulling from large Adaptive Planning models. Refresh times of 30–60 seconds are common in unoptimized workbooks; the techniques below typically cut that to under 10 seconds for the same data.

**What you'll need:**
- OfficeConnect connected to an Adaptive Planning tenant
- A workbook that is currently slow to refresh (more than 15 seconds)

---

## 1. Reduce the number of OfficeConnect formulas

The single biggest performance factor is formula count. Each OfficeConnect formula is a separate server call during refresh.

1. **Use rollup accounts instead of leaf accounts.** If you're reporting on 50 leaf-level expense accounts when a single "Total Operating Expenses" rollup account would suffice, replace them. One rollup formula = one server call instead of 50.
2. **Delete unused rows and columns.** Workbooks accumulate leftover OfficeConnect formulas in hidden rows or off-screen columns. Select unused areas, delete the cells entirely (not just clear contents), and save.
3. **Consolidate time contexts.** If every data cell has its own Time element, replace them with a single Time element in the header row that all data cells reference. OfficeConnect reads the shared element rather than re-querying time for each cell.

## 2. Use summary time periods instead of month-by-month

4. A report showing 24 monthly columns (2 years of months) makes many more server calls than a report showing 8 quarterly columns covering the same period. If your use case allows quarterly or annual granularity, switch to it — refresh time drops proportionally.
5. For trend reports that must show months, consider building two separate sheets: a summary sheet with quarterly data (fast refresh, for sharing) and a detail sheet with monthly data (slower, used only when drilling in).

## 3. Enable background refresh

6. In the OfficeConnect ribbon, click **Workbook Properties**. Look for a **Refresh** section and enable **Background Refresh** if available in your version. Background refresh lets Excel remain responsive while the data loads, instead of freezing the UI.

## 4. Avoid volatile Excel functions in the same sheet

7. Excel functions like `NOW()`, `TODAY()`, `RAND()`, and `OFFSET()` recalculate on every keystroke, which can trigger OfficeConnect recalculations repeatedly. Move these functions to a separate sheet, or replace them with static values where possible.

## 5. Limit the Level scope

8. If your report pulls data for all Levels (all departments) in a large org hierarchy, consider adding a Level filter to scope it to the levels your audience actually needs. A report scoped to a single division refreshes much faster than one showing all 200 cost centers.

> **Tip:** Use the Cell Explorer (OfficeConnect ribbon → **Cell Explorer**) to inspect any slow-refreshing cell. It shows exactly which elements the formula is querying — account, version, time, level, and dimensions. This is the fastest way to spot an unexpectedly broad query.

## 6. Check your network and tenant performance

9. OfficeConnect refresh performance is partly determined by Adaptive Planning server response time. If refresh is slow even on a simple workbook, check:
   - Whether other users are running large reports or processes on the tenant at the same time (peak usage hours are slower)
   - Your network connection to Workday's servers (VPN can add latency)
   - Whether your Adaptive Planning model has recently been optimized (contact your admin)

---

## Related links

- [Fix Slow Performance in Large Reports](/troubleshoot/slow-performance/)
- [Build a Budget vs. Actuals Variance Report](/build-reports/budget-vs-actuals-variance/)
- [Build a Year-over-Year Trend Report](/build-reports/year-over-year-trend/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/optimize-performance/`. Confirm the tip callout renders and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/optimize-performance.md
git commit -m "feat: add Optimize Performance how-to"
```

---

## Task 6: Use OfficeConnect on Mac (How-to)

**Files:**
- Create: `content/build-reports/officeconnect-on-mac.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/officeconnect-on-mac.md`:

```markdown
---
title: "Use OfficeConnect on Mac"
linkTitle: "OfficeConnect on Mac"
weight: 33
description: >
  Install and use OfficeConnect on a Mac with Excel for Mac — what works, what's different from Windows, and how to handle common Mac-specific issues.
tags: ["adaptive-planning", "how-to"]
---

OfficeConnect runs on Excel for Mac (Microsoft 365 subscription required). The core reporting experience — building reports, refreshing data, and navigating the Reporting pane — works the same as Windows. A few things are different, and a handful of Windows-only features are unavailable. This guide covers what you need to know.

**What you'll need:**
- A Mac running macOS 12 (Monterey) or later
- Microsoft 365 with Excel for Mac (version 16.54 or later)
- OfficeConnect deployed by your IT admin, or access to install it from the Microsoft AppSource

---

## 1. Install OfficeConnect on Mac

1. Open **Excel for Mac** and sign in with your Microsoft 365 account.
2. Click the **Insert** tab in the menu bar, then click **Add-ins** (or **Get Add-ins** depending on your Excel version).
3. In the Office Add-ins dialog, search for **OfficeConnect** in the Store tab. If your IT admin deployed it centrally, look in the **Admin Managed** tab instead.
4. Click **Add**. After a moment, an **OfficeConnect** tab appears in the Excel ribbon.

> **Note:** If your organization deploys OfficeConnect via a custom manifest URL, ask your IT admin for the manifest URL and install it via **Insert → Add-ins → Upload My Add-in** (or the equivalent in your version of Excel for Mac).

## 2. Sign in

5. Click the **OfficeConnect** tab in the ribbon, then click **Sign In**.
6. A browser window opens for Workday SSO authentication. Sign in with your Workday credentials. After successful authentication, the browser closes and the Reporting pane opens in Excel.
7. If the browser doesn't open automatically, look for a pop-up notification in Excel and click **Allow**.

## 3. Build and refresh reports

Building reports on Mac works identically to Windows — drag elements from the Reporting pane, build your header structure, and click Refresh. All core features work:

- Account, version, time, level, and custom dimension elements
- Tutorials in the FP&A and Financials sections of this site apply as written
- Keyboard shortcuts for cell navigation (Tab, Enter, arrow keys) work as expected

## 4. Mac-specific differences

| Feature | Windows | Mac |
|---|---|---|
| Keyboard shortcut for Refresh | Configurable | Not supported — use the ribbon button |
| Data entry / writeback | Supported | Supported |
| Workbook Protection | Fully supported | Fully supported |
| Cell Explorer | Supported | Supported |
| Power Automate Desktop automation | Supported | Not supported (Power Automate Desktop is Windows-only) |

## 5. Common Mac-specific issues

**The OfficeConnect tab doesn't appear after install:**
Close and reopen Excel completely. If the tab is still missing, go to **Insert → Add-ins** and verify OfficeConnect is listed as active. If it shows as inactive, click it to re-enable.

**Sign-in browser window is blocked:**
macOS sometimes blocks the authentication pop-up. Check the Safari pop-up blocker settings or try signing in from a different browser by copying the authentication URL. If your organization uses Workday SSO through an identity provider, confirm the SSO flow supports browser-based authentication from Mac.

**Refresh is slower than on Windows:**
Excel for Mac add-ins run in a sandboxed JavaScript environment, which adds some overhead compared to the COM-based add-in on Windows. Performance is generally acceptable for standard reports; very large workbooks (200+ OfficeConnect formulas) may feel noticeably slower. See [Optimize Performance for Large Models](/build-reports/optimize-performance/) for techniques to reduce formula count.

**Formulas show `#VALUE!` after opening a workbook built on Windows:**
This usually means the workbook was saved in a format that includes Windows-specific metadata. Close and reopen the file, then click Refresh to let OfficeConnect re-resolve the formulas.

---

## Related links

- [Get Started with OfficeConnect](/get-started/)
- [Optimize Performance for Large Models](/build-reports/optimize-performance/)
- [Fix Authentication and Token Errors](/troubleshoot/authentication-token-errors/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/officeconnect-on-mac/`. Confirm the note callout, the table, and the list of Mac-specific issues all render correctly. Confirm related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/officeconnect-on-mac.md
git commit -m "feat: add OfficeConnect on Mac how-to"
```

---

## Task 7: Build a Balance Sheet with OfficeConnect (Financials) (Tutorial)

**Files:**
- Create: `content/build-reports/financials/balance-sheet-report.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/balance-sheet-report.md`:

```markdown
---
title: "Build a Balance Sheet with OfficeConnect (Financials)"
linkTitle: "Balance Sheet"
weight: 9
description: >
  Build a formatted balance sheet in Excel using OfficeConnect's Financials data source — assets, liabilities, and equity drawn live from Workday Financial Management.
tags: ["financials", "tutorial", "reporting"]
---

A balance sheet in OfficeConnect pulls directly from Workday Financial Management's general ledger, so your assets, liabilities, and equity balances are always current without manual copy-paste from Workday Report Writer. This tutorial walks through building a structured balance sheet with the three standard sections.

**What you'll build:** A balance sheet workbook with Current Assets, Non-Current Assets, Current Liabilities, Non-Current Liabilities, and Equity sections — all refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect installed and connected to the **Financials** data source (not Adaptive Planning) ([Get Started](/get-started/))
- Workday Financial Management with balance sheet accounts (Assets, Liabilities, Equity) loaded with actuals
- Basic familiarity with the Financials data source — see [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)

---

## Step 1 — Set up the version and time context

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel, click the **OfficeConnect** tab, and sign in. Confirm the Reporting pane shows the **Financials** data source — you should see account types (Assets, Liabilities, Equity) rather than Adaptive Planning versions and levels.
{{< /step >}}

{{< step n="2" title="Add the version and period" >}}
Click cell **B1**. In the Reporting pane, expand **Versions** and drag **Actuals** into B1. Click **B2** and drag your reporting period (for example, the end of the current quarter) into it. Balance sheets are point-in-time, so choose a specific period end date rather than a range.
{{< /step >}}

---

## Step 2 — Build the Assets section

{{< step n="3" title="Add a section header for Current Assets" >}}
Click **A4** and type `CURRENT ASSETS`. Bold and apply an underline to make it a visual section header.
{{< /step >}}

{{< step n="4" title="Add Current Asset accounts" >}}
Click **A5**. In the Reporting pane, expand **Accounts → Assets → Current Assets**. Drag **Cash and Cash Equivalents** into A5. Continue in A6–A8 with **Accounts Receivable**, **Prepaid Expenses**, and **Other Current Assets**. In **A9**, drag the **Total Current Assets** rollup account.
{{< /step >}}

{{< step n="5" title="Add a section header for Non-Current Assets" >}}
Click **A11** and type `NON-CURRENT ASSETS`. Bold and underline.
{{< /step >}}

{{< step n="6" title="Add Non-Current Asset accounts" >}}
In A12–A14, drag **Property Plant and Equipment (Net)**, **Intangible Assets**, and **Other Non-Current Assets** from the Reporting pane. In **A15**, drag **Total Non-Current Assets**. In **A17**, drag **Total Assets** — the top-level rollup.
{{< /step >}}

{{< step n="7" title="Populate data cells for Assets" >}}
Click **B5**. OfficeConnect creates a formula for Actuals (B1), the period (B2), and Cash and Cash Equivalents (A5). Copy **B5** down through **B17**, skipping the section header rows (B4, B10, B11, B16). Each row resolves to the correct account balance.
{{< /step >}}

---

## Step 3 — Build the Liabilities section

{{< step n="8" title="Add Current Liabilities" >}}
Starting in **A20**, type `CURRENT LIABILITIES` (bold, underlined). In A21–A23, drag **Accounts Payable**, **Accrued Liabilities**, and **Other Current Liabilities**. In **A24**, drag **Total Current Liabilities**.
{{< /step >}}

{{< step n="9" title="Add Non-Current Liabilities" >}}
In **A26**, type `NON-CURRENT LIABILITIES`. In A27–A28, drag **Long-Term Debt** and **Other Non-Current Liabilities**. In **A29**, drag **Total Non-Current Liabilities**. In **A31**, drag **Total Liabilities**.
{{< /step >}}

{{< step n="10" title="Populate data cells for Liabilities" >}}
Click **B21** and copy the formula structure down through **B31**, matching the account rows you've built. Skip the header and spacer rows.
{{< /step >}}

---

## Step 4 — Build the Equity section

{{< step n="11" title="Add Equity accounts" >}}
In **A34**, type `EQUITY`. In A35–A37, drag **Common Stock**, **Retained Earnings**, and **Other Comprehensive Income (Loss)**. In **A38**, drag **Total Equity**.
{{< /step >}}

{{< step n="12" title="Add Total Liabilities and Equity" >}}
In **A40**, drag **Total Liabilities and Equity** — the top-level balance sheet rollup account. In **B40**, copy the formula structure from the rows above. This should equal Total Assets (B17) — the balance check.
{{< /step >}}

---

## Step 5 — Verify and format

{{< step n="13" title="Refresh and check the balance" >}}
Click **Refresh** in the OfficeConnect ribbon. All accounts populate. Verify that **B17** (Total Assets) equals **B40** (Total Liabilities and Equity). If they don't match, check that you've used the correct rollup accounts — the discrepancy usually means a leaf account is missing from one section.
{{< /step >}}

{{< step n="14" title="Format as a balance sheet" >}}
Format the number columns with Accounting format (no decimals). Bold the rollup rows (Total Current Assets, Total Non-Current Assets, Total Assets, Total Current Liabilities, Total Non-Current Liabilities, Total Liabilities, Total Equity, Total Liabilities and Equity). Add a double underline below Total Assets and Total Liabilities and Equity to follow standard balance sheet presentation.
{{< /step >}}

---

## Next steps

- Build a cash flow statement — see [Build a Cash Flow Statement](/build-reports/financials/cash-flow-statement/)
- Add prior-period comparison columns — see [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- Reconcile balances to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/balance-sheet-report/`. Confirm all step blocks render, the page appears in the Financials sidebar section, and next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/balance-sheet-report.md
git commit -m "feat: add Balance Sheet tutorial (Financials)"
```

---

## Task 8: Build a Cash Flow Statement with OfficeConnect (Financials) (Tutorial)

**Files:**
- Create: `content/build-reports/financials/cash-flow-statement.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/cash-flow-statement.md`:

```markdown
---
title: "Build a Cash Flow Statement with OfficeConnect (Financials)"
linkTitle: "Cash Flow Statement"
weight: 10
description: >
  Build an indirect-method cash flow statement in Excel using OfficeConnect's Financials data source — operating, investing, and financing activities from Workday Financial Management.
tags: ["financials", "tutorial", "reporting"]
---

A cash flow statement built in OfficeConnect pulls balance changes and net income directly from Workday Financial Management, eliminating the manual work of reconciling figures from Workday Report Writer into Excel. This tutorial builds an indirect-method statement — the most common format for external financial reporting.

**What you'll build:** A cash flow statement with Operating, Investing, and Financing Activities sections, all refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to the **Financials** data source
- Workday Financial Management with a current period closed and journal entries posted
- A completed balance sheet workbook is helpful for cross-referencing — see [Build a Balance Sheet](/build-reports/financials/balance-sheet-report/)

---

## Step 1 — Set up the version and period

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel, click **OfficeConnect**, and sign in. The Reporting pane should show the Financials data source.
{{< /step >}}

{{< step n="2" title="Add version and time context" >}}
Click **B1** and drag **Actuals** from the Reporting pane. Click **B2** and drag your reporting period (for example, Q2 2026 or the full fiscal year). Cash flow statements cover a period of activity, so use a range period (a full quarter or year) rather than a point-in-time date.
{{< /step >}}

---

## Step 2 — Operating activities (indirect method)

{{< step n="3" title="Add the Net Income starting line" >}}
In **A5**, type `OPERATING ACTIVITIES`. Bold and underline. In **A6**, drag **Net Income** from the Reporting pane. This is the starting point for the indirect method — all adjustments are added or subtracted from net income.
{{< /step >}}

{{< step n="4" title="Add non-cash adjustments" >}}
In **A7**, drag **Depreciation and Amortization** (a non-cash expense — added back to net income). In **A8**, type `Changes in Working Capital` and bold it as a sub-section header.
{{< /step >}}

{{< step n="5" title="Add working capital changes" >}}
In A9–A12, drag accounts that represent working capital changes:
- **A9**: Accounts Receivable (change from prior period)
- **A10**: Prepaid Expenses (change)
- **A11**: Accounts Payable (change)
- **A12**: Accrued Liabilities (change)

In **A13**, drag **Net Cash from Operating Activities** (the rollup for this section).
{{< /step >}}

{{< step n="6" title="Populate Operating Activities data cells" >}}
Click **B6** — OfficeConnect creates a formula for Net Income in the selected period. Copy down through **B13**. Check that working capital change accounts show the period-over-period change, not a point-in-time balance — confirm with your chart of accounts setup.
{{< /step >}}

---

## Step 3 — Investing activities

{{< step n="7" title="Add investing activities" >}}
In **A15**, type `INVESTING ACTIVITIES`. Bold and underline. In A16–A17, drag:
- **A16**: Capital Expenditures (purchases of PP&E — typically a negative number)
- **A17**: Proceeds from Asset Sales (positive)

In **A18**, drag **Net Cash from Investing Activities**.
{{< /step >}}

{{< step n="8" title="Populate Investing Activities data cells" >}}
In **B16**, copy the formula structure from B6. Copy down through B18.
{{< /step >}}

---

## Step 4 — Financing activities

{{< step n="9" title="Add financing activities" >}}
In **A20**, type `FINANCING ACTIVITIES`. Bold and underline. In A21–A22, drag:
- **A21**: Proceeds from Borrowings
- **A22**: Repayment of Debt (negative)

In **A23**, drag **Net Cash from Financing Activities**.
{{< /step >}}

{{< step n="10" title="Add net change in cash" >}}
In **A25**, type `Net Increase (Decrease) in Cash`. In **B25**, enter a plain Excel formula:
```
=B13+B18+B23
```
This sums the three activity sections. In **A26**, drag **Cash at Beginning of Period** and in **A27**, drag **Cash at End of Period** from the Reporting pane to cross-check the net change.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Refresh and verify the cash change" >}}
Click **Refresh**. Check that B25 (the sum formula) equals B27 minus B26 (Cash End minus Cash Beginning). A discrepancy means a cash account is missing from one of the three sections or is double-counted.
{{< /step >}}

{{< step n="12" title="Format the statement" >}}
Apply Accounting number format. Bold all subtotal rows (Net Cash from Operating, Investing, Financing, and Net Increase in Cash). Add a thin border above each subtotal row and a double underline under the Cash at End of Period row.
{{< /step >}}

---

## Next steps

- Cross-reference with your balance sheet — see [Build a Balance Sheet](/build-reports/financials/balance-sheet-report/)
- Add prior-year comparison columns to show YoY cash flow — see [Build an Actuals Trend Report](/build-reports/financials/actuals-trend-report/)
- Reconcile figures to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/cash-flow-statement/`. Confirm all step blocks render and next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/cash-flow-statement.md
git commit -m "feat: add Cash Flow Statement tutorial (Financials)"
```

---

## Task 9: Month-End Close Workflow with OfficeConnect (Tutorial)

**Files:**
- Create: `content/build-reports/financials/month-end-close-workflow.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/month-end-close-workflow.md`:

```markdown
---
title: "Month-End Close Workflow with OfficeConnect"
linkTitle: "Month-End Close Workflow"
weight: 11
description: >
  Use OfficeConnect to run a faster month-end close — verify trial balances, check journal completeness, and produce final financial statements directly from Workday Financial Management.
tags: ["financials", "tutorial", "reporting"]
---

Month-end close in Workday Financial Management involves verifying journal completeness, reconciling account balances, and producing financial statements for management review. OfficeConnect lets your accounting team do all of this in Excel — pulling live data from Workday — without waiting for Report Writer outputs or PDF exports. This tutorial walks through a practical close workflow.

**What you'll build:** A close workbook with a trial balance check sheet, a journal completeness check, and a summary P&L — all refreshable as the close progresses.

**What you'll need:**
- OfficeConnect connected to the **Financials** data source
- Workday Financial Management with the current period in a close-in-progress state
- Familiarity with trial balance reports — see [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)

---

## Step 1 — Build a trial balance check sheet

{{< step n="1" title="Set up a Trial Balance tab" >}}
Open a new Excel workbook. Rename **Sheet1** to `Trial Balance`. Click the OfficeConnect tab and sign in. In the Trial Balance tab, build a quick trial balance:

- **B1**: Actuals version (drag from Reporting pane)
- **B2**: Current close period (drag the month being closed, e.g., April 2026)
- **A5 downward**: Drag all P&L and balance sheet rollup accounts from the Reporting pane — Revenue, COGS, Operating Expenses, Assets, Liabilities, Equity sections
- **B5 downward**: Copy the formula from B5 down for each account row
{{< /step >}}

{{< step n="2" title="Add a debit/credit balance check" >}}
In a blank cell below your accounts (for example, **B30**), enter:
```
=SUMIF(B5:B29,">0",B5:B29)+SUMIF(B5:B29,"<0",B5:B29)
```
This sums all account balances. A balanced trial balance produces **0** — debits equal credits. If the result is non-zero, a journal entry is missing or was posted in error.

In **A30**, type `Balance Check` and apply conditional formatting to **B30**: green fill if the value equals 0, red fill otherwise. This gives a clear at-a-glance indicator during close.
{{< /step >}}

{{< step n="3" title="Click Refresh to check current state" >}}
Click **Refresh** in the OfficeConnect ribbon. All account balances populate from Workday as of the current close period. Review the Balance Check cell. If it's red, work with your accounting team to identify the missing or incorrect journal entry before proceeding.
{{< /step >}}

---

## Step 2 — Check journal entry completeness

{{< step n="4" title="Add a Journal Completeness tab" >}}
Add a new sheet tab named `Journal Check`. In this tab, build a list of recurring journal entries you expect every month — things like depreciation, prepaid amortization, accruals for payroll, and rent. In column A, list the description of each expected journal. In column B, pull the relevant account balance using OfficeConnect to confirm it posted.

For example, if depreciation should be approximately $15,000/month: drag the Depreciation account into a cell and check that the current month balance is close to the expected amount. Format the cell with conditional formatting to flag if the balance is 0 (meaning depreciation likely didn't post).
{{< /step >}}

{{< step n="5" title="Add accrual verification rows" >}}
For each significant accrual, add a row with:
- Column A: Accrual description (e.g., "Payroll Accrual — April")
- Column B: OfficeConnect formula pulling the accrued liability account balance
- Column C: Expected amount (typed as a static value or pulled from a budget/prior-month reference)
- Column D: Variance formula `=B-C` with conditional formatting to flag large differences

Refresh this tab after each batch of journal entries posts to confirm completeness progressively.
{{< /step >}}

---

## Step 3 — Produce financial statements for review

{{< step n="6" title="Add a Summary P&L tab" >}}
Add a new sheet named `P&L Summary`. Build a concise income statement using rollup accounts — Revenue, COGS, Gross Profit, Operating Expenses, EBITDA, and Net Income. Use the same Actuals version and close period you set up in the Trial Balance tab.

This sheet is what you share with management for their review sign-off before the period is locked in Workday.
{{< /step >}}

{{< step n="7" title="Add a prior-period comparison column" >}}
In the P&L Summary, add column C with the prior month's period. Drag the same close period as column B but set to the prior month. Add a Variance column (D) with the formula `=B-C`. This shows month-over-month movement — significant swings often reveal missing journals or timing errors worth investigating before close is finalized.
{{< /step >}}

{{< step n="8" title="Final refresh and review" >}}
Once all journals are posted in Workday and the trial balance check shows 0, click **Refresh** on all sheets. Review the P&L Summary for reasonableness. When the accounting team approves the figures, export the P&L Summary as PDF for the management review record.
{{< /step >}}

---

## Step 4 — Lock the period in Workday

{{< step n="9" title="Lock the period after sign-off" >}}
Period locking happens in Workday Financial Management, not in OfficeConnect. Once management has signed off on the financial statements:

{{< admin-note >}}
Go to Workday → **Financial Accounting** → **Close Accounting Period** (or the equivalent task in your Workday tenant). Lock the period to prevent further journal entries. After locking, your OfficeConnect workbook continues to show the final locked balances on refresh — no changes are needed to the workbook itself.
{{< /admin-note >}}
{{< /step >}}

---

## Next steps

- Build a full balance sheet for the close package — see [Build a Balance Sheet](/build-reports/financials/balance-sheet-report/)
- Drill into specific journal lines to investigate variances — see [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/)
- Reconcile final figures to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/month-end-close-workflow/`. Confirm all step blocks render, the admin-note callout renders inside a step block (nested shortcodes), and next steps links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/month-end-close-workflow.md
git commit -m "feat: add Month-End Close Workflow tutorial (Financials)"
```

---

## Task 10: Variance Analysis by Journal Source (How-to)

**Files:**
- Create: `content/build-reports/financials/variance-by-journal-source.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/variance-by-journal-source.md`:

```markdown
---
title: "Variance Analysis by Journal Source in OfficeConnect"
linkTitle: "Variance by Journal Source"
weight: 12
description: >
  Break down account variances by journal source in OfficeConnect — see how much of a balance movement came from manual journals, system-generated entries, or specific subledgers.
tags: ["financials", "how-to", "reporting"]
---

When a GL account balance moves unexpectedly, the first question is: what kind of journal entry caused it? Workday Financial Management categorizes journal entries by **Journal Source** (Manual Journal, Accounts Payable, Payroll, etc.). OfficeConnect can filter by journal source, letting you isolate the impact of each source on any account balance.

**What you'll need:**
- OfficeConnect connected to the Financials data source
- A report showing a balance or variance you want to investigate

---

## 1. Find journal source elements in the Reporting pane

1. Open the OfficeConnect Reporting pane. Expand **Filters** (or **Journal Sources**, depending on your OfficeConnect version). You should see a list of journal sources configured in your Workday tenant — typically including: **Manual Journal**, **Accounts Payable**, **Accounts Receivable**, **Payroll**, **Fixed Assets**, **Intercompany**, and **System**.
2. If you don't see a journal source filter, confirm with your OfficeConnect admin that the Financials data source is configured to expose journal source dimensions.

## 2. Build a journal source comparison report

3. Set up a basic account report:
   - **B1**: Actuals version
   - **B2**: Reporting period (for example, April 2026)
   - **A5 downward**: Accounts you want to analyze (for example, Operating Expenses accounts)

4. In the header row (row 1), add a column for each journal source you want to compare. Drag **Manual Journal** into **C1**, **Accounts Payable** into **D1**, **Payroll** into **E1**.

5. Click **B5** and copy the formula across to C5, D5, E5. Each column now filters the same account balance by its journal source.

6. Add a **Total** column (F1 = "Total") with the formula `=B5+C5+D5+E5`. This should match the unfiltered B column balance — if it doesn't, there are journal sources not represented in your columns.

7. Click **Refresh**. Each column shows how much of the account balance came from each journal source.

## 3. Identify the source of a variance

8. To investigate a month-over-month variance, add a prior period column for each journal source:
   - **B3**: Current month (e.g., April 2026)
   - **G3**: Prior month (e.g., March 2026) — drag the prior period into G3, then copy the journal source structure from B:F into G:K
   - Add variance formulas in a final column set: `=B5-G5`, `=C5-H5`, etc.

9. The journal source with the largest variance between months is typically the one to investigate. For example, if the Manual Journal column shows a $50,000 variance and all other sources are flat, search in Workday for manual journals posted to that account in April.

> **Tip:** After identifying the journal source, use OfficeConnect's drill-through to jump directly to the journal lines. See [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/) for how to set up the drill-through link.

---

## Related links

- [Drill Through to Workday Journal Lines](/build-reports/financials/drill-through-journal-lines/)
- [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/)
- [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/variance-by-journal-source/`. Confirm the tip callout renders and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/variance-by-journal-source.md
git commit -m "feat: add Variance by Journal Source how-to (Financials)"
```

---

## Task 11: Report on Worktag Combinations (How-to)

**Files:**
- Create: `content/build-reports/financials/worktag-combinations.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/worktag-combinations.md`:

```markdown
---
title: "Report on Worktag Combinations in OfficeConnect"
linkTitle: "Worktag Combinations"
weight: 13
description: >
  Build reports that slice GL actuals by multiple Workday worktags simultaneously — Cost Center and Fund, or Cost Center and Project — using OfficeConnect's dimension filters.
tags: ["financials", "how-to", "reporting"]
---

Workday Financial Management uses **worktags** to tag financial transactions — Cost Center, Fund, Program, Project, Grant, and any custom worktags your organization has defined. OfficeConnect exposes worktags as dimension filters, letting you report on specific combinations (for example, all expenses for Cost Center 1001 within Fund ABC).

**What you'll need:**
- OfficeConnect connected to the Financials data source
- Knowledge of which worktags your organization uses (ask your Workday admin if unsure)

---

## 1. Find worktag dimensions in the Reporting pane

1. Open the OfficeConnect Reporting pane and expand **Dimensions** (or **Worktags**). You should see your organization's configured worktags — common ones include: **Cost Center**, **Fund**, **Program**, **Project**, **Grant**, **Region**, and custom worktags.
2. Each worktag has members — for example, Cost Center might list CC-1001 (Sales), CC-1002 (Marketing), etc.

## 2. Filter a report by a single worktag

3. Build a basic account report with an Actuals version and a reporting period.
4. To filter by a single worktag: drag a Cost Center member (for example, **CC-1001**) into any empty header cell. This applies a filter to all OfficeConnect formulas in the workbook — all values now reflect only transactions tagged to CC-1001.
5. Click **Refresh**. All account balances update to show only CC-1001 activity.

## 3. Combine multiple worktags

6. To filter by two worktags simultaneously — for example, CC-1001 AND Fund ABC:
   - Drag **CC-1001** into one header cell (e.g., E1)
   - Drag **Fund ABC** into a second header cell (e.g., F1)
   OfficeConnect applies both filters as an AND condition — the report shows only transactions tagged to CC-1001 that also belong to Fund ABC.

7. Click **Refresh**. The data reflects the intersection of both worktags.

> **Note:** Worktag filtering in OfficeConnect works as an intersection (AND), not a union (OR). If you need to report on CC-1001 OR CC-1002, build two separate column groups — one with CC-1001 and one with CC-1002 — rather than trying to filter both in a single column.

## 4. Build a worktag matrix report

8. To compare multiple Cost Center and Fund combinations:
   - **B1**: Cost Center CC-1001, **C1**: CC-1002, **D1**: CC-1003
   - **B2**: Fund ABC, **C2**: Fund ABC, **D2**: Fund ABC (if all columns share the same fund)
   - Alternatively vary the fund across columns to see different program funding sources

9. OfficeConnect reads the combination of worktag elements in the column — Cost Center in row 1 and Fund in row 2 — and scopes each column to that intersection. Copy your account formula row down for all accounts.

10. Click **Refresh**. You now have a matrix showing account balances for each worktag combination.

## 5. Remove a worktag filter

11. Click the cell containing the worktag element and press **Delete**. Click **Refresh** — the report reverts to including all worktag values (unfiltered) for that dimension.

---

## Related links

- [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Variance Analysis by Journal Source](/build-reports/financials/variance-by-journal-source/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/worktag-combinations/`. Confirm the note callout renders and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/worktag-combinations.md
git commit -m "feat: add Worktag Combinations how-to (Financials)"
```

---

## Task 12: Reconcile OfficeConnect Values to Workday Reports (How-to)

**Files:**
- Create: `content/build-reports/financials/reconcile-to-workday.md`

- [ ] **Step 1: Create the file**

Write the following to `content/build-reports/financials/reconcile-to-workday.md`:

```markdown
---
title: "Reconcile OfficeConnect Values to Workday Reports"
linkTitle: "Reconcile to Workday"
weight: 14
description: >
  Troubleshoot and explain differences between OfficeConnect figures and Workday Report Writer output — common causes of discrepancies and how to resolve them.
tags: ["financials", "how-to", "reporting"]
---

OfficeConnect and Workday Report Writer pull from the same underlying Workday Financial Management data, so their figures should agree. When they don't, the difference almost always comes down to a filter, period definition, or configuration mismatch — not a data error. This guide walks through the most common causes and how to diagnose them.

**What you'll need:**
- OfficeConnect connected to the Financials data source
- Access to Workday Report Writer or a Workday financial report for comparison

---

## 1. Confirm you're comparing the same period

The most common cause of discrepancies is a period definition mismatch.

1. In your OfficeConnect workbook, note the exact period element you've dragged into the time context cell. Click the cell and check the element details in the Reporting pane — is it a month, a quarter, or a fiscal year? Is it calendar year or fiscal year?
2. In Workday Report Writer, check the **Accounting Date** range or period parameter used to run the report. Workday may default to calendar month while OfficeConnect is set to a fiscal period, or vice versa.
3. Set both to the identical period definition and refresh. If the figures converge, period was the cause.

## 2. Check effective date settings

4. OfficeConnect supports effective-date reporting, which reflects the organization structure as of a specific date rather than the posting date of transactions. If OfficeConnect is set to an effective date that differs from Report Writer's configuration, cost center or department allocations may differ.
5. In the Reporting pane, check whether an effective date element is applied to the workbook. Remove it to revert to the default posting-date view, then compare to Report Writer.

## 3. Verify account scope

6. Confirm that the accounts in your OfficeConnect report match exactly what the Workday report includes. OfficeConnect rollup accounts aggregate all child accounts — if Workday's report uses a different account grouping, figures will differ.
7. Build a side-by-side: list the same leaf-level accounts in OfficeConnect (not rollups) and compare each one to the same account line in Workday. This isolates which account has the discrepancy, narrowing the investigation.

## 4. Check company and currency filters

8. If your organization has multiple companies, confirm that both OfficeConnect and Workday Report Writer are scoped to the same company. In OfficeConnect, check for a Company element in the workbook header — see [Filter Reports by Company](/build-reports/financials/filter-by-company/).
9. If your report uses currency conversion, confirm that both tools are using the same exchange rate type and conversion date. OfficeConnect supports both transaction currency and converted currency reporting — check which is active.

## 5. Check for journal sources excluded by Report Writer

10. Some Workday reports are configured to exclude certain journal sources (for example, intercompany elimination entries or system-generated allocations). OfficeConnect by default includes all journal sources.
11. To scope OfficeConnect to match, apply a journal source filter — see [Variance Analysis by Journal Source](/build-reports/financials/variance-by-journal-source/).

## 6. When you can't find the cause

12. If the figures still don't reconcile after checking all of the above, collect the following and share with your Workday admin or OfficeConnect support:
    - The exact account, period, and filter settings in both OfficeConnect and Workday Report Writer
    - The specific figures that differ (both the OfficeConnect amount and the Workday Report Writer amount)
    - Whether the discrepancy is consistent across periods or appears in a specific month only

> **Note:** Small rounding differences (< $1) between OfficeConnect and Workday Report Writer are expected in some configurations due to currency conversion rounding. These are cosmetic and do not indicate a data problem.

---

## Related links

- [Fix Data Discrepancies Between OfficeConnect and Workday](/troubleshoot/data-discrepancies/)
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Variance Analysis by Journal Source](/build-reports/financials/variance-by-journal-source/)
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/build-reports/financials/reconcile-to-workday/`. Confirm the note callout renders and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/build-reports/financials/reconcile-to-workday.md
git commit -m "feat: add Reconcile to Workday how-to (Financials)"
```

---

## Task 13: Fix OfficeConnect Not Refreshing (Troubleshoot)

**Files:**
- Create: `content/troubleshoot/not-refreshing.md`

- [ ] **Step 1: Create the file**

Write the following to `content/troubleshoot/not-refreshing.md`:

```markdown
---
title: "Fix OfficeConnect Not Refreshing"
linkTitle: "Not Refreshing"
weight: 20
description: >
  OfficeConnect shows stale data or the Refresh button does nothing — causes and step-by-step fixes.
tags: ["troubleshoot", "how-to"]
---

## Symptom

You click **Refresh** in the OfficeConnect ribbon and one of the following happens:
- Nothing happens — the button appears to do nothing
- The progress indicator appears briefly then disappears with no data change
- Some cells update but others remain stale
- Excel shows a spinning cursor for a long time, then refresh completes with no data change

---

## Causes

1. OfficeConnect is not connected to the Adaptive Planning or Financials data source (session expired or not signed in)
2. The workbook has no active OfficeConnect formulas (formulas were deleted or overwritten)
3. A network or firewall issue is blocking the connection to Workday servers
4. The OfficeConnect add-in has entered an error state and needs to be reloaded
5. Excel's automatic calculation is disabled

---

## Fix 1: Check your sign-in status

1. Click the **OfficeConnect** tab in the ribbon.
2. If you see a **Sign In** button (instead of **Refresh**, **Submit**, and other tools), you are not signed in. Click **Sign In** and complete authentication through the Workday SSO browser window.
3. Once signed in, click **Refresh**. If the issue was an expired session, data should now load.

## Fix 2: Verify OfficeConnect formulas are intact

4. Click any cell that should contain OfficeConnect data. Look at the formula bar — it should show an OfficeConnect formula (typically a long string starting with `=OC.` or similar). If the cell contains a plain number or is blank, the formula has been overwritten.
5. If formulas are missing, you'll need to rebuild the report or restore from a backup. OfficeConnect does not cache formulas separately from Excel — if they're overwritten, they're gone.

## Fix 3: Test network connectivity

6. Open a browser and navigate to your Workday tenant URL. If Workday loads in the browser, basic connectivity is fine. If it doesn't load, contact your IT team — the issue is network-level.
7. If you're on a VPN, try disconnecting briefly (if policy allows) and refreshing. Some VPN configurations block or slow traffic to Workday's cloud servers.
8. If you're on a corporate network with a proxy, confirm with IT that the OfficeConnect add-in is allowed to make outbound HTTPS connections to Workday's domains.

## Fix 4: Reload the OfficeConnect add-in

9. Close the OfficeConnect task pane: click the **X** on the Reporting pane panel.
10. In the Excel ribbon, click the **OfficeConnect** tab → **Show Pane** (or equivalent button to re-open the pane). This reloads the add-in's JavaScript runtime.
11. Sign in again if prompted, then click **Refresh**.

If reloading the pane doesn't help, close Excel entirely, reopen it, and open the workbook again. Full Excel restart clears add-in state more completely than closing the pane.

## Fix 5: Check Excel calculation mode

12. Go to **Formulas** tab in the Excel ribbon → **Calculation Options**. Confirm it is set to **Automatic** (not Manual). If set to Manual, OfficeConnect formulas won't recalculate even after refresh.
13. Press **Ctrl+Alt+F9** to force a full recalculation. If this populates the cells, switch Calculation Options back to Automatic.

---

## If none of these work

- Check your OfficeConnect version: click **OfficeConnect → Help → About**. If you're on a version older than 6 months, ask your IT admin to update to the latest version — older versions may lose compatibility with Workday API changes.
- Contact Workday support with your tenant URL, OfficeConnect version, and a description of the steps you've already tried.
- Check the [Workday Community](https://community.workday.com) for known issues with your OfficeConnect version.
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/troubleshoot/not-refreshing/`. Confirm the Symptom, Causes, numbered Fix sections, and "If none of these work" section all render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/troubleshoot/not-refreshing.md
git commit -m "feat: add Fix OfficeConnect Not Refreshing troubleshoot article"
```

---

## Task 14: Fix Authentication and Token Errors (Troubleshoot)

**Files:**
- Create: `content/troubleshoot/authentication-token-errors.md`

- [ ] **Step 1: Create the file**

Write the following to `content/troubleshoot/authentication-token-errors.md`:

```markdown
---
title: "Fix Authentication and Token Errors in OfficeConnect"
linkTitle: "Authentication and Token Errors"
weight: 21
description: >
  OfficeConnect shows authentication errors, token expired messages, or fails to sign in — causes and step-by-step fixes for SSO and token issues.
tags: ["troubleshoot", "how-to", "administration"]
---

## Symptom

One or more of the following:
- OfficeConnect shows an error message containing words like "Authentication failed", "Token expired", "Unauthorized", or "401"
- The sign-in browser window opens but returns an error after you authenticate
- OfficeConnect repeatedly asks you to sign in even after a successful authentication
- Refresh fails immediately with an authentication-related error rather than a network error

---

## Causes

1. The Workday SSO session has expired and the access token needs to be refreshed
2. The OfficeConnect client ID or tenant configuration is incorrect or has changed
3. A browser cookie or cached token is corrupted, preventing new authentication from completing
4. The Workday tenant's OAuth application for OfficeConnect has been disabled or its credentials rotated
5. Multi-factor authentication (MFA) requirements have changed and OfficeConnect's browser flow isn't handling the new MFA step

---

## Fix 1: Sign out and sign back in

The fastest fix for most token errors is a clean sign-out and re-authentication.

1. Click the **OfficeConnect** tab in the ribbon.
2. Click **Sign Out** (you may need to look in the **Help** or account menu if Sign Out isn't immediately visible).
3. Close the OfficeConnect pane.
4. Reopen the pane and click **Sign In**.
5. Complete the full SSO flow in the browser window — enter your Workday credentials and complete any MFA step. Don't close the browser window early.
6. After authentication completes, the browser window should close automatically and the Reporting pane should activate.

## Fix 2: Clear browser authentication cache

If signing out and back in doesn't resolve the issue, the cached authentication token may be corrupted.

7. Close Excel completely.
8. Depending on your operating system:
   - **Windows:** Open **Edge** (the browser OfficeConnect uses for authentication internally). Go to Settings → Privacy → Clear browsing data. Select **Cookies and other site data** and **Cached images and files**. Clear data scoped to Workday's domain.
   - **Mac:** Open **Safari**. Go to **Safari → Clear History** and select the Workday domain's cookies.
9. Reopen Excel, open your workbook, and sign in to OfficeConnect again.

## Fix 3: Verify the tenant URL in OfficeConnect settings

10. In the OfficeConnect ribbon, click **Settings** (or **Options**).
11. Confirm the **Tenant URL** matches your Workday tenant. It should be in the format `https://wd3.myworkday.com/yourcompany` or similar. An incorrect URL causes authentication to fail silently — the SSO flow completes against the wrong tenant.

{{< admin-note >}}
If the tenant URL was recently changed by your Workday admin (for example, after a tenant rename or migration), update it in OfficeConnect Settings and redistribute the updated setting to all users. The tenant URL is sometimes configured centrally via registry keys for enterprise deployments — see your IT admin.
{{< /admin-note >}}

## Fix 4: Check the OAuth application in Workday

12. In Workday, search for **Register API Client** or **Manage API Clients** (requires Integration or Security Admin role).
13. Find the API client registered for OfficeConnect. Confirm:
    - The client is active (not expired or disabled)
    - The client secret has not been rotated without updating OfficeConnect's configuration
    - The redirect URI matches what OfficeConnect expects (typically a localhost redirect URI)
14. If the client secret was rotated, work with your OfficeConnect admin to update the client credentials in the OfficeConnect server configuration or manifest.

## Fix 5: Verify MFA compatibility

15. If your organization recently enabled or changed MFA requirements (for example, switching from TOTP to push notifications), the browser-based SSO flow in OfficeConnect may need to be re-tested.
16. Sign in manually through the OfficeConnect browser window and complete the MFA challenge. If the MFA step works but OfficeConnect still shows an error after browser window closes, the issue may be with the redirect handling — contact your OfficeConnect admin.

---

## If none of these work

- Collect the exact error message text (including any error codes) and your OfficeConnect version number (**Help → About**).
- Ask your Workday Security Admin to check the Workday audit log for failed authentication attempts from OfficeConnect — this often reveals the root cause (wrong tenant, expired client, MFA failure, etc.).
- Contact Workday Support with the error code, tenant URL, and OfficeConnect version.
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/troubleshoot/authentication-token-errors/`. Confirm all sections render and the admin-note callout appears correctly.

- [ ] **Step 3: Commit**

```bash
git add content/troubleshoot/authentication-token-errors.md
git commit -m "feat: add Fix Authentication and Token Errors troubleshoot article"
```

---

## Task 15: Fix Slow Performance in Large Reports (Troubleshoot)

**Files:**
- Create: `content/troubleshoot/slow-performance.md`

- [ ] **Step 1: Create the file**

Write the following to `content/troubleshoot/slow-performance.md`:

```markdown
---
title: "Fix Slow Performance in Large Reports"
linkTitle: "Slow Performance"
weight: 22
description: >
  OfficeConnect refresh takes a long time in large workbooks — diagnose the cause and reduce refresh time.
tags: ["troubleshoot", "how-to"]
---

## Symptom

One or more of the following:
- OfficeConnect refresh takes more than 30 seconds to complete
- Excel freezes or becomes unresponsive during refresh
- Refresh completes but only for part of the workbook — some cells remain stale
- Performance was acceptable in the past but has degraded recently

---

## Causes

1. Too many OfficeConnect formulas in the workbook — each formula is a separate server round-trip
2. Leaf-level accounts used instead of rollup accounts — pulling detail that isn't needed
3. Broad dimension scope — formulas pulling data across all cost centers or all levels when only a subset is needed
4. Workday tenant performance issues during peak usage hours
5. Network latency (VPN, proxy, slow connection)
6. Excel calculation mode interfering with OfficeConnect's refresh sequence

---

## Fix 1: Count and reduce formulas

The number of OfficeConnect formulas is the primary driver of refresh time.

1. In an empty cell, enter: `=COUNTIF(A1:ZZ1000,"=OC.*")` (adjust the range to cover your workbook). This counts the approximate number of OfficeConnect formulas. Alternatively, press **Ctrl+F**, check **Look in: Formulas**, and search for `OC.` to see how many cells match.
2. If you have more than 100 formulas, look for consolidation opportunities:
   - Replace 10 leaf-level account rows with 1 rollup account row
   - Remove columns or rows that are rarely used
   - Split the workbook into a summary workbook (few formulas, fast refresh) and a detail workbook (used less often)

## Fix 2: Switch from leaf accounts to rollup accounts

3. Open the Reporting pane and look at the accounts your report uses. If individual leaf-level accounts (like "Office Supplies — Northeast Region") are used instead of a parent rollup (like "Office Supplies"), replace them.
4. To replace: click the cell containing the leaf account, then drag the appropriate rollup account from the Reporting pane onto the same cell. OfficeConnect updates the formula. One rollup formula = one server call, regardless of how many child accounts are under it.

## Fix 3: Narrow the dimension scope

5. If formulas don't have Level or Cost Center filters, they pull data across all levels in the model — which takes longer for large org structures. Add Level or worktag filters to scope each formula to the relevant part of the hierarchy.
6. See [Work with Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/) and [Optimize Performance for Large Models](/build-reports/optimize-performance/) for detailed techniques.

## Fix 4: Test at off-peak hours

7. Workday tenants experience heavier load during business hours, especially at month-end close. If your refresh is slow during peak hours but fast at other times, the bottleneck is server-side rather than workbook-related.
8. For time-sensitive reports, schedule refresh during off-peak hours — see [Refresh Reports Automatically with Power Automate](/build-reports/refresh-with-power-automate/).

## Fix 5: Check network latency

9. Run a speed test or ping your Workday tenant URL from the command line: `ping yourcompany.myworkday.com`. High latency (>100ms) or packet loss indicates a network problem that affects every OfficeConnect round-trip.
10. If you're on a VPN, disconnect briefly (if policy allows) and time a refresh. If performance improves significantly, work with IT to optimize VPN routing to Workday's servers or request a split-tunnel exception for Workday traffic.

## Fix 6: Check Excel calculation mode

11. Go to **Formulas → Calculation Options** and confirm it is set to **Automatic**. If set to Manual, OfficeConnect formula results may not propagate after refresh, causing apparent "slowness" where the data populated but Excel didn't recalculate dependent cells.
12. After setting to Automatic, press **Ctrl+Alt+F9** to force a full recalculation.

---

## If none of these work

- Check whether the workbook performs better on a different machine or network — this helps isolate whether the issue is workbook-specific, machine-specific, or network-specific.
- Review [Optimize Performance for Large Models](/build-reports/optimize-performance/) for additional workbook-level optimizations.
- Contact Workday Support if refresh times are consistently over 60 seconds for a workbook with fewer than 50 formulas — this may indicate a tenant configuration issue.
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/troubleshoot/slow-performance/`. Confirm all sections render correctly.

- [ ] **Step 3: Commit**

```bash
git add content/troubleshoot/slow-performance.md
git commit -m "feat: add Fix Slow Performance troubleshoot article"
```

---

## Task 16: Fix Data Discrepancies Between OfficeConnect and Workday (Troubleshoot)

**Files:**
- Create: `content/troubleshoot/data-discrepancies.md`

- [ ] **Step 1: Create the file**

Write the following to `content/troubleshoot/data-discrepancies.md`:

```markdown
---
title: "Fix Data Discrepancies Between OfficeConnect and Workday"
linkTitle: "Data Discrepancies"
weight: 23
description: >
  OfficeConnect shows different figures than Workday Report Writer or the Workday UI for the same account and period — common causes and how to diagnose them.
tags: ["troubleshoot", "how-to", "reporting"]
---

## Symptom

One or more of the following:
- An account balance in OfficeConnect doesn't match the same account in a Workday financial report
- Figures match at the rollup level but differ at individual account or cost center level
- Prior-period figures differ between OfficeConnect and Workday Report Writer after a restatement or adjustment
- Totals agree but the breakdown by worktag or dimension differs

---

## Causes

1. Period definition mismatch — OfficeConnect and Workday Report Writer using different period boundaries (fiscal vs. calendar, month-end vs. period-end)
2. Account scope mismatch — different account hierarchies or groupings used in each tool
3. Company or ledger filter mismatch — OfficeConnect showing all companies while Report Writer is scoped to one, or vice versa
4. Effective date vs. posting date difference — OfficeConnect set to effective-date view while Report Writer uses posting dates
5. Currency conversion mismatch — different exchange rate types or conversion dates
6. Journal source exclusions — Workday report configured to exclude certain journal sources that OfficeConnect includes
7. Retroactive adjustments — a prior period was restated in Workday after OfficeConnect data was last refreshed

---

## Fix 1: Align the period definition

This is the most common cause. Confirm both tools are using the exact same period.

1. In your OfficeConnect workbook, click the time context cell. Note the exact period element — is it "April 2026" (a calendar month) or a fiscal period name? Does it use the period end date or a date range?
2. In Workday Report Writer, check the report parameters: what date range or period was used to run the report?
3. Adjust one or both tools to use identical period boundaries, then compare again.

## Fix 2: Compare at the leaf account level

4. Rollup accounts aggregate differently depending on which child accounts are included. To isolate which account has the discrepancy:
   - In OfficeConnect, list individual leaf accounts (not rollups) for the section where figures differ
   - In Workday Report Writer, export or view the same report at leaf-account detail
   - Compare line by line — the discrepancy will appear in a specific account

5. Once the specific account is identified, look at whether that account's hierarchy placement differs between what OfficeConnect is using and what Workday's report is using.

## Fix 3: Check company filter

6. In your OfficeConnect workbook, look for a Company element in the header cells. If no Company filter is applied, OfficeConnect shows data for all companies. If the Workday report is scoped to a single company, the figures will differ.
7. Apply a Company filter in OfficeConnect — see [Filter Reports by Company](/build-reports/financials/filter-by-company/). Re-compare.

## Fix 4: Check effective date settings

8. OfficeConnect can be configured to use effective-date reporting, which reflects the org structure (cost centers, levels) as of a specific date rather than the transaction posting date. If your OfficeConnect workbook has an effective date applied, cost center assignments may differ from what Workday Report Writer shows.
9. In the Reporting pane, look for an Effective Date element in the workbook. Remove it and refresh — if figures now match, effective-date was the cause. See [Use Effective Date Reporting After a Reorganization](/build-reports/financials/effective-date-reporting/) for when to use it intentionally.

## Fix 5: Check currency settings

10. In the Reporting pane, confirm whether your report is showing figures in transaction currency or a converted currency. If the Workday report uses a different currency or rate type, figures will differ for any account with multi-currency transactions.
11. Align both to the same currency and rate type — see [Multi-Currency Reporting with the Financials Data Source](/build-reports/financials/multi-currency-financials/).

## Fix 6: Check journal source scope

12. Some Workday financial reports exclude certain journal sources — intercompany, system-generated allocations, or eliminations. OfficeConnect includes all journal sources by default.
13. Apply journal source filters in OfficeConnect to match what the Workday report includes. See [Variance Analysis by Journal Source](/build-reports/financials/variance-by-journal-source/).

## Fix 7: Refresh after checking for retroactive adjustments

14. If a prior period was adjusted or restated in Workday (for example, a correcting journal entry posted after period close), OfficeConnect will show the updated figure after refresh. If your workbook hasn't been refreshed since the adjustment, the figures will differ.
15. Click **Refresh** and compare again.

---

## If none of these work

- See [Reconcile OfficeConnect Values to Workday Reports](/build-reports/financials/reconcile-to-workday/) for a systematic reconciliation process.
- Collect the exact account, period, filter settings, and specific figures that differ from both tools, and share with your Workday admin or Workday Support.
- Rounding differences of less than $1 between OfficeConnect and Workday are expected in some multi-currency configurations and are not data errors.
```

- [ ] **Step 2: Verify it renders**

Open `http://localhost:1313/troubleshoot/data-discrepancies/`. Confirm all sections render correctly and related links resolve.

- [ ] **Step 3: Commit**

```bash
git add content/troubleshoot/data-discrepancies.md
git commit -m "feat: add Fix Data Discrepancies troubleshoot article"
```

---

## Final Task: Push to Main

- [ ] **Step 1: Run hugo build to catch any errors**

```bash
hugo --minify
```

Expected: build completes with no errors. If there are errors, they will show in the output with the file and line number — fix before pushing.

- [ ] **Step 2: Verify tag pages in the built output**

```bash
ls public/tags/
```

Expected: directories for `adaptive-planning`, `financials`, `tutorial`, `how-to`, `troubleshoot`, `data-entry`, `currency`, `reporting`, `sharing`, `administration`. Each should contain an `index.html`.

- [ ] **Step 3: Push to main**

```bash
git push origin main
```

GitHub Actions will deploy the site to officeconnectpro.com. The tag index pages will be live at `/tags/<tag>/` after deployment completes (typically 2–3 minutes).
```
