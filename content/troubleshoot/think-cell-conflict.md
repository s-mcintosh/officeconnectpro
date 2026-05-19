---
title: "Workday OfficeConnect + think-cell: Resolving the Conflict"
linkTitle: "think-cell Conflict"
weight: 25
description: >
  Workday OfficeConnect and think-cell both use Excel COM subclassing and can interfere with each other — refresh failures, broken charts, Excel crashes. Here's the documented fix.
tags: ["troubleshoot", "fpna", "system-admin"]
---

If your finance team uses both Workday OfficeConnect and think-cell (the PowerPoint chart add-in), you've probably hit a conflict: Excel crashes during OfficeConnect refresh, think-cell charts won't update, or one of the two add-ins quietly disables the other. This article documents the conflict and the workaround.

## Symptom

Any of the following with both add-ins installed:

- Excel crashes during OfficeConnect **Refresh**
- think-cell PowerPoint charts won't refresh from the Excel source
- One ribbon tab disappears after a crash (more often OfficeConnect — see [Re-enabling a Disabled COM Add-in](/troubleshoot/reenable-com-addin/))
- *"OfficeConnect has encountered an error"* dialog with no error code
- Sluggish Excel performance with both add-ins loaded

## Root cause

Both OfficeConnect and think-cell are COM add-ins that hook deeply into Excel through **subclassing** — they intercept Excel's internal Windows messages to extend behavior. When two add-ins subclass the same Excel window in incompatible ways, the second one to load can break the first, or both can corrupt Excel's message handling.

think-cell documents this conflict from their side in [KB0231](https://www.think-cell.com/en/resources/kb/0231). The fix is symmetric — it works the same regardless of which add-in you "prefer."

## Fix — Load order workaround

The most reliable workaround is to control **load order** so that one add-in finishes initializing before the other starts.

{{< step n="1" title="Decide which add-in loads first" >}}
think-cell's KB recommends loading think-cell first, then OfficeConnect. We've seen both orders work; if you're hitting crashes, try think-cell-first first.
{{< /step >}}

{{< step n="2" title="Disable both add-ins" >}}
In Excel: **File → Options → Add-ins → Manage: COM Add-ins → Go**. Uncheck both **Adaptive Insights OfficeConnect** (or **Workday OfficeConnect**) and **think-cell**. Click **OK**.
{{< /step >}}

{{< step n="3" title="Restart Excel" >}}
Close Excel completely.
{{< /step >}}

{{< step n="4" title="Enable think-cell first" >}}
Reopen Excel. Go back to **File → Options → Add-ins → Manage: COM Add-ins → Go**. Check **think-cell** only. Click **OK**.
{{< /step >}}

{{< step n="5" title="Wait for think-cell to fully load" >}}
Allow a few seconds for think-cell's ribbon to appear and its initialization to complete.
{{< /step >}}

{{< step n="6" title="Enable OfficeConnect" >}}
Go back to the COM Add-ins dialog and check **OfficeConnect**. Click **OK**.
{{< /step >}}

{{< step n="7" title="Test refresh" >}}
Click **Refresh** on an OfficeConnect workbook. If the workbook refreshes without crashing, the load order workaround is sufficient.
{{< /step >}}

Once you've established the working order, Excel typically remembers it on subsequent starts.

## Fix — Selective loading per workbook

If load-order tweaking doesn't fully resolve crashes for your environment, the next step is to load only one add-in per session:

- For pure OfficeConnect work: disable think-cell, then open the workbook
- For pure think-cell work: disable OfficeConnect, then open the workbook
- For workbooks that need both: accept the risk and save frequently

This is workable for individual users but inconvenient at scale.

## Fix — Separate Excel install profiles (advanced)

For organizations where many users hit the conflict, IT can deploy two Excel "profiles" via Office shared computer activation or a separate Excel install — one with OfficeConnect, one with think-cell — and let users choose per session. This is a heavyweight solution; reserve it for teams that genuinely need both.

{{< admin-note >}}
If you're managing the conflict at scale, capture which users hit crashes and how often. Workday support and think-cell support both want this information to prioritize their respective fixes.
{{< /admin-note >}}

## What doesn't work

- **Updating one add-in alone** rarely fixes the conflict. Both vendors have shipped multiple updates without eliminating it.
- **Office repair** through Control Panel doesn't help — Office itself isn't corrupt.
- **Reinstalling either add-in** doesn't help unless you also clear Excel's add-in load order.

## When to escalate

If the load-order workaround doesn't resolve crashes:

1. Capture an OfficeConnect log (see *Troubleshoot → Capturing Logs* — coming soon).
2. Open a ticket with **both** Workday support and think-cell support, referencing think-cell KB0231 and providing the OfficeConnect log.
3. Note Excel version (File → Account → About Excel), OfficeConnect version, and think-cell version in the ticket.

## Result

Both add-ins coexist in the same Excel install without crashing, even if you have to be deliberate about load order or switch between them per workbook.

## Next steps

- [Re-Enabling a Disabled COM Add-in](/troubleshoot/reenable-com-addin/) — if a crash left OfficeConnect disabled.
- [Optimize Performance](/performance/optimize-performance/) — reduces the refresh windows where crashes are most likely.
- [Check & Update Your Version](/get-started/check-version/) — make sure you're on a current OfficeConnect build.
