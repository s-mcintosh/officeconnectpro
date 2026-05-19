---
title: "Numbers Not Shifting After Inserting Rows"
linkTitle: "Numbers Not Shifting"
weight: 4
description: >
  Why OfficeConnect elements don't move when you insert Excel rows, and how to fix it.
tags: ["reporting", "fp-and-a", "system-admin", "troubleshoot"]
---

When you edit a report's structure with native Excel commands, Workday OfficeConnect element bindings stay glued to the original row numbers — which is why a row insert can leave your data behind. The fix is to use OfficeConnect's own insert/delete commands; see [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/) for the equivalent move pattern.

**Symptom:** You insert rows into your Excel worksheet, but OfficeConnect data in rows below the insertion point doesn't shift down — the elements stay in their original positions.

## Why this happens

OfficeConnect element metadata is attached to specific cells. When you use standard Excel **Insert Rows**, Excel moves the cell values but the OfficeConnect element assignments don't follow — they remain anchored to the original row numbers.

## Fix: Use OfficeConnect's Insert/Delete functions

Instead of Excel's native Insert Rows/Delete Rows, always use OfficeConnect's equivalent:

{{< step n="1" title="Select the row where you want to insert" >}}
Click the row number to select the entire row.
{{< /step >}}

{{< step n="2" title="Right-click and use OfficeConnect → Insert Row" >}}
From the right-click context menu, select **OfficeConnect → Insert Row** (not Excel's standard Insert).
{{< /step >}}

This inserts a row and correctly shifts all OfficeConnect element assignments.

## If you already inserted rows with Excel's native function

1. Undo the insert with **Ctrl+Z** (undo until you're back to the pre-insert state)
2. Reinsert using OfficeConnect's Insert Row function

If undo isn't available, you'll need to re-apply elements to the affected rows manually.

## Next steps

- [Cut, Copy & Move Elements](/build-reports/cut-copy-move-elements/) for the correct way to relocate existing elements
- [Review & Verify Applied Elements](/build-reports/review-applied-elements/) to confirm the right elements landed on the right rows after edits
- [Add Elements to Rows, Columns & Cells](/build-reports/add-elements/) if you need to re-apply elements that were lost
