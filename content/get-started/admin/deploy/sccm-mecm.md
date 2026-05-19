---
title: "Silent Install Workday OfficeConnect with SCCM / MECM"
linkTitle: "SCCM / MECM Deployment"
weight: 70
description: >
  Deploy Workday OfficeConnect through Microsoft Configuration Manager (SCCM/MECM) with silent install switches, detection methods, and required user-rights handling.
tags: ["deployment", "system-admin", "how-to"]
---

{{< admin-note >}}
This is an IT admin / power-user task. Requires Microsoft Configuration Manager (the product formerly known as SCCM, now MECM) admin access and a working software distribution channel.
{{< /admin-note >}}

Microsoft Configuration Manager (MECM, formerly SCCM) is still the dominant on-prem software-deployment tool in many organizations. This guide packages Workday OfficeConnect as an Application in MECM, with silent install, supersedence-aware upgrade behavior, and reliable detection.

For Intune, see [Intune Win32 Packaging](/get-started/admin/deploy/intune-win32/). For tenant configuration after install, see [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/).

## What you'll need

- MECM admin access with **Application creation** rights
- The latest Workday OfficeConnect installer (MSI or EXE) from your Workday community download
- A distribution point that target devices can reach
- A test machine with the MECM client healthy

## Step 1 — Stage the installer in MECM source

