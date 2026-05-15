---
title: "Work with Multiple Instances"
linkTitle: "Multiple Instances"
weight: 2
description: >
  How to switch between production, sandbox, and multi-instances in OfficeConnect.
---

If your user ID has access to more than one Workday instance — a sandbox, a linked multi-instance hierarchy, or simply multiple tenants — OfficeConnect handles them through an **Instance** drop-down in the Reporting and Planning panes.

## Types of multiple instances

| Type | Description |
|---|---|
| **Sandbox** | A clone of your production instance. Use it for testing reports and what-if scenarios without affecting live data. |
| **Multi-instances** | Linked instances in a hierarchical relationship that share data through account and dimension mapping. |

## Switching instances

When your user ID has access to multiple instances, an **Instance** drop-down appears in the Reporting pane.

- The drop-down defaults to your default instance
- Select a different instance to load elements from that instance
- Once you add any elements to a worksheet, **the instance locks** for that workbook

## Key rules

| Scenario | Behavior |
|---|---|
| New workbook | Default instance selected; you can switch before adding elements |
| Existing workbook | Instance is locked — it already has elements from a specific instance |
| Multiple open workbooks | You can open workbooks connected to different instances simultaneously |
| Copy/paste between instances | Not supported — you cannot copy, cut, paste, or merge data across instances |

## Changing instance mid-session

If you're working locally in an Excel report for Instance A and then sign in to Instance B, OfficeConnect will prompt you:

> *"Log in to OfficeConnect — would you like to update this Excel report to work with the current instance?"*

If you click **No**, the file closes and unsaved changes are lost. Save your work before switching instances.

## Change your default instance

1. Click **User Settings** from the OfficeConnect ribbon
2. In the **Connection** section, select your preferred default instance
3. Click **OK**

The new default applies to all new workbooks you create.
