---
title: "How to Reduce OfficeConnect Element Count for Faster Refresh"
linkTitle: "Reduce Element Count"
weight: 40
description: >
  Element count is the single biggest performance lever in Workday OfficeConnect — five concrete tactics to cut it without losing the report you need.
tags: ["performance", "reporting", "fpna", "how-to"]
---

Each Workday OfficeConnect element in a workbook is a server query on refresh. Cutting element count from 500 to 100 cuts refresh time roughly proportionally — far more impact than any other lever. This is a tactical guide to doing exactly that, without losing the report your audience actually needs.

**What you'll need:**
- An OfficeConnect workbook with measurable refresh time (15+ seconds)
- The Reporting pane open (OfficeConnect ribbon → **Reporting**)

---

## How to count elements in a workbook

{{< step n="1" title="Open the Reporting pane" >}}
Click **Reporting** in the OfficeConnect ribbon.
{{< /step >}}

{{< step n="2" title="Switch to the Review tab" >}}
At the top of the Reporting pane, click **Review**. The pane now lists every element in the workbook, grouped by type (Account, Time, Version, Level, Custom Dimensions).
{{< /step >}}

{{< step n="3" title="Note the totals" >}}
The total at the top of the Review tab is your element count. Capture it now — you'll compare against it after each tactic below.
{{< /step >}}

A workbook with 80 elements should refresh in under 10 seconds on a healthy tenant. If yours is much higher, the tactics below should each take a chunk out.

## Tactic 1 — Use rollup accounts instead of leaves

Most P&L reports get built by dragging 30-50 leaf-level expense accounts (Office Supplies, Postage, Subscriptions, Software, Hardware…) into rows. If your audience only ever looks at the total, replace the leaves with a single rollup — **Total Operating Expenses**, or whatever your model calls it. One element where there were 30.

This is the single highest-yield change in this article. Reach for it first.

{{< tip >}}
If a senior audience wants the rollup but a junior audience wants the leaves, build two sheets: a fast summary on rollups for the executive view, and a slower detail sheet for analysts. Don't pay the leaf-level cost on every refresh.
{{< /tip >}}

## Tactic 2 — Use element groups where available

Adaptive Planning supports **element groups** (saved sets of accounts, levels, or dimensions). A group counts as one element in OfficeConnect but expands to many on refresh. If your admin has defined groups for common reporting cuts (e.g., "Discretionary Spend Accounts," "North America Levels"), use them instead of multi-selecting items individually.

If no groups exist for your use case, ask your Adaptive admin to create one — it's a five-minute task on their end and a permanent performance win for every report that uses it.

## Tactic 3 — Consolidate time elements into a single header

A classic anti-pattern: every data cell in a 12-month report references its own Time element ("January" in B3, "January" in B4, "January" in B5…). That's the same time period queried over and over.

Replace it with a single Time element in the header row (B2 = January), and have every data cell in column B reference B2. OfficeConnect treats the column as one Time element, not dozens. Apply the same pattern to Version and Level headers — one element each in the corner of the report, every data cell referencing them.

A 12-column × 50-row report can drop from 600+ time elements to 12.

## Tactic 4 — Audit hidden rows and columns

Workbooks accumulate cruft: an analyst hides a row of test formulas, never deletes it, and three years later it's still there, refreshing on every open. Unhide everything (Ctrl+A, right-click a row header, **Unhide**; repeat for columns), press Ctrl+End to find the last used cell, and delete orphan rows or columns entirely (right-click → **Delete** → **Entire row/column**). Clearing contents leaves the cell formatted; deleting actually shrinks the used range. Save afterward.

{{< warning >}}
Before deleting anything you didn't create, save a copy of the workbook. Hidden rows occasionally hold lookup tables or named-range anchors that other formulas depend on — broken-formula `#REF!` errors will appear immediately if so.
{{< /warning >}}

## Tactic 5 — Use repeating rows correctly

A **repeating row** is one element that expands to many rows on refresh based on a Level or dimension list. A repeating row generating 200 cost-center rows is one element, not 200. This is huge — for any report listing all the children of a parent, repeating rows are dramatically more efficient than dragging each child in manually.

The catch: repeating rows that overlap with manually-placed rows, or with another repeating row, create unpredictable element counts and breakage. Keep repeats clean — one repeating range per sheet, scoped tightly with a Level filter. See [Large Repeating Reports](/wiki/performance/large-repeating-reports/) for the patterns.

## Putting it together

Apply the tactics in order, re-counting after each. A typical 500-element legacy workbook drops to 280 after rollups, 180 after element groups, 110 after header consolidation, 95 after hidden-row cleanup, and 40 after repeating rows — roughly a 90% reduction in refresh time.

{{< admin-note >}}
For chronic offenders — workbooks that grow back to 500 elements every quarter as analysts add detail — establish a workbook standard with maximum element budgets per sheet (e.g., "no more than 150 elements per tab") and audit existing reports quarterly. The cleanup is easier as a habit than as a rescue mission.
{{< /admin-note >}}

## Result

A workbook with one-fifth to one-tenth the original element count and a refresh time that drops proportionally. The report shows the same numbers — it just stops being painful to use.

## Next steps

- [Refresh Time Benchmarks](/wiki/performance/refresh-benchmarks/) — confirm your new element count puts you in the expected refresh bucket.
- [Large Repeating Reports](/wiki/performance/large-repeating-reports/) — for tactic 5 in depth.
- [Optimize Performance for Large Models](/wiki/performance/optimize-performance/) — the broader playbook this article fits into.
