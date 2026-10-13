# Delivery business skills

Your team gets the same kind of data from Swiggy, Zomato, Uber Eats, DoorDash, ad platforms and your POS, each in a different format. Most of the week goes into collating it and refreshing dashboards, and very little goes into acting on it.

These skills are generic versions of the ones a two-person delivery team built to fix that, without an engineering background. They come from post #1 of **AI-Native, One Person at a Time**, a series by [yoursonly.ai](https://yoursonly.ai) (@yoursonly_ai on Instagram and YouTube).

No company data is included. The skills don't assume anything about your business: they ask you, and save your answers in a `business-context/` folder that every skill reads.

| Skill | What it does |
|---|---|
| `setup-delivery-harness` | Interviews you about your channels, locations, metrics, thresholds, plan and what your team does about each problem, then writes `business-context/` |
| `normalize-partner-data` | Converts any partner's file into one standard dataset, and remembers each new format so it runs unattended next time |
| `find-actionables` | Reads the unified data and writes a short action list per outlet, city and region, ranked by impact |
| `aop-tracker` | Compares month-to-date actuals with your annual operating plan, checks ROAS, and says where to intervene |

## Install

**Claude Code**
```
/plugin marketplace add yoursonlyorg/delivery-business
/plugin install delivery-business@delivery-business
```
Then start with:
```
/delivery-business:setup-delivery-harness
```
After that, ask in plain English ("normalize this Swiggy file", "what should each outlet fix this week?") or call a skill by name, for example `/delivery-business:find-actionables`.

**Claude.ai or Claude Desktop**
Zip each folder in `skills/` (start with `setup-delivery-harness`) and upload it under Settings → Capabilities → Skills.

**Any other agent**
Each skill is a plain `SKILL.md`. Copy the folder wherever your agent reads skills from.

## Use them in this order
1. Run `setup-delivery-harness`. Do the playbook section with the people who act on the outputs.
2. Learn what ETL means: extract each file, transform it to one format, load it in one place. Then run `normalize-partner-data` on one sample file per source. Nothing else works until all data looks the same.
3. Run it every day as a scheduled routine.
4. Build dashboards on the unified data. The original team built theirs in React and HTML, behind Google sign-in.
5. Add `find-actionables`, then send each outlet its own list automatically.
6. Add `aop-tracker` once the daily data is trusted.

## It gets better as you use it
When you correct an output, the skill proposes the exact change to `business-context/` and saves it once you agree, with a dated line in `changelog.md`. Over a few weeks the folder becomes your team's business logic, written down.

## Keep your business context private
`business-context/` holds your definitions, thresholds and playbook. Keep it in a private repository or folder, not a public one.

The mindset behind all of this: define the input, define the outcome. The middle is the AI harness.

## License
MIT
