# Workbook & Worksheet Properties

Configure rounding, data clearing, filters, and display options for your reports.


---


Workday OfficeConnect has three levels of settings that control report behavior, each overriding the one above it. If you're new to the Excel side of the product, get oriented with the [Reporting Pane Tour](/get-started/build-reports/reporting-pane-tour/) first — these properties dialogs all hang off that same ribbon.

1. **User Settings** — your personal defaults for all new workbooks
2. **Workbook Properties** — settings for the current workbook (overrides User Settings)
3. **Selection Properties** — settings for a specific row, column, or cell (overrides Workbook Properties)

## User Settings

Access via **OfficeConnect ribbon → User Settings**.

| Setting | Default | Description |
|---|---|---|
| **Round to** | Thousands | How to round numbers. Options: Hundreds, Thousands, Ten Thousands, …, Billions, No Rounding |
| **Show zero in cells with no data** | On | Shows `0` instead of blank for empty cells |
| **Security block result text** | `n/a` | The placeholder text shown in linked cells after data is cleared on save |
| **Show refresh errors** | On | Shows a list of cell errors after refresh |
| **Show refresh warnings** | On | Shows a list of warnings after refresh |

User Settings apply to all new workbooks you create. They don't change existing open workbooks.

## Workbook Properties

Access via **OfficeConnect ribbon → Workbook Properties**.

### General tab

| Setting | Description |
|---|---|
| **Clear Data** | *Always clear data upon save* — replaces data with security text on save (recommended for sensitive data). *Never clear data upon save* — retains data when saving. |
| **Include update groups in refresh** | Auto-updates element groups when you refresh |

### Filters tab

| Setting | Description |
|---|---|
| **Enable filters** | Toggles workbook-level filters on/off |
| **Display unknown elements** | Shows elements that aren't accessible or don't exist in the hierarchy for a given date |

### Format tab

| Setting | Description |
|---|---|
| **Round to** | Overrides User Settings rounding for this workbook only. Applies to all sheets. After changing, click **Refresh > All Sheets**. |
| **Report date** | Sets the date displayed by `{Report Date}` labels |

## Selection Properties

Access by right-clicking a row, column, or cell → **OfficeConnect → Row/Column/Cell Properties**.

Selection Properties override Workbook Properties for the selected area. Useful for:
- Suppressing rounding on specific cells that contain percentages
- Controlling row/column display (hide zeros, hide blanks) for part of a report

## Precedence summary

`Selection Properties > Workbook Properties > User Settings`

The most specific setting always wins.

## Next steps

- [Change Rounding Settings](/reference/troubleshoot/change-rounding-settings/) for the most common reason to override workbook defaults
- [Suppress & Hide Zeros and Blanks](/reference/troubleshoot/suppress-zeros-blanks/) to fine-tune row display
- [Lock and Protect Reports for Distribution](/get-started/build-reports/lock-protect-reports/) once your workbook settings are finalized
