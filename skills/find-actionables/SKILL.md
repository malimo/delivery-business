---
name: find-actionables
description: Read the unified daily dataset and write a short, specific action list for each outlet, city and region, ranked by impact.
---

# Find actionables

Use this after `normalize-partner-data` has run for the day.

## Before you start
1. Read `business-context/` (made by `setup-delivery-harness`). If the folder doesn't exist, say so and offer to run the setup interview first.
2. If something this skill needs is missing or marked `TODO`, ask the user for it, **one question at a time**, with a suggested default where it helps. Save each answer to the right file in `business-context/` after the user confirms it.
3. Never invent a business rule, threshold, definition or play. If the user doesn't know, record `TODO` and work without it, saying what you left out.

This skill needs: `metrics.md` (which comparisons to trust), `thresholds.md`, `playbook.md`, and optionally `plan.csv`.

If `playbook.md` is empty, don't make one up. Ask: "When [flag] happens, what does your team do today, who does it, and by when?" for each flag type you are about to report, and save the answers as plays.

## Inputs
- `data/unified/`: the standard dataset.
- `business-context/`: thresholds, playbook, plan, and who reads the output.

## Steps
1. For each outlet, run the comparisons the user chose in `metrics.md`, and compare with `plan.csv` where it has a line.
2. Flag only changes that cross a threshold in `thresholds.md`.
3. For each flag, find the likely cause in the data (which source, which metric, which days), then pick the matching action from `playbook.md`. If no play fits, say so; don't invent one.
4. Rank actions by expected impact (sales at stake or complaints affected). Keep at most 3 actions per outlet unless the user set a different number.
5. Write one list per outlet, and a roll-up per city and region, in plain language the people named in `business.md` can act on today. Route each list as set in `routines.md`.
6. Every action shows the number behind it, so a person can check it.

## Output format (per outlet)
```
Outlet: [name] ([city])
1. [Action] — because [metric] went from [a] to [b] on [source] since [date].
2. ...
```

## Learn from corrections
When the user corrects an output ("that's not how we define sales", "we never discount on weekends"), propose the exact change to the matching file in `business-context/` and save it only after they agree. Log it in `business-context/changelog.md`.
