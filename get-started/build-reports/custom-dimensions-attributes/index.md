# Work with Custom Dimensions and Attributes in OfficeConnect

Report on custom dimensions and attributes defined in your Adaptive Planning model — filter by product line, region, project, or any other custom segment your team uses.


---


Adaptive Planning models often include custom dimensions beyond the standard account and level hierarchy — things like Product Line, Region, Project Code, or Customer Segment. OfficeConnect exposes these as **Custom Dimensions** in the Reporting pane, letting you filter and report on any segment your model defines.

**What you'll need:**
- OfficeConnect connected to an Adaptive Planning model that includes custom dimensions
- Familiarity with building basic reports — see [Budget vs. Actuals Variance](/get-started/build-reports/budget-vs-actuals-variance/)

---

## 1. Find your custom dimensions in the Reporting pane

1. Open the OfficeConnect Reporting pane. Scroll down past Accounts, Versions, Time, and Levels to find the **Custom Dimensions** section (it may also appear as **Dimensions** depending on your OfficeConnect version).
2. Expand **Custom Dimensions** to see the dimensions your model administrator has defined. Each dimension has members — for example, a "Region" dimension might have members: North America, EMEA, APAC.

> **Note:** Custom dimensions are model-specific. If you don't see a **Custom Dimensions** section, your model may not have any configured. Contact your Adaptive Planning model administrator to confirm.

## 2. Add a custom dimension filter to a report

3. Build a basic report with account rows, a version header, and a time context — see [Budget vs. Actuals Variance](/get-started/build-reports/budget-vs-actuals-variance/) for a walkthrough.
4. To filter the entire report by a single dimension member (for example, show only North America figures): In the Reporting pane, expand **Custom Dimensions → Region** and drag the **North America** member into any blank cell in the header area of your report (for example, E1). OfficeConnect adds a filter element — this restricts all formulas in the workbook to that member of the dimension.
5. Click **Refresh**. All data cells update to show values scoped to North America only.

## 3. Build a multi-column report across dimension members

6. To compare multiple dimension members side by side — one column per region, for example — place each member in a separate column header:
   - Drag **North America** into **B1**
   - Drag **EMEA** into **C1**
   - Drag **APAC** into **D1**
7. Add the version in a row above (or incorporate it directly into the formula by keeping a version element in the workbook). Add a time context in row 2.
8. In **B3**, OfficeConnect creates a formula referencing the account in A3, the version, the time in B2, and the North America member in B1. Copy across to C3 and D3 — each resolves to the correct region automatically.
9. Click **Refresh** to populate all columns.

## 4. Use attributes to filter within a dimension

10. Some Adaptive Planning models use **Attributes** — metadata attached to dimension members (for example, attaching a "Business Unit" attribute to each Region member). In the Reporting pane, look for an **Attributes** section under the relevant dimension.
11. Drag an attribute value into your report header to filter by it. This works the same way as a dimension member — OfficeConnect includes all members that have that attribute value.

## 5. Remove a dimension filter

12. To remove a filter, click the cell containing the dimension element and press **Delete**. Click **Refresh** — the report reverts to returning values across all members of that dimension (unfiltered).

---

## Related links

- [Budget vs. Actuals Variance](/get-started/build-reports/budget-vs-actuals-variance/)
- [Set Up Scenario Comparison](/get-started/build-reports/scenario-comparison/)
- [Build a Department P&L Report](/get-started/build-reports/department-pl-report/)
