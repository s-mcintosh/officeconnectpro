---
title: "Optimize Performance for Large Models in OfficeConnect"
linkTitle: "Optimize Performance"
weight: 10
description: >
  Speed up Workday OfficeConnect reports that are slow to refresh — reduce formula count, use efficient time contexts, and configure workbook settings for large Adaptive Planning models.
tags: ["adaptive-planning", "performance", "fpna", "system-admin", "how-to"]
aliases:
  - /build-reports/optimize-performance/
---

Workday OfficeConnect reports can slow down significantly when workbooks contain hundreds of formulas pulling from large Adaptive Planning models. Refresh times of 30–60 seconds are common in unoptimized workbooks; the techniques below typically cut that to under 10 seconds for the same data.

**What you'll need:**
- Workday OfficeConnect connected to an Adaptive Planning tenant
- A workbook that is currently slow to refresh (more than 15 seconds)

---

## 1. Reduce the number of OfficeConnect formulas

The single biggest performance factor is formula count. Each OfficeConnect formula is a separate server call during refresh.

1. **Use rollup accounts instead of leaf accounts.** If you're reporting on 50 leaf-level expense accounts when a single "Total Operating Expenses" rollup account would suffice, replace them. One rollup formula = one server call instead of 50.
2. **Delete unused rows and columns.** Workbooks accumulate leftover OfficeConnect formulas in hidden rows or off-screen columns. Select unused areas, delete the cells entirely (not just clear contents), and save.
3. **Consolidate time contexts.** If every data cell has its own Time element, replace them with a single Time element in the header row that all data cells reference. OfficeConnect reads the shared element rather than re-querying time for each cell.

## 2. Use summary time periods instead of month-by-month

4. A report showing 24 monthly columns (2 years of months) makes many more server calls than a report showing 8 quarterly columns covering the same period. If your use case allows quarterly or annual granularity, switch to it — refresh time drops proportionally.
5. For trend reports that must show months, consider building two separate sheets: a summary sheet with quarterly data (fast refresh, for sharing) and a detail sheet with monthly data (slower, used only when drilling in).

## 3. Enable background refresh

6. In the OfficeConnect ribbon, click **Workbook Properties**. Look for a **Refresh** section and enable **Background Refresh** if available in your version. Background refresh lets Excel remain responsive while the data loads, instead of freezing the UI.

## 4. Avoid volatile Excel functions in the same sheet

7. Excel functions like `NOW()`, `TODAY()`, `RAND()`, and `OFFSET()` recalculate on every keystroke, which can trigger OfficeConnect recalculations repeatedly. Move these functions to a separate sheet, or replace them with static values where possible.

## 5. Limit the Level scope

8. If your report pulls data for all Levels (all departments) in a large org hierarchy, consider adding a Level filter to scope it to the levels your audience actually needs. A report scoped to a single division refreshes much faster than one showing all 200 cost centers.

> **Tip:** Use the Cell Explorer (OfficeConnect ribbon → **Cell Explorer**) to inspect any slow-refreshing cell. It shows exactly which elements the formula is querying — account, version, time, level, and dimensions. This is the fastest way to spot an unexpectedly broad query.

## 6. Check your network and tenant performance

9. Workday OfficeConnect refresh performance is partly determined by Adaptive Planning server response time. If refresh is slow even on a simple workbook, check:
   - Whether other users are running large reports or processes on the tenant at the same time (peak usage hours are slower)
   - Your network connection to Workday's servers (VPN can add latency)
   - Whether your Adaptive Planning model has recently been optimized (contact your admin)

## Result

A workbook that previously took 30-60 seconds to refresh should now complete in under 10 seconds with these techniques applied.

## Next steps

- [Fix Slow Performance in Large Reports](/troubleshoot/slow-performance/) — if you're still seeing slowness after these changes.
- [Cell Explorer / Drill Down](/build-reports/cell-explorer-drill-down/) — find the cells driving slow refresh.
- [Filter Data](/build-reports/filter-data/) — scope reports for faster queries.
