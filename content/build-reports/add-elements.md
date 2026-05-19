---
title: "Add Elements to Rows, Columns & Cells"
linkTitle: "Add Elements"
weight: 2
description: >
  How to drag accounts, time periods, versions, and levels into your Excel report.
tags: ["adaptive-planning", "reporting", "fp-and-a", "tutorial"]
---

Elements are the building blocks of an OfficeConnect report. You add them to rows, columns, or cells in your worksheet to define what data appears at each intersection.

> **Best practice:** Add elements to entire rows and columns rather than individual cells. When applied to a row or column, a bolded (parent) element also expands its children — each child gets its own row or column automatically.

## Basic steps

{{< step n="1" title="Select your target in the grid" >}}
Click to select the cells, rows, or columns where you want data to appear. To select an entire row or column, click the row number or column letter.
{{< /step >}}

{{< step n="2" title="Open the Elements tab in the Reporting pane" >}}
Click **Show Reporting Pane** if the pane is hidden, then click the **Elements** tab.
{{< /step >}}

{{< step n="3" title="Browse to the element you want" >}}
Expand the element tree to find what you need:
- **Accounts** → expand to find specific accounts or account groups
- **Time** → expand to find years, quarters, or months
- **Level** → find your organizational level
- **Versions** → select actuals, budget, or forecast versions
{{< /step >}}

{{< step n="4" title="Apply the element" >}}
Use any of these methods:
- **Drag and drop** the element onto your selected row, column, or cell
- **Right-click** the element → **Apply to Selection**
- Click the element and click **Apply to Selection** in the Elements pane toolbar
{{< /step >}}

{{< figure src="/images/screenshots/oc-elements-drag-drop.png" alt="Dragging an account from the Elements tree onto a row in the worksheet" caption="Drag an account from the Elements tree and drop it onto a selected row — OfficeConnect inserts the element reference." >}}

{{< step n="5" title="Click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon to load the data.
{{< /step >}}

## Add multiple elements to one row or column

1. Select the target row or column
2. Hold **Ctrl** and click each element you want
3. Drag them all at once into the selection
4. Click **Refresh**

All selected elements populate into the single row or column. Data rolls up by the elements.

## Expand and collapse elements

In the Elements pane, right-click a parent element:
- **Expand All** — shows all children and descendants of that element
- **Collapse All** — hides all children and descendants, showing only that parent element collapsed

## Element groups

Applying a bolded parent element creates an **element group** — each child gets its own row or column and the report updates dynamically when your Adaptive Planning structure changes.

{{< figure src="/images/screenshots/oc-element-group-expanded.png" alt="A parent account element expanded into individual child rows in the worksheet" caption="A parent account applied to a row automatically expands its children — each child account gets its own row." >}}

## Next steps

→ [Work with Time & Contexts](/build-reports/time-and-contexts/) to add time periods and period-to-date comparisons
