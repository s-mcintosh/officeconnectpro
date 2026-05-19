---
title: "Workday OfficeConnect Glossary"
linkTitle: "Glossary"
weight: 10
description: >
  Alphabetical reference for every Workday OfficeConnect term — elements, filters, contexts, write-back, tenants, and more.
tags: ["reference", "fpna", "system-admin"]
---

The vocabulary for Workday OfficeConnect overlaps with Workday Adaptive Planning, Workday Financial Management, and Excel. This glossary defines every term as it's used inside OfficeConnect and links to the canonical guide for each.

## A

**Access OfficeConnect** — A Workday security permission that grants a user the right to sign in to OfficeConnect. Set in the user's permission set in Workday. See [Set Up Workday SSO](/get-started/admin/configure/workday-sso/).

**Account** — In Adaptive Planning, an item like *Salaries* or *Total Revenue* that holds a value. Appears in the **Accounts** node of the Reporting pane. In the Financials data source, equivalent to a **Ledger Account**. See [Add Elements](/get-started/build-reports/add-elements/).

**Adaptive Planning** — The Workday application that holds budget, forecast, and plan data. One of two **data sources** OfficeConnect can connect to. See [Financials vs. Adaptive Planning](/get-started/migration-comparison/financials-vs-adaptive-planning/).

**Add-in** — In Microsoft Office, an extension that adds features to Excel, Word, or PowerPoint. OfficeConnect is a COM add-in on Windows and a JavaScript add-in on Mac. See [Install for End Users](/get-started/install-end-user/).

**Alias** — Hugo front-matter field that creates a URL redirect. Used internally on relocated OfficeConnect Pro articles so old URLs still resolve. Not a Workday OfficeConnect feature.

**API client** — A configuration in Workday that issues a Client ID, Authorization Endpoint URL, and API Endpoint URL, allowing OfficeConnect to authenticate to the tenant. See [Set Up Workday SSO](/get-started/admin/configure/workday-sso/).

**Attribute** — A dimension applied to accounts or other elements (e.g., *Department Type*, *Product Family*). Appears in the Reporting pane under **Attributes**.

**Authorization Endpoint URL** — One of three values from the Workday API client used to configure an OfficeConnect tenant. See [Sign In & Create a Tenant](/get-started/admin/configure/sign-in-create-tenant/).

## B

**Background refresh** — A workbook setting that lets Excel remain responsive while OfficeConnect data loads. Enable in **Workbook Properties → Refresh**. See [Optimize Performance](/get-started/performance/optimize-performance/).

## C

**Cell Explorer** — An OfficeConnect feature that shows every element (account, version, time, level, dimension) affecting the value in a selected cell. The fastest way to debug an unexpected number. See [Cell Explorer / Drill Down](/get-started/build-reports/cell-explorer-drill-down/).

**Client ID** — One of three values from the Workday API client used to configure an OfficeConnect tenant.

**COM add-in** — The Windows version of OfficeConnect uses Microsoft's COM (Component Object Model) extensibility, in contrast to the JavaScript add-in model used on Mac. See [Re-enabling a Disabled COM Add-in](/reference/troubleshoot/reenable-com-addin/).

**Custom dimension** — An additional reporting dimension defined in Adaptive Planning (e.g., *Project Code*, *Region*). Appears in the Reporting pane under its configured name. See [Custom Dimensions & Attributes](/get-started/build-reports/custom-dimensions-attributes/).

## D

**Data entry** — Mode where typed values in cells are submitted back to Adaptive Planning via **Submit**. See [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/).

**Data source** — The Workday system OfficeConnect pulls from. Either **Adaptive Planning** (budgets/forecasts) or **Financials** (general-ledger actuals from Workday Financial Management).

**Drill-through** — Following a cell value back to the underlying journal lines in Workday Financial Management. Financials data source only. See [Drill-through to Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/).

## E

**Effective date** — In the Financials data source, the date used to resolve organizational hierarchy for a report. Useful for reporting after a reorg.

**Element** — Any item dragged from the Reporting pane onto a worksheet: an account, version, time period, level, attribute, or custom dimension.

