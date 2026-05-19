---
title: "32-bit vs 64-bit Excel for Workday OfficeConnect"
linkTitle: "32-bit vs 64-bit Excel"
weight: 30
description: >
  Why 64-bit Excel matters for large Workday OfficeConnect workbooks, how to check which version you're running, and how to switch without breaking other add-ins.
tags: ["performance", "admin-power-user", "fp-and-a", "how-to"]
---

The single biggest hardware-level ceiling for large Workday OfficeConnect workbooks isn't your laptop's RAM — it's whether you're running 32-bit or 64-bit Excel. 32-bit Excel caps each Excel process at roughly 2 GB of memory regardless of how much RAM you have. 64-bit Excel removes that ceiling. For OfficeConnect users pushing past a few hundred formulas with repeating rows and charts, this is often the difference between a workbook that opens and one that crashes.

**What you'll need:**
- Microsoft 365 or a recent perpetual Office license
- Admin rights to reinstall Office (or your IT team)

---

## The memory ceiling, in concrete terms

Every running program on Windows is a process. 32-bit processes can address about 2 GB of memory each — a hard architectural limit, not a configurable one. 64-bit processes can address terabytes (effectively unlimited for spreadsheet work).

For a small OfficeConnect workbook this never matters. Excel sits at 150-300 MB and you have plenty of headroom. For a large workbook — say 800 OfficeConnect formulas, several repeating-row regions, three or four charts pulling from those ranges — Excel can climb past 1.5 GB during refresh, and you start seeing:

- "Excel ran out of resources" errors during refresh
- The application going unresponsive ("Not Responding" in the title bar) for minutes
- Outright crashes mid-refresh with no error
- Charts that won't redraw or copy/paste failures with "not enough memory"

64-bit Excel doesn't make refresh faster (server calls are the same), but it removes the cliff.

## When 32-bit Excel becomes the bottleneck

You're likely hitting the 32-bit ceiling if any of these apply:

- Workbook file size over 50 MB
- More than 500 OfficeConnect formulas, especially with repeating rows
- Several charts built on top of OfficeConnect ranges
- Frequent unexplained crashes during refresh on a machine with plenty of free RAM
- Other Excel workbooks open at the same time, each contributing to the 2 GB pool — note that each Excel **window** is part of the same process

If none of these apply, 32-bit is fine and switching is unnecessary.

## How to check which Excel you have

{{< step n="1" title="Open Excel" >}}
Any workbook will do.
{{< /step >}}

{{< step n="2" title="Go to File then Account" >}}
Click **File** in the ribbon, then **Account** in the left rail.
{{< /step >}}

{{< step n="3" title="Click About Excel" >}}
On the right side under **Product Information**, click **About Excel**. A dialog opens. The first line shows the version and build, and at the end of that line it reads **32-bit** or **64-bit**.
{{< /step >}}

If it says 32-bit and you fit any of the symptoms above, plan a switch.

## How to switch to 64-bit Excel

Bitness is set at Office install time. You cannot toggle it from inside Excel — you uninstall the 32-bit edition and install the 64-bit edition. Your files, settings, and OfficeConnect installation transfer cleanly because the OfficeConnect installer supports both.

{{< warning >}}
Back up any custom Excel templates, personal macro workbooks (`PERSONAL.XLSB`), and ribbon customizations before reinstalling. The uninstall does not remove these files, but rare cases of profile corruption have been reported. Belt and suspenders.
{{< /warning >}}

{{< step n="1" title="Uninstall the current Office" >}}
On Windows, open **Settings** → **Apps** → **Installed apps**, locate **Microsoft 365** (or your Office edition), and click **Uninstall**. Reboot when prompted.
{{< /step >}}

{{< step n="2" title="Install the 64-bit edition" >}}
Sign in to office.com with the same account. On the install page, expand **Other install options** and select **64-bit**. Run the installer. The install takes 10-20 minutes on a typical machine.
{{< /step >}}

{{< step n="3" title="Reinstall Workday OfficeConnect" >}}
The OfficeConnect add-in must be reinstalled to match the new Excel bitness. Download the installer from your Adaptive Planning tenant (the same package works for both 32 and 64-bit Excel) and run it.
{{< /step >}}

{{< step n="4" title="Verify and reopen workbooks" >}}
Repeat the File → Account → About Excel check. The dialog should now say **64-bit**. Open your largest OfficeConnect workbook and refresh — it should now complete without memory errors.
{{< /step >}}

## Tradeoffs and gotchas

- **Legacy COM add-ins.** Older custom add-ins built for 32-bit Excel (Bloomberg, FactSet, Capital IQ, and any internally-built `.xla` or `.xll` files) may not have a 64-bit build. Check each add-in's documentation before switching, and confirm a 64-bit version exists.
- **VBA with `Declare` statements.** Macros that call Windows APIs via `Declare` need `PtrSafe` keywords for 64-bit. Excel will refuse to run unmodified 32-bit `Declare` calls.
- **No performance gain for small workbooks.** Don't expect faster refresh on a 100-formula report — 64-bit only helps when memory was the bottleneck.

{{< admin-note >}}
For company-wide rollouts, coordinate with your IT team. Many organizations standardize on 32-bit Office because of legacy COM add-ins; getting a 64-bit exception for FP&A users is usually straightforward but requires a documented business case. A frequently-crashing budget workbook is exactly the kind of case that makes the request easy.
{{< /admin-note >}}

## Result

Large OfficeConnect workbooks that previously crashed or hung mid-refresh now open and refresh reliably. You've removed an architectural ceiling that no amount of workbook tuning could work around.

## Next steps

- [Refresh Time Benchmarks](/performance/refresh-benchmarks/) — measure your improvement after switching.
- [Reduce OfficeConnect Element Count](/performance/reduce-element-count/) — tuning that complements the memory upgrade.
- [Optimize Performance for Large Models](/performance/optimize-performance/) — the broader optimization playbook.
