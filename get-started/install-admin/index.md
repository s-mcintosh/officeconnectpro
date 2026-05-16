# Install as an IT Admin

Deploy OfficeConnect to multiple users using per-machine installation and group policy or scripts.


---


{{< admin-note >}}
This page is for IT administrators deploying OfficeConnect to multiple users or machines. End users installing on their own machine should see [Install as an End User](/get-started/install-end-user/).
{{< /admin-note >}}

## Two installation modes

| Mode | When to use |
|---|---|
| **Per-user** | Each user installs on their own workstation. Users can install future updates without admin permissions. |
| **Per-machine** | Installed once on a shared machine for all users on that computer. Requires admin permissions for all updates. |

Per-user installation is generally preferred — it lets users self-update and reduces IT overhead.

## Per-machine installation steps

{{< step n="1" title="Prepare prerequisites on target machines" >}}
Before running the per-machine installer, verify these are installed on each target machine:
- WebView2 Runtime
- Microsoft .NET Framework 4.8
- VSTO 2010 runtime
- Workday Event Log Components

Deploy these via your preferred software distribution tool (SCCM, Intune, etc.) if not already present.
{{< /step >}}

{{< step n="2" title="Run the per-machine installer" >}}
Download the **per-machine** setup file from **Product Downloads** in your Workday Adaptive Planning instance (it is a separate file from the per-user `OfficeConnectSetup.exe`). Run it with elevated privileges:

```cmd
OfficeConnectSetup-PerMachine.exe /quiet
```

The installer creates install files, registry entries, and certificates in the machine profile rather than the user profile.
{{< /step >}}

{{< step n="3" title="Deploy tenant configuration" >}}
After installation, users need tenant details to sign in. You can push these via registry rather than having each user configure them manually.

See [Deploy Tenants via Registry](/connect/deploy-tenants-registry/) for the full registry deployment guide.
{{< /step >}}

{{< step n="4" title="Verify on a test machine" >}}
Open Excel on a test machine and confirm the OfficeConnect tab is present. Sign in with a test account and verify you can connect to the tenant.
{{< /step >}}

## Keeping OfficeConnect updated

Make sure your team updates together — users on older versions cannot open workbooks created with a newer version. Coordinate updates and deploy the latest installer to all machines at the same time.

## Next steps

→ [Deploy Tenants via Registry](/connect/deploy-tenants-registry/) — push tenant config to user machines without manual setup
