---
title: "Workday OfficeConnect Refresh Time Benchmarks"
linkTitle: "Refresh Benchmarks"
weight: 20
description: >
  Rough benchmarks for what a normal Workday OfficeConnect refresh should take by formula count, what moves the numbers, and how to measure your own workbooks.
tags: ["performance", "fpna", "system-admin", "reference"]
---

"Is my workbook slow?" is a question with no universal answer — refresh time depends on formula count, server load, network path, and how complex your Adaptive Planning model is. This reference gives you rough Workday OfficeConnect benchmarks to compare against, and a method for measuring your own.

**What you'll need:**
- A Workday OfficeConnect workbook you can refresh end-to-end
- A stopwatch (your phone is fine) or the Excel status bar

---

## Benchmark table

The numbers below assume a healthy Adaptive Planning tenant, a wired or strong wireless network, and 64-bit Excel. Cut the workbook into one of these buckets by counting OfficeConnect formulas (Reporting pane → **Review** tab → **Workbook Elements** count).

| OfficeConnect formulas | Expected refresh | What "slow" looks like |
|---|---|---|
| Under 50 | Under 5 seconds | Over 10 seconds |
| 50–200 | 5–10 seconds | Over 20 seconds |
| 200–500 | 10–30 seconds | Over 60 seconds |
| 500–1,000 | 30–60 seconds | Over 2 minutes |
| 1,000+ | 1+ minute | Over 5 minutes |

A workbook in the "slow" column isn't necessarily broken — it might be running against a heavily-loaded tenant or pulling unusually complex modeled accounts — but it's almost always optimizable.

{{< tip >}}
Repeating rows count as a single element regardless of how many rows they expand into on refresh. A 200-row report built from one repeating element behaves like a 1-formula workbook, not a 200-formula one. See [Large Repeating Reports](/performance/large-repeating-reports/).
{{< /tip >}}

## Factors that move the benchmark

Even within the right formula bucket, several variables shift expected refresh time:

- **Tenant load.** Peak budget season (typically Q4 and Q1) and end-of-month close can double or triple response times. The same workbook can refresh in 8 seconds at 7 a.m. and 25 seconds at 2 p.m.
- **Network path.** A corporate VPN routing through a distant data center adds latency to every server call. A 100-formula workbook on direct internet may take 6 seconds; the same workbook over VPN can take 20.
- **Model complexity.** Modeled (calculated) accounts cascade through formulas server-side before returning a value. A report pulling 50 modeled accounts is meaningfully slower than 50 input accounts.
- **Time granularity.** Monthly columns make 12x the server calls of annual columns covering the same year, all else equal.
- **Level scope.** Pulling all 200 cost centers is slower than pulling one division, even when the cells aggregate to the same number.

## How to measure your own refresh time

{{< step n="1" title="Close other heavy applications" >}}
Quit anything pulling on the same network or pegging CPU — Teams calls, large downloads, other Excel workbooks mid-refresh. You want a clean baseline.
{{< /step >}}

{{< step n="2" title="Open the workbook and let Excel settle" >}}
Wait 5 seconds after the file finishes opening so Excel's own recalculation doesn't get counted in your refresh time.
{{< /step >}}

{{< step n="3" title="Start the stopwatch and click Refresh" >}}
Click **Refresh** in the OfficeConnect ribbon and start the stopwatch in the same moment. Watch the Excel status bar — most refresh progress is reflected there.
{{< /step >}}

{{< step n="4" title="Stop when the status bar clears" >}}
The refresh is complete when the status bar returns to **Ready** and the Refresh button is no longer greyed out. Record the time.
{{< /step >}}

{{< step n="5" title="Repeat twice more and average" >}}
The first refresh of a session is often slower (cold cache). Run two more and average all three for a representative number.
{{< /step >}}

{{< admin-note >}}
For workbooks shared across a team, ask 2-3 planners to run the same three-refresh measurement from their own desks and share the numbers. A wide spread (e.g., 8 seconds in one office, 45 in another) almost always indicates a network or VPN difference rather than a workbook problem. Centralizing those workbooks on SharePoint or OneDrive doesn't fix the underlying network path.
{{< /admin-note >}}

## When to take action

Apply the rule of thumb: if your measured time is more than **2x** the benchmark for your formula bucket, optimize. If it's within the bucket, accept it — further tuning has diminishing returns and risks breaking the report.

If it's far outside the bucket (10x+) and you've ruled out network and tenant load, something specific is wrong: an oversized hidden range, a runaway repeating row, or a modeled-account explosion. Use Cell Explorer to find which cells are taking the longest.

## Result

You have a defensible answer to "is this workbook slow?" — measured against a benchmark, not a feeling — and a triage path for what to do next.

## Next steps

- [Optimize Performance for Large Models](/performance/optimize-performance/) — the canonical tuning checklist once you've decided action is warranted.
- [Reduce OfficeConnect Element Count](/performance/reduce-element-count/) — the single biggest lever, in detail.
- [Fix Slow Performance in Large Reports](/troubleshoot/slow-performance/) — diagnostic walkthrough when refresh is far outside the benchmark.
