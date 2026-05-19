---
title: "Fix OfficeConnect Not Refreshing"
linkTitle: "Not Refreshing"
weight: 20
description: >
  OfficeConnect shows stale data or the Refresh button does nothing — causes and step-by-step fixes.
tags: ["adaptive-planning", "performance", "fp-and-a", "admin-power-user", "troubleshoot"]
---

If Workday OfficeConnect won't pull fresh data, the cause is almost always a session, formula, or connection problem rather than a corrupted workbook. Confirm your tenant connection on [Sign In & Create a Tenant](/admin/configure/sign-in-create-tenant/) before working through the fixes below.

## Symptom

You click **Refresh** in the OfficeConnect ribbon and one of the following happens:
- Nothing happens — the button appears to do nothing
- The progress indicator appears briefly then disappears with no data change
- Some cells update but others remain stale
- Excel shows a spinning cursor for a long time, then refresh completes with no data change

---

## Causes

1. OfficeConnect is not connected to the Adaptive Planning or Financials data source (session expired or not signed in)
2. The workbook has no active OfficeConnect formulas (formulas were deleted or overwritten)
3. A network or firewall issue is blocking the connection to Workday servers
4. The OfficeConnect add-in has entered an error state and needs to be reloaded
5. Excel's automatic calculation is disabled

---

## Fix 1: Check your sign-in status

1. Click the **OfficeConnect** tab in the ribbon.
2. If you see a **Sign In** button (instead of **Refresh**, **Submit**, and other tools), you are not signed in. Click **Sign In** and complete authentication through the Workday SSO browser window.
3. Once signed in, click **Refresh**. If the issue was an expired session, data should now load.

## Fix 2: Verify OfficeConnect formulas are intact

4. Click any cell that should contain OfficeConnect data. Look at the formula bar — it should show an OfficeConnect formula (typically a long string starting with `=OC.` or similar). If the cell contains a plain number or is blank, the formula has been overwritten.
5. If formulas are missing, you'll need to rebuild the report or restore from a backup. OfficeConnect does not cache formulas separately from Excel — if they're overwritten, they're gone.

## Fix 3: Test network connectivity

6. Open a browser and navigate to your Workday tenant URL. If Workday loads in the browser, basic connectivity is fine. If it doesn't load, contact your IT team — the issue is network-level.
7. If you're on a VPN, try disconnecting briefly (if policy allows) and refreshing. Some VPN configurations block or slow traffic to Workday's cloud servers.
8. If you're on a corporate network with a proxy, confirm with IT that the OfficeConnect add-in is allowed to make outbound HTTPS connections to Workday's domains.

## Fix 4: Reload the OfficeConnect add-in

9. Close the OfficeConnect task pane: click the **X** on the Reporting pane panel.
10. In the Excel ribbon, click the **OfficeConnect** tab → **Show Pane** (or equivalent button to re-open the pane). This reloads the add-in's JavaScript runtime.
11. Sign in again if prompted, then click **Refresh**.

If reloading the pane doesn't help, close Excel entirely, reopen it, and open the workbook again. Full Excel restart clears add-in state more completely than closing the pane.

## Fix 5: Check Excel calculation mode

12. Go to **Formulas** tab in the Excel ribbon → **Calculation Options**. Confirm it is set to **Automatic** (not Manual). If set to Manual, OfficeConnect formulas won't recalculate even after refresh.
13. Press **Ctrl+Alt+F9** to force a full recalculation. If this populates the cells, switch Calculation Options back to Automatic.

---

## If none of these work

- Check your OfficeConnect version: click **OfficeConnect → Help → About**. If you're on a version older than 6 months, ask your IT admin to update to the latest version — older versions may lose compatibility with Workday API changes.
- Contact Workday support with your tenant URL, OfficeConnect version, and a description of the steps you've already tried.
- Check the [Workday Community](https://community.workday.com) for known issues with your OfficeConnect version.

## Next steps

- [Fix authentication and token errors](/troubleshoot/authentication-token-errors/) if Sign In keeps failing
- [Optimize OfficeConnect performance](/performance/optimize-performance/) if refresh completes but takes too long
- [Run the troubleshooting tool](/troubleshoot/troubleshooting-tool/) to collect logs before contacting Workday Support
