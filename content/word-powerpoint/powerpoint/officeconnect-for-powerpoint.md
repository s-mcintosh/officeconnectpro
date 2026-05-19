---
title: "OfficeConnect for PowerPoint"
linkTitle: "For PowerPoint"
weight: 10
description: >
  Link live data from your Workday OfficeConnect Excel workbook into PowerPoint slides.
tags: ["sharing", "reporting", "fp-and-a", "tutorial"]
aliases:
  - /share-publish/officeconnect-for-powerpoint/
---

Workday OfficeConnect for PowerPoint lets you link tables and charts from your Excel workbook directly into PowerPoint slides. When the underlying Excel data refreshes, you can update the presentation with one click — no copy-pasting.

## How it works

1. You define **named ranges** in your Workday OfficeConnect Excel workbook (a named range is a labeled group of cells)
2. In PowerPoint, you link those named ranges into slides as tables or charts
3. When you're ready to update the presentation (e.g., for a new reporting period), refresh the links

## Start OfficeConnect for PowerPoint

{{< step n="1" title="Open PowerPoint" >}}
After Workday OfficeConnect is installed (see [Install for End Users](/get-started/install-end-user/)), an **OfficeConnect** tab appears in PowerPoint's ribbon.
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
Enter your Adaptive Planning credentials, or click **Log in with Workday**. If you're already signed in to OfficeConnect for Excel, PowerPoint logs you in automatically. See [Sign In & Create a Tenant](/admin/configure/sign-in-create-tenant/) if you haven't set up the connection yet.
{{< /step >}}

## Create a named range in Excel

Before linking to PowerPoint, you need to name the range in Excel:

{{< step n="1" title="Select the cells in your OfficeConnect Excel report" >}}
Select the table or chart data range you want to embed in PowerPoint.
{{< /step >}}

{{< step n="2" title="Click in the Name Box" >}}
The Name Box is the cell reference field at the top-left of the Excel grid (usually shows something like `A1`). Click it so the contents are selected.
{{< /step >}}

{{< step n="3" title="Type a name and press Enter" >}}
Enter a descriptive name (e.g., `Q3_Revenue_Summary`) with no spaces. The named range is created.
{{< /step >}}

## Link a named range into a PowerPoint slide

{{< step n="1" title="In PowerPoint, navigate to the slide" >}}
Go to the slide where you want to insert the linked data.
{{< /step >}}

{{< step n="2" title="In the OfficeConnect tab, click Link from Excel" >}}
Browse to your Workday OfficeConnect Excel workbook and open it.
{{< /step >}}

{{< step n="3" title="Select the named range to link" >}}
Choose from the available named ranges in the workbook.
{{< /step >}}

{{< step n="4" title="The table or chart appears on the slide" >}}
It's now a live link — formatted exactly as it appears in Excel.
{{< /step >}}

## Update for a new period

When you're ready to update the presentation (e.g., for the next month's board deck):

1. Update the data in your Workday OfficeConnect Excel workbook (change the time element or refresh)
2. In PowerPoint, go to the OfficeConnect tab and click **Refresh Links**
3. Go to the linked slides and verify the data has updated
4. Save the presentation

## Disconnect a link

If you want to stop a slide's data from updating:
1. In PowerPoint, go to **File → Info → Edit Links to Files**
2. Select the link you want to disconnect
3. Click **Break Link**

The table or chart remains as a static object on the slide.

## Result

Your PowerPoint deck refreshes from Excel with one click each period. No more copy-pasting tables from finance into the board pack.

## Next steps

- [Publish to PowerPoint (full tutorial)](/build-reports/publish-to-powerpoint/) — a step-by-step walkthrough of building a deck.
- [OfficeConnect for Word](/word-powerpoint/word/officeconnect-for-word/) — the same workflow for narrative reports.
- [Share Reports via Teams, SharePoint & OneDrive](/word-powerpoint/sharing/share-teams-sharepoint-onedrive/) — distribute the final deck.
