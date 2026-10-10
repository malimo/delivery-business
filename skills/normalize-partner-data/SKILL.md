---
name: normalize-partner-data
description: Convert a partner or platform data file (any format) into one standard dataset, saving the column mapping so the same format runs unattended next time.
---

# Normalize partner data

Use this when a data file arrives from a partner, marketplace or ad platform and needs to join the standard dataset.

## The standard schema
Every row in the output has exactly these columns. Edit this list once for your business, then keep it fixed.

| column | meaning |
|---|---|
| `date` | the day the number belongs to (YYYY-MM-DD) |
| `source` | which partner or platform the file came from |
| `outlet_id` | your own ID for the store, cafe or location |
| `city` | city of the outlet |
| `region` | your region grouping |
| `metric` | one of: [orders, gross_sales, menu_views, cart_adds, ad_spend, ad_sales, rating, complaints, ...] |
| `value` | the number |

## Steps
1. Identify the source and report type from the file name, headers and a sample of rows. Say what you think it is.
2. Look in `mappings/` for a saved mapping for this source and report type.
   - If one exists and every header matches, apply it without asking.
   - If headers changed, show the differences and ask before continuing.
3. If there is no mapping, propose one: each source column → a schema column or metric, plus any unit or date-format conversion. Ask the user to confirm. **Never guess a mapping silently.**
4. Map the partner's outlet names or IDs to `outlet_id` using `outlets.csv`. List any that don't match; don't drop them silently.
5. Convert to long format (one row per date, outlet and metric).
6. Validate: no empty dates, no negative counts, totals match the source file's totals. Report any mismatch.
7. Save the confirmed mapping to `mappings/<source>-<report-type>.json`.
8. Append the clean rows to `data/unified/` and write a short run report: rows in, rows out, rows skipped and why.

## Running daily
Once a mapping is saved, the same file format can run as a scheduled routine. The routine should stop and alert a person if step 2 finds changed headers or step 6 finds a mismatch.
