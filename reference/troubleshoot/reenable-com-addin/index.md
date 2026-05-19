---
title: "Re-Enabling a Disabled OfficeConnect COM Add-in"
url: "https://officeconnectpro.com/reference/troubleshoot/reenable-com-addin/"
description: "If Excel disabled Workday OfficeConnect after a crash or stall, the ribbon tab disappears and reinstalling doesn't help — re-enable it from Excel's Disabled Items list.\n"
tags: ["troubleshoot","fpna","system-admin"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


When Excel crashes or hangs while Workday OfficeConnect is running, Excel sometimes responds by disabling the add-in to prevent future crashes. The next time you open Excel, the OfficeConnect tab is gone — and reinstalling OfficeConnect doesn't bring it back.

The fix is to re-enable it from Excel's **Disabled Items** list. This article walks through it.

If your OfficeConnect tab is missing for a different reason (never installed, install corrupted, JavaScript add-in on Mac), see also [Task Pane Not Displaying](/reference/troubleshoot/task-pane-not-displaying/) and [Install for End Users](/get-started/install-end-user/).

## Symptom

- The **OfficeConnect** tab no longer appears in Excel's ribbon
- Reinstalling OfficeConnect doesn't restore the tab
- Excel was recently force-closed, crashed, or stalled with OfficeConnect open

## What you'll see

- Excel ribbon shows Home, Insert, Page Layout, Formulas, Data, Review, View, Help — but no OfficeConnect tab
- File → Options → Add-ins lists OfficeConnect under **Disabled Application Add-ins** at the bottom

## Root cause

When a COM add-in causes Excel to hang or crash, Excel's reliability protection automatically disables it. The add-in stays installed, but isn't loaded on subsequent Excel starts.

## Fix — Windows

{{< step n="1" title="Open Excel Options" >}}
In Excel, click **File → Options**.
{{< /step >}}

{{< step n="2" title="Go to the Add-ins section" >}}
In the left navigation, click **Add-ins**. You'll see lists of Active, Inactive, and **Disabled Application Add-ins**.
{{< /step >}}

{{< step n="3" title="Open the Disabled Items dialog" >}}
At the bottom of the Add-ins page, find the **Manage** dropdown. Select **Disabled Items** and click **Go**.

The Disabled Items dialog opens.
{{< /step >}}

{{< step n="4" title="Find OfficeConnect in the list" >}}
You'll see one or more entries. Look for one whose name starts with **Adaptive Insights OfficeConnect** or **Workday OfficeConnect** (the exact name varies by version).
{{< /step >}}

{{< step n="5" title="Select it and click Enable" >}}
Click the OfficeConnect entry to highlight it, then click **Enable**.

If the dialog closes silently — good, it worked.
{{< /step >}}

{{< step n="6" title="Restart Excel" >}}
Close Excel completely (all open workbooks) and reopen it. The OfficeConnect tab should reappear in the ribbon.
{{< /step >}}

## If Enable doesn't bring it back

Excel re-disables add-ins that crash on the next startup. If you enabled and Excel disabled it again, you're hitting an underlying crash.

{{< step n="7" title="Make sure you're on a supported OfficeConnect version" >}}
See [Check & Update Your Version](/get-started/check-version/).
{{< /step >}}

{{< step n="8" title="Check for add-in conflicts" >}}
OfficeConnect has known conflicts with think-cell, Bloomberg, Macabacus, and Power Pivot. See *Troubleshoot → Add-in Conflicts* (coming soon).
{{< /step >}}

{{< step n="9" title="Try Safe Mode" >}}
Hold Ctrl while clicking Excel to start in Safe Mode. If the OfficeConnect tab appears, the crash is caused by another add-in or a workbook auto-load script.
{{< /step >}}

{{< step n="10" title="Reset the add-in registration" >}}
As an Admin, repair the OfficeConnect install via Control Panel → Programs and Features. See [Install for Admins](/get-started/install-admin/).
{{< /step >}}

{{< step n="11" title="Capture logs and contact Workday support" >}}
See *Troubleshoot → Capture Logs for Workday Support* (coming soon).
{{< /step >}}

## Mac

The Disabled Items mechanism is Windows-specific (it's tied to COM add-ins). On Mac, OfficeConnect runs as a JavaScript add-in and doesn't get "disabled" the same way. If your OfficeConnect tab is missing on Mac:

{{< step n="1" title="Open Insert → Add-ins in Excel for Mac" >}}
In Excel for Mac, go to **Insert → Add-ins** to view your installed add-ins.
{{< /step >}}

{{< step n="2" title="Verify OfficeConnect is listed as active" >}}
Check that OfficeConnect appears in the add-ins list and shows as active.
{{< /step >}}

{{< step n="3" title="Re-enable if listed but inactive" >}}
If OfficeConnect appears but is inactive, click it to re-enable it.
{{< /step >}}

See [OfficeConnect on Mac](/reference/troubleshoot/officeconnect-on-mac/) for the full Mac troubleshooting flow.

## Prevent it from happening again

- **Don't force-close Excel.** Always use File → Close or File → Exit. Force-quit while OfficeConnect is mid-refresh is the most common trigger.
- **Save large workbooks before refreshing.** A refresh that takes 30+ seconds is much more likely to be force-closed by an impatient user.
- **Tune performance.** See [Optimize Performance](/get-started/performance/optimize-performance/) to keep refresh times under 10 seconds so users don't reach for force-quit.

## Result

OfficeConnect is back in the ribbon, and Excel will load it normally on next startup.

## Next steps

- [Optimize Performance](/get-started/performance/optimize-performance/) — reduce the refresh times that cause force-quits in the first place.
- [Task Pane Not Displaying](/reference/troubleshoot/task-pane-not-displaying/) — if the tab is there but the pane won't show.
- [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/) — if you re-enabled but sign-in fails.

