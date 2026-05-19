---
title: "Enter Budget Data in Excel with OfficeConnect"
linkTitle: "Enter Budget Data"
weight: 10
description: >
  Use Workday OfficeConnect's data entry mode to write budget figures directly from Excel into Adaptive Planning — no need to log in to the Adaptive Planning web interface.
tags: ["adaptive-planning", "data-entry", "write-back", "fp-and-a", "tutorial"]
aliases:
  - /build-reports/enter-budget-data/
---

Workday OfficeConnect isn't just for reading data from Adaptive Planning — it can write data back. This tutorial walks through setting up a data entry workbook that lets planners enter budget figures in Excel and submit them directly to an Adaptive Planning version.

**What you'll build:** A data entry workbook with account rows and period columns where planners type figures and click Submit to push them into a Budget version in Adaptive Planning.

**What you'll need:**
- Workday OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
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

## Result

You have a distributable Excel data entry workbook that writes back to Workday Adaptive Planning. Planners can complete their inputs without ever leaving Excel.

## Next steps

- Protect the workbook before sharing — see [Lock and Protect Reports](/build-reports/lock-protect-reports/)
- Compare submitted budget to actuals — see [Budget vs. Actuals Variance](/build-reports/budget-vs-actuals-variance/)
- Distribute the workbook via SharePoint — see [Share via Teams & SharePoint](/word-powerpoint/sharing/share-teams-sharepoint-onedrive/)
