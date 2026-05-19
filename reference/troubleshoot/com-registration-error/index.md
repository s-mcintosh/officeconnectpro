---
title: "Fix COM Registration Errors"
url: "https://officeconnectpro.com/reference/troubleshoot/com-registration-error/"
description: "How to resolve COM registration errors when installing or updating OfficeConnect.\n"
tags: ["deployment","system-admin","fpna","troubleshoot"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


COM registration errors usually surface during a Workday OfficeConnect install or upgrade and point to a broken Microsoft Office add-in registration. Confirm your machine meets the [system requirements](/wiki/system-requirements/) before working through the fixes — multiple Office versions installed side by side is the most common root cause.

**Symptom:** You receive an error like the following when trying to install or update OfficeConnect:

```
System.InvalidCastException: Unable to cast COM object of type 'System.__ComObject'
to interface type 'Microsoft.Office.Core.IRibbonUI'.
```

## Why this happens

OfficeConnect is an Excel COM add-in that relies on Excel objects registered correctly by your Microsoft Office installation. This error occurs when:

- Excel's COM objects aren't registered correctly
- You have multiple versions of Microsoft Office installed (e.g., Project 2016 and Excel 2013), leading to conflicting versions of the MS-VSTO library

## Fix option 1: Repair Microsoft Office

Many users resolve this by repairing the Office installation:

{{< step n="1" title="Open Windows Settings" >}}
Go to **Start → Settings → Apps & Features**.
{{< /step >}}

{{< step n="2" title="Find Microsoft Office and click Modify" >}}
Select **Microsoft Office** from the list and click **Modify**.
{{< /step >}}

{{< step n="3" title="Choose Online Repair" >}}
Select **Online Repair** (not Quick Repair) and click **Repair**. This fully reinstalls Office components and re-registers COM objects.
{{< /step >}}

{{< step n="4" title="Try installing OfficeConnect again" >}}
After the repair completes, run the OfficeConnect installer again.
{{< /step >}}

## Fix option 2: Registry key correction

If the repair doesn't work, the troubleshooting tool will identify the specific registry key causing the problem. Your IT department can make adjustments to the registry keys listed in the tool's output.

See [Run the Troubleshooting Tool](/reference/troubleshoot/troubleshooting-tool/) to generate a diagnostic log.

## Fix option 3: Disable conflicting add-ins

{{< step n="1" title="Open Excel and go to Options" >}}
**File → Options → Add-Ins**.
{{< /step >}}

{{< step n="2" title="Change Manage to COM Add-ins and click Go" >}}
This shows all active COM add-ins.
{{< /step >}}

{{< step n="3" title="Uncheck all add-ins except Adaptive Planning for Excel" >}}
Click **OK**, then close and reopen Excel.
{{< /step >}}

{{< step n="4" title="Try signing in to OfficeConnect" >}}
If this resolves the issue, re-enable add-ins one at a time to identify the conflict.
{{< /step >}}

## Next steps

- [Resolve OfficeConnect Update Errors](/reference/troubleshoot/update-errors/) if the issue only appears during version updates
- [Run the troubleshooting tool](/reference/troubleshoot/troubleshooting-tool/) to capture the exact registry keys at fault
- [Install as an IT Admin](/wiki/install-admin/) to redeploy a clean per-machine installation across users

