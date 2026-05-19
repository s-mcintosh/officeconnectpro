---
title: Performance & Optimization
linkTitle: Performance
weight: 55
type: docs
description: 'Make Workday OfficeConnect reports fast — refresh-time benchmarks, 32-bit
  vs 64-bit Excel, element-count tradeoffs, and large-workbook patterns.

  '
cascade:
  type: docs
tags:
- performance
- fpna
- system-admin
- reference
---

A slow OfficeConnect report is usually a design problem, not a product limitation. These guides cover refresh benchmarks, the 32-bit vs 64-bit Excel decision, element-count reduction, and patterns for very large workbooks.

## Articles in this section

- [Optimize Performance](/performance/optimize-performance/) — Speed up Workday OfficeConnect reports that are slow to refresh — reduce formula count, use efficient time contexts, and configure workbook settings for large Adaptive Planning models
- [Refresh Benchmarks](/performance/refresh-benchmarks/) — Rough benchmarks for what a normal Workday OfficeConnect refresh should take by formula count, what moves the numbers, and how to measure your own workbooks
- [32-bit vs 64-bit Excel](/performance/32-vs-64-bit/) — Why 64-bit Excel matters for large Workday OfficeConnect workbooks, how to check which version you're running, and how to switch without breaking other add-ins
- [Reduce Element Count](/performance/reduce-element-count/) — Element count is the single biggest performance lever in Workday OfficeConnect — five concrete tactics to cut it without losing the report you need
- [Large Repeating Reports](/performance/large-repeating-reports/) — Patterns and pitfalls for Workday OfficeConnect reports that use repeating rows to generate hundreds of lines from a single element