**Element group** — A predefined collection of elements treated as one. Adaptive Planning only.

## F

**Filter** — A scope restriction applied at the worksheet or workbook level. See [Filter Data](/get-started/build-reports/filter-data/).

**Financials (data source)** — General-ledger actuals from Workday Financial Management, exposed in OfficeConnect through the Financials data source. See [Financials vs. Adaptive Planning](/get-started/migration-comparison/financials-vs-adaptive-planning/).

**Forced upgrade** — Workday's policy of requiring an OfficeConnect version update within a grace period (typically 30 days per-user, 60 days per-machine) after a new release. See [Check & Update Your Version](/get-started/check-version/).

## L

**Label** — A free-text annotation on a worksheet (e.g., a row title typed manually). Distinct from elements, which always reference Adaptive Planning data.

**Ledger account** — The Financials data source equivalent of an Account.

**Level** — An organizational unit in the Adaptive Planning hierarchy (e.g., a department, region, or cost center). Equivalent to **Company** in the Financials data source.

## M

**Multi-instance** — Linked Adaptive Planning instances in a hierarchical relationship that share data through account and dimension mapping. See [Multiple Instances](/get-started/admin/configure/multiple-instances/).

## N

**Named range** — An Excel feature that labels a group of cells with a name. OfficeConnect uses named ranges to link Excel tables and values into Word and PowerPoint. See [OfficeConnect for PowerPoint](/get-started/word-powerpoint/powerpoint/officeconnect-for-powerpoint/).

## P

**Personal what-if scenario** — A 2026R1 feature letting end users create their own what-if versions without admin involvement. See [Personal what-if scenarios (2026R1)](/reference/whats-new/2026r1-personal-scenarios/).

## R

**Refresh** — Pulling current data from Adaptive Planning into your workbook. The OfficeConnect ribbon's central command.

**Repeating rows** — A pattern where OfficeConnect generates one row per item in a list (e.g., one row per cost center) automatically. See [Repeating Reports](/get-started/build-reports/repeating-reports/).

**Reporting pane** — The right-hand panel in Excel where you browse and drag elements into your worksheet.

## S

**Sandbox** — A non-production Adaptive Planning instance used for testing. Configure as a separate tenant in OfficeConnect.

**Single sign-on (SSO)** — Sign-in flow using your organization's identity provider (Okta, Microsoft Entra ID, Ping) routed through Workday. See [Set Up Workday SSO](/get-started/admin/configure/workday-sso/).

**Submit** — The OfficeConnect ribbon command that writes pending data-entry values back to Adaptive Planning.

## T

**Tenant** — A saved OfficeConnect connection to a specific Workday instance, identified by Client ID and endpoint URLs. See [Sign In & Create a Tenant](/get-started/admin/configure/sign-in-create-tenant/).

**Time context** — The time period applied to an element or a worksheet. Can be absolute (*Jan 2026*) or relative (*This Month*, *Prior Year*). See [Time and Contexts](/get-started/build-reports/time-and-contexts/).

## V

**Version** — A snapshot or variant of plan data (e.g., *Working Forecast*, *Budget v3*, *Actuals*). Selected as an element in any report.

**View By** — A 2026R1 ribbon command that opens a cell's underlying data in a separate sheet for ad-hoc manipulation. See [View By (2026R1)](/reference/whats-new/2026r1-view-by/).

## W

**Workbook Properties** — Settings that control workbook-wide OfficeConnect behavior (refresh, security, data entry). See [Workbook & Worksheet Properties](/get-started/build-reports/workbook-worksheet-properties/).

**Worktag** — A Workday Financial Management dimension tag (e.g., *Cost Center*, *Project*). Financials data source only. See [Worktag Combinations](/get-started/build-reports/financials/worktag-combinations/).

**Write-back** — Submitting data from Excel back to Adaptive Planning. Generally available since 2025R1. See [Enter Budget Data](/get-started/data-entry-writeback/enter-budget-data/).

## Next steps

- [Element Types Reference](/reference/element-types/) — every element you can drag.
- [Version Compatibility Matrix](/reference/version-compatibility/) — which features arrived in which release.
