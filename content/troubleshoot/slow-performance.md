---
title: "Fix Slow Performance in Large Reports"
linkTitle: "Slow Performance"
weight: 22
description: >
  OfficeConnect refresh takes a long time in large workbooks — diagnose the cause and reduce refresh time.
tags: ["performance", "adaptive-planning", "fp-and-a", "system-admin", "troubleshoot"]
---

Large Workday OfficeConnect workbooks can grind to a halt if formula counts, dimension scope, or network paths aren't tuned. Before tearing the report apart, review the workbook-level techniques in [Optimize OfficeConnect Performance](/performance/optimize-performance/).

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

1. Press **Ctrl+F** (Find). In the Find dialog, click **Options**, set **Look in** to **Formulas**, and search for `OC.`. The match count shown tells you how many cells contain OfficeConnect formulas. On Mac, use **Cmd+F** and set the same options.
2. If you have more than 100 formulas, look for consolidation opportunities:
   - Replace 10 leaf-level account rows with 1 rollup account row
   - Remove columns or rows that are rarely used
   - Split the workbook into a summary workbook (few formulas, fast refresh) and a detail workbook (used less often)

## Fix 2: Switch from leaf accounts to rollup accounts

3. Open the Reporting pane and look at the accounts your report uses. If individual leaf-level accounts (like "Office Supplies — Northeast Region") are used instead of a parent rollup (like "Office Supplies"), replace them.
4. To replace: click the cell containing the leaf account, then drag the appropriate rollup account from the Reporting pane onto the same cell. OfficeConnect updates the formula. One rollup formula = one server call, regardless of how many child accounts are under it.

## Fix 3: Narrow the dimension scope

5. If formulas don't have Level or Cost Center filters, they pull data across all levels in the model — which takes longer for large org structures. Add Level or worktag filters to scope each formula to the relevant part of the hierarchy.
6. See [Work with Custom Dimensions and Attributes](/build-reports/custom-dimensions-attributes/) and [Optimize OfficeConnect Performance](/performance/optimize-performance/) for detailed techniques.

## Fix 4: Test at off-peak hours

7. Workday tenants experience heavier load during business hours, especially at month-end close. If your refresh is slow during peak hours but fast at other times, the bottleneck is server-side rather than workbook-related.
8. For time-sensitive reports, schedule refresh during off-peak hours — see [Refresh Reports Automatically with Power Automate](/admin/configure/refresh-with-power-automate/).

## Fix 5: Check network latency

9. Run a speed test or ping your Workday tenant URL from the command line: `ping yourcompany.myworkday.com`. High latency (>100ms) or packet loss indicates a network problem that affects every OfficeConnect round-trip.
10. If you're on a VPN, disconnect briefly (if policy allows) and time a refresh. If performance improves significantly, work with IT to optimize VPN routing to Workday's servers or request a split-tunnel exception for Workday traffic.

## Fix 6: Check Excel calculation mode

11. Go to **Formulas → Calculation Options** and confirm it is set to **Automatic**. If set to Manual, OfficeConnect formula results may not propagate after refresh, causing apparent "slowness" where the data populated but Excel didn't recalculate dependent cells.
12. After setting to Automatic, press **Ctrl+Alt+F9** to force a full recalculation.

---

## If none of these work

- Check whether the workbook performs better on a different machine or network — this helps isolate whether the issue is workbook-specific, machine-specific, or network-specific.
- Review [Optimize OfficeConnect Performance](/performance/optimize-performance/) for additional workbook-level optimizations.
- Contact Workday Support if refresh times are consistently over 60 seconds for a workbook with fewer than 50 formulas — this may indicate a tenant configuration issue.

## Next steps

- [Optimize OfficeConnect Performance](/performance/optimize-performance/) for the full set of workbook tuning tips
- [Fix OfficeConnect not refreshing](/troubleshoot/not-refreshing/) if refresh stalls completely rather than runs slowly
- [Refresh Reports Automatically with Power Automate](/admin/configure/refresh-with-power-automate/) to move heavy refreshes to off-peak hours
