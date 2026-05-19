---
title: "Workday OfficeConnect Patterns for Large Repeating Reports"
linkTitle: "Large Repeating Reports"
weight: 50
description: >
  Patterns and pitfalls for Workday OfficeConnect reports that use repeating rows to generate hundreds of lines from a single element.
tags: ["performance", "reporting", "fp-and-a", "how-to"]
---

Repeating rows are the most powerful performance feature in Workday OfficeConnect. One element can expand to 500 rows on refresh, querying the server as a single operation rather than 500 individual ones. But the same feature, used carelessly, produces workbooks that grow unpredictably, break charts, and confuse the next person who opens them. This guide is the pattern catalog.

**What you'll need:**
- A workbook where repeating rows are appropriate (cost-center lists, account lists, project rosters)
- Reporting pane open, with at least one element that has children (a Level rollup or account rollup)

---

## How repeating rows work

A normal OfficeConnect formula resolves one intersection. A **repeating** formula resolves one intersection per child of a parent element — make "Total US Operations" a repeating Level and the row expands on refresh into one row per cost center under it.

The server returns all rows in a single query, whether that's 10 rows or 1,000. This makes repeating rows fast (one element, many results) and dynamic (add a cost center in Adaptive, the report grows automatically). It also makes them risky to mix with manually-arranged content.

## Pitfall 1 — Forgotten range expansion

The repeat inserts new rows on refresh. Any content **below** the range gets pushed down. A "Total" row that was at row 50 when the report had 30 cost centers is wrong when the company adds 5 new cost centers and refresh expands to 35 rows. Charts and SUMIFs anchored to absolute rows go silently wrong.

**Pattern:** Anchor anything below a repeating range using structured references or Excel Tables. If you must use absolute references, leave buffer rows and add a sanity check (e.g., `=IF(COUNTA(B:B)>expected, "EXPANDED — REVIEW", "ok")`).

## Pitfall 2 — Nested repeats

Two repeating dimensions in the same range — say, repeating Level **and** repeating Account in the same rows — multiplies their child counts. 50 cost centers × 30 accounts = 1,500 rows. Almost always more detail than anyone wanted.

**Pattern:** One repeat dimension per range. If you need a matrix, put one on rows and the other on columns so the result is a grid, not a fan-out.

{{< warning >}}
A nested repeat that accidentally expands to tens of thousands of rows can lock Excel for minutes and may exhaust memory on 32-bit installations. Scope tightly first; remove the scope only after you've seen the row count.
{{< /warning >}}

## Pitfall 3 — Mixing repeating and manual rows

Inserting a manual subtotal row inside a repeating range almost always breaks — the repeat regenerates and your manual row gets overwritten, displaced, or duplicated.

**Pattern:** Keep repeating ranges contiguous. Put subtotals above or below the range. Use the repeating row's own grouping options if you need between-group subtotals.

## Pattern 1 — Scope the repeat with a Level filter

The most common cause of out-of-control repeat expansion is starting from the top of the Level hierarchy. Repeating from "Total Company" gives you every cost center in the org.

{{< step n="1" title="Find the right parent" >}}
In the Reporting pane Level section, find the lowest rollup that still includes everything your report needs — don't start at the top. A report for the North America VP starts at "North America," not "Total Company" — same data for that VP, a quarter of the rows.
{{< /step >}}

{{< step n="2" title="Add a Level filter for further scoping" >}}
Combine the repeat parent with a Level filter (e.g., only operating cost centers, excluding eliminations) to keep the row count predictable.
{{< /step >}}

## Pattern 2 — Split a 1,000-row report across sheets

A single sheet with 1,000 repeating rows is unwieldy regardless of how efficiently OfficeConnect handles it — scrolling, filtering, and printing all suffer. Split by a natural cut (region, business unit, account category) into one sheet per group, each with its own scoped repeat. A summary sheet at the front pulls totals from each detail sheet. Refresh time is roughly the same; the workbook is far easier to navigate.

## Pattern 3 — Pre-aggregate at the source

The cleanest fix for "too much detail" is often to aggregate in Adaptive Planning, not Excel. A custom rollup in the model gives you one row in the report with no repeat at all. Requires admin cooperation but pays off across every workbook that uses it.

{{< admin-note >}}
Treat repeating rows as the second choice and pre-aggregation as the first. A custom rollup in Adaptive is reusable across reports, dashboards, and integrations; a repeating-row pattern only helps the one workbook it lives in. Maintain a shared catalog of rollups.
{{< /admin-note >}}

## When NOT to use repeating rows

Reach for a static row list instead when the output rows are a hand-picked subset that doesn't match any rollup parent, when the list almost never changes (and predictability matters more than dynamism), when the report mixes OfficeConnect data with manual planning inputs in alternating rows, or when downstream consumers (a Power BI export, a SharePoint workflow) depend on a stable row count. In each case, manual rows are slower per refresh but vastly easier to reason about.

## Result

You can build OfficeConnect reports that span hundreds or thousands of rows without runaway refresh time or unexplained breakage. The repeat is doing the heavy lifting; you've scoped it cleanly and isolated it from the rest of the workbook.

## Next steps

- [Reduce OfficeConnect Element Count](/performance/reduce-element-count/) — the broader element-count playbook this article extends.
- [Refresh Time Benchmarks](/performance/refresh-benchmarks/) — what a well-built large report should refresh in.
- [Optimize Performance for Large Models](/performance/optimize-performance/) — the parent guide.
