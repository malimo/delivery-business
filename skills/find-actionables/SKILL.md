---
name: find-actionables
description: Read the unified daily dataset and write a short, specific action list for each outlet, city and region, ranked by impact.
---

# Find actionables

Use this after `normalize-partner-data` has run for the day.

## Inputs
- `data/unified/`: the standard dataset.
- `targets.csv`: optional targets per outlet and metric.
- `playbook.md`: what your team does about each kind of problem (for example "rating below 4.0: check the last 20 complaints and brief the outlet manager"). Write this with the people who will act on it.

## Steps
1. For each outlet, compare the last 7 days with the 4 weeks before, and with target where one exists.
2. Flag only changes that matter. Default rules (edit for your business):
   - funnel conversion (views → cart → order) down more than [10]%
   - complaints up more than [20]%, or rating down more than [0.2]
   - ad spend up while ad-attributed sales are flat or down
   - sales growth below the city average by more than [x]%
3. For each flag, find the likely cause in the data (which source, which metric, which days), then pick the matching action from `playbook.md`. If no play fits, say so; don't invent one.
4. Rank actions by expected impact (sales at stake or complaints affected). Keep at most [3] actions per outlet.
5. Write one list per outlet, and a roll-up per city and region, in plain language a store manager can act on today.
6. Every action shows the number behind it, so a person can check it.

## Output format (per outlet)
```
Outlet: [name] ([city])
1. [Action] — because [metric] went from [a] to [b] on [source] since [date].
2. ...
```
