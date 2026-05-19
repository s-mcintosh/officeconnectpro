---
title: "Share Reports via Teams, SharePoint & OneDrive"
linkTitle: "Share via Teams & SharePoint"
weight: 1
description: >
  Save and share OfficeConnect workbooks through Microsoft Teams, SharePoint, or OneDrive.
---

You can save OfficeConnect reports to shared locations in Microsoft Teams, SharePoint, or OneDrive so multiple colleagues can access them.

> **Limitation:** OfficeConnect does not support multiple users editing the same file simultaneously. There's always a risk of data loss if two people work on the same file at the same time.

## How to share a report

{{< step n="1" title="Finish building and refreshing your report" >}}
Make sure the report is complete and you've clicked **Refresh** to load the latest data.
{{< /step >}}

{{< step n="2" title="Save to a shared location" >}}
Use Excel's standard **File → Save As** to save the workbook to a Teams channel folder, SharePoint document library, or OneDrive shared folder.
{{< /step >}}

{{< step n="3" title="Share the link" >}}
Use the Teams or SharePoint sharing feature to send a link to colleagues. They can open the workbook and refresh it themselves if they have OfficeConnect installed and appropriate Adaptive Planning permissions.
{{< /step >}}

## What recipients need

For a colleague to open and refresh a shared OfficeConnect report, they need:
- OfficeConnect installed (same version or newer)
- Access to the same Workday Adaptive Planning tenant
- Appropriate Adaptive Planning permissions for the data in the report

## Concurrent access risks

| Scenario | Risk |
|---|---|
| User A opens and signs in; User B opens read-only | Low risk — User B sees the file but can't save changes |
| Both users sign in and make changes | High risk — the last save wins; earlier changes can be overwritten |

**Best practice:** Treat shared OfficeConnect files like shared Excel files — coordinate with colleagues to avoid simultaneous editing.

## Data clearing on shared files

By default, OfficeConnect clears data on save (replacing it with `n/a`). When someone without OfficeConnect opens a shared file, they'll see placeholder text rather than financial data. This is intentional — it prevents sensitive data from being visible to users who haven't authenticated.

Recipients with OfficeConnect can click **Refresh** to load their data view.

## Next steps

→ [OfficeConnect for PowerPoint](/build-reports/officeconnect-for-powerpoint/) — embed live charts and tables in presentations
