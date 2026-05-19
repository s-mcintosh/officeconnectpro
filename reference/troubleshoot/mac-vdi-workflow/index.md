---
title: "Workday OfficeConnect on Mac: The VDI Workflow"
url: "https://officeconnectpro.com/reference/troubleshoot/mac-vdi-workflow/"
description: "Mac users can run the full Windows OfficeConnect experience through a VDI like Azure Virtual Desktop, AWS WorkSpaces, or Parallels — here's the realistic decision guide and setup.\n"
tags: ["troubleshoot","deployment","fpna","system-admin","how-to"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


The native Mac version of Workday OfficeConnect (Excel for Mac JavaScript add-in) supports most reporting workflows, but a few power-user features remain Windows-only — most notably Power Automate Desktop integration, configurable refresh shortcuts, and the broadest set of add-in interop. For Mac users who need parity with their Windows colleagues, a VDI (virtual desktop infrastructure) is the established workaround.

This article compares the three realistic options and walks through the simplest setup.

If you only need the native Mac experience and are okay with the limitations, see [OfficeConnect on Mac](/reference/troubleshoot/officeconnect-on-mac/) first.

## When you actually need a VDI

| Need | Native Mac OK? | VDI required? |
|---|---|---|
| Build and refresh reports | ✓ | — |
| Write-back / data entry | ✓ | — |
| Cell Explorer drill-down | ✓ | — |
| Configurable refresh keyboard shortcut | ✗ | ✓ |
| Power Automate Desktop automation | ✗ | ✓ |
| Conflict-prone add-in interop (think-cell, etc.) | partial | ✓ |
| IT-policy-required Windows environment | — | ✓ |

If none of your work hits a "VDI required" row, stay on native Mac.

## Option 1 — Azure Virtual Desktop (AVD)

**Best for:** organizations already using Microsoft 365 at scale.

- Lives in Azure; users connect via the AVD client or browser
- Microsoft 365 + Office is licensed naturally through your Microsoft tenant
- Identity integration with Microsoft Entra ID is automatic
- IT admin can pre-install Workday OfficeConnect and deploy tenant config via [registry](/wiki/admin/deploy/deploy-tenants-registry/)

**Setup:** Have your IT team provision an AVD host pool with Office installed, then push OfficeConnect via Intune. The Mac user opens the AVD client, signs in to their session, and uses Excel + OfficeConnect normally.

## Option 2 — AWS WorkSpaces

**Best for:** organizations already on AWS or wanting AWS-side cost controls.

- Comparable to AVD; Windows desktop in AWS, accessed via WorkSpaces client
- Office licensing brought via your existing volume license or bundled
- Slightly more setup effort for identity integration than AVD if you're not on AWS Directory Service

**Setup:** Provision a WorkSpace bundle with Office, install OfficeConnect, deploy tenant config. Mac user installs the WorkSpaces client and connects.

## Option 3 — Parallels Desktop on the Mac

**Best for:** individual users without IT-managed VDI access.

- A full Windows VM running on the Mac itself
- One-time cost (Parallels license + Windows license)
- No reliance on cloud / network — works offline
- IT can't centrally manage it; the user is on the hook for Windows patching and OfficeConnect upgrades

**Setup:** Buy and install Parallels Desktop. Install Windows 11. Install Microsoft 365. Install Workday OfficeConnect via [Install for End Users](/wiki/install-end-user/). Configure your tenant via [Sign In & Create a Tenant](/wiki/admin/configure/sign-in-create-tenant/).

## Workflow tips for any VDI

- **Store workbooks in OneDrive or SharePoint**, not on the local Mac, so the VDI session can open them directly without file shuttling.
- **Use the VDI for OfficeConnect work specifically.** Reading the news, taking video calls, etc. is still better on the native Mac.
- **Two monitors help.** Most VDI clients support displaying the Windows desktop on a separate Mac monitor.
- **Latency matters.** A 100ms-plus connection makes drag-and-drop in the Reporting pane feel sluggish. Choose a VDI region close to you.

## Tenant config in a VDI

Whichever VDI you pick, install OfficeConnect once on the VDI image and deploy tenant config centrally — your Mac users shouldn't have to configure tenants manually. See [Deploy Tenants via Registry](/wiki/admin/deploy/deploy-tenants-registry/).

## What about Office for the Web?

Excel for the Web does not currently support Workday OfficeConnect — neither the JavaScript Mac add-in nor the Windows COM add-in. A VDI is still the answer.

## Decision shortcut

- **Already on Microsoft cloud?** Pick AVD.
- **Already on AWS?** Pick WorkSpaces.
- **No IT-managed VDI option?** Pick Parallels.
- **None of the above and you don't need the Windows-only features?** Stay on native Mac.

## Result

Mac users get parity with Windows for Workday OfficeConnect features that genuinely need it, without abandoning their preferred laptop.

## Next steps

- [OfficeConnect on Mac](/reference/troubleshoot/officeconnect-on-mac/) — the native Mac path if you don't need VDI.
- [Deploy Tenants via Registry](/wiki/admin/deploy/deploy-tenants-registry/) — push tenant config to the VDI image.
- [Install for Admins](/wiki/install-admin/) — admin-side install patterns that apply inside the VDI.

