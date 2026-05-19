---
title: "Task Pane Not Displaying Correctly"
linkTitle: "Task Pane Issues"
weight: 3
description: >
  How to fix the OfficeConnect Reporting pane when it's not showing or displaying incorrectly.
tags: ["deployment", "fp-and-a", "admin-power-user", "troubleshoot"]
---

## Symptom: Reporting pane is invisible or blank

If the OfficeConnect Reporting pane disappears or shows as blank, it's usually a display rendering issue in Excel.

**Fix:**

{{< step n="1" title="Open Excel Options" >}}
Go to **File → Options → General**.
{{< /step >}}

{{< step n="2" title="Change the rendering setting" >}}
Find the option **"Optimize for best appearance"** and change it to **"Optimize for compatibility"**.
{{< /step >}}

{{< step n="3" title="Close and reopen Excel" >}}
The Reporting pane should now display correctly.
{{< /step >}}

## Symptom: Floating pane has disappeared

If you undocked the Reporting pane and lost it:

**Fix:** In the OfficeConnect ribbon, click **Show Reporting Pane** — even if it's already checked. The pane will reappear.

## Symptom: OfficeConnect tab is missing from the ribbon

If the entire OfficeConnect tab is gone from the ribbon:

{{< step n="1" title="Check if the add-in is disabled" >}}
Go to **File → Options → Add-Ins**. Change **Manage** to **Disabled Items** and click **Go**. If OfficeConnect appears there, select it and click **Enable**.
{{< /step >}}

{{< step n="2" title="Check COM Add-ins" >}}
Change **Manage** to **COM Add-ins** and click **Go**. Make sure **Adaptive Planning for Excel** is checked.
{{< /step >}}

{{< step n="3" title="Reinstall if needed" >}}
If the add-in isn't listed, it may need reinstalling. See [Install as an End User](/get-started/install-end-user/).
{{< /step >}}
