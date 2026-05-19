---
title: "Fix Authentication and Token Errors in OfficeConnect"
url: "https://officeconnectpro.com/reference/troubleshoot/authentication-token-errors/"
description: "OfficeConnect shows authentication errors, token expired messages, or fails to sign in — causes and step-by-step fixes for SSO and token issues.\n"
tags: ["sso","security","system-admin","fpna","troubleshoot"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


Token and sign-in errors usually mean the SSO session has lapsed or the tenant configuration has drifted. Confirm Workday OfficeConnect is pointed at a valid tenant on [Sign In & Create a Tenant](/wiki/admin/configure/sign-in-create-tenant/), and review your [Workday SSO configuration](/wiki/admin/configure/workday-sso/) if multiple users hit the same error.

## Symptom

One or more of the following:
- OfficeConnect shows an error message containing words like "Authentication failed", "Token expired", "Unauthorized", or "401"
- The sign-in browser window opens but returns an error after you authenticate
- OfficeConnect repeatedly asks you to sign in even after a successful authentication
- Refresh fails immediately with an authentication-related error rather than a network error

---

## Causes

1. The Workday SSO session has expired and the access token needs to be refreshed
2. The OfficeConnect client ID or tenant configuration is incorrect or has changed
3. A browser cookie or cached token is corrupted, preventing new authentication from completing
4. The Workday tenant's OAuth application for OfficeConnect has been disabled or its credentials rotated
5. Multi-factor authentication (MFA) requirements have changed and OfficeConnect's browser flow isn't handling the new MFA step

---

## Fix 1: Sign out and sign back in

The fastest fix for most token errors is a clean sign-out and re-authentication.

1. Click the **OfficeConnect** tab in the ribbon.
2. Click **Sign Out** (you may need to look in the **Help** or account menu if Sign Out isn't immediately visible).
3. Close the OfficeConnect pane.
4. Reopen the pane and click **Sign In**.
5. Complete the full SSO flow in the browser window — enter your Workday credentials and complete any MFA step. Don't close the browser window early.
6. After authentication completes, the browser window should close automatically and the Reporting pane should activate.

## Fix 2: Clear browser authentication cache

If signing out and back in doesn't resolve the issue, the cached authentication token may be corrupted.

7. Close Excel completely.
8. Depending on your operating system:
   - **Windows:** Open **Edge** (the browser OfficeConnect uses for authentication internally). Go to Settings → Privacy → Clear browsing data. Select **Cookies and other site data** and **Cached images and files**. Clear data scoped to Workday's domain.
   - **Mac:** Open **Safari**. Go to **Safari → Clear History** and select the Workday domain's cookies.
9. Reopen Excel, open your workbook, and sign in to OfficeConnect again.

## Fix 3: Verify the tenant URL in OfficeConnect settings

10. In the OfficeConnect ribbon, click **Settings** (or **Options**).
11. Confirm the **Tenant URL** matches your Workday tenant. It should be in the format `https://wd3.myworkday.com/yourcompany` or similar. An incorrect URL causes authentication to fail silently — the SSO flow completes against the wrong tenant.

{{< admin-note >}}
If the tenant URL was recently changed by your Workday admin (for example, after a tenant rename or migration), update it in OfficeConnect Settings and redistribute the updated setting to all users. The tenant URL is sometimes configured centrally via registry keys for enterprise deployments — see your IT admin.
{{< /admin-note >}}

## Fix 4: Check the OAuth application in Workday

12. In Workday, search for **Register API Client** or **Manage API Clients** (requires Integration or Security Admin role).
13. Find the API client registered for OfficeConnect. Confirm:
    - The client is active (not expired or disabled)
    - The client secret has not been rotated without updating OfficeConnect's configuration
    - The redirect URI matches what OfficeConnect expects (typically a localhost redirect URI)
14. If the client secret was rotated, work with your OfficeConnect admin to update the client credentials in the OfficeConnect server configuration or manifest.

## Fix 5: Verify MFA compatibility

15. If your organization recently enabled or changed MFA requirements (for example, switching from TOTP to push notifications), the browser-based SSO flow in OfficeConnect may need to be re-tested.
16. Sign in manually through the OfficeConnect browser window and complete the MFA challenge. If the MFA step works but OfficeConnect still shows an error after browser window closes, the issue may be with the redirect handling — contact your OfficeConnect admin.

---

## If none of these work

- Collect the exact error message text (including any error codes) and your OfficeConnect version number (**Help → About**).
- Ask your Workday Security Admin to check the Workday audit log for failed authentication attempts from OfficeConnect — this often reveals the root cause (wrong tenant, expired client, MFA failure, etc.).
- Contact Workday Support with the error code, tenant URL, and OfficeConnect version.

## Next steps

- [Fix OfficeConnect not refreshing](/reference/troubleshoot/not-refreshing/) once sign-in succeeds but data still won't load
- [Configure Workday SSO](/wiki/admin/configure/workday-sso/) to keep token issues from recurring
- [Run the troubleshooting tool](/reference/troubleshoot/troubleshooting-tool/) if you need to share diagnostic logs with Workday Support