{{< step n="1" title="Create a versioned source folder" >}}
On your MECM source share: `\\mecm-source\Apps\Workday\OfficeConnect\2026R1\` (use the OfficeConnect release version, not your internal app version). Drop the installer in.
{{< /step >}}

{{< step n="2" title="Add a deployment script (optional)" >}}
For installers that need pre/post actions (registry tweaks, log capture), wrap the install in a PowerShell script:

```powershell
# install-officeconnect.ps1
$ErrorActionPreference = "Stop"
$installer = Join-Path $PSScriptRoot "OfficeConnectSetup.exe"
Start-Process -FilePath $installer -ArgumentList "/quiet /norestart" -Wait -PassThru | Out-Null
exit $LASTEXITCODE
```

Otherwise, the installer can be called directly in the MECM install command.
{{< /step >}}

## Step 2 — Create the Application in MECM

{{< step n="3" title="Console → Software Library → Applications → Create Application" >}}
Use the **Manually specify the application information** option (not the auto-detect from MSI, since the installer often does additional work the auto-detect misses).
{{< /step >}}

{{< step n="4" title="Application Information" >}}
- **Name:** `Workday OfficeConnect 2026R1`
- **Manufacturer:** `Workday`
- **Software version:** match the installer
- **Optional reference:** internal Jira ticket or change number
{{< /step >}}

{{< step n="5" title="Add a Deployment Type" >}}
Type: **Script Installer**. Click **Next**.
{{< /step >}}

{{< step n="6" title="Content settings" >}}
- **Content location:** `\\mecm-source\Apps\Workday\OfficeConnect\2026R1\`
- **Persist content in client cache:** unchecked unless you have a specific reason
{{< /step >}}

{{< step n="7" title="Install command" >}}
```
OfficeConnectSetup.exe /quiet /norestart
```

Or if using the PowerShell wrapper:
```
powershell.exe -ExecutionPolicy Bypass -File install-officeconnect.ps1
```

Uninstall command:
```
OfficeConnectSetup.exe /uninstall /quiet /norestart
```
{{< /step >}}

{{< step n="8" title="Detection method" >}}
Add a detection rule based on the installed file:

- **Setting Type:** File System
- **Type:** File
- **Path:** `%ProgramFiles%\Adaptive Insights\OfficeConnect\`
- **File or folder name:** `OfficeConnect.dll`
- **Detection criteria:** **The file system setting must exist**
- Optionally add a version comparison if the DLL carries a version stamp matching the release

Avoid registry-based detection alone — registry keys for OfficeConnect aren't fully reliable across versions.
{{< /step >}}

{{< step n="9" title="User Experience" >}}
- **Installation behavior:** Install for system
- **Logon requirement:** Whether or not a user is logged on
- **Installation program visibility:** Hidden
- **Maximum allowed run time:** 30 minutes (generous)
- **Estimated installation time:** 5 minutes
{{< /step >}}

{{< step n="10" title="Requirements" >}}
Add a requirement: **Operating System** is `Windows 10 (64-bit)` or `Windows 11`. Filter your collection separately if you have additional constraints.
{{< /step >}}

{{< step n="11" title="Distribute content" >}}
Right-click the application → **Distribute Content** → push to your distribution points.
{{< /step >}}

## Step 3 — Deploy

{{< step n="12" title="Right-click the application → Deploy" >}}
Choose your target Collection (typically a Finance Users collection or a device-based collection for finance laptops).
{{< /step >}}

{{< step n="13" title="Deployment settings" >}}
- **Action:** Install
- **Purpose:** Required (mandatory) for the primary rollout; Available for opt-in pilots
- **Schedule:** As soon as possible (test deploys) or per a maintenance window
{{< /step >}}

{{< step n="14" title="User experience" >}}
- **User notifications:** Display in Software Center and only show notifications for computer restarts (avoid noisy popups)
- **Suppress device restarts:** unchecked — OfficeConnect typically doesn't require restart but the option keeps you safe
{{< /step >}}

## Step 4 — Handle upgrades with Supersedence

When the next OfficeConnect release ships:

{{< step n="15" title="Create the new version application" >}}
Repeat Steps 1-2 for the new release in a new source folder (e.g., `\\mecm-source\Apps\Workday\OfficeConnect\2026R2\`).
{{< /step >}}

{{< step n="16" title="Add the new version as a Supersedence" >}}
On the new application's properties → **Supersedence** tab → add the prior version. Set **Uninstall** = unchecked (let the new installer handle upgrade in-place).
{{< /step >}}

{{< step n="17" title="Re-deploy" >}}
Distribute and deploy the new version. MECM identifies machines with the old version and upgrades them on the next policy refresh.
{{< /step >}}

## Verify on a test machine

On the test machine:

{{< step n="18" title="Trigger Software Center policy refresh" >}}
Open `Configuration Manager Properties → Actions → Application Deployment Evaluation Cycle → Run Now`.
{{< /step >}}

{{< step n="19" title="Watch AppEnforce.log for the install execution" >}}
Monitor `C:\Windows\CCM\Logs\AppEnforce.log` to confirm the install runs successfully.
{{< /step >}}

{{< step n="20" title="Open Excel and verify the OfficeConnect tab" >}}
Launch Excel on the test machine and confirm the OfficeConnect tab appears in the ribbon.
{{< /step >}}

## Common gotchas

- **Detection method too narrow:** A registry-key-only detection often misses upgrade scenarios. File-based detection is more reliable.
- **User vs system install:** If users complain OfficeConnect is missing despite the deploy succeeding, the installer may have run per-user instead of per-machine. See Per-User vs Per-Machine Install (coming soon).
- **Conflict with other Excel COM add-ins:** A successful install on a machine that already has think-cell loaded can mask refresh failures — see [think-cell Conflict](/reference/troubleshoot/think-cell-conflict/).
- **Workday version compatibility:** Make sure the version you're deploying is accepted by your Workday tenant. See the [Version Compatibility Matrix](/reference/version-compatibility/).

## Result

Workday OfficeConnect deploys silently across MECM-managed devices, upgrades cleanly on each release via supersedence, and is detected reliably on subsequent inventories.

## Next steps

- [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/) — push tenant configuration in the same wave.
- [Intune Win32 Packaging](/get-started/admin/deploy/intune-win32/) — the Intune equivalent for cloud-managed devices.
- Upgrade Governance (coming soon) — managing the forced-upgrade cadence at scale.
