# Report in Constant Currency in OfficeConnect

Use a constant currency version in Adaptive Planning to remove FX impact from OfficeConnect reports — useful for multinational teams comparing performance across periods.


---


Constant currency reporting holds foreign exchange rates fixed at a baseline period so you can see underlying business performance without FX noise. In Adaptive Planning, this is done through a dedicated constant currency version. OfficeConnect surfaces that version like any other — you just need to know which one to select.

## How constant currency works in Adaptive Planning

Your Adaptive Planning administrator sets up a constant currency version by configuring currency conversion rules that use a fixed rate (for example, the prior-year average rate or a budget rate). When you report against this version, all values are translated at that fixed rate regardless of the reporting period.

This is different from reporting in a single currency (e.g., USD only) — constant currency still shows values in your chosen currency but removes the variability caused by rate fluctuations between periods.

## Steps

1. Open your OfficeConnect workbook and click the **OfficeConnect** tab.

2. Identify your constant currency version — common names include **Constant Currency**, **CC Actuals**, **FX Neutral**, or **Budget Rate Actuals**. If you're unsure, ask your Adaptive Planning administrator which version uses fixed rates.

3. Set up your report as usual with account rows and time columns.

4. In your version column header (e.g., **B1**), drag the constant currency version from the Reporting pane into the cell instead of your standard Actuals version.

5. To compare constant currency actuals against reported actuals, add a second column (**C1**) with the standard Actuals version.

6. Add an Excel variance column (**D**) with the formula `=B3-C3` to show the FX impact.

7. Click **Refresh**. Column B shows performance at fixed rates; column C shows performance at actual rates; column D shows the FX impact.

> **Note:** If your model does not have a constant currency version, OfficeConnect cannot create one — this must be configured in Adaptive Planning. See your Workday administrator to set up currency conversion rules.

## Labeling your report clearly

Constant currency reports can confuse readers who don't know which rates were used. Add a text cell near the top of your workbook noting the base period rate — for example: *"Values in column B translated at FY2025 average rates."*

## Related

- [Compare Two Planning Versions Side by Side](/build-reports/compare-planning-versions/)
- [Multi-Currency Reporting with the Financials Data Source](/build-reports/financials/multi-currency-financials/) — currency options for accounting teams on the Financials data source
