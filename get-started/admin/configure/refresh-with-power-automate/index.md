---
title: "Refresh Reports Automatically with Power Automate"
url: "https://officeconnectpro.com/get-started/admin/configure/refresh-with-power-automate/"
description: "Use Power Automate Desktop to schedule Workday OfficeConnect report refreshes automatically — keep distributed Excel reports up to date without manual intervention.\n"
tags: ["integration","adaptive-planning","system-admin","how-to"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Workday OfficeConnect doesn't have a built-in scheduler, but you can automate report refresh using **Power Automate Desktop** — Microsoft's desktop automation tool included with Windows 10/11 and Microsoft 365. This how-to sets up a scheduled desktop flow that opens your report workbook, refreshes OfficeConnect data, saves, and closes — on any schedule you set.

**What you'll need:**
- Windows 10 or 11 with Power Automate Desktop installed ([download from Microsoft](https://powerautomate.microsoft.com/en-us/desktop/))
- Microsoft 365 subscription (Power Automate Desktop is included)
- Your Workday OfficeConnect report workbook saved to a local path or a network/SharePoint location accessible from the machine

{{< admin-note >}}
The machine running the flow must be on and signed in for the scheduled flow to run. This approach works best on a server or shared workstation that stays online. For cloud-only approaches, consider saving the refreshed file to SharePoint so downstream users always see the latest version.
{{< /admin-note >}}

---

## 1. Create the desktop flow

1. Open **Power Automate Desktop** from the Start menu.
2. Click **+ New flow**, give it a name like `Refresh OfficeConnect Monthly Report`, and click **Create**.
3. The flow designer opens. You will build the flow by adding actions from the left panel.

## 2. Add actions to open, refresh, save, and close the workbook

4. In the **Actions** panel, search for **Launch Excel** and drag it into the flow. Set:
   - **Launch Excel**: With a blank document — change to **Open the following document**
   - **Document path**: Enter the full path to your workbook, e.g. `C:\Reports\Monthly-PL.xlsx`
   - Leave **Make instance visible** checked so you can see the automation in progress during testing

5. Add a **Wait** action after the Launch step. Set it to wait **10 seconds** — this gives Excel time to fully load and activate the OfficeConnect add-in before the next action runs.

6. Add a **Send keys** action. Set **Send keys to**: the Excel window (select it from the dropdown). In the **Text to send** field, enter the keyboard shortcut to trigger OfficeConnect Refresh. OfficeConnect does not have a default keyboard shortcut, so you have two options:

   **Option A — Use a macro:** Record a macro in Excel that calls `Application.Run "OfficeConnect.Refresh"` and assign it a keyboard shortcut (e.g., `Ctrl+Shift+R`). Then use **Send keys** to send `^+R` (Ctrl+Shift+R).

   **Option B — Use Office Scripts (Microsoft 365 E3/E5):** Write an Office Script that calls the OfficeConnect COM object. This is more reliable but requires an Office Scripts-enabled license.

   For most setups, Option A is simpler. Create the macro once in the workbook and save the workbook with macros (`.xlsm` format).

7. Add another **Wait** action — wait **30 seconds** to allow the refresh to complete. Adjust this value based on your model size; large models may need 60–90 seconds.

8. Add a **Send keys** action to save: send `^s` (Ctrl+S). Add another **Wait** of 5 seconds.

9. Add a **Close Excel** action. Set **Before closing Excel**: **Save document**.

## 3. Test the flow manually

10. Click **Run** in the Power Automate Desktop toolbar. Watch the automation open Excel, wait, trigger refresh, save, and close. Verify the workbook's data is updated after the flow completes.

## 4. Schedule the flow

11. In the Power Automate Desktop home screen, the flow you created appears in your list. To schedule it, go to the **Power Automate web portal** (flow.microsoft.com) and create a **Scheduled cloud flow** that triggers on your desired schedule (daily, weekly, monthly).

12. In the cloud flow, add an action: **Power Automate Desktop → Run a flow built with Power Automate Desktop**. Select your desktop flow. This cloud flow triggers the desktop flow on schedule.

{{< admin-note >}}
The desktop machine must be running and signed in for the cloud-triggered desktop flow to execute. Configure the machine to auto-login on startup if it needs to run unattended overnight.
{{< /admin-note >}}

## Result

Your Workday OfficeConnect report refreshes on schedule, even when no one is at the keyboard. Downstream users pulling from the SharePoint copy always see the latest period.

## Next steps

- [Build a Formatted Executive Report for Distribution](/get-started/build-reports/formatted-executive-report/)
- [Share via Teams & SharePoint](/get-started/word-powerpoint/sharing/share-teams-sharepoint-onedrive/)
- [Lock and Protect Reports](/get-started/build-reports/lock-protect-reports/)

