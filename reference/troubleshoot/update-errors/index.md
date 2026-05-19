---
title: "Resolve OfficeConnect Update Errors"
url: "https://officeconnectpro.com/reference/troubleshoot/update-errors/"
description: "How to fix errors that occur when updating OfficeConnect to a new version.\n"
tags: ["upgrade","deployment","system-admin","fpna","troubleshoot"]
date: "0001-01-01"
lastmod: "2026-05-19"
---


**Symptom:** When updating OfficeConnect, you see:

```
An error occurred while downloading the update. Details: The underlying connection
was closed: An unexpected error occurred on a send.
```

## Common causes and fixes

### Cause 1: Network or proxy blocking the update

Your corporate network or proxy may be blocking the update download.

**Fix:** Work with your IT team to allowlist the Workday update servers. Alternatively, download the latest installer manually from **Product Downloads** in Workday and install it directly — bypassing the auto-update.

### Cause 2: TLS version too old (Windows 7)

If you're on Windows 7, your system may be using TLS 1.0 or 1.1. Workday dropped support for these between 2017 and 2019.

**Fix:** Work with IT to enable TLS 1.2 as the default on Windows 7 (see Microsoft's documentation for instructions). Or upgrade to Windows 10/11.

### Cause 3: Corrupted installation

Sometimes a partial update leaves OfficeConnect in a broken state.

**Fix:**

{{< step n="1" title="Uninstall OfficeConnect" >}}
Go to **Start → Settings → Apps & Features**, find **OfficeConnect**, and click **Uninstall**.
{{< /step >}}

{{< step n="2" title="Download the latest installer" >}}
Get the current `OfficeConnectSetup.exe` from **Product Downloads** in your Workday Adaptive Planning instance.
{{< /step >}}

{{< step n="3" title="Run the installer" >}}
Install fresh. This eliminates any partial-update state.
{{< /step >}}

## Still stuck?

Run the [Troubleshooting Tool](/reference/troubleshoot/troubleshooting-tool/) to generate a diagnostic log and send it to Workday Support.

