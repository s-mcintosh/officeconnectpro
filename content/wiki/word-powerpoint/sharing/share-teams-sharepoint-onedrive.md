---
title: "Share Reports via Teams, SharePoint & OneDrive"
linkTitle: "Share via Teams & SharePoint"
weight: 10
description: >
  Save and share Workday OfficeConnect workbooks through Microsoft Teams, SharePoint, or OneDrive.
tags: ["sharing", "fpna", "system-admin", "how-to"]
aliases:
  - /share-publish/share-teams-sharepoint-onedrive/
  - /wiki/build-reports/share-teams-sharepoint-onedrive/
---

You can save Workday OfficeConnect reports to shared locations in Microsoft Teams, SharePoint, or OneDrive so multiple colleagues can access them.

{{< admin-note >}}
**Limitation:** Workday OfficeConnect does not support multiple users editing the same file simultaneously. There's always a risk of data loss if two people work on the same file at the same time.
{{< /admin-note >}}

## How to share a report

{{< step n="1" title="Finish building and refreshing your report" >}}
Make sure the report is complete and you've clicked **Refresh** to load the latest data. See [Build Your First Report](/wiki/build-reports/build-first-report/) if you're still in the build phase.
{{< /step >}}

{{< step n="2" title="Save to a shared location" >}}
Use Excel's standard **File → Save As** to save the workbook to a Teams channel folder, SharePoint document library, or OneDrive shared folder.
{{< /step >}}

{{< step n="3" title="Share the link" >}}
Use the Teams or SharePoint sharing feature to send a link to colleagues. They can open the workbook and refresh it themselves if they have Workday OfficeConnect installed and appropriate Adaptive Planning permissions.
{{< /step >}}

## What recipients need

For a colleague to open and refresh a shared OfficeConnect report, they need:
- Workday OfficeConnect installed (same version or newer) — see [Install for End Users](/wiki/install-end-user/)
- Access to the same Workday Adaptive Planning tenant
- Appropriate Adaptive Planning permissions for the data in the report

## Concurrent access risks

| Scenario | Risk |
|---|---|
| User A opens and signs in; User B opens read-only | Low risk — User B sees the file but can't save changes |
| Both users sign in and make changes | High risk — the last save wins; earlier changes can be overwritten |

**Best practice:** Treat shared Workday OfficeConnect files like shared Excel files — coordinate with colleagues to avoid simultaneous editing.

## Data clearing on shared files

By default, Workday OfficeConnect clears data on save (replacing it with `n/a`). When someone without OfficeConnect opens a shared file, they'll see placeholder text rather than financial data. This is intentional — it prevents sensitive data from being visible to users who haven't authenticated. See [Secure OfficeConnect Workbooks](/wiki/admin/govern/secure-workbooks/) for the security model.

Recipients with OfficeConnect can click **Refresh** to load their data view.

## Result

The workbook lives in your team's shared location, and authorized users can refresh their own view of the data.

## Next steps

- [OfficeConnect for PowerPoint](/wiki/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) — embed live charts and tables in presentations.
- [OfficeConnect for Word](/wiki/word-powerpoint/word/officeconnect-for-word/) — embed live data into narrative reports.
- [Secure OfficeConnect Workbooks](/wiki/admin/govern/secure-workbooks/) — harden saved files against data leakage.
