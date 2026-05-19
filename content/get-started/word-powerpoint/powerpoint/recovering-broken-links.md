---
title: "Recovering Broken Links in a Workday OfficeConnect PowerPoint Deck"
linkTitle: "Recovering Broken Links"
weight: 40
description: >
  When a Workday OfficeConnect PowerPoint link breaks — file moved, named range renamed, workbook deleted — here are the fix paths in order of cost.
tags: ["sharing", "troubleshoot", "fpna", "how-to"]
---

A linked PowerPoint deck breaks the first time someone moves the source Excel workbook, renames a named range, or saves a copy under a new filename without updating the deck. This article documents how to recognize a broken link and the cheapest fix.

If you're new to linked decks, start with [OfficeConnect for PowerPoint](/get-started/word-powerpoint/powerpoint/officeconnect-for-powerpoint/).

## How a broken link looks

When you open a deck whose source file can't be found, PowerPoint shows one of these symptoms:

- A dialog at open: *"This presentation contains links to other files. Update links?"* (PowerPoint can't find the linked workbook)
- Linked tables show their last-cached values but won't refresh
- Linked charts show as static images with no live data
- Refresh Links returns errors slide-by-slide
- A red error indicator appears on the affected slide thumbnail

## Diagnose first — what's actually broken?

{{< step n="1" title="Open File → Info → Edit Links to Files" >}}
PowerPoint shows every external link with its source file path and status.
{{< /step >}}

{{< step n="2" title="Identify the failure category" >}}
Common categories:

- **Source file moved or renamed** — the path PowerPoint expects no longer exists
- **Named range removed from Excel** — the link target inside the workbook is gone
- **Workbook on SharePoint, sync broken** — the file exists but the local sync path can't reach it
- **Workbook permissions changed** — the file exists but the user lacks read access
- **Workbook upgraded to a new format** — sometimes happens when an older `.xls` is converted
{{< /step >}}

## Fix 1 — Source file moved or renamed (most common)

{{< step n="3" title="Find the new file location" >}}
Locate the workbook in its new location (Teams, SharePoint, OneDrive, or a different folder).
{{< /step >}}

{{< step n="4" title="In the OfficeConnect ribbon, click Manage Links" >}}
The Manage Links dialog opens with every linked element listed.
{{< /step >}}

{{< step n="5" title="Select the links to repoint and click Change Source" >}}
Select all (or a subset) of broken links and click **Change Source**. Browse to the new file location and select it.
{{< /step >}}

{{< step n="6" title="Confirm and refresh" >}}
PowerPoint reconnects the selected links to the new file path. Click **Refresh Links** to pull current data through the new path.
{{< /step >}}

## Fix 2 — Named range removed or renamed in Excel

{{< step n="7" title="Open the source workbook" >}}
Open the Excel workbook and go to **Formulas → Name Manager**. Look for the named range PowerPoint expects.
{{< /step >}}

{{< step n="8" title="Re-create or rename the missing range" >}}
If the range was deleted, re-create it pointing to the original cells. If it was renamed, the simplest fix is to rename it back to the original name. Save the workbook.
{{< /step >}}

{{< step n="9" title="In PowerPoint, Refresh Links" >}}
With the named range restored, **Refresh Links** in PowerPoint should now succeed.
{{< /step >}}

If you can't rename back (the new name is in use elsewhere), use Manage Links → Change Source as in Fix 1, pointing to the same workbook but the new named range.

## Fix 3 — SharePoint or OneDrive sync issue

{{< step n="10" title="Verify the file is reachable in a browser" >}}
Open the file in SharePoint or OneDrive web. If you can see it there, the file exists.
{{< /step >}}

{{< step n="11" title="Sync the parent folder locally" >}}
In your File Explorer, navigate to the file. If it shows a sync-pending or sync-error icon, right-click the folder and trigger sync.
{{< /step >}}

{{< step n="12" title="Repoint to the local synced path" >}}
Once the file is locally available, use Manage Links → Change Source to repoint to the local synced path. PowerPoint generally prefers local paths over remote URLs.
{{< /step >}}

## Fix 4 — Workbook permissions changed

{{< step n="13" title="Request read access from the file owner" >}}
If the source workbook moved to a folder you don't have access to, request **Read** permission. View-only is enough; you don't need edit.
{{< /step >}}

## Last resort — break the link and re-link

If a link is truly unrecoverable and you have an alternate source:

{{< step n="14" title="Manage Links → Break Link" >}}
Select the broken link and click **Break Link**. The linked element becomes a static object on the slide.
{{< /step >}}

{{< step n="15" title="Insert a new link" >}}
On the same slide, use OfficeConnect → **Link from Excel** to insert a new linked element from the available source workbook.
{{< /step >}}

{{< warning >}}
Break Link is permanent. The static object on the slide retains its last-rendered visual but can no longer refresh. Don't break a link unless you're sure you don't need to refresh it again.
{{< /warning >}}

## Preventing broken links

- **Use consistent file paths.** Decide where source workbooks live (e.g., `\\Teams\Finance\Reports\`) and don't move them mid-cycle.
- **Use stable named-range names.** Once you've named a range `BP_PL_Summary`, don't rename it next month.
- **Avoid renaming or moving source workbooks during a board cycle.** Wait until next cycle for any file reorganization.
- **For shared decks, store the source workbook alongside the deck.** Easier for anyone refreshing to find both files.
- **Pin a "source location" note in slide 1 speaker notes.** Future-you (and anyone inheriting the deck) will thank you.

## Result

You can recover from any link breakage in a few minutes instead of rebuilding the deck. And the prevention practices keep most breakages from happening at all.

## Next steps

- [Refreshing All Slides Safely](/get-started/word-powerpoint/powerpoint/refresh-all-slides/) — the discipline that keeps refresh from breaking.
- [Designing a Board Pack Template](/get-started/word-powerpoint/powerpoint/board-pack-template/) — naming conventions that minimize breakage risk.
- [OfficeConnect for PowerPoint](/get-started/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) — the underlying linking workflow.
