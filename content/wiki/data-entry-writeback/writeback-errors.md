---
title: "Common Workday OfficeConnect Write-Back Errors"
linkTitle: "Write-Back Errors"
weight: 40
description: >
  Diagnose and fix the most common Workday OfficeConnect write-back errors — symptoms, root causes, fixes, and how to prevent each from recurring.
tags: ["write-back", "troubleshoot", "fpna", "system-admin"]
---

Write-back errors in Workday OfficeConnect look intimidating but almost always trace to one of seven causes. This article is the catalog — symptom, root cause, fix, prevention — to use as a lookup when a submit fails.

**What you'll need:** a workbook returning a write-back error, the exact error text, and (for some fixes) access to your Adaptive Planning admin.

---

## Error 1 — "Cannot write to non-leaf intersection"

**Symptom.** Cells fail to submit; they often look correct (they show a number) but the submit rejects them.

**Root cause.** The cell resolves to a rollup, not a leaf. OfficeConnect can only write to a single, fully-specified intersection: one leaf account, one leaf level, one single time period, one version.

**Fix.** Open Cell Explorer on the failing cell (OfficeConnect ribbon → **Cell Explorer**). The element with a triangle or "+ children" indicator is the rollup. Replace it with its leaf-level child.

**Prevention.** Build input ranges from the lowest level of the hierarchy. If you need rollup rows for visual context, put them in non-input rows excluded from the submit range.

## Error 2 — "Version is locked"

**Symptom.** Every cell in the submit fails with the same error.

**Root cause.** The target version is not in **Input** state. OfficeConnect cannot override a locked version regardless of user permissions.

**Fix.** Ask your Adaptive admin to re-open the version for input if appropriate. If intentionally closed, the planner needs to write to a different version — usually a new Draft.

**Prevention.** Add a visible label to the workbook showing the target version and its state. See [Write-Back Permissions](/wiki/data-entry-writeback/writeback-permissions/) for the broader version-state pattern.

## Error 3 — "Insufficient permission"

**Symptom.** Some cells submit successfully; others fail, usually clustered around specific rows or columns.

**Root cause.** The user's Adaptive role doesn't grant Input on the version, Level, account, or custom dimension touched by the failed cells.

**Fix.** Compare failing intersections (via Cell Explorer) to the user's role permissions. The mismatch is usually a Level the user shouldn't see — the workbook was distributed too broadly. Trim the workbook to the user's scope, or extend permissions if appropriate.

**Prevention.** Distribute workbooks scoped to each planner's permissions. Use Adaptive's Level-based role assignments and build per-planner workbooks where practical.

{{< warning >}}
Granting broader permissions to silence the error is a common temptation and almost always the wrong fix. The error is doing its job — telling the user they're trying to write something they shouldn't. Fix the workbook scope, not the role.
{{< /warning >}}

## Error 4 — "Value overridden after submit"

**Symptom.** Submit returns success, but on refresh the cell shows a different number than what was submitted.

**Root cause.** An allocation rule, calculated account, or modeled formula recalculated the cell after the input landed. The submit worked — the value just got overwritten by model logic.

**Fix.** The cell is downstream of a calculation. Submit at the **source** — the input account or driver the calculation reads from — not at the result. Your model admin can trace the source in the Adaptive formula editor.

**Prevention.** Verify each input row resolves to an account marked as "Input" type in Adaptive, not "Calculated" or "Modeled." Cell Explorer shows the account type.

## Error 5 — "Submit failed: timeout"

**Symptom.** A large submit hangs and returns a timeout. Some cells may have landed before the timeout; others didn't.

**Root cause.** The submit exceeded Adaptive's processing window for a single request. Large submits, slow networks, or heavy tenant load all push toward the limit.

**Fix.** Split the submit into smaller batches. Submit half, verify, then submit the other half. For chronic large submits, redesign into multiple smaller input sheets that each submit independently.

**Prevention.** Keep individual submits under a few hundred cells. Network and timing also matter — submitting at 2 a.m. local often succeeds when the same submit times out at 2 p.m.

{{< tip >}}
After a partial failure, run **Refresh** before resubmitting. Refresh shows which cells actually landed, so the resubmit only sends the missing ones. Resubmitting blind can double-submit cells that already went through.
{{< /tip >}}

## Error 6 — "Modeled account cannot accept input"

**Symptom.** Specific account rows always fail submit, regardless of user or version.

**Root cause.** The account is a Modeled (calculated) account in Adaptive — its value is computed from other accounts. Modeled accounts are read-only by design.

**Fix.** Identify the input accounts that feed the modeled account's formula and write to those. Your admin can show the formula and its inputs.

**Prevention.** Before building an input range, ask which accounts are Input vs Modeled. Build inputs only on Input accounts; use Modeled accounts as display rows only.

## Error 7 — "Time period out of input range"

**Symptom.** Some columns submit fine, others fail — usually clustered at the start or end of the year.

**Root cause.** The version's input window only covers a specific date range. A Budget 2026 version with an input window of Jan–Dec 2026 rejects writes to 2025 historical or 2027 projection periods.

**Fix.** Confirm the version's input window with your admin. Either restrict the workbook to periods within the window, or extend the window if the broader range is legitimately needed.

**Prevention.** Build period headers from a Time element that respects the version's input range. Document the input window prominently in the workbook.

{{< admin-note >}}
For recurring errors across many users, instrument them. A simple shared log (SharePoint list, Teams channel, ticket queue) where planners post the error and the cell builds the picture you need. Most write-back error storms trace to a single mis-configured role, a too-broadly-distributed workbook, or a model change that wasn't communicated.
{{< /admin-note >}}

## Result

You can triage any write-back error in under a minute: match the symptom to one of the seven entries above, apply the fix, and apply the prevention to keep it from coming back.

## Next steps

- [Designing Write-Back Permissions](/wiki/data-entry-writeback/writeback-permissions/) — most "Insufficient permission" and "Version is locked" errors are permission-design issues.
- [Auditing Write-Back Submissions](/wiki/data-entry-writeback/writeback-audit-trail/) — confirm what actually landed after a partial-failure scenario.
- [Write-Back Complete Guide](/wiki/data-entry-writeback/writeback-complete-guide/) — the canonical reference for how write-back works end to end.
