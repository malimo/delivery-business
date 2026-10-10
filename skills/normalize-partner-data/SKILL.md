---
name: normalize-partner-data
description: Convert a partner or platform data file (any format) into one standard dataset, saving the column mapping so the same format runs unattended next time.
---

# Normalize partner data

Use this when a data file arrives from a partner, marketplace or ad platform and needs to join the standard dataset.

## Before you start
1. Read `business-context/` (made by `setup-delivery-harness`). If the folder doesn't exist, say so and offer to run the setup interview first.
2. If something this skill needs is missing or marked `TODO`, ask the user for it, **one question at a time**, with a suggested default where it helps. Save each answer to the right file in `business-context/` after the user confirms it.
3. Never invent a business rule, threshold, definition or play. If the user doesn't know, record `TODO` and work without it, saying what you left out.

This skill needs: `sources.md`, `outlets.csv`, and `metrics.md`.

## The standard schema
Every row in the output has exactly these columns. The list of metrics comes from `business-context/metrics.md`; don't add one the user hasn't defined.

| column | meaning |
|---|---|
| `date` | the day the number belongs to (YYYY-MM-DD) |
| `source` | which partner or platform the file came from |
| `outlet_id` | your own ID for the store, cafe or location |
| `level_1`, `level_2` | the grouping levels named in `business.md` (for example city, region) |
| `metric` | one of the metrics in `business-context/metrics.md` |
| `value` | the number |

## Steps
1. Identify the source and report type from the file name, headers and a sample of rows. Say what you think it is.
2. Look in `mappings/` for a saved mapping for this source and report type.
   - If one exists and every header matches, apply it without asking.
   - If headers changed, show the differences and ask before continuing.
3. If there is no mapping, ask the user what this report is used for, then propose one: each source column → a schema column or metric, plus any unit or date-format conversion. Ask the user to confirm. **Never guess a mapping silently.**
4. Map the partner's outlet names or IDs to `outlet_id` using `business-context/outlets.csv` and its `aliases` column. For any that don't match, ask the user which outlet it is and add the alias once they confirm. Don't drop rows silently.
5. Convert to long format (one row per date, outlet and metric).
6. Validate: no empty dates, no negative counts, totals match the source file's totals. Report any mismatch.
7. Save the confirmed mapping to `mappings/<source>-<report-type>.json`.
8. Append the clean rows to `data/unified/` and write a short run report: rows in, rows out, rows skipped and why.
9. If the source or report type isn't in `sources.md` yet, add it after the user confirms.

## Running daily
Once a mapping is saved, the same file format can run as a scheduled routine. The routine should stop and alert a person if step 2 finds changed headers or step 6 finds a mismatch.

## Learn from corrections
When the user corrects an output ("that's not how we define sales", "we never discount on weekends"), propose the exact change to the matching file in `business-context/` and save it only after they agree. Log it in `business-context/changelog.md`.
