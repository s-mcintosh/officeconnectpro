---
title: "Link to External Excel Files"
url: "https://officeconnectpro.com/reference/troubleshoot/link-external-excel-files/"
description: "How to link to a plain Excel file from within an OfficeConnect workbook.\n"
tags: ["reporting","fpna","system-admin","troubleshoot"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


**Question:** Can I create a link from my OfficeConnect workbook to a regular (non-OfficeConnect) Excel file?

## Yes — use Excel's standard external link

OfficeConnect workbooks are Excel files. You can use Excel's standard external reference syntax to pull data from any other Excel file:

```text
=[OtherWorkbook.xlsx]Sheet1!$A$1
```

This creates a standard Excel external link — it's not an OfficeConnect-managed link, so it works just like any other Excel cross-workbook reference.

## Create an Excel copy without OfficeConnect links

If you need to send a colleague a version of your OfficeConnect report that doesn't contain any live OfficeConnect connections (e.g., they don't have OfficeConnect installed and you want them to see the data, not `n/a` placeholders):

{{< step n="1" title="Refresh the report so all data is loaded" >}}
Click **Refresh** to populate all cells with current data.
{{< /step >}}

{{< step n="2" title="Copy the entire worksheet" >}}
Right-click the sheet tab → **Move or Copy** → check **Create a copy** → place at end.
{{< /step >}}

{{< step n="3" title="On the copy, select all cells (Ctrl+A) and copy" >}}
{{< /step >}}

{{< step n="4" title="Paste as values only" >}}
Right-click → **Paste Special → Values**. This replaces the OfficeConnect-linked cells with static values.
{{< /step >}}

{{< step n="5" title="Save the copy as a new Excel file" >}}
**File → Save As** → give it a different name. This file has no OfficeConnect dependencies.
{{< /step >}}

