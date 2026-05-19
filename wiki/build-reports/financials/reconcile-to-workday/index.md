---
title: "Reconcile OfficeConnect Values to Workday Reports"
url: "https://officeconnectpro.com/wiki/build-reports/financials/reconcile-to-workday/"
description: "Troubleshoot and explain differences between OfficeConnect figures and Workday Report Writer output — common causes of discrepancies and how to resolve them.\n"
tags: ["financials","accounting","reporting","fpna","troubleshoot"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


OfficeConnect and Workday Report Writer pull from the same underlying Workday Financial Management data, so their figures should agree. When they don't, the difference almost always comes down to a filter, period definition, or configuration mismatch — not a data error. This guide walks through the most common causes and how to diagnose them.

**What you'll need:**
- OfficeConnect connected to the Financials data source
- Access to Workday Report Writer or a Workday financial report for comparison

---

{{< step n="1" title="Confirm you're comparing the same period" >}}
The most common cause of discrepancies is a period definition mismatch. In your OfficeConnect workbook, note the exact period element you've dragged into the time context cell. Click the cell and check the element details in the Reporting pane — is it a month, a quarter, or a fiscal year? Is it calendar year or fiscal year? In Workday Report Writer, check the **Accounting Date** range or period parameter used to run the report. Workday may default to calendar month while OfficeConnect is set to a fiscal period, or vice versa. Set both to the identical period definition and refresh. If the figures converge, period was the cause.
{{< /step >}}

{{< step n="2" title="Check effective date settings" >}}
OfficeConnect supports effective-date reporting, which reflects the organization structure as of a specific date rather than the posting date of transactions. If OfficeConnect is set to an effective date that differs from Report Writer's configuration, cost center or department allocations may differ. In the Reporting pane, check whether an effective date element is applied to the workbook. Remove it to revert to the default posting-date view, then compare to Report Writer.
{{< /step >}}

{{< step n="3" title="Verify account scope" >}}
Confirm that the accounts in your OfficeConnect report match exactly what the Workday report includes. OfficeConnect rollup accounts aggregate all child accounts — if Workday's report uses a different account grouping, figures will differ. Build a side-by-side: list the same leaf-level accounts in OfficeConnect (not rollups) and compare each one to the same account line in Workday. This isolates which account has the discrepancy, narrowing the investigation.
{{< /step >}}

{{< step n="4" title="Check company and currency filters" >}}
If your organization has multiple companies, confirm that both OfficeConnect and Workday Report Writer are scoped to the same company. In OfficeConnect, check for a Company element in the workbook header — see [Filter Reports by Company](/wiki/build-reports/financials/filter-by-company/). If your report uses currency conversion, confirm that both tools are using the same exchange rate type and conversion date. OfficeConnect supports both transaction currency and converted currency reporting — check which is active.
{{< /step >}}

{{< step n="5" title="Check for journal sources excluded by Report Writer" >}}
Some Workday reports are configured to exclude certain journal sources (for example, intercompany elimination entries or system-generated allocations). OfficeConnect by default includes all journal sources. To scope OfficeConnect to match, apply a journal source filter — see [Variance Analysis by Journal Source](/wiki/build-reports/financials/variance-by-journal-source/).
{{< /step >}}

{{< step n="6" title="When you can't find the cause" >}}
If the figures still don't reconcile after checking all of the above, collect the following and share with your Workday admin or OfficeConnect support:

- The exact account, period, and filter settings in both OfficeConnect and Workday Report Writer
- The specific figures that differ (both the OfficeConnect amount and the Workday Report Writer amount)
- Whether the discrepancy is consistent across periods or appears in a specific month only
{{< /step >}}

> **Note:** Small rounding differences (< $1) between OfficeConnect and Workday Report Writer are expected in some configurations due to currency conversion rounding. These are cosmetic and do not indicate a data problem.

---

## Related links

- [Fix Data Discrepancies Between OfficeConnect and Workday](/reference/troubleshoot/data-discrepancies/)
- [Filter Reports by Company](/wiki/build-reports/financials/filter-by-company/)
- [Variance Analysis by Journal Source](/wiki/build-reports/financials/variance-by-journal-source/)

