---
name: aop-tracker
description: Compare month-to-date actuals with the annual operating plan (AOP) by channel, city and region, project the month-end gap and suggest interventions.
---

# AOP tracker

## Inputs
- `aop.csv`: the plan, by month, channel, city or region, and metric (sales, orders, ad spend, ROAS).
- `data/unified/`: actuals from `normalize-partner-data`.

## Steps
1. Sum month-to-date actuals at the same level as the plan.
2. Project month-end using the daily run rate of the last [7] days. Show the method.
3. Compute the gap to plan for each line, in absolute terms and as a percentage.
4. For marketing lines, compute ROAS (ad-attributed sales ÷ ad spend) and compare with the plan's ROAS.
5. Flag lines more than [5]% behind plan, and lines where spend is ahead of plan but ROAS is behind.
6. For each flag, suggest up to two interventions from `playbook.md`, with the number that justifies each.
7. Output a one-page summary: overall status, the five biggest gaps, suggested interventions, and what to check tomorrow.

## Rules
- Never change the plan. Only report against it.
- Show every calculation so finance can audit it.
