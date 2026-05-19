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

1. **Wait 60-90 seconds, then retry.** Most server-side locks clear in under a minute.
2. **Check with your Adaptive admin** whether a long-running job is in flight.
3. **Avoid the busiest hour.** Many organizations peak in the first hour of the workday or just before month-end close. Schedule large refreshes outside the peak.

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

1. **Split the refresh.** Refresh one sheet at a time via Sheet Properties → **Refresh this sheet only**, instead of the workbook-wide Refresh.
2. **Reduce formula count.** Use rollup accounts, consolidate time elements, scope by Level. See [Optimize Performance](/get-started/performance/optimize-performance/).
3. **Check for repeating rows that exploded.** A misconfigured repeating range can generate thousands of unintended formulas. See [Repeating Reports](/get-started/build-reports/repeating-reports/).

### 5. Add-in conflict (think-cell, Bloomberg, Power Pivot, Macabacus)

In rare cases, another add-in's hooks into Excel cause OfficeConnect's refresh to fail mid-query. The think-cell conflict is the most documented one (see think-cell KB0231).

**Fix:**

1. **Test in Safe Mode.** Hold Ctrl while clicking Excel to start in Safe Mode. If refresh succeeds, an add-in conflict is the cause.
2. **Disable add-ins one at a time** to identify the culprit.
3. **Apply the documented workaround** — for think-cell, see *Troubleshoot → think-cell Conflict* (coming soon).

## When to actually contact technical support

If you've worked through all five causes above and refresh still fails:

1. **Capture an OfficeConnect log file.** See *Troubleshoot → Capturing Logs* (coming soon) for the procedure.
2. **Note the time of the failure** so Workday support can correlate to server-side events.
3. **Include a sample workbook** that reproduces the failure (anonymize sensitive data first).

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
