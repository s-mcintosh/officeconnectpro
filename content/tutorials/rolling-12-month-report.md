---
title: "Create a Rolling 12-Month Report"
linkTitle: "Rolling 12-Month Report"
weight: 2
description: >
  Build a report whose time columns automatically advance each month without manual updates.
---

A rolling 12-month report always shows the current month plus the 11 preceding months — no matter when you open it. This tutorial shows how to build one using OfficeConnect's relative time contexts so the columns update automatically on each refresh.

**What you'll need:**
- An existing OfficeConnect workbook or a blank one ([Build Your First Report](/tutorials/build-first-report/))
- Your Adaptive Planning instance populated with at least 12 months of actuals or forecast data

---

<!-- VIDEO PLACEHOLDER
When the YouTube video is ready, uncomment the section below and replace VIDEO_ID with the 11-character YouTube video ID (e.g. dQw4w9WgXcQ).

## Watch

{{< youtube VIDEO_ID >}}

-->

## How rolling time works in OfficeConnect

OfficeConnect supports **relative time contexts** — time elements that are defined as offsets from the current period rather than as fixed calendar months. When you use *Current Month*, *Current Month -1*, *Current Month -2*, etc., OfficeConnect resolves each offset at refresh time against the current date.

This means your column headers and data update automatically every month without you touching the workbook.

---

## Step 1 — Set up the column headers

{{< step n="1" title="Select the header row" >}}
Click cell **B1** in your workbook. This will hold your oldest month (Current Month -11).
{{< /step >}}

{{< step n="2" title="Add a relative time element" >}}
In the Reporting pane, expand **Time → Relative Periods**. Drag **Current Month -11** into B1. OfficeConnect inserts a time context formula.
{{< /step >}}

{{< step n="3" title="Fill the remaining 11 columns" >}}
Repeat for C1 through M1, adding **Current Month -10** through **Current Month** in order. You should now have 12 header cells spanning a rolling year.
{{< /step >}}

---

## Step 2 — Add account rows

{{< step n="4" title="Add your accounts" >}}
Click cell **B2**. In the Reporting pane, expand **Accounts** and drag your first account (for example, *Revenue*) into B2. Drag your version into A2.
{{< /step >}}

{{< step n="5" title="Extend across the row" >}}
OfficeConnect formulas reference the time element in the header row, so you can copy cell B2 across to M2 and each cell will pick up the correct month automatically.
{{< /step >}}

{{< step n="6" title="Add more account rows" >}}
Copy row 2 down for each account you need (Gross Profit, Operating Expenses, Net Income, etc.). The time headers are shared, so the copies resolve correctly.
{{< /step >}}

For repeating rows across many accounts, see [Repeating Reports](/build-reports/repeating-reports/).

---

## Step 3 — Refresh and verify

{{< step n="7" title="Click Refresh" >}}
Click **Refresh** on the OfficeConnect ribbon. All 12 columns should populate with data for the rolling window ending on the current month.
{{< /step >}}

{{< step n="8" title="Verify the month labels" >}}
Confirm that B1 shows the month 11 periods ago and M1 shows the current month. If the labels look wrong, check that your Adaptive Planning instance has the **Current Period** set correctly in Administration settings.
{{< /step >}}

---

## Step 4 — Lock the column widths and save

{{< step n="9" title="Format the header row" >}}
OfficeConnect time context labels can be long. Shorten them by adding a custom Excel number format to the header cells (for example, `mmm-yy`) so they display as *Jan-25*, *Feb-25*, etc.
{{< /step >}}

{{< step n="10" title="Save and schedule a refresh" >}}
Save the workbook. Each month, open the file and click **Refresh** — the window shifts forward automatically. No column editing needed.
{{< /step >}}

---

## Next steps

- Learn about fixed date ranges alongside rolling ones in [Fixed Date Columns](/troubleshoot/fixed-date-columns/)
- See how to set up a trailing 12-month view in [Trailing 12-Month Report](/troubleshoot/trailing-12-month-report/)
- Share the finished report via SharePoint so the whole team always has the latest version — [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
