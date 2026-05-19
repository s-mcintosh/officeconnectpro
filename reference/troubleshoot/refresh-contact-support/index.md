# Why Your Refresh Shows 'Contact Technical Support'

The vague "Refresh failed — contact technical support" dialog in Workday OfficeConnect almost always has one of five concrete causes. Diagnose and fix.


---


You click **Refresh** in Workday OfficeConnect. After 5-30 seconds, a dialog appears:

> *"Refresh failed. Please contact technical support."*

The dialog is famously unhelpful — it doesn't say what went wrong. In practice, almost every instance of this error has one of five concrete causes. Work through them in order.

## What you'll see

- Excel freezes briefly during refresh
- A modal dialog appears: *"Refresh failed. Please contact technical support."*
- After dismissing, your OfficeConnect cells either show stale values or `n/a`
- No error code is shown
- The Excel status bar may briefly show an OfficeConnect error before the dialog appears

## Root causes (in order of frequency)

### 1. Your session has timed out

By far the most common cause. After 60 minutes of inactivity (or your tenant's configured timeout), OfficeConnect's token expires. The next refresh fails with this generic dialog instead of a clear "session expired" message.

**Fix:**

{{< step n="1" title="Sign out, then sign back in" >}}
In the OfficeConnect ribbon, click **Log Out** (or **Sign Out**). Then click **Log In** and re-authenticate.
{{< /step >}}

{{< step n="2" title="Click Refresh again" >}}
If a stale session was the cause, refresh now succeeds.
{{< /step >}}

If sign-in itself fails, see [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/).

### 2. The Adaptive Planning server is locked or under load

If too many users are running large reports at once, or if a tenant-level job (import, allocation run, version copy) holds a lock, refresh requests can fail with this generic error.

**Fix:**

{{< step n="1" title="Wait 60-90 seconds, then retry" >}}
Most server-side locks clear in under a minute. Click **Refresh** again after waiting.
{{< /step >}}

{{< step n="2" title="Check with your Adaptive admin" >}}
Confirm whether a long-running job (import, allocation run, version copy) is currently in flight.
{{< /step >}}

{{< step n="3" title="Avoid the busiest hour" >}}
Many organizations peak in the first hour of the workday or just before month-end close. Schedule large refreshes outside the peak.
{{< /step >}}

### 3. A workbook element references something that no longer exists

If an account, version, or level referenced in your formulas was deleted or renamed in Adaptive Planning since the workbook was last opened, OfficeConnect can fail the refresh with this generic error rather than per-cell.

**Fix:**

{{< step n="3" title="Check the Review tab of the Reporting pane" >}}
In the Reporting pane, click the **Review** tab. It shows every element used in the workbook. Look for any flagged as missing or unresolved.
{{< /step >}}

{{< step n="4" title="Replace or remove broken elements" >}}
For each missing element, either remove it from the workbook or replace it with the renamed equivalent. See [Review Applied Elements](/get-started/build-reports/review-applied-elements/).
{{< /step >}}

### 4. Workbook is too large; the refresh times out

Some refreshes fail because the underlying query exceeds OfficeConnect's timeout — typically on workbooks with hundreds of formulas hitting a large Adaptive Planning model.

**Fix:**

{{< step n="1" title="Split the refresh" >}}
Refresh one sheet at a time via Sheet Properties → **Refresh this sheet only**, instead of the workbook-wide Refresh.
{{< /step >}}

{{< step n="2" title="Reduce formula count" >}}
Use rollup accounts, consolidate time elements, and scope by Level to cut the number of server calls. See [Optimize Performance](/get-started/performance/optimize-performance/).
{{< /step >}}

{{< step n="3" title="Check for repeating rows that exploded" >}}
A misconfigured repeating range can generate thousands of unintended formulas. See [Repeating Reports](/get-started/build-reports/repeating-reports/).
{{< /step >}}

### 5. Add-in conflict (think-cell, Bloomberg, Power Pivot, Macabacus)

In rare cases, another add-in's hooks into Excel cause OfficeConnect's refresh to fail mid-query. The think-cell conflict is the most documented one (see think-cell KB0231).

**Fix:**

{{< step n="1" title="Test in Safe Mode" >}}
Hold Ctrl while clicking Excel to start in Safe Mode. If refresh succeeds, an add-in conflict is the cause.
{{< /step >}}

{{< step n="2" title="Disable add-ins one at a time to identify the culprit" >}}
In File → Options → Add-ins, disable each add-in individually and test refresh after each.
{{< /step >}}

{{< step n="3" title="Apply the documented workaround" >}}
For think-cell, see [think-cell Conflict](/reference/troubleshoot/think-cell-conflict/) for the load-order fix.
{{< /step >}}

## When to actually contact technical support

If you've worked through all five causes above and refresh still fails:

{{< step n="1" title="Capture an OfficeConnect log file" >}}
See *Troubleshoot → Capturing Logs* (coming soon) for the procedure.
{{< /step >}}

{{< step n="2" title="Note the time of the failure" >}}
Record the exact time refresh failed so Workday support can correlate it to server-side events.
{{< /step >}}

{{< step n="3" title="Include a sample workbook that reproduces the failure" >}}
Attach the workbook to the support ticket — anonymize any sensitive data first.
{{< /step >}}

A well-prepared support ticket with logs, timing, and a repro typically resolves in 1-2 days; without those, it can drag for weeks.

## Prevention

- **Treat session timeout as inevitable.** Build the habit of re-signing-in at the start of any work session over an hour old.
- **Manage workbook size.** Keep formula counts under a few hundred per workbook; split larger reports across multiple files.
- **Coordinate with your Adaptive admin** on long-running jobs that affect tenant lock behavior.

## Result

You'll resolve "Contact technical support" in seconds instead of opening a Workday support ticket every time. And when you do open a ticket, it'll close fast.

## Next steps

- [Authentication Token Errors](/reference/troubleshoot/authentication-token-errors/) — the related token-side issues.
- [Not Refreshing](/reference/troubleshoot/not-refreshing/) — when Refresh doesn't fail but produces no update.
- [Optimize Performance](/get-started/performance/optimize-performance/) — fix the workbook-size variant.
