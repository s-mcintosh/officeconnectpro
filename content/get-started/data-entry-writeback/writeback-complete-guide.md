---
title: "Write-Back to Adaptive from Excel: A Complete Guide"
linkTitle: "Write-Back Complete Guide"
weight: 20
description: >
  The 2025R1 write-back feature in Workday OfficeConnect — what it does, who can use it, how to set up a write-back workbook, and how to recover when it fails.
tags: ["write-back", "data-entry", "adaptive-planning", "fpna", "system-admin", "tutorial"]
---

{{< new-in-release version="2025R1" >}}
**Write-back** — submitting data from Excel cells back to Workday Adaptive Planning — became generally available in OfficeConnect 2025R1 (March 2025). It changes OfficeConnect from a one-way reporting surface into a two-way planning surface.
{{< /new-in-release >}}

This guide is the canonical reference for write-back: the concept, what it can and can't do, how to design a workbook for it, and what to do when something goes wrong.

**What you'll need:**
- Workday OfficeConnect 2025R1 or later
- An Adaptive Planning tenant with at least one version that's open for input
- A user account with **Input** permission on that version
- This article assumes you've already built basic OfficeConnect reports — start with [Build Your First Report](/get-started/build-reports/build-first-report/) if not.

## How write-back works

When data entry is enabled on a workbook, OfficeConnect formulas can be **overwritten** with typed values. Typing a number over an existing formula marks the cell as a pending input. Clicking **Submit** in the OfficeConnect ribbon sends every pending input to Adaptive Planning, where it persists in the target version.

After submit completes, the cell's OfficeConnect formula is restored, and the next refresh resolves to the value you submitted.

## What you can write back

| Target | Supported? |
|---|---|
| Leaf-level intersections (single cost center + single account + single time period + single version) | ✓ |
| Rollup accounts | ✗ — must be a leaf account |
| Rollup levels | ✗ — must be a leaf level |
| Aggregated time (e.g., a full quarter cell) | ✗ — must be a single period (month, week, etc., per your model) |
| Calculated / modeled accounts | ✗ — accounts whose value is computed from other accounts cannot accept input |
| Closed or locked versions | ✗ — version must be in input mode |
| Custom dimensions and Worktags | ✓ — when the underlying intersection is otherwise valid |

If you submit to an invalid intersection, OfficeConnect returns an error per cell. See [Common Write-back Errors](#common-write-back-errors).

## Step 1 — Confirm the version is open for input

Write-back requires the target version in Adaptive Planning to be set to **Input** state. If it's locked, submits will fail.

{{< admin-note >}}
This check is usually done by an Adaptive Planning admin (or a power user with model-management permissions). Confirm with your admin that the version you're writing to is in Input state for the time periods you need.
{{< /admin-note >}}

## Step 2 — Enable data entry on the workbook

{{< step n="1" title="Open Workbook Properties" >}}
In the OfficeConnect ribbon, click **Workbook Properties**.
{{< /step >}}

{{< step n="2" title="Set Allow Data Entry to Yes" >}}
In the **Data Entry** section, set **Allow Data Entry** to **Yes**. Click **OK**.
{{< /step >}}

The **Submit** button in the ribbon is now active. OfficeConnect formulas in this workbook can be overwritten with typed values.

## Step 3 — Build the input region

The full step-by-step is in [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/), but the short version:

1. **Rows** = leaf input accounts (one per row)
2. **Columns** = single time periods (one per column)
3. **Headers** = single version, single level, and any required custom dimensions

Use Cell Explorer on a sample data cell after refresh to confirm the intersection is a single, valid leaf. If Cell Explorer shows a rollup, your cell isn't writable.

## Step 4 — Enter values and submit

{{< step n="3" title="Refresh to load current values" >}}
Cells populate with whatever's currently in the version for each intersection.
{{< /step >}}

{{< step n="4" title="Type new values" >}}
Click any data cell and type a number. The cell highlights as a pending input.
{{< /step >}}

{{< step n="5" title="Click Submit" >}}
OfficeConnect pushes every pending input to Adaptive Planning. A confirmation dialog summarizes the result.
{{< /step >}}

## Step 5 — Verify

Click **Refresh** after submit. The cells you submitted should show your new values. If a cell reverts to a different number, an allocation rule, formula, or calculated account in Adaptive Planning has overridden your input — talk to your model administrator.

## Designing for safe write-back

A few patterns make write-back workbooks safer to distribute:

- **One version per workbook.** Mixing two input versions in one file is the fastest way to accidentally submit to the wrong one.
- **Lock non-input cells.** Use Excel's **Protect Sheet** to lock everything except the input region. See [Lock and Protect Reports](/get-started/build-reports/lock-protect-reports/).
- **Show the version name on the sheet.** A visible label like *"Submitting to: Budget 2026 Draft"* prevents misroutes.
- **Add a Cell Explorer reminder.** Note in the workbook that planners should run Cell Explorer on any cell that doesn't accept their input.
- **Pre-flight with a small region first.** Submit 1-2 cells before submitting hundreds — confirms the path is open.

## Common write-back errors

| Error | Cause | Fix |
|---|---|---|
| *"Cannot write to non-leaf intersection"* | Cell resolves to a rollup account, level, or time period | Replace the element with its leaf-level child |
| *"Version is locked"* | Target version is not in Input state | Ask the Adaptive admin to open the version |
| *"Insufficient permission"* | User lacks Input on this version or level | Adjust permissions in Adaptive Planning |
| *"Value overridden after submit"* | An allocation rule or modeled-account formula recalculated the cell | Submit at the source of the calculation, not the result |
| *"Submit failed: timeout"* | Slow network or very large submit (hundreds+ cells) | Split the submit into batches; see [Optimize Performance](/get-started/performance/optimize-performance/) |

## Governance: who should have Input permission?

Write-back grants users the ability to change planning data directly from Excel. Governance recommendations:

- **Production budget/forecast versions:** restricted to designated planners per Level, with review/approval workflow in Adaptive Planning
- **Working drafts:** broader Input access, snapshot to a locked version when finalized
- **What-if scenarios:** in 2026R1+, use [Personal what-if scenarios](/reference/whats-new/2026r1-personal-scenarios/) instead of granting Input to a shared version
- **Audit trail:** every submit is logged in Adaptive Planning with timestamp + user. Review periodically.

## Result

Your team can plan and re-plan in Excel without leaving the tool they live in. Workbook governance, version state, and Adaptive Planning's permission model keep write-back from becoming a foot-gun.

## Next steps

- [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/) — full step-by-step tutorial.
- [Personal what-if scenarios (2026R1)](/reference/whats-new/2026r1-personal-scenarios/) — the safer alternative for one-off branches.
- [Lock and Protect Reports](/get-started/build-reports/lock-protect-reports/) — protect the workbook before distributing.
