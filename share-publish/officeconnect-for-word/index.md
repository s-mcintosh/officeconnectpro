# OfficeConnect for Word

Link live financial data from OfficeConnect Excel into Word reports and board narratives.


---


OfficeConnect for Word lets you embed live tables and single-cell values from your OfficeConnect Excel workbook into Word documents. Board reports, investor letters, and executive narratives can update automatically when the underlying data changes.

## What you can link

- **Tables** — complete tables from named ranges in Excel, formatted exactly as they appear in Excel
- **Single cells** — individual values (e.g., a total revenue figure or a percentage)
- **Qualitative text** — words like "increased" or "decreased" that update based on cell values

## Start OfficeConnect for Word

{{< step n="1" title="Open Word" >}}
After OfficeConnect is installed, an **OfficeConnect** tab appears in Word's ribbon. An **OfficeConnect links pane** docks to the left side.
{{< /step >}}

{{< step n="2" title="Click Log In" >}}
Enter your Adaptive Planning credentials, or click **Log in with Workday**. If you're already signed in to OfficeConnect for Excel, Word logs you in automatically.
{{< /step >}}

## Connect to an Excel workbook

{{< step n="1" title="In the OfficeConnect tab, click Link to Workbook" >}}
Browse to and open your OfficeConnect Excel workbook. The workbook's named ranges appear in the OfficeConnect links pane under **Table Links** (multi-cell ranges) and **Single Links** (single cells).
{{< /step >}}

## Link a table into Word

{{< step n="1" title="Place your cursor in the document" >}}
Click where you want the table to appear.
{{< /step >}}

{{< step n="2" title="In the links pane, find the table link" >}}
Right-click the named range under **Table Links** and select **Apply to Selection**.
{{< /step >}}

The table appears formatted exactly as it looks in Excel. No reformatting required (unless the table is wider than the Word document margins, in which case OfficeConnect proportionally scales it down).

## Refresh the document for a new period

When source data changes (e.g., for a new month's report):

{{< step n="1" title="Update the linked Excel workbook" >}}
In Excel, update time elements or refresh from Adaptive Planning.
{{< /step >}}

{{< step n="2" title="In Word, click Refresh in the OfficeConnect tab" >}}
All linked data updates from the Excel workbook.
{{< /step >}}

## Change the source file for a new period

If you save your Excel workbook under a new filename for each period (e.g., `Board_Report_Q3_2025.xlsx`):

1. In the OfficeConnect tab, click **Manage Links**
2. Check the links you want to update
3. Click **Change Source** and browse to the new file
4. Click **Close**

Because the new file is a copy of the old one, the named ranges are identical and the links transfer cleanly.

## Disconnect a link

1. In the OfficeConnect tab, click **Manage Links**
2. Check the link(s) to disconnect
3. Click **Break Link**

The data remains in the document as static text/table, but no longer updates from Excel.
