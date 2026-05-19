# Variance Analysis by Journal Source in OfficeConnect

Break down account variances by journal source in OfficeConnect — see how much of a balance movement came from manual journals, system-generated entries, or specific subledgers.


---


When a GL account balance moves unexpectedly, the first question is: what kind of journal entry caused it? Workday Financial Management categorizes journal entries by **Journal Source** (Manual Journal, Accounts Payable, Payroll, etc.). OfficeConnect can filter by journal source, letting you isolate the impact of each source on any account balance.

**What you'll need:**
- OfficeConnect connected to the Financials data source
- A report showing a balance or variance you want to investigate

---

## 1. Find journal source elements in the Reporting pane

1. Open the OfficeConnect Reporting pane. Expand **Filters** (or **Journal Sources**, depending on your OfficeConnect version). You should see a list of journal sources configured in your Workday tenant — typically including: **Manual Journal**, **Accounts Payable**, **Accounts Receivable**, **Payroll**, **Fixed Assets**, **Intercompany**, and **System**.
2. If you don't see a journal source filter, confirm with your OfficeConnect admin that the Financials data source is configured to expose journal source dimensions.

## 2. Build a journal source comparison report

3. Set up a basic account report:
   - **B1**: Actuals version
   - **B2**: Reporting period (for example, April 2026)
   - **A5 downward**: Accounts you want to analyze (for example, Operating Expenses accounts)

4. In the header row (row 1), add a column for each journal source you want to compare. Drag **Manual Journal** into **C1**, **Accounts Payable** into **D1**, **Payroll** into **E1**.

5. Click **B5** and copy the formula across to C5, D5, E5. Each column now filters the same account balance by its journal source.

6. Add a **Total** column (F1 = "Total") with the formula `=B5+C5+D5+E5`. This should match the unfiltered B column balance — if it doesn't, there are journal sources not represented in your columns.

7. Click **Refresh**. Each column shows how much of the account balance came from each journal source.

## 3. Identify the source of a variance

8. To investigate a month-over-month variance, add a prior period column for each journal source:
   - **B3**: Current month (e.g., April 2026)
   - **G3**: Prior month (e.g., March 2026) — drag the prior period into G3, then copy the journal source structure from B:F into G:K
   - Add variance formulas in a final column set: `=B5-G5`, `=C5-H5`, etc.

9. The journal source with the largest variance between months is typically the one to investigate. For example, if the Manual Journal column shows a $50,000 variance and all other sources are flat, search in Workday for manual journals posted to that account in April.

> **Tip:** After identifying the journal source, use OfficeConnect's drill-through to jump directly to the journal lines. See [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/) for how to set up the drill-through link.

---

## Related links

- [Drill Through to Workday Journal Lines](/get-started/build-reports/financials/drill-through-journal-lines/)
- [Build a Trial Balance Report](/get-started/build-reports/financials/trial-balance-report/)
- [Reconcile OfficeConnect Values to Workday Reports](/get-started/build-reports/financials/reconcile-to-workday/)
