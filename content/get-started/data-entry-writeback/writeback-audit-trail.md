---
title: "Auditing Workday OfficeConnect Write-Back Submissions"
linkTitle: "Write-Back Audit Trail"
weight: 50
description: >
  Where Workday OfficeConnect write-back submissions are logged in Adaptive Planning, what's captured, and how to build a SOX-grade review process around the audit trail.
tags: ["write-back", "governance", "security", "system-admin", "reference"]
---

Every Workday OfficeConnect write-back submission is logged server-side in Adaptive Planning. The audit trail captures who changed what, when, and to what value — the foundation of any control around write-back. This reference covers where to find the logs, what's captured, and how to operationalize a review cadence for internal audit or SOX.

**What you'll need:** an Adaptive admin role (or a role with audit log access), the version(s) being written to, and a defined review cadence and reviewer.

---

## Where the audit log lives

In Adaptive Planning, navigate to **Administration** → **Audit** (on newer UIs: **Tools** → **Audit Log**). The log is centralized — Web UI inputs, integration API writes, and OfficeConnect submits all land in the same place. Filter by **Source** to isolate OfficeConnect submissions; the source value is typically **OfficeConnect** or **Excel Add-in** depending on tenant version.

{{< admin-note >}}
If you don't see the Audit menu, your role doesn't include audit access — an elevated permission separate from version-data permissions. Request it with a documented business reason (typically "SOX control owner" or "internal audit reviewer").
{{< /admin-note >}}

## What the log captures

Per submission entry, the log records:

| Field | What it captures |
|---|---|
| Timestamp | Server time of the submit (UTC; convert for your timezone) |
| User | The Adaptive Planning user who submitted |
| Source | OfficeConnect, Web UI, Import, API, etc. |
| Version | Target version of the write |
| Intersection | Account, Level, Time period, custom dimensions |
| Old value | The value present in the version before the submit |
| New value | The value after the submit |
| Result | Success or the error returned (for failed submits) |

A single OfficeConnect submit of 100 cells generates 100 log entries — one per cell that changed. Cells that were unchanged (refreshed value equals typed value) are not logged.

## Why this matters for controls

Write-back changes financial planning data. For organizations subject to SOX, that change is in scope when the planning data flows into financial statements, allocations, or board-reported metrics. The audit trail is the control evidence that only authorized users made changes, changes happened within the approved cycle, changes can be reconstructed if questioned, and anomalies surface through review. Even outside SOX, the trail answers the inevitable forensic questions: "who entered this number?" and "when did Marketing's Q3 budget jump $400k?"

## Setting up a periodic review process

A monthly cadence is the typical baseline. The review is mechanical and shouldn't take more than 30 minutes per cycle for a mid-sized organization.

{{< step n="1" title="Export the prior month's submissions" >}}
Filter the audit log to Source = OfficeConnect and date range = prior calendar month. Export to Excel.
{{< /step >}}

{{< step n="2" title="Sort and bucket by user" >}}
Group submissions by user and version. Calculate per-user totals: submissions, cells changed, largest single change, count over materiality threshold.
{{< /step >}}

{{< step n="3" title="Flag anomalies" >}}
Watch for: submissions outside the planning cycle window, submissions by users not on the approved planner roster, large single-value changes (> 10% of the line item) that weren't pre-discussed, and many small reversals (submit, refresh, submit-different) suggesting confusion in a production version.
{{< /step >}}

{{< step n="4" title="Review with the FP&A lead" >}}
For each flag, the FP&A lead confirms it was legitimate. Document in a review log; unresolved anomalies become tickets.
{{< /step >}}

{{< step n="5" title="Archive the export" >}}
Save the export and review log to a permanent, immutable location (GRC tool, controlled SharePoint, records management). This is audit evidence on demand.
{{< /step >}}

## Sample write-back audit report

A simple monthly report built in Excel from the exported log:

| Section | Content |
|---|---|
| Header | Period, reviewer name, review date |
| Summary | Total submissions, cells changed, active users |
| By version | Submissions and cells changed per version (highlights writes to non-Draft versions) |
| By user | Submissions, cells, largest change; flags users not on the approved roster |
| Anomalies | Each flagged item with reviewer disposition (legitimate / under investigation / reverted) |
| Sign-off | Reviewer signature, date, evidence archive link |

This template plus the exported log is typically sufficient for internal audit walk-throughs.

{{< tip >}}
For large planner populations, automate the export and bucketing with a scheduled query against the Adaptive audit API where available. The reviewer then only sees the anomaly report, not the raw log.
{{< /tip >}}

## SOX implications in plain terms

If finance relies on Adaptive Planning data for any externally-reported metric (revenue forecast, MD&A headcount, capex commitments) and OfficeConnect users can change that data, then:

- **The control is the audit trail + review.** The log itself isn't the control; the documented review is.
- **The control owner needs evidence.** Monthly export + reviewer sign-off + archive.
- **The control needs to operate consistently.** Skipping a month means it failed for that period.

External auditors will ask for the review evidence, not the log itself.

{{< warning >}}
Never delete or modify audit log entries — even obvious test data. Logs are append-only; tampering invalidates the entire log as control evidence. Polluting test data is a tenant-separation issue (use a sandbox), not a cleanup issue.
{{< /warning >}}

## Result

You have a defensible, repeatable audit process around OfficeConnect write-back. Every change is traceable to a user and a moment in time; anomalies surface monthly; the evidence trail satisfies internal audit and external SOX walk-throughs.

## Next steps

- [Designing Write-Back Permissions](/data-entry-writeback/writeback-permissions/) — the prevention side; good permissions reduce the volume of anomalies you'll see in the log.
- [Common Write-Back Errors](/data-entry-writeback/writeback-errors/) — failed submits also appear in the audit log; this article explains what each error means.
- [Secure Workbooks (Admin)](/admin/govern/secure-workbooks/) — broader workbook governance practices that complement the write-back controls.
