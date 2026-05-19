# Use OfficeConnect on Mac

Install and use Workday OfficeConnect on a Mac with Excel for Mac — what works, what's different from Windows, and how to handle common Mac-specific issues.


---


Workday OfficeConnect runs on Excel for Mac (Microsoft 365 subscription required). The core reporting experience — building reports, refreshing data, and navigating the Reporting pane — works the same as Windows. A few things are different, and a handful of Windows-only features are unavailable. This guide covers what you need to know.

**What you'll need:**
- A Mac running macOS 12 (Monterey) or later
- Microsoft 365 with Excel for Mac (version 16.54 or later)
- Workday OfficeConnect deployed by your IT admin, or access to install it from the Microsoft AppSource

---

## 1. Install OfficeConnect on Mac

1. Open **Excel for Mac** and sign in with your Microsoft 365 account.
2. Click the **Insert** tab in the menu bar, then click **Add-ins** (or **Get Add-ins** depending on your Excel version).
3. In the Office Add-ins dialog, search for **OfficeConnect** in the Store tab. If your IT admin deployed it centrally, look in the **Admin Managed** tab instead.
4. Click **Add**. After a moment, an **OfficeConnect** tab appears in the Excel ribbon.

> **Note:** If your organization deploys Workday OfficeConnect via a custom manifest URL, ask your IT admin for the manifest URL and install it via **Insert → Add-ins → Upload My Add-in** (or the equivalent in your version of Excel for Mac).

## 2. Sign in

5. Click the **OfficeConnect** tab in the ribbon, then click **Sign In**.
6. A browser window opens for Workday SSO authentication. Sign in with your Workday credentials. After successful authentication, the browser closes and the Reporting pane opens in Excel.
7. If the browser doesn't open automatically, look for a pop-up notification in Excel and click **Allow**.

See [Sign In & Create a Tenant](/get-started/admin/configure/sign-in-create-tenant/) for the full tenant setup walkthrough.

## 3. Build and refresh reports

Building reports on Mac works identically to Windows — drag elements from the Reporting pane, build your header structure, and click Refresh. All core features work:

- Account, version, time, level, and custom dimension elements
- Tutorials in the FP&A and Financials sections of this site apply as written
- Keyboard shortcuts for cell navigation (Tab, Enter, arrow keys) work as expected

See [Build Your First Report](/get-started/build-reports/build-first-report/) for the standard tutorial.

## 4. Mac-specific differences

| Feature | Windows | Mac |
|---|---|---|
| Keyboard shortcut for Refresh | Configurable | Not supported — use the ribbon button |
| Data entry / writeback | Supported | Supported |
| Workbook Protection | Fully supported | Fully supported |
| Cell Explorer | Supported | Supported |
| Power Automate Desktop automation | Supported | Not supported (Power Automate Desktop is Windows-only) |

## 5. Common Mac-specific issues

**The OfficeConnect tab doesn't appear after install:**
Close and reopen Excel completely. If the tab is still missing, go to **Insert → Add-ins** and verify OfficeConnect is listed as active. If it shows as inactive, click it to re-enable. See also [Task Pane Not Displaying](/reference/troubleshoot/task-pane-not-displaying/).

**Sign-in browser window is blocked:**
macOS sometimes blocks the authentication pop-up. Check the Safari pop-up blocker settings or try signing in from a different browser by copying the authentication URL. If your organization uses Workday SSO through an identity provider, confirm the SSO flow supports browser-based authentication from Mac. See [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/).

**Refresh is slower than on Windows:**
Excel for Mac add-ins run in a sandboxed JavaScript environment, which adds some overhead compared to the COM-based add-in on Windows. Performance is generally acceptable for standard reports; very large workbooks (200+ OfficeConnect formulas) may feel noticeably slower. See [Optimize Performance for Large Models](/get-started/performance/optimize-performance/) for techniques to reduce formula count.

**Formulas show `#VALUE!` after opening a workbook built on Windows:**
This usually means the workbook was saved in a format that includes Windows-specific metadata. Close and reopen the file, then click Refresh to let OfficeConnect re-resolve the formulas.

## Result

You can build, refresh, and submit Workday OfficeConnect reports from Excel for Mac for most workflows. For Windows-only features (Power Automate Desktop, configurable refresh shortcut), you'll need a Windows machine — see the upcoming guides on Parallels and Azure Virtual Desktop setups.

## Next steps

- [Optimize Performance for Large Models](/get-started/performance/optimize-performance/) — if refresh feels slow on Mac.
- [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/) — if sign-in misbehaves.
- [Get Started with OfficeConnect](/get-started/) — the broader onboarding flow.
