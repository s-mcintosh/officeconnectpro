# OfficeConnect Formula Reference

What's actually inside a Workday OfficeConnect cell — formula structure, components, and how to read it.


---


When you drag an element into a cell, Workday OfficeConnect inserts a custom function. This reference explains what that function looks like, what each part means, and what's possible when you read it with the formula bar open.

## The shape of an OfficeConnect formula

A typical OfficeConnect cell formula looks like:

```
=OfficeConnectFunction("Version=Working_Forecast;Account=Total_Expenses;Time=Jan_2026;Level=East_Region")
```

The function call is opaque on purpose — you should not edit it directly. The single argument is a delimited string of **element references**, one per dimension that resolves the cell to a single value in Adaptive Planning.

Internally, the cell resolves to a value when OfficeConnect submits a query containing every element on the cell, plus any worksheet- or workbook-level filters that apply.

## Component pieces

| Piece | What it is | Example |
|---|---|---|
| **Function name** | The OfficeConnect add-in function. Don't change. | `OfficeConnectFunction` (the exact name may vary by version) |
| **Element references** | Each `Dimension=Value` pair the cell carries. The combination must resolve to a single intersection. | `Version=Working_Forecast` |
| **Hierarchy resolution** | Spaces in element names become underscores in the reference. The display name is preserved separately. | *East Region* → `East_Region` |
| **Source workbook scope** | Filters from the worksheet and workbook are appended at refresh time, not stored in the formula. | (implicit) |

## What you can do with the formula

Although you shouldn't hand-edit the function call, the cell behaves like any Excel cell otherwise.

- **Wrap it in Excel functions.** `=IF(A1<0, "Over budget", A1)` works fine — the OfficeConnect value is evaluated first, then your wrapper.
- **Reference it elsewhere.** `=A1*1.05` for a manual override.
- **Format it.** Excel number, currency, and percentage formatting all apply.
- **Inspect it with Cell Explorer.** Click the cell, then OfficeConnect ribbon → **Cell Explorer** — much more readable than the raw formula. See [Cell Explorer / Drill Down](/build-reports/cell-explorer-drill-down/).

## What you should not do

- **Don't edit the function arguments by hand.** OfficeConnect will not warn you; the cell may stop refreshing, or refresh to a wrong value.
- **Don't copy-paste OfficeConnect cells with standard Excel copy.** Use the OfficeConnect ribbon's copy/paste commands — see [Cut, Copy, Move Elements](/build-reports/cut-copy-move-elements/). Standard Excel paste breaks the linkage.
- **Don't put `NOW()`, `TODAY()`, `RAND()`, or `OFFSET()` in the same sheet.** These volatile Excel functions trigger OfficeConnect recalcs on every keystroke. See [Optimize Performance](/performance/optimize-performance/).

## Common formula behaviors

| Behavior | What it means |
|---|---|
| `n/a` value | The element combination has no data at that intersection (e.g., that account has no value in that version for that time period). |
| `#VALUE!` | An element reference can no longer be resolved — usually an account was deleted or renamed in Adaptive Planning. |
| Empty cell after refresh | The intersection is genuinely zero or null. Check workbook **Suppress Zeros** setting. See [Suppress Zeros and Blanks](/troubleshoot/suppress-zeros-blanks/). |
| Cell shows old value | Workbook hasn't been refreshed since the source changed. Click **Refresh**. If that fails, see [Not Refreshing](/troubleshoot/not-refreshing/). |

## Data-entry formulas (Write-back)

When data entry is enabled on the workbook, typing a value over an OfficeConnect formula replaces the formula with the typed number (highlighted as a pending input). After **Submit**, OfficeConnect restores the formula and the underlying Adaptive Planning value reflects what you entered. See [Enter Budget Data](/data-entry-writeback/enter-budget-data/).

## Result

Reading an OfficeConnect formula tells you exactly which intersection it queries. Combined with Cell Explorer, you can debug any unexpected number in under a minute.

## Next steps

- [Element Types Reference](/reference/element-types/) — every element you'll see inside formulas.
- [Cell Explorer / Drill Down](/build-reports/cell-explorer-drill-down/) — the friendlier formula inspector.
- [Glossary](/reference/glossary/) — definitions for every term used here.
