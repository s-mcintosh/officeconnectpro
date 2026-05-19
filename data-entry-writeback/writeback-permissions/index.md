# Designing Write-Back Permissions for Workday OfficeConnect

Design Adaptive Planning permissions so Workday OfficeConnect write-back is safe by default — least-privilege roles, version-state gates, and Level-scoped assignments.


---


Workday OfficeConnect write-back inherits Adaptive Planning's permission model. There is no separate "OfficeConnect role" — if a user's Adaptive role grants Input on a version and a Level, they can write to it from Excel. That means good permission design in Adaptive is good write-back governance in OfficeConnect. This article lays out the design principles and the patterns that make write-back safe by default.

**What you'll need:**
- An Adaptive Planning admin or model-management role
- A target version (typically a Budget or Forecast) that planners will write to
- A clear list of who plans for what (planner → Levels they own)

---

## The permission model in plain language

Three things control whether a write-back submit succeeds: **version state** (the version must be in **Input** state — Submitted, Locked, and Closed all reject writes), **role permission on the version** (the user's role must include **Input** on that specific version), and **Level scope** (the user's role grants Input on a set of Levels; submits outside that set fail per cell). All three must align. A planner with Input on Budget 2026 but only for the Sales division cannot write back to a Marketing cost center, even if the workbook lets them type into the cell.

## Design principle 1 — Least privilege

Grant Input only where the user needs it. The default for any new role should be **read-only** on every version; Input is opt-in per version, per Level group. The two most common over-grants are "All Levels" Input on a planner role (because it was easier than mapping each planner to their cost centers) and Input on the closed prior-year version (cloned from the current-year role and never trimmed). Audit role definitions quarterly and flag anything broader than the role's actual job needs.

## Design principle 2 — Version-state gates

Use Adaptive's version states as a write-protect mechanism. A version's input window should be open only when planners are actively working, and closed the rest of the time. A typical annual cycle has Budget Draft (Input open, broad access, July–September), Budget Draft v2 (narrower access for revision, October), Budget Approved (locked at creation, no Input ever), and Budget Final (locked, the baseline going forward). When the cycle moves forward, close the previous version's input window. Even if a planner's role still includes Input, the locked version rejects writes — your floor of protection.

{{< warning >}}
Locking a version does not remove existing data — it only prevents new writes. If you need to undo bad data already submitted, that's a model-data recovery task (snapshot restore or manual correction), not a permissions task. Lock the version first to stop the bleeding, then recover.
{{< /warning >}}

## Design principle 3 — Level-scoped per planner

Assign Input by Level so each planner only touches their own department. Adaptive supports this through Level-based role permissions — the planner role gets Input on Budget 2026, but each user's assignment limits that role to specific Levels. Create one **Planner** role with Input on the active draft, then assign the role per user with their Level scope. Planners can open the same shared workbook and only their own cells will accept submits; others return permission errors. A single budget workbook can be distributed to 20 planners and the permission model prevents cross-department writes.

## Pattern — Draft (broad Input) + Approved (locked)

The single most useful pattern: **Budget 2026 Draft** stays open with planners' Level-scoped Input; **Budget 2026 Approved** is created as a locked snapshot of Draft when finance signs off. Reports compare actuals to Approved (the immutable line); planners iterate on Draft. If a re-plan is needed, create Draft v2 from Approved, open Input, snapshot to a new Approved when done. Approved is your audit baseline.

## Pattern — Pair with Adaptive's approval workflow

Adaptive's submit/approve workflow gives you a review gate. Planners submit through OfficeConnect into Draft; a reviewer in Adaptive approves into Approved. Because OfficeConnect submits go to the version in its current state, if Draft is the only Input-state version, OfficeConnect physically cannot bypass the reviewer.

{{< admin-note >}}
For SOX-relevant planning data, document the write-back permission model as IT general controls: "Only authorized planners can modify planning data; modifications are restricted by version state and Level scope; an immutable Approved version exists as baseline; all submissions are logged." See [Auditing Write-Back Submissions](/data-entry-writeback/writeback-audit-trail/).
{{< /admin-note >}}

## The role of Personal what-if scenarios (2026R1)

Personal what-if scenarios, introduced in 2026R1, give individual users a private space to model changes without touching a shared version. For one-off exploration, this is safer than granting Input on a shared scratch version. Rule of thumb: shared collaborative plan → versioned Input with the patterns above; individual exploration → Personal what-if scenario; reference data → no Input granted, ever. See [Personal what-if scenarios (2026R1)](/whats-new/2026r1-personal-scenarios/) for the feature mechanics.

{{< tip >}}
For new planners, default them to Personal what-if scenarios for their first cycle. Promote them to Input on the shared draft only after they've shown they understand the data model.
{{< /tip >}}

## Result

Your OfficeConnect users can write back productively without the ability to damage planning data they don't own. The permission model in Adaptive does the heavy lifting; OfficeConnect inherits it correctly because there's nothing to override.

## Next steps

- [Common Write-Back Errors](/data-entry-writeback/writeback-errors/) — the errors users will see when permissions don't align, and how to fix each.
- [Auditing Write-Back Submissions](/data-entry-writeback/writeback-audit-trail/) — review what was actually submitted, by whom.
- [Write-Back Complete Guide](/data-entry-writeback/writeback-complete-guide/) — the canonical reference for the write-back feature.
