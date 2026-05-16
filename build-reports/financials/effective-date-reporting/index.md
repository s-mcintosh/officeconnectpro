# Use Effective Date Reporting After a Reorganization

Use OfficeConnect's effective date setting to report against your organization's structure as it existed on a specific date — essential after a reorganization.


---


When your organization restructures mid-year, historical reports can show cost centers, companies, or hierarchies that no longer exist — or omit ones that didn't exist yet. OfficeConnect's Financials data source supports **effective date reporting**, which lets you select the org structure as it existed on a specific date.

> **Note:** Effective date reporting requires configuration in Workday's financial reporting data model. If the effective date option isn't available in your tenant, contact your Workday Security Administrator.

## When to use effective date reporting

- **After a reorganization:** Report Q1 actuals under the pre-reorg structure to compare apples to apples
- **For historical audits:** View the org hierarchy as it was at a specific point in time
- **For restatements:** Show actuals under the structure that was in place when the transactions were posted

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. In the Reporting pane, look for the **Effective Date** setting. It typically appears near the top of the pane or in a data source settings panel. (If you don't see it, effective date is not enabled on your tenant — see the note above.)

3. Click the effective date field and enter the date you want to report as of — for example, `03/31/2025` to see the org structure as it was at end of Q1 2025.

4. Build or refresh your report as usual. OfficeConnect applies the effective date to all dimension hierarchies — cost centers, companies, and any other org elements resolve to their structure as of that date.

5. To return to the current structure, clear the effective date field and refresh again.

## What changes with an effective date

| Element | Without effective date | With effective date |
|---|---|---|
| Cost centers | Current hierarchy | Hierarchy as of selected date |
| Companies | Current structure | Structure as of selected date |
| Dimension rollups | Current | As of selected date |
| Transaction amounts | Unchanged | Unchanged (only the org structure changes) |

## Related

- [Report on Actuals by Cost Center](/build-reports/financials/actuals-by-cost-center/)
- [Filter Reports by Company](/build-reports/financials/filter-by-company/)
- [Adaptive Planning vs. Financials Data Source](/build-reports/financials-vs-adaptive-planning/) — effective date is a Financials-only feature
