---
title: "Create Repeating Reports"
url: "https://officeconnectpro.com/get-started/build-reports/repeating-reports/"
description: "Automatically generate one copy of a report per department, region, or any other level.\n"
tags: ["reporting","adaptive-planning","fpna","recipe"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


The **Repeating Reports** feature in Workday OfficeConnect copies a finished report worksheet once for each element you choose — for example, one sheet per cost center or one sheet per region. Each copy is automatically filtered to show data for its element. Start from a polished single-sheet template, such as the one built in [Build a Department P&L Report](/get-started/build-reports/department-pl-report/).

## What it does

When you create repeating reports, OfficeConnect:
- Copies the worksheet for each selected element
- Applies one element as a filter to each copy
- Optionally refreshes each copy automatically
- Names each worksheet based on your naming convention
- Preserves all Excel formatting, formulas, and OfficeConnect metadata

Once created, each repeating report is **independent** — it's not linked to the original. To update them with new report formatting, delete and recreate them.

## Steps

{{< step n="1" title="Build and finalize the original report" >}}
Complete the report on one worksheet — all elements applied, formatting done, formulas in place. This is the template that gets copied.

Optionally shorten the worksheet name (e.g., rename `Profit and Loss` to `P&L`) — the copies will be named based on this.
{{< /step >}}

{{< step n="2" title="(Optional) Add a repeating report label" >}}
If you want each copy to show the name of its filter element (e.g., the department name), add a label:

1. Select the cell where you want the label
2. Click **Labels** in the OfficeConnect ribbon
3. Set **Label Type** to `System Variable` and **Label Type Value** to `{Repeating Report Element}`
4. Click **Add Expression**

This label is blank on the original but populates on each copy during the creation process.
{{< /step >}}

{{< step n="3" title="Open Repeating Reports" >}}
In the OfficeConnect ribbon, click **Repeating Reports**.
{{< /step >}}

{{< step n="4" title="Select the filter element type" >}}
Choose what to copy by — e.g., filter by Level to create one sheet per organizational level.
{{< /step >}}

{{< step n="5" title="Select which elements to include" >}}
Check the specific elements (levels, versions, etc.) you want copies for.
{{< /step >}}

{{< step n="6" title="Set the naming convention and refresh option" >}}
Define how worksheets will be named. Optionally choose to refresh all copies immediately after creation.
{{< /step >}}

{{< step n="7" title="Click Create" >}}
OfficeConnect creates one worksheet per selected element and refreshes each one (if you chose auto-refresh).
{{< /step >}}

## Updating repeating reports

Repeating reports don't stay linked to the original. To incorporate structural changes to the report:

{{< step n="8" title="Delete the existing repeating report worksheets" >}}
Right-click each repeating report tab and choose **Delete** to remove the old copies.
{{< /step >}}

{{< step n="9" title="Update the original template" >}}
Make your structural changes on the original template worksheet.
{{< /step >}}

{{< step n="10" title="Re-run the Repeating Reports process" >}}
Click **Repeating Reports** in the OfficeConnect ribbon and create new copies from the updated template.
{{< /step >}}

## Next steps

- [Build a Department P&L Report](/get-started/build-reports/department-pl-report/) for a strong single-sheet template to repeat
- [Lock and Protect Reports for Distribution](/get-started/build-reports/lock-protect-reports/) before sharing the multi-sheet pack with stakeholders
- [Optimize OfficeConnect Performance](/get-started/performance/optimize-performance/) if generating dozens of sheets makes refresh slow

