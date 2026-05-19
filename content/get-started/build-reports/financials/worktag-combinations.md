---
title: "Report on Worktag Combinations in OfficeConnect"
linkTitle: "Worktag Combinations"
weight: 13
description: >
  Build reports that slice GL actuals by multiple Workday worktags simultaneously — Cost Center and Fund, or Cost Center and Project — using OfficeConnect's dimension filters.
tags: ["financials", "accounting", "reporting", "fpna", "how-to"]
---

Workday Financial Management uses **worktags** to tag financial transactions — Cost Center, Fund, Program, Project, Grant, and any custom worktags your organization has defined. OfficeConnect exposes worktags as dimension filters, letting you report on specific combinations (for example, all expenses for Cost Center 1001 within Fund ABC).

**What you'll need:**
- OfficeConnect connected to the Financials data source
- Knowledge of which worktags your organization uses (ask your Workday admin if unsure)

---

{{< step n="1" title="Find worktag dimensions in the Reporting pane" >}}
Open the OfficeConnect Reporting pane and expand **Dimensions** (or **Worktags**). You should see your organization's configured worktags — common ones include: **Cost Center**, **Fund**, **Program**, **Project**, **Grant**, **Region**, and custom worktags. Each worktag has members — for example, Cost Center might list CC-1001 (Sales), CC-1002 (Marketing), etc.
{{< /step >}}

{{< step n="2" title="Filter a report by a single worktag" >}}
Build a basic account report with an Actuals version and a reporting period. To filter by a single worktag, drag a Cost Center member (for example, **CC-1001**) into any empty header cell. This applies a filter to all OfficeConnect formulas in the workbook — all values now reflect only transactions tagged to CC-1001. Click **Refresh**. All account balances update to show only CC-1001 activity.
{{< /step >}}

{{< step n="3" title="Combine multiple worktags" >}}
To filter by two worktags simultaneously — for example, CC-1001 AND Fund ABC:

- Drag **CC-1001** into one header cell (e.g., E1)
- Drag **Fund ABC** into a second header cell (e.g., F1)

OfficeConnect applies both filters as an AND condition — the report shows only transactions tagged to CC-1001 that also belong to Fund ABC. Click **Refresh**. The data reflects the intersection of both worktags.

> **Note:** Worktag filtering in OfficeConnect works as an intersection (AND), not a union (OR). If you need to report on CC-1001 OR CC-1002, build two separate column groups — one with CC-1001 and one with CC-1002 — rather than trying to filter both in a single column.
{{< /step >}}

{{< step n="4" title="Build a worktag matrix report" >}}
To compare multiple Cost Center and Fund combinations, set up your column headers:

- **B1**: Cost Center CC-1001, **C1**: CC-1002, **D1**: CC-1003
- **B2**: Fund ABC, **C2**: Fund ABC, **D2**: Fund ABC (if all columns share the same fund)
- Alternatively vary the fund across columns to see different program funding sources

OfficeConnect reads the combination of worktag elements in the column — Cost Center in row 1 and Fund in row 2 — and scopes each column to that intersection. Copy your account formula row down for all accounts. Click **Refresh**. You now have a matrix showing account balances for each worktag combination.
{{< /step >}}

{{< step n="5" title="Remove a worktag filter" >}}
Click the cell containing the worktag element and press **Delete**. Click **Refresh** — the report reverts to including all worktag values (unfiltered) for that dimension.
{{< /step >}}

---

## Related links

- [Report on Actuals by Cost Center](/get-started/build-reports/financials/actuals-by-cost-center/)
- [Filter Reports by Company](/get-started/build-reports/financials/filter-by-company/)
- [Variance Analysis by Journal Source](/get-started/build-reports/financials/variance-by-journal-source/)
