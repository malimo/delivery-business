---
name: aop-tracker
description: Compare month-to-date actuals with the annual operating plan (AOP) by channel, city and region, project the month-end gap and suggest interventions.
---

# AOP tracker

## Before you start
1. Read `business-context/` (made by `setup-delivery-harness`). If the folder doesn't exist, say so and offer to run the setup interview first.
2. If something this skill needs is missing or marked `TODO`, ask the user for it, **one question at a time**, with a suggested default where it helps. Save each answer to the right file in `business-context/` after the user confirms it.
3. Never invent a business rule, threshold, definition or play. If the user doesn't know, record `TODO` and work without it, saying what you left out.

This skill needs: `plan.csv`, `metrics.md` and `playbook.md`. If there is no plan yet, ask the user for their plan file and which levels it is set at (channel, location level, month), then save it as `business-context/plan.csv`. Ask how they want month-end projected; suggest the run rate of the last 7 days.

## Inputs
- `business-context/plan.csv`: the plan, by month, channel, location level and metric.
- `data/unified/`: actuals from `normalize-partner-data`.

## Steps
1. Sum month-to-date actuals at the same level as the plan.
2. Project month-end using the method saved in `metrics.md`. Show the method.
3. Compute the gap to plan for each line, in absolute terms and as a percentage.
4. For spend lines, compute the efficiency measure the user defined (for example ROAS = ad-attributed sales ÷ ad spend) and compare with the plan.
5. Flag lines further behind plan than the limit in `thresholds.md`, and lines where spend is ahead of plan but ROAS is behind.
6. For each flag, suggest up to two interventions from `business-context/playbook.md`, with the number that justifies each.
7. Output a one-page summary: overall status, the five biggest gaps, suggested interventions, and what to check tomorrow.

## Rules
- Never change the plan. Only report against it.
- Show every calculation so finance can audit it.

## Learn from corrections
When the user corrects an output ("that's not how we define sales", "we never discount on weekends"), propose the exact change to the matching file in `business-context/` and save it only after they agree. Log it in `business-context/changelog.md`.
