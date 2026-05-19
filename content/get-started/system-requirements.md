---
title: "System Requirements"
linkTitle: "System Requirements"
weight: 3
description: >
  Hardware and software prerequisites before installing OfficeConnect.
tags: ["deployment", "system-admin", "reference"]
---

Verify your machine meets these requirements before installing OfficeConnect.

## Required software

All of the following must be installed before running the OfficeConnect installer:

| Software | Notes |
|---|---|
| **WebView2 Runtime** | Required for the OfficeConnect sign-in UI |
| **Microsoft .NET Framework 4.8** | [Download from Microsoft](https://dotnet.microsoft.com/download/dotnet-framework/net48) |
| **VSTO 2010** | Visual Studio Tools for Office runtime |
| **Workday Event Log Components** | Installed by the OfficeConnect setup wizard if you have admin rights |

> **Tip:** If you have administrator rights on your machine, the per-user installer handles prerequisites automatically. If you don't, ask your IT team to install these before you run OfficeConnect setup.

## Microsoft Office

- Microsoft Office (Excel, Word, PowerPoint) — 32-bit or 64-bit
- Office 365, Office 2016, Office 2019, or Office 2021 are all supported
- For large reports with many Show Details rows, 64-bit Excel is recommended for performance

## Operating system

- Windows 10 or Windows 11
- OfficeConnect is a Windows-only application

## Network

- HTTPS access to your Workday Adaptive Planning instance
- If your organization uses a proxy or network filtering, work with IT to allowlist the Workday API endpoints

## Next steps

→ [Install OfficeConnect as an End User](/get-started/install-end-user/) if you're setting up your own machine.

→ [Install OfficeConnect as an IT Admin](/get-started/install-admin/) if you're deploying to multiple users.
