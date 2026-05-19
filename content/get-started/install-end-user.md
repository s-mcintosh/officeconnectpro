---
title: "Install as an End User"
linkTitle: "Install (End User)"
weight: 4
description: >
  Install OfficeConnect on your own machine without requiring IT involvement.
tags: ["deployment", "fp-and-a", "tutorial"]
---

Follow these steps to install OfficeConnect on your own Windows machine. You'll need administrator rights, or IT must pre-install the prerequisites.

## Prerequisites

- All [system requirements](/get-started/system-requirements/) are met
- You have your Workday Adaptive Planning login credentials

## Steps

{{< step n="1" title="Download the installer" >}}
Go to **Product Downloads** in your Workday Adaptive Planning instance (ask your admin for the link if you don't have it). Download **OfficeConnectSetup.exe** — always use the latest version.
{{< /step >}}

{{< step n="2" title="Run the installer" >}}
Double-click `OfficeConnectSetup.exe`. If you have administrator rights on your machine, Windows will prompt you to allow the installation to run elevated — click **Yes**.

If you don't have admin rights, the installer will stop and tell you to contact IT. In that case, see [Install as an IT Admin](/get-started/install-admin/).
{{< /step >}}

{{< step n="3" title="Complete the setup wizard" >}}
Follow the on-screen prompts. The installer will:
- Install any missing prerequisites (WebView2, .NET 4.8, VSTO 2010, Workday Event Log Components)
- Install the OfficeConnect add-in for Excel, Word, and PowerPoint
{{< /step >}}

{{< step n="4" title="Verify the installation" >}}
Open Microsoft Excel. You should see an **OfficeConnect** tab in the ribbon between the regular Excel tabs.

Open Word and PowerPoint to verify the tab also appears there.
{{< /step >}}

{{< figure src="/images/screenshots/oc-ribbon-tab.png" alt="The OfficeConnect tab in the Excel ribbon" caption="The OfficeConnect tab confirms successful installation. If it doesn't appear, see Troubleshooting below." >}}

## Result

The OfficeConnect tab appears in Excel, Word, and PowerPoint. You're ready to [sign in and create your first tenant](/admin/configure/sign-in-create-tenant/).

## Troubleshooting

If the OfficeConnect tab doesn't appear after installation, see [Task Pane Not Displaying Correctly](/troubleshoot/task-pane-not-displaying/) or [Fix COM Registration Errors](/troubleshoot/com-registration-error/).

## Next steps

→ [Sign in and create your first tenant](/admin/configure/sign-in-create-tenant/)
