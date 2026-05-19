---
title: "Single Sign-On for Workday OfficeConnect with Microsoft Entra ID"
url: "https://officeconnectpro.com/wiki/admin/configure/sso-entra/"
description: "Configure Microsoft Entra ID (formerly Azure AD) to authenticate Workday OfficeConnect users via Workday SSO — enterprise application setup, claim mapping, and Conditional Access tuning.\n"
tags: ["sso","security","system-admin","how-to"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


{{< admin-note >}}
Requires Entra ID Application Administrator (or higher) and Workday Security Administrator access. End users don't change anything; this is a tenant-level configuration.
{{< /admin-note >}}

Workday OfficeConnect doesn't authenticate to Microsoft Entra ID directly. OfficeConnect authenticates to Workday, and Workday uses Entra ID as its identity provider. The configuration sits on the Workday side, with Entra ID providing the SAML or OIDC backbone.

This guide assumes Entra ID-to-Workday SSO is already working for the Workday web app. If not, do that integration first (Entra's enterprise app gallery has a "Workday" SAML template).

For generic SSO concepts, see [Set Up Workday SSO](/wiki/admin/configure/workday-sso/).

## Step 1 — Verify OfficeConnect is enabled and the API client exists

{{< step n="1" title="Confirm OfficeConnect is enabled on the Workday tenant" >}}
Run **Enable Features After User Sync** in Workday and confirm OfficeConnect is enabled.
{{< /step >}}

{{< step n="2" title="Confirm the OfficeConnect API client is in place" >}}
The API client provides Client ID + two endpoint URLs. See [Set Up Workday SSO](/wiki/admin/configure/workday-sso/) Step 2 if not yet created.
{{< /step >}}

## Step 2 — Configure (or verify) Workday in the Entra ID enterprise app gallery

{{< step n="3" title="In the Entra admin center, find or add the Workday app" >}}
**Identity → Applications → Enterprise applications → New application → Workday**. If Workday already appears, open it instead of re-adding.
{{< /step >}}

{{< step n="4" title="Configure SAML single sign-on" >}}
Choose **SAML** as the SSO method. Fill in:

- **Identifier (Entity ID):** your Workday tenant URL (e.g., `https://impl.workday.com/example`)
- **Reply URL:** Workday's ACS URL — the exact value comes from your Workday SSO configuration page
- **Sign on URL:** the Workday tenant URL users should land at after SSO
- **Relay State:** leave default unless your Workday admin says otherwise
{{< /step >}}

{{< step n="5" title="Map the user identifier" >}}
The default user identifier (`user.userprincipalname`) is correct for most setups where Workday usernames match Entra UPNs. If your organization uses email or a custom attribute, adjust here.
{{< /step >}}

{{< step n="6" title="Download the SAML signing certificate (Base64 .cer)" >}}
Download the certificate file. You'll upload it to Workday in the next step.
{{< /step >}}

## Step 3 — Configure Workday's SSO settings

{{< step n="7" title="Run Edit Tenant Setup - Security in Workday" >}}
Workday Security Administrator role required. Find the SSO configuration section.
{{< /step >}}

{{< step n="8" title="Upload the Entra SAML certificate" >}}
Paste or upload the certificate downloaded in Step 6. Configure the Entra **Login URL** (provided in the Entra SAML config page, ends with `/saml2`).
{{< /step >}}

{{< step n="9" title="Test with the Workday web app first" >}}
Sign in to the Workday web app as a test user. The Entra sign-in page should appear, then Workday loads. If this doesn't work, OfficeConnect won't either — fix the web flow before continuing.
{{< /step >}}

## Step 4 — Assign users in Entra

{{< step n="10" title="Entra → Workday enterprise app → Users and groups" >}}
Assign the users (or, better, a group) who need OfficeConnect access.
{{< /step >}}

{{< step n="11" title="Grant the Access OfficeConnect permission in Workday" >}}
The same users need the **Access OfficeConnect** permission in their Workday security permission set. Without it, SSO succeeds but OfficeConnect-side access fails.
{{< /step >}}

## Step 5 — Conditional Access considerations

Most organizations apply Entra Conditional Access policies that require MFA or compliant devices for SaaS apps.

{{< step n="12" title="Review Conditional Access policies for the Workday app" >}}
**Entra → Protection → Conditional Access**. Find policies that target the Workday application. The OfficeConnect sign-in flow runs through the same Workday app, so the policy applies.
{{< /step >}}

{{< step n="13" title="Be deliberate about device compliance" >}}
If a Conditional Access policy requires a compliant or Entra-joined device, Mac users running OfficeConnect from Excel for Mac may be blocked. Consider either: an exception for the OfficeConnect path, a VDI-only access pattern (see [Mac VDI Workflow](/reference/troubleshoot/mac-vdi-workflow/)), or a compliance baseline that includes Macs.
{{< /step >}}

## Step 6 — Test from Excel

{{< step n="14" title="Open Excel and click OfficeConnect → Log In" >}}
Click **Log in with Workday**. The browser panel opens, routes through Entra, possibly hits MFA, then returns to OfficeConnect.
{{< /step >}}

{{< step n="15" title="Verify the Reporting pane populates" >}}
Success: accounts, levels, time appear. Failure: see the failure modes below.
{{< /step >}}

## Common failure modes

| Symptom | Likely cause | Fix |
|---|---|---|
| Entra sign-in succeeds, then OfficeConnect shows "Cannot connect" | Missing **Access OfficeConnect** permission in Workday | Add the permission to the user's permission set |
| Sign-in loop bounces back to Entra | Browser blocking third-party cookies | Allow cookies for `myworkday.com` and `login.microsoftonline.com` |
| MFA prompt never returns | Authenticator app push timing out, or device not registered | Verify Microsoft Authenticator on the user's phone is registered for Entra MFA |
| Conditional Access blocks OfficeConnect | Device compliance or location policy excludes the path | Adjust the policy or create an exception for OfficeConnect's sign-in URL |
| "Worked yesterday, broken today" | Entra certificate rotation that wasn't synced to Workday | Re-upload the current Entra certificate in Workday |
| Some users get in, others don't | Group assignment in Entra missing the affected users | Verify Users and groups in the Workday enterprise app |

## Result

Workday OfficeConnect users sign in with their Entra credentials, MFA and Conditional Access policies flow correctly, and no Adaptive Planning password is required.

## Next steps

- [Set Up Workday SSO](/wiki/admin/configure/workday-sso/) — generic SSO concepts.
- [SSO with Okta](/wiki/admin/configure/sso-okta/) — the Okta equivalent.
- [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/) — when sign-in succeeds but tokens later fail.

