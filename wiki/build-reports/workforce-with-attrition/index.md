---
title: "Build a Workforce Plan with Attrition"
url: "https://officeconnectpro.com/wiki/build-reports/workforce-with-attrition/"
description: "Build a headcount forecast that layers attrition, hiring plan, and fully-loaded cost per FTE — broken out by organizational level with repeating rows.\n"
tags: ["reporting","adaptive-planning","fpna","recipe"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Workforce planning is where most operating expense lives, and getting it right means modeling *both* sides of the headcount equation — the hires you plan to add and the people who'll leave naturally. This tutorial walks through building a Workday OfficeConnect workforce plan with attrition baked in, broken out by organizational Level, with fully-loaded cost per FTE calculated alongside.

**What you'll build:** A report that shows beginning headcount, attrition losses, planned hires, ending headcount, and fully-loaded cost — by Level, by month, for the next 12 months.

**What you'll need:**
- OfficeConnect installed and signed in ([Build Your First Report](/wiki/build-reports/build-first-report/))
- A model with headcount-related accounts (Beginning Headcount, Hires, Attrition, Ending Headcount) plus a personnel cost account
- An organizational structure with multiple Levels you want to break out
- Familiarity with repeating rows ([Repeating Reports](/wiki/build-reports/repeating-reports/))

---

## Step 1 — Set up the time and structure

{{< step n="1" title="Add the time headers" >}}
On a blank sheet, click **B1** and drag **Current Month**. Continue across C1:M1 for the next 11 months — a full 12-month forward window.
{{< /step >}}

{{< step n="2" title="Build the row block per Level" >}}
In column A, type a five-row block per Level: `Beginning HC`, `Hires`, `Attrition`, `Ending HC`, `Fully-Loaded Cost`. Leave a blank row between Levels.
{{< /step >}}

---

## Step 2 — Populate the headcount accounts

{{< step n="3" title="Drag the Level into the block header" >}}
Above each five-row block, drag the relevant **Level** element from the Reporting pane (for example, **Engineering**, **Sales**, **G&A**). The Level scopes all rows beneath it until the next Level changes scope.
{{< /step >}}

{{< step n="4" title="Map accounts to rows" >}}
In the Beginning HC row, drag the **Beginning Headcount** account into B. In Hires, drag the **Planned Hires** account. In Attrition, drag the **Attrition** account (usually a negative value). In Ending HC, drag **Ending Headcount**. Copy each cell across B:M.
{{< /step >}}

{{< step n="5" title="Verify the headcount math" >}}
The relationship `Beginning HC + Hires - Attrition = Ending HC` should hold in every column. If it doesn't, the underlying model formula is misconfigured — check the account definitions in Adaptive Planning.
{{< /step >}}

---

## Step 3 — Add fully-loaded cost

{{< step n="6" title="Pull the personnel cost account" >}}
In the Fully-Loaded Cost row, drag the **Total Personnel Cost** account (typically salary + benefits + payroll taxes + equity). Copy across.
{{< /step >}}

{{< step n="7" title="Calculate cost per FTE" >}}
In an additional row labeled `Cost per FTE`, write `=B[FullyLoaded]/B[EndingHC]` referencing the rows above. Format as currency. This gives you a sanity check on whether the cost model is producing reasonable per-head economics.
{{< /step >}}

{{< admin-note >}}
Attrition is often modeled as a percentage rate in Adaptive Planning rather than absolute headcount loss. If your model uses a rate, the Attrition row will show the implied loss in whole FTEs. Confirm with the workforce model owner before interpreting.
{{< /admin-note >}}

---

## Step 4 — Use repeating rows across Levels

{{< step n="8" title="Convert to repeating rows" >}}
Rather than copying the five-row block manually per Level, configure the block as a repeating row scoped on the **Level** dimension. OfficeConnect will expand the block automatically on refresh — one set per Level. The full repeating-rows pattern is covered in [Repeating Reports](/wiki/build-reports/repeating-reports/).
{{< /step >}}

{{< step n="9" title="Add a Total row" >}}
At the bottom, add a Total row that sums Ending HC and Fully-Loaded Cost across all Levels. Use plain Excel `SUM` references or drag the top-level rollup into the cell.
{{< /step >}}

---

## Step 5 — Refresh and validate

{{< step n="10" title="Refresh and spot-check" >}}
Click **Refresh**. Verify that Ending HC for the current month matches your HRIS report — that's the trust anchor. From there, the forward-month projections reflect the hiring plan and attrition assumptions from the model.
{{< /step >}}

---

## Result

You now have a 12-month workforce plan that shows where every FTE comes from and goes to, broken out by Level, with cost layered in. When the CFO asks why personnel cost is growing $1.4M next quarter, the answer is in the report — 18 planned hires in Engineering, partially offset by 6 attrition losses across G&A.

## Next steps

- Pull headcount into your operating P&L — see [Show Headcount in a Financial Report](/wiki/build-reports/headcount-in-financial-report/)
- Build a department-level operating view to pair with this — see [Build a Department P&L Report](/wiki/build-reports/department-pl-report/)
- Use the repeating-rows pattern for other dimensions too — see [Repeating Reports](/wiki/build-reports/repeating-reports/)

