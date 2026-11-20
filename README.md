# ERP Workforce and Cost Dashboard (Looker Studio demo)

A one-page dashboard for a Head of ERP. It compares workforce and cost against plan, split by internal and external staff and by site, with a drill-down by person.

All data is fictional and built for demo purposes. No real company, team, person or vendor data is used.

- Live dashboard: https://datastudio.google.com/reporting/08e784d3-056f-4207-8609-641beab1bb6e
- Data: `data/workforce_costs_2026.csv` (48 people, 3 sites, Jan to Oct 2026, CHF)
- Build steps: `BUILD_GUIDE.md`
- Demo talk track: `DEMO_SCRIPT.md`

## The question it answers

Each month: are we on plan for people and cost, and if not, why?

## What it shows

- October 2026: 47 people, 40.4% external (19 of 47), spend CHF 472,843, +2.7% over plan.
- Year to date, Jan to Oct: CHF 45,482 over plan (+1.0%).
- The cause: Basel external contractors have run about 15% over plan since July, because of a program ramp-up. Before July they were on plan.
- Headcount by site in October: Kuala Lumpur 20, Hyderabad 15, Basel 12.

## How to read it

1. The four numbers on the left are the month view. The date control sets the month.
2. The bar chart shows headcount by site and by internal or external.
3. The table is sorted by variance %. The largest overruns sit at the top and show in red.
4. The trend chart and the YTD numbers always show Jan to Oct. They do not change with the date control.
5. The Location and Type filters apply to the whole page.

## Why I built it

I come from service delivery and business analysis. I wanted hands-on proof of planned-versus-actual reporting in a BI tool, not only a claim on a CV.

## What I did, and where I used help

- Claude helped draft the dataset and the build plan.
- I built the report in Looker Studio myself: calculated fields, scorecards, charts, table, filters and sharing.
- I checked every number against a QA list before sharing.

## What went wrong, and what I fixed

- Two scorecards showed 0 instead of 40.4% and +2.7%. They were ratios typed as numbers. I set the type to Percent.
- The trend chart changed with the date control. I moved it outside the group so it stays fixed.

## Limits

- Fictional data, one page, one currency (CHF).
- No live connection to a real ERP or finance system.

## Built with

Google Sheets and Looker Studio.
