# Build a Cash Flow Statement with OfficeConnect (Financials)

Build an indirect-method cash flow statement in Excel using OfficeConnect's Financials data source — operating, investing, and financing activities from Workday Financial Management.


---


A cash flow statement built in OfficeConnect pulls balance changes and net income directly from Workday Financial Management, eliminating the manual work of reconciling figures from Workday Report Writer into Excel. This tutorial builds an indirect-method statement — the most common format for external financial reporting.

**What you'll build:** A cash flow statement with Operating, Investing, and Financing Activities sections, all refreshable from Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to the **Financials** data source
- Workday Financial Management with a current period closed and journal entries posted
- A completed balance sheet workbook is helpful for cross-referencing — see [Build a Balance Sheet](/get-started/build-reports/financials/balance-sheet-report/)

---

## Step 1 — Set up the version and period

{{< step n="1" title="Open Excel and activate OfficeConnect" >}}
Open Excel, click **OfficeConnect**, and sign in. The Reporting pane should show the Financials data source.
{{< /step >}}

{{< step n="2" title="Add version and time context" >}}
Click **B1** and drag **Actuals** from the Reporting pane. Click **B2** and drag your reporting period (for example, Q2 2026 or the full fiscal year). Cash flow statements cover a period of activity, so use a range period (a full quarter or year) rather than a point-in-time date.
{{< /step >}}

---

## Step 2 — Operating activities (indirect method)

{{< step n="3" title="Add the Net Income starting line" >}}
In **A5**, type `OPERATING ACTIVITIES`. Bold and underline. In **A6**, drag **Net Income** from the Reporting pane. This is the starting point for the indirect method — all adjustments are added or subtracted from net income.
{{< /step >}}

{{< step n="4" title="Add non-cash adjustments" >}}
In **A7**, drag **Depreciation and Amortization** (a non-cash expense — added back to net income). In **A8**, type `Changes in Working Capital` and bold it as a sub-section header.
{{< /step >}}

{{< step n="5" title="Add working capital changes" >}}
In A9–A12, drag accounts that represent working capital changes:
- **A9**: Accounts Receivable (change from prior period)
- **A10**: Prepaid Expenses (change)
- **A11**: Accounts Payable (change)
- **A12**: Accrued Liabilities (change)

In **A13**, drag **Net Cash from Operating Activities** (the rollup for this section).
{{< /step >}}

{{< step n="6" title="Populate Operating Activities data cells" >}}
Click **B6** — OfficeConnect creates a formula for Net Income in the selected period. Copy down through **B13**. Check that working capital change accounts show the period-over-period change, not a point-in-time balance — confirm with your chart of accounts setup.
{{< /step >}}

---

## Step 3 — Investing activities

{{< step n="7" title="Add investing activities" >}}
In **A15**, type `INVESTING ACTIVITIES`. Bold and underline. In A16–A17, drag:
- **A16**: Capital Expenditures (purchases of PP&E — typically a negative number)
- **A17**: Proceeds from Asset Sales (positive)

In **A18**, drag **Net Cash from Investing Activities**.
{{< /step >}}

{{< step n="8" title="Populate Investing Activities data cells" >}}
In **B16**, copy the formula structure from B6. Copy down through B18.
{{< /step >}}

---

## Step 4 — Financing activities

{{< step n="9" title="Add financing activities" >}}
In **A20**, type `FINANCING ACTIVITIES`. Bold and underline. In A21–A22, drag:
- **A21**: Proceeds from Borrowings
- **A22**: Repayment of Debt (negative)

In **A23**, drag **Net Cash from Financing Activities**.
{{< /step >}}

{{< step n="10" title="Add net change in cash" >}}
In **A25**, type `Net Increase (Decrease) in Cash`. In **B25**, enter a plain Excel formula:
```
=B13+B18+B23
```
This sums the three activity sections. In **A26**, drag **Cash at Beginning of Period** and in **A27**, drag **Cash at End of Period** from the Reporting pane to cross-check the net change.
{{< /step >}}

---

## Step 5 — Refresh and verify

{{< step n="11" title="Refresh and verify the cash change" >}}
Click **Refresh**. Check that B25 (the sum formula) equals B27 minus B26 (Cash End minus Cash Beginning). A discrepancy means a cash account is missing from one of the three sections or is double-counted.
{{< /step >}}

{{< step n="12" title="Format the statement" >}}
Apply Accounting number format. Bold all subtotal rows (Net Cash from Operating, Investing, Financing, and Net Increase in Cash). Add a thin border above each subtotal row and a double underline under the Cash at End of Period row.
{{< /step >}}

---

## Next steps

- Cross-reference with your balance sheet — see [Build a Balance Sheet](/get-started/build-reports/financials/balance-sheet-report/)
- Add prior-year comparison columns to show YoY cash flow — see [Build an Actuals Trend Report](/get-started/build-reports/financials/actuals-trend-report/)
- Reconcile figures to Workday Report Writer — see [Reconcile OfficeConnect Values to Workday Reports](/get-started/build-reports/financials/reconcile-to-workday/)
