---
title: "Check & Update Your Version. "
linkTitle: "Check Your Version"
weight: 6
description: >
  How to check which version of OfficeConnect you have and update to the latest release.
tags: ["upgrade", "system-admin", "how-to"]
---

Keeping OfficeConnect up to date is important — users on different versions may not be able to share workbooks. Check your version regularly and update with your team.

## Check your current version

{{< step n="1" title="Open Excel and click the OfficeConnect tab" >}}
The OfficeConnect tab appears in the Excel ribbon after installation.
{{< /step >}}

{{< step n="2" title="Open the Help menu" >}}
In the OfficeConnect tab, click the **Help** drop-down.
{{< /step >}}

{{< step n="3" title="Click About" >}}
The About dialog shows your current version number (e.g., `2026.104.3019.3004`).
{{< /step >}}

## Understand the version number

OfficeConnect version numbers follow the pattern `YYYY.release.weekday.build`, where `weekday` encodes the week and day of the build.

Example: `2026.104.3019.3004` = 2026 release, release 104, week 30 day 19 of the build calendar.

## Update OfficeConnect

OfficeConnect checks for updates automatically when you sign in. If a newer version is available, you are prompted to install it.

To update manually:
1. Download the latest installer from **Product Downloads** in your Workday Adaptive Planning instance
2. Run the installer — it upgrades your existing installation in place

{{< admin-note >}}
Coordinate updates across your team. A workbook saved with a newer version of OfficeConnect cannot be opened by users on older versions. Plan a coordinated update window so everyone upgrades together.
{{< /admin-note >}}

## Next steps

→ [Sign in and create your first tenant](/get-started/admin/configure/sign-in-create-tenant/)
