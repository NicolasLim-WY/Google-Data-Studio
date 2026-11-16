# Demo script: ERP Workforce and Cost Dashboard

Use this for the Roche screening call and the hiring manager interview.
Fictional data. Built in one evening to prepare for the Business Analyst - ERP Operations role.

## The 60-second version

"I built this dashboard to show how I would support the Head of ERP. It answers one monthly question: are we on plan for people and cost, and if not, why?

The top row gives four numbers for the selected month: headcount, external share, spend and variance against plan. Below it, headcount by location and staff type, and a drill-down by person.

The trend chart shows the story. Spend tracked plan from January to June. From July, it runs 2 to 3% over. When I filter to Basel and external staff, the cause is clear: four program contractors run 15% over plan from July, because of a ramp-up. They explain the whole year-to-date overspend of about CHF 45,000.

So the decision for the department head is simple: approve the ramp-up and re-baseline the plan, or move part of that work to a lower-cost site."

## The 3-minute walkthrough (with clicks)

1. **Frame the reader (15 sec).** "The reader is the Head of ERP. One page, monthly, drill-down when needed."
2. **Top row (30 sec).** Point at the four KPIs for October. "47 people, 40% external, CHF 473k spend, 2.7% over plan."
3. **Headcount mix (30 sec).** "Kuala Lumpur carries the most people. Hyderabad is the most external-heavy. Basel is small but expensive."
4. **Trend (45 sec).** "On plan to June. Over plan from July. The bars split sustainment and program cost, so you can see the overspend sits in program work."
5. **Drill down (45 sec).** Filter Location = Basel, Type = External. "Four contractors, all on the program, 15% over plan from July. That one group explains the full-year variance."
6. **Close with the decision (15 sec).** "Approve and re-baseline, or shift work to a lower-cost site. I would bring both options with the cost of each."

## Likely questions and answers

**Why did you build this?**
"The role asks for workforce baselines, plan vs actual tracking and leadership dashboards. I wanted to show you how I think, not just tell you."

**Have you used Looker Studio before?**
"Not in a past job. I built this to close that gap. My reporting background is ServiceNow, JIRA and Excel and Google Sheets trackers. Looker Studio sits naturally on Google Sheets, which Roche already uses."

**How did you use AI here?**
"I used Claude to generate the fictional dataset and draft a build plan. I built the report, set up the calculated fields and checked every number against a QA list myself. That is how I would use AI at Roche: faster first drafts, with a human check before anything reaches leadership."

**How would this work with real data?**
"Headcount would come from the HR system and the vendor list. Cost would come from finance actuals and the approved plan. I would land both in one Google Sheet or a BigQuery table each month, with checks on row counts, totals and duplicates before the dashboard refreshes."

**How do you make sure the numbers are right?**
"I keep a QA list of expected totals and check them after every refresh. In my SDM role, I tracked workload, coverage, SLA and KPI results across shifts, and wrong numbers lose trust fast."

**What would you add in v2?**
"Cost category detail, a year-end forecast, local currency to CHF, and a capacity scenario: what happens to cost if work moves from Basel to Kuala Lumpur."

**How does this connect to your past work?**
"At my last delivery role, I found the team was delivering managed-service outcomes under a staff augmentation contract. I built an uplift model to show the gap, and it supported a multi-million ringgit SOW renewal. This dashboard is the same habit: show leaders the gap, the cause and the decision."

## Before the call

- Open the dashboard link in an incognito window. Make sure it loads without a login.
- Set the date control to October 2026 and clear all filters.
- Have the QA list from BUILD_GUIDE.md open in another tab.
- Practise the 60-second version out loud three times.
