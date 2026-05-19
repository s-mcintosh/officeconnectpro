# Silent Install Workday OfficeConnect with Microsoft Intune (Win32 App)

Package Workday OfficeConnect as a Win32 app for Microsoft Intune, push to all users silently, and verify deployment.


---


{{< admin-note >}}
This is an IT admin / power-user task. Requires Microsoft Intune admin access and the Microsoft Win32 Content Prep Tool.
{{< /admin-note >}}

Microsoft Intune deploys Workday OfficeConnect cleanly through its Win32 app model — silent install, mandatory assignment, automatic upgrade on new releases. This guide walks through packaging, uploading, and assigning the app.

For the SCCM/MECM equivalent, see [Silent Install with SCCM/MECM](/get-started/admin/deploy/sccm-mecm/). For tenant configuration after install, see [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/).

## What you'll need

- Microsoft Intune tenant with **Application Management** rights
- The latest Workday OfficeConnect installer (MSI or EXE) from your Workday community download
- [Microsoft Win32 Content Prep Tool](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) (downloaded once)
- A Windows test machine enrolled in Intune for verification

## Step 1 — Stage the installer

{{< step n="1" title="Download the latest OfficeConnect installer" >}}
Get the current installer from your Workday community downloads (typically `OfficeConnectSetup.exe` or `OfficeConnect.msi`). Confirm the version matches what your tenants will accept — see [Check & Update Your Version](/get-started/check-version/).
{{< /step >}}

{{< step n="2" title="Stage in a working folder" >}}
Create `C:\IntunePackaging\OfficeConnect\Source\` and drop the installer in. Keep one installer per folder — the prep tool packages everything in the source folder.
{{< /step >}}

## Step 2 — Build the .intunewin package

{{< step n="3" title="Run the Win32 Content Prep Tool" >}}
Open a Command Prompt as administrator and run:

```cmd
IntuneWinAppUtil.exe -c C:\IntunePackaging\OfficeConnect\Source -s OfficeConnectSetup.exe -o C:\IntunePackaging\OfficeConnect\Output
```

The tool produces `OfficeConnectSetup.intunewin` in the output folder.
{{< /step >}}

## Step 3 — Upload to Intune

{{< step n="4" title="Create a new Win32 app in Intune" >}}
In the Microsoft Endpoint Manager admin center: **Apps → Windows → Add → Windows app (Win32)**. Browse to the `.intunewin` file.
{{< /step >}}

{{< step n="5" title="Fill in app information" >}}
Set Name (`Workday OfficeConnect`), Publisher (`Workday`), App version (match the installer version), and a brief description. Add an icon if you have one.
{{< /step >}}

{{< step n="6" title="Configure install command" >}}
Use the silent-install switches from the installer:

```
OfficeConnectSetup.exe /quiet /norestart
```

For the MSI variant: `msiexec /i OfficeConnect.msi /quiet /norestart`

See Silent Install Switches Reference (coming soon) for the full list.
{{< /step >}}

{{< step n="7" title="Configure uninstall command" >}}
```
OfficeConnectSetup.exe /uninstall /quiet /norestart
```
{{< /step >}}

{{< step n="8" title="Set install behavior" >}}
- **Install behavior:** System (deploy per-machine) — recommended for most organizations
- **Device restart behavior:** App install may force a device restart (or "No specific action")
- **Return codes:** Defaults are fine; the installer returns standard MSI exit codes
{{< /step >}}

{{< step n="9" title="Define requirements" >}}
- **Operating system architecture:** 64-bit
- **Minimum operating system:** Windows 10 1903 (or current organizational baseline)
- **Disk space:** 500 MB (generous; the installer is small)
{{< /step >}}

{{< step n="10" title="Define detection rules" >}}
Detection rule type: **File** — check for the presence of the OfficeConnect install directory or its main DLL. Example:

- **Path:** `C:\Program Files\Adaptive Insights\OfficeConnect\`
- **File or folder:** `OfficeConnect.dll`
- **Detection method:** File or folder exists
{{< /step >}}

{{< step n="11" title="Skip dependencies, supersedence (optional)" >}}
Unless you're upgrading from a previously deployed Intune package, skip these.
{{< /step >}}

{{< step n="12" title="Assign the app" >}}
Assign to **Required** group(s) — typically your "Finance Users" Azure AD group. Click **Create**.
{{< /step >}}

## Step 4 — Verify on a test machine

{{< step n="13" title="Trigger an Intune sync" >}}
On the test machine: Settings → Accounts → Access work or school → click the work account → Sync. Wait 5-10 minutes for the install to download and run.
{{< /step >}}

{{< step n="14" title="Open Excel and verify" >}}
Excel should show the OfficeConnect ribbon tab. If your registry tenant deploy is already in place, sign-in should offer your tenant in the drop-down.
{{< /step >}}

## Common gotchas

- **App version mismatch:** Intune uses the version field to detect upgrades. Increment it each new OfficeConnect release so Intune knows to redeploy.
- **Detection rule fails after upgrade:** If the install path or DLL name changes between releases, your detection rule will think the upgrade failed. Test detection after each version bump.
- **Per-user installs in a per-machine deployment:** Some OfficeConnect installer variants default to per-user. Confirm `/AllUsers` or equivalent switch if you need per-machine — see Per-User vs Per-Machine Install (coming soon).
- **Slow first refresh after install:** If users see slow first refresh after the deploy, the **Adaptive Insights** registry path may need pre-population. Pair this deploy with [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/).

## Result

Workday OfficeConnect installs silently across your organization on the Intune assignment schedule, with no user action required. New releases re-deploy automatically when you upload an updated `.intunewin` package and bump the version.

## Next steps

- [Deploy Tenants via Registry](/get-started/admin/deploy/deploy-tenants-registry/) — push tenant configuration alongside the install.
- [Silent Install with SCCM/MECM](/get-started/admin/deploy/sccm-mecm/) — the SCCM equivalent for non-Intune shops.
- [Set Up Workday SSO](/get-started/admin/configure/workday-sso/) — wire up identity so users don't enter credentials manually.
