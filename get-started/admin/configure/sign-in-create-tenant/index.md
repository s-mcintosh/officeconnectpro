---
title: "Sign In \u0026 Create Your First Tenant"
url: "https://officeconnectpro.com/get-started/admin/configure/sign-in-create-tenant/"
description: "Sign in to Workday OfficeConnect for the first time and configure your Workday tenant connection.\n"
tags: ["sso","deployment","system-admin","tutorial"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


A **tenant** in Workday OfficeConnect is a saved connection to a Workday instance. You create it once, and OfficeConnect remembers it for future sessions.

## What you'll need

Before you start, gather these details from your Workday administrator:

| Detail | Where to find it |
|---|---|
| **Client ID** | Workday OfficeConnect API client |
| **API Endpoint URL** | Workday OfficeConnect API client |
| **Authorization Endpoint URL** | Workday OfficeConnect API client |

If your admin hasn't yet generated these, see [Set Up Workday SSO](/get-started/admin/configure/workday-sso/).

## Steps

{{< step n="1" title="Open Excel and click the OfficeConnect tab" >}}
After installation, the OfficeConnect tab appears in the Excel ribbon. If you don't see it, see [Install for End Users](/get-started/install-end-user/).
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
The Workday Adaptive Planning sign-in page opens in a browser panel.
{{< /step >}}

{{< step n="3" title="Click 'Log in with Workday'" >}}
This takes you to the tenant configuration screen.
{{< /step >}}

{{< step n="4" title="Enter your tenant details" >}}
Fill in the tenant form:

| Field | Example | Notes |
|---|---|---|
| **Name** | Production | A friendly name you'll see in the sign-in drop-down |
| **Data Source** | Adaptive Planning | Choose **Financials** only if you're connecting to Workday Financial Management |
| **Client ID** | `abc0MjQw...` | From your Workday API client |
| **API Endpoint URL** | `https://example.myworkday.com/ccx/api/v1/tenant` | From your Workday API client |
| **Authorization Endpoint URL** | `https://example.myworkday.com/tenant/authorize` | From your Workday API client |

Click **Save**.
{{< /step >}}

{{< figure src="/images/screenshots/oc-tenant-form.png" alt="The OfficeConnect tenant configuration form" caption="Enter your Client ID and endpoint URLs from the Workday API client configuration." >}}

{{< step n="5" title="Sign in with your Workday credentials" >}}
After saving the tenant, the Workday sign-in page appears. Enter your Workday username and password.
{{< /step >}}

## Result

Workday OfficeConnect connects to your tenant. The Reporting pane appears in Excel with your instance's accounts, time periods, and levels available.

{{< figure src="/images/screenshots/oc-reporting-pane-connected.png" alt="The Reporting pane after successfully connecting to a tenant" caption="After sign-in, the Reporting pane populates with your Adaptive Planning accounts, time periods, and levels." >}}

The tenant name appears in the sign-in drop-down for future sessions — you won't need to re-enter these details.

## Add additional tenants (optional)

From the Log In drop-down, select **Manage Tenants** to add, edit, or remove tenants. Your organization can mix Adaptive Planning and Financials tenants.

## Next steps

- [Work with Multiple Instances](/get-started/admin/configure/multiple-instances/) if your organization has sandbox or multi-instance setups.
- [Build Your First Report](/get-started/build-reports/build-first-report/) now that you're signed in.
- Push tenant config to many machines via [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/).

