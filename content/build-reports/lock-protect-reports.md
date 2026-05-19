---
title: "Lock and Protect Reports for Distribution"
linkTitle: "Lock and Protect Reports"
weight: 25
description: >
  Protect an OfficeConnect workbook for distribution so recipients can't accidentally break formulas — while keeping Refresh working.
tags: ["adaptive-planning", "sharing", "fpna", "system-admin", "how-to"]
---

When you share an OfficeConnect report with people who shouldn't edit it, Excel's sheet protection prevents accidental changes. The catch: you must leave OfficeConnect formula cells unlocked, or Refresh will fail with a "sheet is protected" error.

## How OfficeConnect cells work with protection

OfficeConnect stores data in formula cells. When you click Refresh, OfficeConnect writes new values into those cells. If the sheet is protected and those cells are locked, Refresh fails. The solution: unlock the OfficeConnect cells before protecting the sheet.

## Steps

1. Open your OfficeConnect workbook and click **Refresh** once to make sure all OfficeConnect cells are populated.

2. Select all cells: **Ctrl+A** (or **Cmd+A** on Mac).

3. Open Format Cells: **Ctrl+1** (or right-click → Format Cells). Go to the **Protection** tab. Check **Locked**. Click OK. This locks every cell by default.

4. Now select only the OfficeConnect cells — the cells containing element formulas (they typically look like `=OC(...)` or similar). You can identify them by clicking each cell and checking the formula bar for an OfficeConnect formula.

   > **Tip:** Use **Ctrl+G → Special → Formulas** to select all formula cells at once. This selects both OfficeConnect formulas and any Excel formulas you've added (like variance calculations). Deselect the Excel-only formula cells if you want those locked.

5. With the OfficeConnect cells selected, open Format Cells again → Protection → **uncheck Locked** → OK.

6. Go to **Review → Protect Sheet**. Set a password if desired. Under "Allow all users of this worksheet to:", leave the defaults (select locked cells, select unlocked cells). Click OK.

7. Click **Refresh** to confirm it still works. If you see a protection error, repeat steps 4–5 — some OfficeConnect cells were missed.

## What recipients can and can't do

| Action | Allowed |
|---|---|
| Click Refresh | Yes (OfficeConnect cells are unlocked) |
| Read data | Yes |
| Edit OfficeConnect formulas | No |
| Edit your Excel labels and headers | No (unless you unlocked them) |
| Add rows or columns | No |

## Related

- [Share via Teams & SharePoint](/word-powerpoint/sharing/share-teams-sharepoint-onedrive/) — distribute the protected workbook
- [Secure Workbooks](/admin/govern/secure-workbooks/) — additional security options at the tenant level
