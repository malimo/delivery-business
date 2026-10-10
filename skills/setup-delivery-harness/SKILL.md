---
name: setup-delivery-harness
description: Interview the user about their delivery business (channels, outlets, metrics, targets, what the team does about problems) and write the business context files every other delivery skill reads. Run this first, and again whenever the business changes.
---

# Set up the delivery harness

The other skills in this plugin know nothing about your business. They read it from `business-context/`. This skill builds that folder by asking you questions. Nothing is assumed; every rule in the folder is something you said.

## How to interview
- Ask **one question at a time**. Wait for the answer before the next one.
- Where it helps, offer a suggested default and say it is only a suggestion ("Most teams start with 7 days. Use that?").
- If the user says "I don't know", record it as `TODO` with the question, and move on. Never fill a gap with an invented number.
- If the user has a file that answers a question (an outlet list, a plan sheet, a sample partner export), ask for it instead of making them type.
- After each section, read back what you understood in a short list and ask "Is this right?" before saving.
- If `business-context/` already exists, show what is there and ask only about what is missing, marked `TODO`, or what the user wants to change.

## Sections and questions

### 1. The business (→ `business-context/business.md`)
1. In one line, what do you sell through delivery?
2. Which delivery channels do you sell on? (marketplaces, your own app or website, quick-commerce, others)
3. How do you group your locations? (for example outlet → city → region, or store → zone) What are the level names?
4. Who will read the outputs, and who acts on them? (outlet managers, city leads, the channel team, leadership)
5. What currency and time zone should every report use? What day does your week start?

### 2. Data sources (→ `business-context/sources.md`)
For each channel from question 1.2:
1. Which reports do you get from it? (sales, funnel, ad spend, ratings and complaints, payouts, others)
2. How do they arrive, and how often? (download, email, API, shared drive)
3. Can you share one sample file of each? Use it to propose a mapping later with `normalize-partner-data`.

### 3. Locations (→ `business-context/outlets.csv`)
1. Share your list of locations with your own ID, name, and each level from 1.3. If you don't have one, build it with the user from a sample partner file.
2. Does each channel use its own names or IDs for your locations? Record the matching in an `aliases` column.

### 4. Metrics and definitions (→ `business-context/metrics.md`)
1. Which numbers matter most to you? Offer a starting list: orders, gross sales, net sales, menu views, add-to-cart, conversion, ad spend, ad-attributed sales, ROAS, rating, complaints. Keep only what the user picks.
2. For each one, how exactly do you define it? (for example: is "sales" before or after discounts and commissions?) Ask about every definition that two people in the company could disagree on.
3. Which comparisons do you trust? (last 7 days vs previous 4 weeks, same day last week, same-store growth, against target)

### 5. When something needs action (→ `business-context/thresholds.md`)
For each metric picked in 4.1:
1. How big a change should raise a flag? Offer a default, and ask the user to change it.
2. Is a flag at outlet level enough, or only when a city or region moves?

### 6. The playbook (→ `business-context/playbook.md`)
This is the most important section. Ask it with the people who act on the outputs.
1. When [each flag from section 5] happens, what does your team actually do today?
2. Who does it, and by when?
3. What is the one thing they should never do in that situation?
Write each answer as a play: `trigger → action → owner → deadline`.

### 7. Plan and targets (→ `business-context/plan.csv`)
1. Do you have an annual or monthly plan by channel and location level? Ask for the file.
2. Which lines matter for spend efficiency (for example ROAS or cost per order), and what is the target?

### 8. Routines (→ `business-context/routines.md`)
1. Which outputs should run on a schedule, and when? (daily action lists, weekly review, monthly review)
2. Where should each one go? (a file, an email, a chat group per outlet, a dashboard)

## Finish
1. Write all files in `business-context/`. Keep the user's own words in definitions and plays.
2. List every `TODO` left, with the question that would close it.
3. Tell the user which skill to run next: usually `normalize-partner-data` with one sample file per source.

## Keeping it current
Any skill in this plugin may propose a change to `business-context/` when the user corrects it. Show the exact line to change and save it only after the user says yes. Add a dated line to `business-context/changelog.md` for each change, so the team can see how its rules evolved.

## Privacy
`business-context/` holds your business logic. Keep it in a private repository or folder. Don't commit it to a public one.
