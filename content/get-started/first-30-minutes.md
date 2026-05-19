---
title: "Your First 30 Minutes with Workday OfficeConnect"
linkTitle: "First 30 Minutes"
weight: 2
description: >
  Install, sign in, build your first report, and refresh it — a complete onboarding path from zero to a live Workday OfficeConnect report in half an hour.
tags: ["adaptive-planning", "fpna", "tutorial"]
---

This is the fastest path from "Workday OfficeConnect isn't installed yet" to "I have a refreshable Excel report showing live Adaptive Planning data." It threads together the canonical guides for each step so you don't have to figure out the right order.

**What you'll have at the end:** A working OfficeConnect installation, a tenant connection, and an Excel workbook with at least one live account/period/version intersection pulling from your Workday tenant.

**What you'll need:**
- A Windows PC running Excel (Microsoft 365 or Excel 2021 standalone) — Mac works too, see [OfficeConnect on Mac](/reference/troubleshoot/officeconnect-on-mac/)
- Your Workday OfficeConnect API client details from your Workday administrator (Client ID + two endpoint URLs)
- Workday sign-in credentials with the **Access OfficeConnect** permission
- 30 minutes

---

## Minutes 0-10 — Install

{{< step n="1" title="Verify system requirements" >}}
Skim [System Requirements](/get-started/system-requirements/) to confirm your Excel version is supported.
{{< /step >}}

{{< step n="2" title="Install OfficeConnect" >}}
Follow [Install for End Users](/get-started/install-end-user/). If your IT team deploys OfficeConnect centrally, they may have already done this for you — check Excel's ribbon for an **OfficeConnect** tab.
{{< /step >}}

{{< admin-note >}}
If you're deploying to an organization rather than installing individually, jump to [Install for Admins](/get-started/install-admin/) for the silent-install and registry-deploy approach.
{{< /admin-note >}}

---

## Minutes 10-15 — Sign in and create your tenant

{{< step n="3" title="Open Excel and click the OfficeConnect tab" >}}
The OfficeConnect tab appears between the standard Excel ribbon tabs after installation.
{{< /step >}}

{{< step n="4" title="Sign in and configure your tenant" >}}
Follow [Sign In & Create Your First Tenant](/get-started/admin/configure/sign-in-create-tenant/). You'll need the Client ID and two endpoint URLs from your Workday administrator. The tenant configuration is one-time; OfficeConnect remembers it for future sessions.
{{< /step >}}

After sign-in, the Reporting pane appears on the right side of Excel populated with your Adaptive Planning accounts, time periods, and levels.

---

## Minutes 15-25 — Build your first report

{{< step n="5" title="Tour the Reporting pane" >}}
Spend two minutes on the [Reporting Pane Tour](/get-started/build-reports/reporting-pane-tour/) to understand the three tabs (Elements, Filters, Review) and how dragging works.
{{< /step >}}

{{< step n="6" title="Build the report" >}}
Follow [Build Your First Report](/get-started/build-reports/build-first-report/). It's a 10-step walkthrough that produces a refreshable departmental expense report from an empty workbook.
{{< /step >}}

---

## Minutes 25-30 — Save and explore

{{< step n="7" title="Save your workbook" >}}
Save as a standard `.xlsx`. The OfficeConnect formulas are preserved.
{{< /step >}}

{{< step n="8" title="Explore a cell with Cell Explorer" >}}
Click any data cell in your report, then click **Cell Explorer** in the OfficeConnect ribbon. See how the value is constructed from individual elements. This is your most-used debugging tool — see [Cell Explorer / Drill Down](/get-started/build-reports/cell-explorer-drill-down/).
{{< /step >}}

{{< step n="9" title="Re-open the workbook tomorrow" >}}
Close Excel, reopen the workbook, and click **Refresh**. The numbers update from current Adaptive Planning data. This is the core OfficeConnect loop — build once, refresh forever.
{{< /step >}}

## Result

You have a live, refreshable Workday OfficeConnect report and you understand the core build → refresh → drill workflow. From here, every other tutorial on the site builds on this foundation.

## Next steps

- **Common next builds:** [Rolling 12-Month Report](/get-started/build-reports/rolling-12-month-report/), [Budget vs Actuals Variance](/get-started/build-reports/budget-vs-actuals-variance/), [Department P&L](/get-started/build-reports/department-pl-report/).
- **Working with Financials data?** Jump straight to [Trial Balance Report](/get-started/build-reports/financials/trial-balance-report/).
- **Picking between OfficeConnect and Adaptive web reports?** See the [decision framework](/get-started/migration-comparison/oc-vs-web-reports/).
