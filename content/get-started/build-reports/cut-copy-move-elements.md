---
title: "Cut, Copy & Move Elements"
linkTitle: "Cut, Copy & Move"
weight: 5
description: >
  How to move OfficeConnect elements within and between rows, columns, and cells.
tags: ["reporting", "adaptive-planning", "fpna", "how-to"]
---

OfficeConnect provides its own cut, copy, and paste commands that move elements together with their metadata.

> **Important:** Always use OfficeConnect's own cut/copy/paste commands — not Excel's standard Ctrl+C/Ctrl+V. Excel's clipboard doesn't carry the OfficeConnect element metadata; only OfficeConnect commands do.

## Three ways to cut, copy, and paste

**Ribbon buttons:** Use the functions in the **OfficeConnect** tab, not the Home tab.

**Right-click menu:** Right-click the cell, row, or column → **OfficeConnect** → **Cut Elements** or **Copy Elements**, then **Paste Elements**.

**Keyboard shortcuts:**
| Action | Shortcut |
|---|---|
| Cut | `Shift + Ctrl + Alt + X` |
| Copy | `Shift + Ctrl + Alt + C` |
| Paste | `Shift + Ctrl + Alt + V` |

## What you can paste where

| Cut/Copy from | Can paste into |
|---|---|
| Cells | Cells, rows, or columns |
| Rows | Rows or columns |
| Columns | Rows or columns |

## Steps

{{< step n="1" title="Select the source" >}}
Select the entire row, column, or cell containing the elements you want to move. Highlight the full row or column — not just a few cells within it.
{{< /step >}}

{{< step n="2" title="Cut or copy" >}}
Use the ribbon, right-click menu, or keyboard shortcut to cut or copy.
{{< /step >}}

{{< step n="3" title="Select the destination" >}}
Highlight the entire destination row, column, or cell.
{{< /step >}}

{{< step n="4" title="Paste" >}}
Use the ribbon, right-click menu, or keyboard shortcut to paste.
{{< /step >}}

## Append vs replace when dragging

When you drag and drop an element into a location that already has an element:

- OfficeConnect asks whether to **Append** (add to existing) or **Replace** (overwrite existing)
- Choose **Replace** to swap one element for another
- Choose **Append** to combine elements at that location

## Note on merged cells

If your workbook uses merged cells, OfficeConnect cannot update or refresh elements applied to those merged cells. Avoid merging cells that contain OfficeConnect elements.

## Next steps

→ [Review & Verify Applied Elements](/get-started/build-reports/review-applied-elements/) to inspect which elements are driving each cell's data
