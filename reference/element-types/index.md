# Element Types Reference

Every element type you can drag from the Workday OfficeConnect Reporting pane, what it represents, and where it lives in each data source.


---


The Reporting pane in Workday OfficeConnect groups all available content into **element types**. This reference defines each type, the data source it applies to, and the typical role it plays in a report.

## Quick table

| Element | Adaptive Planning | Financials | Typical role |
|---|---|---|---|
| Account | ✓ | ✓ (as Ledger Account) | Rows in P&L, BS, expense reports |
| Version | ✓ | ✓ | Identifies which plan/actuals snapshot |
| Time | ✓ | ✓ | Columns in trend reports |
| Level | ✓ | ✓ (as Company) | Organizational scope (department, region) |
| Attribute | ✓ | ✓ | Slicer or filter (Department Type, Product Family) |
| Custom Dimension | ✓ | ✓ (as Dimension / Worktag) | Project Code, Region, Customer |
| Element Group | ✓ | — | Pre-grouped collection of elements |
| Label | ✓ | ✓ | Free text annotation (not Adaptive data) |
| Modeled Account | ✓ | — | Calculated account with drill-down to its components |

## Account

**Adaptive Planning:** A line item that holds a value, such as *Salaries*, *Travel*, or *Total Revenue*. Accounts form a hierarchy — leaf accounts hold values, rollup accounts sum their children.

**Financials:** Called **Ledger Account**. Same idea: a chart-of-accounts line item that holds general-ledger values.

Where to find: `Reporting pane → Accounts`. See [Add Elements](/get-started/build-reports/add-elements/).

## Version

A snapshot or variant of plan data. Examples:

- *Actuals* — the default version in the Financials data source
- *Working Forecast* — a typical Adaptive Planning rolling forecast
- *Budget 2026* — a locked annual budget
- *Plan vs Reforecast — Q3* — an analyst's variance comparison

Where to find: `Reporting pane → Versions`. See [Compare Planning Versions](/get-started/build-reports/compare-planning-versions/).

## Time

A time period — typically a month, quarter, or year. Time elements can be:

- **Absolute** — *January 2026*, *Q4 2025*. Doesn't move when the calendar advances.
- **Relative** — *This Month*, *Prior Year YTD*. Rolls forward automatically.
- **Range** — *Jan 2026 through Dec 2026*. Used in repeating reports.

Where to find: `Reporting pane → Time`. See [Time and Contexts](/get-started/build-reports/time-and-contexts/).

## Level

The organizational unit in the Adaptive Planning hierarchy. A Level can be a department, cost center, region, or any node defined in your model. Levels are hierarchical: the *East Region* Level rolls up children like *Boston* and *New York*.

In the Financials data source, the equivalent is **Company**.

Where to find: `Reporting pane → Levels`. See [Department P&L Report](/get-started/build-reports/department-pl-report/).

## Attribute

A categorical tag applied to accounts or other elements. Examples: *Department Type = Cost Center*, *Product Family = SaaS*. Useful as filters or slicers.

Where to find: `Reporting pane → Attributes`. See [Custom Dimensions & Attributes](/get-started/build-reports/custom-dimensions-attributes/).

## Custom Dimension

An additional reporting dimension defined in your Adaptive Planning model — typical examples are *Project Code*, *Customer*, *Region*, *Channel*. Each Custom Dimension appears under its configured name in the Reporting pane.

In the Financials data source, custom dimensions are called **Worktags**. See [Worktag Combinations](/get-started/build-reports/financials/worktag-combinations/).

## Element Group

**Adaptive Planning only.** A predefined collection of elements treated as one. For example, a *Headcount Accounts* element group might bundle *Salaries*, *Benefits*, *Payroll Taxes*. Dropping the group into one cell pulls the rollup.

Element groups are configured in Adaptive Planning, not in OfficeConnect.

## Label

A free-text annotation on a worksheet — usually a row header like *Operating Expenses* typed by the user. Labels do **not** pull data from Adaptive Planning; they're just text. They show in the Reporting pane's Review tab as a recognized worksheet item, but the value is whatever you typed.

## Modeled Account

**Adaptive Planning only.** A calculated account whose value is derived from a formula across other accounts. Dragging a modeled account into a cell behaves like any other account — refresh resolves to the computed value. Cell Explorer can show the underlying components.

## Result

You can now pick the right element type for whatever column or row you're building. When in doubt, drag the closest element into a scratch cell, click Cell Explorer to see what it resolved to, then refine.

## Next steps

- [Formula Reference](/reference/formula-reference/) — what these elements look like inside the cell formula.
- [Add Elements](/get-started/build-reports/add-elements/) — step-by-step on dragging each type into a worksheet.
- [Filter Data](/get-started/build-reports/filter-data/) — how Attributes and Custom Dimensions work as filters.
