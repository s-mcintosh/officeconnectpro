---
title: "Set Up Your Reporting Model"
url: "https://officeconnectpro.com/wiki/set-up-reporting-model/"
description: "Use the Run Set Up Reporting Model task in Workday to configure how OfficeConnect Financials reports are structured.\n"
tags: ["financials","accounting","system-admin","how-to"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


{{< admin-note >}}
This page is for Workday System Administrators. End users don't need to complete this — it's a one-time configuration step that controls what data OfficeConnect Financials reports can access.
{{< /admin-note >}}

## What this task does

The **Run Set Up Reporting Model** task replaced the earlier **Set Up Financial Reporting and Analytics Data Model** task. It allows System Administrators to edit existing reporting data models — controlling the OfficeConnect-specific fields that determine how Financials data is structured and surfaced in Excel.

Fields you can configure include:

- **Time periods** — which periods are available in OfficeConnect Financials reports
- **Account structures** — how accounts and hierarchies are organized
- **Data sources** — which Workday Financial Management data sources the model draws from

## Prerequisites

- Workday System Administrator role
- An existing Financials reporting data model configured in your Workday tenant

{{< admin-note >}}
Depending on your tenant's security configuration, Workday Security Administrator access may also be required. If you receive an access error when running the task, contact your Workday Security Administrator.
{{< /admin-note >}}

## Steps

{{< step n="1" title="Search for the task in Workday" >}}
In the Workday search bar, type **Run Set Up Reporting Model** and select the task from the results.
{{< /step >}}

{{< step n="2" title="Open the task" >}}
Click the task to open it. Workday will load the reporting model configuration screen.
{{< /step >}}

{{< step n="3" title="Select an existing reporting model" >}}
From the list of available reporting models, select the one used by OfficeConnect. If your organization has multiple models (e.g., separate models for different companies or regions), select each one you want to update.
{{< /step >}}

{{< step n="4" title="Edit the reporting model fields" >}}
Update the fields as needed — time periods, account structures, and data sources. Save your changes when done.
{{< /step >}}

## Result

OfficeConnect Financials reports will reflect the updated model configuration the next time users refresh their workbooks. No reinstallation or tenant reconfiguration is required.

## Next steps

→ [Sign In & Create Your First Tenant](/wiki/admin/configure/sign-in-create-tenant/) to connect OfficeConnect to your Workday Financials instance
→ [Financials vs Adaptive Planning](/wiki/migration-comparison/financials-vs-adaptive-planning/) for an overview of how the two data sources differ in OfficeConnect

