---
title: "Sign In & Create Your First Tenant"
linkTitle: "Sign In & Create Tenant"
weight: 1
description: >
  Sign in to OfficeConnect for the first time and configure your Workday tenant connection.
---

A **tenant** in OfficeConnect is a saved connection to a Workday instance. You create it once, and OfficeConnect remembers it for future sessions.

## What you'll need

Before you start, gather these details from your Workday administrator:

| Detail | Where to find it |
|---|---|
| **Client ID** | Workday OfficeConnect API client |
| **API Endpoint URL** | Workday OfficeConnect API client |
| **Authorization Endpoint URL** | Workday OfficeConnect API client |

## Steps

{{< step n="1" title="Open Excel and click the OfficeConnect tab" >}}
After installation, the OfficeConnect tab appears in the Excel ribbon.
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

{{< step n="5" title="Sign in with your Workday credentials" >}}
After saving the tenant, the Workday sign-in page appears. Enter your Workday username and password.
{{< /step >}}

## Result

OfficeConnect connects to your tenant. The Reporting pane appears in Excel with your instance's accounts, time periods, and levels available.

The tenant name appears in the sign-in drop-down for future sessions — you won't need to re-enter these details.

## Add additional tenants (optional)

From the Log In drop-down, select **Manage Tenants** to add, edit, or remove tenants. Your organization can mix Adaptive Planning and Financials tenants.

## Next steps

→ [Work with Multiple Instances](/connect/multiple-instances/) if your organization has sandbox or multi-instance setups
