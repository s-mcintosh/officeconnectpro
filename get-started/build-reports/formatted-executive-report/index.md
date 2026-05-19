---
title: "Build a Formatted Executive Report for Distribution"
url: "https://officeconnectpro.com/get-started/build-reports/formatted-executive-report/"
description: "Build a polished, print-ready executive summary report in OfficeConnect with custom formatting, logos, and page layout — ready to share as PDF or Excel.\n"
tags: ["adaptive-planning","reporting","sharing","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


A raw OfficeConnect report shows the right numbers, but an executive report needs to look the part. This tutorial walks through building a formatted P&L summary with branding, clean layout, and print-ready page setup — the kind of report you can share as a PDF without touching it in PowerPoint first.

**What you'll build:** A one-page executive P&L summary with a header, logo, formatted number columns, and page layout configured for PDF export.

**What you'll need:**
- OfficeConnect installed and connected to an Adaptive Planning tenant ([Get Started](/get-started/))
- An Adaptive Planning model with P&L accounts, actuals, and budget loaded
- Basic familiarity with building variance reports — see [Budget vs. Actuals Variance](/get-started/build-reports/budget-vs-actuals-variance/)

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

- Share the PDF automatically — see [Share via Teams & SharePoint](/get-started/word-powerpoint/sharing/share-teams-sharepoint-onedrive/)
- Schedule the refresh automatically — see [Refresh Reports Automatically with Power Automate](/get-started/admin/configure/refresh-with-power-automate/)
- Add it to a PowerPoint deck — see [OfficeConnect for PowerPoint](/get-started/word-powerpoint/powerpoint/officeconnect-for-powerpoint/)

