---
title: "Drill Through to Workday Journal Lines from OfficeConnect"
linkTitle: "Drill Through to Journal Lines"
weight: 2
description: >
  Use OfficeConnect's Show Details feature to see the individual journal lines behind any GL balance — and drill through to the source transaction in Workday.
tags: ["financials", "reporting", "fp-and-a", "tutorial"]
---

When a number in your OfficeConnect report doesn't look right, you don't need to leave Excel. OfficeConnect's **Show Details** feature opens a panel showing every journal line contributing to that cell's balance. From there, you can drill through directly to the transaction in Workday Financial Management.

**What you'll need:**
- OfficeConnect connected to a **Financials data source** tenant
- A report with at least one populated cell (actuals data for a ledger account, company, and period)

---

## Step 1 — Build or open a Financials report

{{< step n="1" title="Open a report with Financials data" >}}
Open any OfficeConnect workbook using the Financials data source and click **Refresh** to ensure cells are populated. If you need to build one from scratch, follow [Build a Trial Balance Report](/build-reports/financials/trial-balance-report/) first.
{{< /step >}}

---

## Step 2 — Open Show Details

{{< step n="2" title="Right-click a populated cell" >}}
Right-click any cell containing an OfficeConnect Financials value (a cell with a balance, not a header or label cell).
{{< /step >}}

{{< step n="3" title="Select Show Details" >}}
In the context menu, click **Show Details**. A detail pane opens below or beside your report (depending on your OfficeConnect layout settings). This pane lists every journal line that contributed to the cell's balance.
{{< /step >}}

{{< step n="4" title="Review the journal lines" >}}
The Show Details pane shows each journal line with columns including:
- **Journal Source** — where the entry originated (e.g., Accounts Payable, Payroll)
- **Journal Date** — the accounting date of the entry
- **Ledger Account** — the account charged
- **Amount** — the debit or credit amount
- **Memo** — the journal line description if one was entered
{{< /step >}}

---

## Step 3 — Drill through to Workday

{{< step n="5" title="Click a journal line to drill through" >}}
Click any row in the Show Details pane. OfficeConnect opens the corresponding transaction in Workday Financial Management in your default browser — logged in as your current Workday user.
{{< /step >}}

{{< step n="6" title="Review the source transaction" >}}
In Workday, you'll see the full accounting journal: all lines, the journal source, the preparer, any attachments, and the approval chain. This is the authoritative source of the posted entry.
{{< /step >}}

---

> **Note:** Drill-through requires that your Workday user account has access to view journals in Workday Financial Management. If the Workday page shows an error or access denied message, contact your Workday Security Administrator to verify your security role includes journal viewing permissions.

---

## What Show Details vs. Explore Cell means

If you're switching between Adaptive Planning and Financials tenants, note that the right-click menu is different:

| Data Source | Right-click option | What it shows |
|---|---|---|
| Financials | Show Details | Contributing journal lines, with drill-through to Workday |
| Adaptive Planning | Explore Cell | Contributing dimension splits within the Adaptive Planning model |

See [Adaptive Planning vs. Financials Data Source](/migration-comparison/financials-vs-adaptive-planning/) for a full comparison.

---

## Next steps

- Build a trial balance to have a full set of balances to drill into — see [Trial Balance Report](/build-reports/financials/trial-balance-report/)
- Build an actuals trend to find the period where a variance appears — see [Actuals Trend Report](/build-reports/financials/actuals-trend-report/)
