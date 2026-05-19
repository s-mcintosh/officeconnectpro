---
title: "Refreshing All Slides Safely in a Workday OfficeConnect PowerPoint Deck"
linkTitle: "Refresh All Slides"
weight: 30
description: >
  The disciplined refresh workflow that keeps Workday OfficeConnect PowerPoint decks consistent — never a deck with mixed-period numbers.
tags: ["sharing", "fp-and-a", "how-to"]
---

The single failure mode that destroys a board-pack workflow is shipping a deck where some slides have current numbers and others have last month's. Recipients lose trust in every number on every page. This article documents the refresh discipline that prevents it.

If you're still building your first linked deck, start with [OfficeConnect for PowerPoint](/word-powerpoint/powerpoint/officeconnect-for-powerpoint/) and [Designing a Board Pack Template](/word-powerpoint/powerpoint/board-pack-template/).

## The refresh order rule

Always refresh in this order:

1. **Excel** — open the source workbook, click OfficeConnect → **Refresh**, wait for completion, save and close
2. **PowerPoint** — open the deck, click OfficeConnect → **Refresh Links**, wait for completion, save and close

Doing PowerPoint first pulls whatever is currently in the Excel file, which may be last month's data if Excel wasn't refreshed.

## Step 1 — Refresh Excel first

{{< step n="1" title="Open the source workbook" >}}
Open the Excel workbook that backs the deck. Confirm it's the right one — check the filename and time period in the workbook's metadata.
{{< /step >}}

{{< step n="2" title="Update period elements if needed" >}}
If you're producing the deck for a new month, update the Time elements first (e.g., change *Mar 2026* to *Apr 2026*). If you're using relative dates like *Current Period*, no edit is needed — refresh will roll forward automatically.
{{< /step >}}

{{< step n="3" title="Click Refresh and wait for completion" >}}
Click the OfficeConnect ribbon **Refresh**. Wait until the status bar shows refresh complete — don't start clicking around prematurely.
{{< /step >}}

{{< step n="4" title="Spot-check key numbers" >}}
Eyeball revenue, EBITDA, and headcount. If anything looks off (sign flip, wrong magnitude), debug in Excel before opening PowerPoint.
{{< /step >}}

{{< step n="5" title="Save and close" >}}
Save the workbook. Close it. (Leaving it open during PowerPoint refresh is technically fine but adds risk of accidental edits.)
{{< /step >}}

## Step 2 — Refresh PowerPoint

{{< step n="6" title="Open the deck" >}}
Open the PowerPoint deck. Wait for OfficeConnect to detect the linked workbook.
{{< /step >}}

{{< step n="7" title="Refresh Links" >}}
OfficeConnect ribbon → **Refresh Links**. Every linked table and chart updates from the Excel source. This takes 10-60 seconds depending on the number of linked elements.
{{< /step >}}

{{< step n="8" title="Watch for refresh errors" >}}
If a link fails to refresh, PowerPoint flags it. Common causes: the workbook moved, was renamed, or a named range was deleted. See [Recovering Broken Links](/word-powerpoint/powerpoint/recovering-broken-links/).
{{< /step >}}

## Step 3 — Visual scan every slide

This is the step everyone skips and everyone regrets.

{{< step n="9" title="Click through every slide" >}}
Go to slide 1 and use the right-arrow key to step through the whole deck. On each slide, check:

- The time period in headers and titles is correct
- Numbers are in the expected ranges
- Charts are populated (no blank chart frames)
- Tables don't show `n/a` or `#REF` placeholders
{{< /step >}}

{{< step n="10" title="Spot-check three numbers against Excel" >}}
Pick three numbers on different slides and verify they match the Excel workbook. If they don't, a refresh didn't propagate — return to Step 6.
{{< /step >}}

## Step 4 — Lock the deck before distribution

{{< step n="11" title="Break links for the distributed copy (optional)" >}}
For the version you actually email or post, you may want to break links so recipients can't accidentally refresh and pull future data. See [Recovering Broken Links](/word-powerpoint/powerpoint/recovering-broken-links/) for the break-link procedure.

Keep the live version with intact links in your team's working folder for next month.
{{< /step >}}

{{< tip >}}
A cleaner pattern: maintain the live linked deck as `BoardPack_Apr2026_LIVE.pptx` and ship a static copy as `BoardPack_Apr2026.pptx` with links broken. Naming makes the difference obvious.
{{< /tip >}}

## What to do if refresh fails mid-deck

If PowerPoint shows some slides refreshed and others didn't:

1. **Don't save yet** — preserve your ability to undo
2. Run **Refresh Links** again — most transient failures clear on retry
3. If a specific slide consistently fails, check the linked named range in the Excel source (it may have been renamed or deleted)
4. See [Recovering Broken Links](/word-powerpoint/powerpoint/recovering-broken-links/) for the link-repair procedure

## Common refresh-day mistakes

| Mistake | Consequence | Fix |
|---|---|---|
| Refresh PowerPoint without refreshing Excel first | Deck shows last period's data | Refresh in the right order |
| Refresh only the "problem" slide | Mixed-period deck | Always refresh-all, never partial |
| Skip the visual scan | Ship a broken slide | Build the scan into your checklist |
| Refresh into the master template | Pollute the template for next month | Always copy template to a dated file first |
| Save the linked deck without breaking links for distribution | Recipients may unintentionally refresh and see unfinalized data | Break links on the distributed copy |

## Result

Every deck you ship has a consistent point-in-time view of the data, with no mixed-period surprises and a documented procedure your team can follow in 10 minutes a month.

## Next steps

- [Designing a Board Pack Template](/word-powerpoint/powerpoint/board-pack-template/) — the upstream template design that makes refresh easy.
- [Recovering Broken Links](/word-powerpoint/powerpoint/recovering-broken-links/) — when refresh doesn't go smoothly.
- [Charts That Update with the Period](/word-powerpoint/powerpoint/period-aware-charts/) — the chart-side of period-aware design.
