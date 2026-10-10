# Delivery business skills

Your team gets the same kind of data from Swiggy, Zomato, Uber Eats, DoorDash, ad platforms and your POS, each in a different format. Most of the week goes into collating it and refreshing dashboards, and very little goes into acting on it.

These skills are generic versions of the ones a two-person delivery team built to fix that, without an engineering background. They come from post #1 of **AI-Native, One Person at a Time**, a LinkedIn series by [Mohit Malik](https://yoursonly.ai).

No company data is included. Replace every `[bracket]` with your own values.

| Skill | What it does |
|---|---|
| `normalize-partner-data` | Converts any partner's file into one standard dataset, and remembers each new format so it runs unattended next time |
| `find-actionables` | Reads the unified data and writes a short action list per outlet, city and region, ranked by impact |
| `aop-tracker` | Compares month-to-date actuals with your annual operating plan, checks ROAS, and says where to intervene |

## Install

**Claude Code**
```
/plugin marketplace add malimo/delivery-business
/plugin install delivery-business@delivery-business
```
Then ask in plain English ("normalize this Swiggy file", "what should each outlet fix this week?") or call a skill by name, for example `/delivery-business:find-actionables`.

**Claude.ai or Claude Desktop**
Zip one folder from `skills/` and upload it under Settings → Capabilities → Skills.

**Any other agent**
Each skill is a plain `SKILL.md`. Copy the folder wherever your agent reads skills from.

## Use them in this order
1. Learn what ETL means: extract each file, transform it to one format, load it in one place.
2. Set up `normalize-partner-data` first. Nothing else works until all data looks the same.
3. Run it every day as a scheduled routine.
4. Build dashboards on the unified data. The original team built theirs in React and HTML, behind Google sign-in.
5. Add `find-actionables`, then send each outlet its own list automatically.
6. Add `aop-tracker` once the daily data is trusted.

The mindset behind all three: define the input, define the outcome. The middle is the AI harness.

## License
MIT
