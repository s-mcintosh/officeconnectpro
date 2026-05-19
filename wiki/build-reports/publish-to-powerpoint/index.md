---
title: "Publish a Report to PowerPoint"
url: "https://officeconnectpro.com/wiki/build-reports/publish-to-powerpoint/"
description: "Link a live OfficeConnect Excel report into a PowerPoint deck so slides update with one refresh.\n"
tags: ["adaptive-planning","sharing","fpna","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


This tutorial covers linking an OfficeConnect Excel report into a PowerPoint presentation. Once linked, refreshing OfficeConnect in Excel automatically updates the numbers in your slides — no copy-pasting needed.

**What you'll need:**
- A finished OfficeConnect Excel report with data populated ([Build Your First Report](/wiki/build-reports/build-first-report/))
- PowerPoint (Microsoft 365 or Office 2019+)
- OfficeConnect installed on the same machine

---

<!-- VIDEO PLACEHOLDER
When the YouTube video is ready, uncomment the section below and replace VIDEO_ID with the 11-character YouTube video ID (e.g. dQw4w9WgXcQ).

## Watch

{{< youtube VIDEO_ID >}}

-->

## How Excel-to-PowerPoint linking works

OfficeConnect for PowerPoint creates links between named ranges or tables in your Excel workbook and shapes in your PowerPoint slides. When you click **Refresh** in PowerPoint, OfficeConnect re-reads the current Excel values and updates the slide content — even if you are not looking at the Excel file at the time.

---

## Step 1 — Name your ranges in Excel

{{< step n="1" title="Select the data range in Excel" >}}
Open your OfficeConnect Excel report and click **Refresh** to make sure all cells are populated with current data. Select the range you want to appear in PowerPoint — for example, a summary table of revenue and expenses.
{{< /step >}}

{{< step n="2" title="Define a named range" >}}
With the range selected, click the **Name Box** (the field to the left of the formula bar) and type a descriptive name such as `SummaryTable`. Press **Enter**. This named range is what OfficeConnect for PowerPoint will reference.
{{< /step >}}

---

## Step 2 — Insert the link in PowerPoint

{{< step n="3" title="Open your PowerPoint presentation" >}}
Open the PowerPoint deck where you want the data to appear. Navigate to the slide that should contain the table or chart.
{{< /step >}}

{{< step n="4" title="Open the OfficeConnect pane in PowerPoint" >}}
On the **OfficeConnect** ribbon tab in PowerPoint, click **Open Pane**. The pane opens on the right.
{{< /step >}}

{{< step n="5" title="Click 'Add Link'" >}}
In the OfficeConnect pane, click **Add Link**. A dialog appears asking you to select the source workbook and named range.
{{< /step >}}

{{< step n="6" title="Select the workbook and named range" >}}
Browse to your Excel workbook and select the named range `SummaryTable` (or whatever name you used in Step 2). Click **OK**. OfficeConnect inserts a linked table on the slide.
{{< /step >}}

---

## Step 3 — Refresh and verify

{{< step n="7" title="Click Refresh in PowerPoint" >}}
On the OfficeConnect ribbon in PowerPoint, click **Refresh**. OfficeConnect reads the current values from the Excel file and updates the table on the slide.
{{< /step >}}

{{< step n="8" title="Verify the data matches" >}}
Check that the numbers on the slide match the values in your Excel workbook. If any cells show `n/a` or `#REF!`, the named range may have moved — redefine it in Excel and update the link.
{{< /step >}}

---

## Step 4 — Update for a new period

{{< step n="9" title="Refresh Excel first" >}}
At the start of each reporting cycle, open your Excel workbook and click **Refresh** on the OfficeConnect ribbon. This pulls the latest data from Adaptive Planning into Excel.
{{< /step >}}

{{< step n="10" title="Refresh PowerPoint second" >}}
Switch to PowerPoint and click **Refresh** again. The slides update to reflect the new Excel values. The entire deck is now current with no manual editing.
{{< /step >}}

---

## Tips

- **Multiple ranges per slide:** You can link several named ranges to different shapes on the same slide — useful for separate revenue and expense tables.
- **Charts:** OfficeConnect can also link to Excel charts. Select the chart in Excel, give it a name via the **Name Box**, and link it using the same workflow above.
- **Sharing the deck:** Save the updated PowerPoint and share it via SharePoint or email. Recipients who open it will see the static snapshot of the data at the time of your last refresh.

---

## Next steps

- Link data into Word for board reports and narratives — [OfficeConnect for Word](/wiki/word-powerpoint/word/officeconnect-for-word/)
- Share your Excel source report so colleagues can refresh it themselves — [Share via Teams & SharePoint](/wiki/word-powerpoint/sharing/share-teams-sharepoint-onedrive/)

