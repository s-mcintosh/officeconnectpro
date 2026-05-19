---
title: "Workday OfficeConnect Version Compatibility Matrix"
linkTitle: "Version Compatibility"
weight: 40
description: >
  Which Workday OfficeConnect client versions work with which Workday Adaptive Planning releases — including the forced-upgrade grace periods.
tags: ["reference", "upgrade", "system-admin"]
---

Workday ships OfficeConnect alongside Adaptive Planning releases on a roughly six-month cadence (R1 in spring, R2 in fall). Each release ships a new OfficeConnect client, and the older client is blocked at sign-in after a grace period.

This matrix tracks what's compatible right now and what's coming.

{{< new-in-release version="2026R1" >}}
Currently shipping: **OfficeConnect 2026R1**, released March 14, 2026. See [What's New in 2026R1](/whats-new/2026r1/).
{{< /new-in-release >}}

## Current support matrix

| Workday Release | OfficeConnect client | Status | Notes |
|---|---|---|---|
| **2026R1** | 2026R1 | Current — fully supported | Released March 14, 2026. Adds View By and personal what-if scenarios. |
| **2025R2** | 2025R2 or 2026R1 | Supported with grace period | September 2025 release. End-of-life when 2026R2 ships (fall 2026). |
| **2025R1** | 2025R1 or newer | Outside grace window — clients blocked at sign-in | Introduced write-back. Upgrade is mandatory. |
| **2024R2** and earlier | — | Unsupported | Client blocked at sign-in. Upgrade immediately. |

## Forced-upgrade grace periods

Each release has a grace period during which the prior client can still sign in. After the grace ends, the older client is blocked.

| Install model | Grace period from release date |
|---|---|
| Per-user (current-user only install) | 30 days |
| Per-machine (all-users install) | 60 days |

The grace clock starts on the **release date** (not the day your tenant adopts it). Plan upgrade waves accordingly.

## Feature-by-release table

| Feature | First shipped | Notes |
|---|---|---|
| Personal what-if scenarios | 2026R1 | Requires tenant administrator to enable |
| View By (open cell data in new sheet) | 2026R1 | Ribbon command, no admin gate |
| Write-back from Excel to Adaptive | 2025R1 | Tenant version must be in Input state; requires Input permission |
| OfficeConnect for Word | Long-standing | Compatible with all current releases |
| OfficeConnect for PowerPoint | Long-standing | Compatible with all current releases |
| Cell Explorer | Long-standing | Behavior tweaks each release; check release notes |
| Repeating reports | Long-standing | Performance characteristics improve incrementally each release |

## Excel compatibility

| Excel version | Windows | Mac |
|---|---|---|
| Microsoft 365 (current build) | Full support | Full support (JavaScript add-in) |
| Office 2021 standalone | Full support | Full support |
| Office 2019 standalone | Full support (until Microsoft's mainstream EOL) | Not supported |
| Office 2016 | No longer tested by Workday | Not supported |
| Excel for the Web | Not supported | Not supported |
| Excel mobile (iOS/Android) | Not supported | Not supported |

For the Mac-specific story including the VDI fallback, see [OfficeConnect on Mac](/troubleshoot/officeconnect-on-mac/) and [Mac VDI Workflow](/troubleshoot/mac-vdi-workflow/).

## How this matrix is maintained

Articles on this site carry `minVersion` and `releaseAdded` fields in their front matter. The maintenance cadence:

1. When Workday announces a release date, this page gets a "next release" row marked **Preview**.
2. On release day, the row flips to **Current** and a new "What's new" article ships within 14 days — see [What's New](/whats-new/) hub.
3. When the next release ships, the prior version moves to "Supported with grace period."
4. Once the grace period expires, the version moves to "Outside grace window."

## What to check before an upgrade

For organizations on a managed deployment cadence:

- **Pilot the new version on 5-10 users for 2 weeks** before broad rollout. See [Upgrade Governance](/admin/upgrade/upgrade-governance/) (coming soon).
- **Re-check tenant compatibility.** Workday occasionally introduces a tenant-side change that requires the new client (e.g., write-back required 2025R1+).
- **Re-validate add-in conflicts.** Each release can subtly change Excel hook behavior — see [think-cell Conflict](/troubleshoot/think-cell-conflict/) if your finance team uses both.
- **Update Intune/SCCM packages.** Bump app version so deployment systems recognize the upgrade — see [Intune Win32 Packaging](/admin/deploy/intune-win32/) and [SCCM/MECM Deployment](/admin/deploy/sccm-mecm/).

## End-user upgrade flow

End users hit the forced-upgrade prompt at sign-in once their grace period expires. They can either:

- Run the installer themselves (per [Install for End Users](/get-started/install-end-user/))
- Wait for the IT-managed deployment to push the new version automatically

See [Check & Update Your Version](/get-started/check-version/) for the end-user-facing flow.

## Result

You can answer the "is this version still supported?" question in seconds, plan upgrade waves around the grace periods, and verify your deployment infrastructure is keyed to current releases.

## Next steps

- [What's New in 2026R1](/whats-new/2026r1/) — most recent release.
- [Check & Update Your Version](/get-started/check-version/) — end-user upgrade flow.
- [Upgrade Governance](/admin/upgrade/upgrade-governance/) (coming soon) — managing the forced-upgrade cadence at scale.
