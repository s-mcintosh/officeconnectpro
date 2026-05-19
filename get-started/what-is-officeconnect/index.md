# What is OfficeConnect?

An overview of OfficeConnect — what it does, who it's for, and how it works with Workday Adaptive Planning.


---

OfficeConnect is a Microsoft Office add-in that streams live data from Workday Adaptive Planning directly into Excel, Word, and PowerPoint. Instead of exporting static spreadsheets, your reports stay connected to your planning instance and refresh on demand.

## What OfficeConnect does

- **In Excel:** Build financial reports by dragging and dropping accounts, time periods, versions, and organizational levels into your spreadsheet. Data refreshes from Adaptive Planning with one click.
- **In PowerPoint:** Link tables and charts from your OfficeConnect Excel workbook into presentation slides. Update a presentation for a new period by refreshing the links.
- **In Word:** Link named ranges from Excel into board reports and narratives. Qualitative text (like "increased" or "favorable") can update automatically.

## Who it's for

| Audience | How they use it |
|---|---|
| **End users** (FP&A, finance teams) | Build and refresh Excel reports, share via Teams/SharePoint, publish to PowerPoint and Word |
| **IT admins** | Install the add-in across the organization, configure tenants, manage SSO and registry deployment |

## How it works

OfficeConnect appears as an extra tab in the Excel, Word, and PowerPoint ribbons after installation.

{{< figure src="/images/screenshots/oc-ribbon-tab.png" alt="The OfficeConnect ribbon tab in Excel" caption="The OfficeConnect ribbon tab appears between standard Excel tabs after installation." >}}

In Excel, a **Reporting pane** docks to the side of your worksheet — it contains three tabs:

- **Elements** — browse and drag accounts, time periods, versions, and levels into your report
- **Filters** — apply worksheet and workbook-level filters
- **Review** — inspect exactly which elements are affecting any cell

When you click **Refresh**, OfficeConnect queries your Workday Adaptive Planning instance and populates the connected cells with current data.

{{< figure src="/images/screenshots/oc-reporting-pane-overview.png" alt="The OfficeConnect Reporting pane docked to the right side of Excel" caption="The Reporting pane docked to the right of the worksheet, showing the Elements, Filters, and Review tabs." >}}

## Data sources

OfficeConnect supports two data sources:

- **Adaptive Planning** — your budgets, forecasts, and plan data from Workday Adaptive Planning
- **Financials** — general ledger data from Workday Financial Management (requires separate configuration)

## Next steps

→ [Check system requirements](/get-started/system-requirements/) before installing.
