# Personal What-If Scenarios (2026R1)

Workday OfficeConnect 2026R1 lets end users create personal what-if scenarios without involving an Adaptive Planning admin — scoped to the individual, branched from a parent version, and invisible to others.


---


{{< new-in-release version="2026R1" >}}
**Personal what-if scenarios** are new in Workday OfficeConnect 2026R1. End users can create their own scenario versions in Excel, branched from a parent version, without involving an Adaptive Planning administrator and without cluttering the shared version list.
{{< /new-in-release >}}

Before 2026R1, every what-if version had to be created in Adaptive Planning by a planning admin or modeler — a slow process that produced a long, shared list of one-off versions. Personal scenarios solve both problems at once.

**What you'll need:**
- Workday OfficeConnect 2026R1 or later
- A tenant where your administrator has enabled personal scenarios (it's an Adaptive Planning model setting)
- Permission to read from the version you want to branch from

## What a personal scenario is

A personal scenario is a **version** like any other, with three differences:

| Property | Personal scenario | Standard version |
|---|---|---|
| Visibility | Only the creator | Anyone with permissions |
| Creation | End user, in Excel | Adaptive Planning admin / modeler |
| Lifecycle | Created and deleted by the user | Governed by the admin |
| Storage | Branched from a parent version | Standalone |

Personal scenarios are stored on the Adaptive Planning server (so they survive workbook deletion and Excel crashes) but never appear in anyone else's version list.

## Step 1 — Create a personal scenario

{{< step n="1" title="Open the Reporting pane and find Versions" >}}
In the OfficeConnect Reporting pane, expand the **Versions** node. You'll see your normal shared versions plus a new **My Scenarios** group (only present in 2026R1+ tenants with the feature enabled).
{{< /step >}}

{{< step n="2" title="Right-click the parent version" >}}
Right-click any version you can read — typically *Working Forecast* or *Budget* — and choose **Create Personal Scenario from this version**.
{{< /step >}}

{{< step n="3" title="Name your scenario" >}}
Give it a memorable name like `WhatIf_HiringFreeze_2026Q3`. The name appears only to you.
{{< /step >}}

## Step 2 — Use the scenario in a report

{{< step n="4" title="Drag the scenario into a Version slot like any other" >}}
The new scenario appears under **My Scenarios** in the Reporting pane. Drag it into a worksheet cell exactly as you would a shared version. See [Add Elements](/get-started/build-reports/add-elements/) for the standard workflow.
{{< /step >}}

{{< step n="5" title="Write data back to the scenario" >}}
If you have write-back enabled, you can modify values in the scenario and submit them — the changes affect only your personal scenario, not the parent version. See [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/).
{{< /step >}}

## Step 3 — Compare to the parent

A common pattern: build a variance report comparing your personal scenario to its parent.

{{< step n="6" title="Place parent and scenario side-by-side" >}}
In separate columns, drag the parent version (B1) and your personal scenario (C1). Subtract them in column D: `=C2-B2`.
{{< /step >}}

{{< step n="7" title="Refresh" >}}
You'll see the deltas — exactly the impact of your what-if assumption.
{{< /step >}}

## Tips

- **Don't share workbooks containing personal scenarios.** Other users won't see your scenario in their Reporting pane, so the linked cells will show `n/a` for them. If you want to share, copy the values out as static numbers or republish on the parent version.
- **Use clear naming.** When you have several what-if branches active, names like `WhatIf_HiringFreeze_2026Q3` are far more useful than `Scenario_1`.
- **Clean up regularly.** Right-click any scenario in **My Scenarios** and choose **Delete** when you no longer need it. The server stores them indefinitely if you don't.
- **Personal scenarios don't replace formal version management.** For board-presentation what-ifs that multiple people need to see, ask your Adaptive Planning admin for a shared version.

## Limitations

- Not available before 2026R1
- Requires the model administrator to enable personal scenarios on the tenant
- Personal scenarios cannot be made shared after the fact — copy data into a new shared version if needed
- The number of personal scenarios per user may be capped by your administrator

## Result

You can branch any shared version into your own private what-if without admin involvement, evaluate the impact in Excel, then discard the branch when done.

## Next steps

- [View By (2026R1)](/reference/whats-new/2026r1-view-by/) — the other big 2026R1 feature.
- [Compare Planning Versions](/get-started/build-reports/compare-planning-versions/) — patterns for comparing any two versions, including personal vs parent.
- [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/) — write-back to a personal scenario uses the same flow.
