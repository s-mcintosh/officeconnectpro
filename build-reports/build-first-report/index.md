# Build Your First OfficeConnect Report

A complete walkthrough for creating a live Adaptive Planning report in Excel from scratch.


---


This tutorial walks through building a basic departmental expense report from an empty workbook to a live, refreshable OfficeConnect report. By the end you will have a working report that pulls real data from Adaptive Planning with one click.

**What you'll need:**
- OfficeConnect installed and connected to your Workday tenant ([Get Started](/get-started/))
- An Adaptive Planning instance with at least one version of data loaded
- A blank Excel workbook

---

<!-- VIDEO PLACEHOLDER
When the YouTube video is ready, uncomment the section below and replace VIDEO_ID with the 11-character YouTube video ID (e.g. dQw4w9WgXcQ).

## Watch

{{< youtube VIDEO_ID >}}

-->

## Step 1 — Open the Reporting pane

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel. On the **OfficeConnect** ribbon tab, click **Open Pane**. The Reporting pane appears on the right side of the screen.
{{< /step >}}

{{< step n="2" title="Sign in if prompted" >}}
If the pane shows a sign-in prompt, click **Sign In** and complete the Workday authentication flow. See [Sign In and Create a Tenant](/connect/sign-in-create-tenant/) if you need help.
{{< /step >}}

---

## Step 2 — Add your first element

{{< step n="3" title="Click a cell in your workbook" >}}
Click cell **B2** — this is where the first data value will land.
{{< /step >}}

{{< step n="4" title="Add an Account element" >}}
In the Reporting pane, expand **Accounts** and locate the account you want (for example, *Total Expenses*). Double-click it or drag it to cell B2. OfficeConnect inserts a formula referencing that account.
{{< /step >}}

{{< step n="5" title="Add a Time element" >}}
Click cell **B1** (the header row). In the Reporting pane, expand **Time** and drag the time period you want (for example, *Jan 2025*) into B1. Repeat for as many months as you need across columns C1, D1, and so on.
{{< /step >}}

{{< step n="6" title="Add a Version element" >}}
Click cell **A2**. Expand **Versions** in the pane and drag your target version (for example, *Working Forecast*) into A2.
{{< /step >}}

For more detail on each element type, see [Add Elements to a Report](/build-reports/add-elements/).

---

## Step 3 — Refresh and review

{{< step n="7" title="Click Refresh" >}}
On the OfficeConnect ribbon, click **Refresh**. OfficeConnect queries Adaptive Planning and populates your cells with live data. You should see numbers appear in B2 onward.
{{< /step >}}

{{< step n="8" title="Check for n/a values" >}}
If any cell shows `n/a`, the element combination has no data for that intersection (account + time + version). Verify the version contains data for the selected time period in Adaptive Planning.
{{< /step >}}

---

## Step 4 — Format and save

{{< step n="9" title="Apply Excel formatting" >}}
Format the cells with currency, number, or percentage formatting as needed using Excel's standard formatting tools. OfficeConnect data cells are normal Excel cells — any Excel format works.
{{< /step >}}

{{< step n="10" title="Save the workbook" >}}
Save the file as a standard `.xlsx`. The OfficeConnect formulas are preserved and will refresh again the next time you open the file and click **Refresh**.
{{< /step >}}

---

## Next steps

- **Add filters** to scope data to a specific department or cost center — see [Filter Data](/build-reports/filter-data/)
- **Repeat rows** to build multi-account reports automatically — see [Repeating Reports](/build-reports/repeating-reports/)
- **Share the report** with a colleague via SharePoint — see [Share via Teams & SharePoint](/share-publish/share-teams-sharepoint-onedrive/)
