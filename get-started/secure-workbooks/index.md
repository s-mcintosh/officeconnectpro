# Secure OfficeConnect Workbooks

How OfficeConnect handles security, timeouts, and data clearing to protect sensitive financial data.


---


## Automatic timeout

OfficeConnect uses a session timeout to keep your reports secure. If you haven't refreshed your report in **60 minutes** (or your configured timeout period), OfficeConnect prompts you to re-authenticate the next time you try to refresh.

The timeout duration is set by your Adaptive Planning administrator.

## Data clearing on save

By default, OfficeConnect **clears all data when you save** a workbook. Connected cells display a placeholder (default: `n/a`) until the next refresh. This means:

- A saved workbook sent to someone who doesn't have OfficeConnect shows placeholder text, not live financial data
- The recipient needs OfficeConnect and appropriate Adaptive Planning permissions to see actual numbers

### Change the placeholder text

{{< step n="1" title="Open User Settings" >}}
From the OfficeConnect ribbon tab, click **User Settings**.
{{< /step >}}

{{< step n="2" title="Update the security block text" >}}
On the **General** tab, find the **Security block result text** field. Enter whatever text you want (e.g., `[Refresh to load data]`).
{{< /step >}}

{{< step n="3" title="Click OK" >}}
The new text replaces `n/a` the next time you clear data or save the workbook.
{{< /step >}}

### Disable data clearing for a specific workbook

If you want a workbook to retain data on save (not recommended for sensitive data):

{{< step n="1" title="Open the workbook" >}}
Open the workbook you want to modify in Excel.
{{< /step >}}

{{< step n="2" title="Click Workbook Properties" >}}
In the OfficeConnect ribbon tab, click **Workbook Properties**.
{{< /step >}}

{{< step n="3" title="Disable data clearing" >}}
On the **General** tab, set **Clear Data** to **Never clear data upon save**.
{{< /step >}}

## User-based data access

OfficeConnect respects Adaptive Planning's security model. Each user sees only the data their Adaptive Planning permission set allows. A user who can only access data from a specific organizational level will only see that level's data when they refresh — even if the report template was designed with broader access.

## Sharing workbooks

See [Share Reports via Teams, SharePoint & OneDrive](/build-reports/share-teams-sharepoint-onedrive/) for guidelines on sharing workbooks through Microsoft collaboration tools.
