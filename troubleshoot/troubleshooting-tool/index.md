# Run the Troubleshooting Tool

How to use the OCSystemChecker tool to generate a diagnostic log for Workday Support.


---


When standard troubleshooting steps don't resolve your issue, the **OCSystemChecker** tool gathers detailed diagnostic information from your machine to help Workday Support investigate.

## When to use it

- You're getting an error during installation or startup that other fixes haven't resolved
- Workday Support asks you to run the tool as part of a support case
- You want a diagnostic log before reaching out to Support

## Steps

{{< step n="1" title="Download OCSystemChecker.zip" >}}
Download the `OCSystemChecker.zip` file from the Workday Community or ask your Workday Support contact for the link. Save it to your Desktop.
{{< /step >}}

{{< step n="2" title="Extract the zip file" >}}
Right-click `OCSystemChecker.zip` → **Extract All**. Open the extracted folder.
{{< /step >}}

{{< step n="3" title="Launch OCSystemChecker.exe" >}}
Double-click `OCSystemChecker.exe`. Windows may prompt you to allow it to run — click **Yes**.
{{< /step >}}

{{< step n="4" title="Select the application with the error" >}}
Choose **OfficeConnect for Excel** (or the appropriate application) and click **Next**.
{{< /step >}}

{{< step n="5" title="Select the type of issue" >}}
Choose the closest match (installation error, refresh error, startup error, etc.). If it's file-specific, attach the problematic file when prompted. Click **Next**.
{{< /step >}}

{{< step n="6" title="Reproduce the error on the 'Re-create Issue' page" >}}
**Important:** While the Re-create Issue page is open, perform the action that causes the error. For example:
- If the error happens when installing, run the installer now
- If the error happens when refreshing a file, open and refresh the file now

Then click **Next**.
{{< /step >}}

{{< step n="7" title="Finish and find your log file" >}}
Click **Finish**. Your Temp folder opens automatically, containing a file named `AdaptiveEnvironmentInfoPackage`.
{{< /step >}}

{{< step n="8" title="Send the log to Support" >}}
Attach `AdaptiveEnvironmentInfoPackage` to your active support ticket in the Workday Customer Center.
{{< /step >}}
