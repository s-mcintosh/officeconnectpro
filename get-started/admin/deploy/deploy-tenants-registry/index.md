# Deploy Tenants via Registry

Push Workday OfficeConnect tenant configuration to user machines using the Windows registry.


---


{{< admin-note >}}
This is an IT admin / power-user task. It requires access to Windows group policy, deployment scripts, or software distribution tools (e.g., SCCM, Intune).
{{< /admin-note >}}

Instead of having each user manually enter tenant details, you can deploy tenant configuration directly to the Windows registry. This is the recommended approach for organizations with many users.

## Registry locations

Choose one:

| Location | Scope |
|---|---|
| `HKEY_LOCAL_MACHINE\Software\Adaptive Insights` | All users on the machine (preferred) |
| `HKEY_CURRENT_USER\Software\Adaptive Insights` | The current user only |

## Configuration file format

Create an XML configuration file with your tenant details:

```xml
<connections>
  <connection name="Adaptive Planning - Production">
    <Type>adaptiveplanning</Type>
    <WorkdayAuthorizationUrl>https://example.myworkday.com/prodtenant/authorize</WorkdayAuthorizationUrl>
    <WorkdayRestApiUrl>https://example.myworkday.com/ccx/api/v1/prodtenant</WorkdayRestApiUrl>
    <WorkdayClientId>YOUR_CLIENT_ID_HERE</WorkdayClientId>
  </connection>
  <connection name="Adaptive Planning - Sandbox">
    <Type>adaptiveplanning</Type>
    <WorkdayAuthorizationUrl>https://example.myworkday.com/sandboxtenant/authorize</WorkdayAuthorizationUrl>
    <WorkdayRestApiUrl>https://example.myworkday.com/ccx/api/v1/sandboxtenant</WorkdayRestApiUrl>
    <WorkdayClientId>YOUR_SANDBOX_CLIENT_ID_HERE</WorkdayClientId>
  </connection>
</connections>
```

For Workday Financial Management (Financials) connections, use `<Type>financials</Type>`.

## Deployment steps

{{< step n="1" title="Add the registry key" >}}
In the desired registry hive, create the key:
`Software\Adaptive Insights\Connections`
{{< /step >}}

{{< step n="2" title="Deploy using your preferred method" >}}
Add the XML configuration using any standard deployment method:
- **Group Policy** — create a GPO that writes the registry key on login
- **PowerShell script** — push via Intune or SCCM
- **Registry .reg file** — import on each machine

Example PowerShell snippet:
```powershell
$regPath = "HKLM:\Software\Adaptive Insights\Connections"
New-Item -Path $regPath -Force
Set-ItemProperty -Path $regPath -Name "Config" -Value (Get-Content connections.xml -Raw)
```
{{< /step >}}

{{< step n="3" title="Verify on a test machine" >}}
Open Excel on a test machine. Click **Log In** in the OfficeConnect tab. Your deployed tenant names should appear in the sign-in drop-down without the user needing to enter any details.
{{< /step >}}

## Note on authentication URLs

Authorization URLs and API endpoint URLs vary based on your Workday data center location. Get the exact URLs from your Workday Security Administrator or from the OfficeConnect API client in Workday — see [Set Up Workday SSO](/get-started/admin/configure/workday-sso/).

## Next steps

- [Install for Admins](/get-started/install-admin/) — the install side of the same rollout.
- [Set Up Workday SSO](/get-started/admin/configure/workday-sso/) — get the API client values you'll deploy.
- [Sign In & Create a Tenant](/get-started/admin/configure/sign-in-create-tenant/) — what your users will see after registry deploy.
