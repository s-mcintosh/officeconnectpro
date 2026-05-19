---
title: "Single Sign-On for Workday OfficeConnect with Okta"
linkTitle: "SSO with Okta"
weight: 40
description: >
  Configure Okta to authenticate Workday OfficeConnect users via Workday SSO — application setup, claim mapping, MFA pairing, and the common failure modes.
tags: ["sso", "security", "system-admin", "how-to"]
---

{{< admin-note >}}
Requires Okta administrator access and Workday Security Administrator access. End users don't change anything on their side; this is a tenant-level configuration.
{{< /admin-note >}}

Workday OfficeConnect doesn't authenticate to Okta directly. Instead, OfficeConnect authenticates to Workday, and Workday uses Okta as its identity provider. This indirection is important — the configuration lives on the Workday side, not directly in OfficeConnect — and explains why many SSO problems surface as Workday auth failures rather than Okta errors.

This guide assumes you already have Okta-to-Workday SSO working for the regular Workday web app. If not, set that up first (in Okta's catalog: "Workday" with SAML 2.0 or OpenID Connect).

For the generic SSO concepts, see [Set Up Workday SSO](/admin/configure/workday-sso/).

## Step 1 — Verify the Workday OfficeConnect API client is in place

{{< step n="1" title="Confirm OfficeConnect is enabled on the tenant" >}}
In Workday: run **Enable Features After User Sync** and confirm OfficeConnect is enabled.
{{< /step >}}

{{< step n="2" title="Confirm the OfficeConnect API client exists" >}}
The API client provides the **Client ID** and two endpoint URLs OfficeConnect needs. If not yet created, see [Set Up Workday SSO](/admin/configure/workday-sso/) Step 2.
{{< /step >}}

## Step 2 — Configure the Okta application for Workday (if not already done)

{{< step n="3" title="Add the Workday application from Okta's catalog" >}}
In the Okta admin console: **Applications → Browse App Catalog → "Workday"**. Use the SAML 2.0 integration unless your Workday tenant is specifically OIDC-configured.
{{< /step >}}

{{< step n="4" title="Provide the Workday Tenant URL" >}}
Enter your Workday subdomain (e.g., `example.myworkday.com`) and tenant name.
{{< /step >}}

{{< step n="5" title="Map the username attribute" >}}
The default — Okta username — works for most organizations. Confirm with your Workday admin that the username in Workday matches the Okta value being asserted.
{{< /step >}}

{{< step n="6" title="Download the SAML metadata or certificate" >}}
You'll need either the metadata XML or the signing certificate to upload to Workday.
{{< /step >}}

## Step 3 — Configure Workday's SSO settings

{{< step n="7" title="Run the Edit Tenant Setup - Security task in Workday" >}}
Workday Security Administrator role required. Navigate to **Edit Tenant Setup - Security** and find the SSO configuration section.
{{< /step >}}

{{< step n="8" title="Upload the Okta SAML metadata or certificate" >}}
Paste or upload the metadata XML / certificate you downloaded from Okta in Step 6. Configure the SSO endpoint to match Okta's URL.
{{< /step >}}

{{< step n="9" title="Test with the Workday web app first" >}}
Sign in to the Workday web app as a test user — the Okta sign-in page should appear, then Workday loads. If this doesn't work, OfficeConnect won't either; fix the web-side SSO before continuing.
{{< /step >}}

## Step 4 — Assign Okta users to the Workday app

{{< step n="10" title="In Okta, assign users or a group" >}}
**Applications → Workday → Assignments**. Assign the users who need OfficeConnect access.
{{< /step >}}

{{< step n="11" title="Grant the Access OfficeConnect permission in Workday" >}}
The same users need the **Access OfficeConnect** permission in their Workday security permission set. SSO without this permission produces a confusing "signed in successfully but cannot access OfficeConnect" failure.
{{< /step >}}

## Step 5 — Test from Excel

{{< step n="12" title="Open Excel and click OfficeConnect → Log In" >}}
Click **Log in with Workday**. A browser panel opens and routes through Okta's sign-in page. After Okta authenticates the user, the panel returns to OfficeConnect with the tenant connected.
{{< /step >}}

{{< step n="13" title="Verify the Reporting pane populates" >}}
If the Reporting pane populates with accounts/levels/time, SSO is end-to-end working.
{{< /step >}}

## Common failure modes

| Symptom | Likely cause | Fix |
|---|---|---|
| Okta sign-in succeeds, but OfficeConnect reports "Cannot connect" | User lacks **Access OfficeConnect** permission | Add the permission to the user's permission set in Workday |
| Sign-in loop — page bounces back to login | Okta session not persisting due to third-party cookie blocking | Confirm browser allows cookies for `myworkday.com` and the Okta domain |
| MFA prompt appears but never returns | MFA factor (push notification) requires a separately approved device | Verify the user has Okta Verify or the assigned factor enrolled |
| "Tenant switcher" required but absent | Multi-tenant SSO scenarios — see Tenant Switcher Missing (coming soon) | Configure **Show tenant selector at sign-in** in OfficeConnect User Settings |
| Worked yesterday, broken today | Okta certificate rotation that wasn't communicated to Workday | Re-upload the current Okta SAML metadata in Workday |

## Result

Workday OfficeConnect users sign in with their Okta credentials, MFA flows work, and no separate Adaptive Planning password is required.

## Next steps

- [Set Up Workday SSO](/admin/configure/workday-sso/) — the generic concepts.
- [SSO with Microsoft Entra ID](/admin/configure/sso-entra/) — the Entra equivalent.
- [Authentication Token Errors](/troubleshoot/authentication-token-errors/) — when sign-in succeeds but tokens fail.
