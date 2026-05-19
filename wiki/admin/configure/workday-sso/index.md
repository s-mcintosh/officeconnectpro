---
title: "Set Up Workday SSO"
url: "https://officeconnectpro.com/wiki/admin/configure/workday-sso/"
description: "Configure Workday OfficeConnect to use Workday Single Sign-On for your organization.\n"
tags: ["sso","system-admin","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


{{< admin-note >}}
This page requires Workday Security Administrator access. End users don't need to do anything — SSO is configured at the tenant level by admins and power users.
{{< /admin-note >}}

## What Workday SSO does for OfficeConnect

With SSO enabled, users sign in to Workday OfficeConnect using their existing Workday credentials through your identity provider. They don't need a separate Adaptive Planning username and password.

For identity-provider-specific guides, see SSO with Okta, SSO with Microsoft Entra ID, or SSO with Ping Identity (coming soon under [Admin → Configure](/wiki/admin/configure/)).

## Prerequisites

- Workday Security Administrator role

## Steps

{{< step n="1" title="Enable OfficeConnect in Workday" >}}
In Workday, run the **Enable Features After User Sync** task and enable the OfficeConnect feature for your tenant.
{{< /step >}}

{{< step n="2" title="Generate the OfficeConnect API client" >}}
In Workday, create an API client specifically for OfficeConnect. This produces:
- **Client ID**
- **Authorization Endpoint URL**
- **API Endpoint URL**

Record all three — users and IT will need them when configuring tenants. These are the same values referenced in [Sign In & Create a Tenant](/wiki/admin/configure/sign-in-create-tenant/).
{{< /step >}}

{{< step n="3" title="Assign the Access OfficeConnect permission" >}}
In Workday, ensure users who need OfficeConnect access have the **Access OfficeConnect** permission in their security permission set.
{{< /step >}}

{{< step n="4" title="Configure the Connection user setting (optional)" >}}
If your users are automatically signed in by your identity provider, enable the **Show tenant selector at sign-in** option in OfficeConnect user settings. This prompts users to select their tenant when signing in, which is useful when:
- Multiple tenants are configured for SSO
- Your identity provider auto-signs users in
- Users work with both Financials and Adaptive Planning data sources
{{< /step >}}

## Result

Users can sign in to Workday OfficeConnect using their Workday credentials. They'll see the Workday sign-in page when they click **Log In** in the OfficeConnect tab.

## Next steps

- [Deploy Tenants via Registry](/wiki/admin/deploy/deploy-tenants-registry/) to push tenant configuration to user machines automatically.
- [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/) if users hit sign-in problems.
- [Secure OfficeConnect Workbooks](/wiki/admin/govern/secure-workbooks/) to harden saved files.

