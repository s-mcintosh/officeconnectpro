# Financials vs. Adaptive Planning Data Sources

Key differences in OfficeConnect behavior depending on whether you're using the Adaptive Planning or Financials data source.


---


OfficeConnect supports two data sources. Most organizations use **Adaptive Planning** (budget and forecast data). Organizations using Workday Financial Management also have access to the **Financials** data source (general ledger actuals).

The data source is set when you configure your tenant. Some OfficeConnect features behave differently depending on which source is active.

## Feature comparison

| Feature | Adaptive Planning | Financials |
|---|---|---|
| **Elements hierarchy** | Accounts, Level, Custom Dimensions | Ledger Accounts, Company, Dimensions |
| **Minimum valid intersection** | Version + Level + Time + Account | Version + Company + Time + Ledger Account |
| **Default rounding** | Thousands | No Rounding |
| **Make new time elements relative** | On by default | Off by default |
| **Always clear data upon save** | On by default | Off by default |
| **Element groups** | Available | Not available |
| **Cell Details** | Explore Cell (drill into cell data) | Show Details (contributing journal lines; drill through to Workday) |
| **Default version** | Depends on your model | Actuals |
| **Exclude elimination on expand** | Not available | Available (in user settings and Expand dialog) |

## Which data source am I using?

Check your tenant configuration: in the OfficeConnect sign-in drop-down, each tenant shows its data source type.

## Effective dates (Financials only)

When using the Financials data source, you can select an **effective date** for your report. This reflects your organization's structure as of that date — useful for reporting after reorganizations.

> **Note:** Effective date support requires configuration in your Workday reporting model. Ask your System Administrator to enable it via the **Run Set Up Reporting Model** task in Workday, or contact your Workday Security Administrator.

## Alternate hierarchies (Financials only)

If your administrator configures alternate hierarchies for dimensions in the financial reporting data model, you can select different hierarchy views in your OfficeConnect report — useful for viewing company, ledger account, or cost center dimensions from multiple perspectives.
