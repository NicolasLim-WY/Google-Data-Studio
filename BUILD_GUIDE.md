# Build guide: ERP Workforce and Cost Dashboard (Looker Studio)

Target: a one-page dashboard in about 60 minutes.
Data: `data/workforce_costs_2026.csv`, fictional, 48 people, 3 sites, Jan to Oct 2026, CHF.

Reader: Head of ERP. Each month they check headcount and spend against plan, split by internal vs external staff and by location. They decide where to add, cut or shift capacity between sustainment work and the transformation program.

---

## Step 1. Load the data into Google Sheets (5 min)

1. Open your Google Sheet. Go to File > Import > Upload and pick `workforce_costs_2026.csv`.
2. Choose "Replace current sheet". Keep "Convert text to numbers, dates and formulas" ticked.
3. Rename the tab to `data`.
4. Check: 473 rows including the header, 11 columns, and the Month column shows dates.

## Step 2. Connect Looker Studio (5 min)

1. Go to lookerstudio.google.com > Create > Report.
2. Add data > Google Sheets > your sheet > tab `data`. Tick "Use first row as headers". Click Add.
3. Open Resource > Manage added data sources > Edit. Check the field types:
   - Month: Date & Time > Date
   - Headcount, External Flag, Planned Cost CHF, Actual Cost CHF: Number, aggregation Sum
   - Planned Cost CHF and Actual Cost CHF: you can set type Currency > CHF
   - All other fields: Text

## Step 3. Add calculated fields (10 min)

In the data source editor, click "Add a field" for each one. Pick field names from the autocomplete list so the spelling matches.

| Field name | Formula | Type |
|---|---|---|
| Variance CHF | `SUM(Actual Cost CHF) - SUM(Planned Cost CHF)` | Currency CHF |
| Variance % | `(SUM(Actual Cost CHF) - SUM(Planned Cost CHF)) / SUM(Planned Cost CHF)` | Percent |
| External Share % | `SUM(External Flag) / SUM(Headcount)` | Percent |
| Actual Sustainment CHF | `CASE WHEN Cost Line = "Sustainment" THEN Actual Cost CHF ELSE 0 END` | Currency CHF, aggregation Sum |
| Actual Program CHF | `CASE WHEN Cost Line = "Program" THEN Actual Cost CHF ELSE 0 END` | Currency CHF, aggregation Sum |

## Step 4. Page setup (3 min)

1. Theme and layout: pick a plain light theme. Canvas size 1200 x 900 works well.
2. Add a text box at the top: **ERP Workforce and Cost: Plan vs Actual**
3. Add a smaller text box under it: `Fictional data for demo purposes. Reporting currency CHF. Actuals Jan to Oct 2026.`

## Step 5. The month block (20 min)

This block shows one selected month. Build these items, then group them with the date control in step 5.6.

### 5.1 Date range control
- Insert > Date range control. Place it top right.
- Default date range: Custom, 1 Oct 2026 to 31 Oct 2026.

### 5.2 Four KPI scorecards (one row)
Insert > Scorecard, four times. In each, set Date range dimension = Month.

| Scorecard | Metric | Label |
|---|---|---|
| 1 | Headcount (Sum) | Headcount |
| 2 | External Share % | External share |
| 3 | Actual Cost CHF (Sum) | Spend this month |
| 4 | Variance % | Variance vs plan |

Tip: on scorecard 4, use Style > Conditional formatting: red when Variance % is greater than 0.02.

### 5.3 Headcount by location
- Insert > Bar chart (stacked).
- Dimension: Location. Breakdown dimension: Type. Metric: Headcount (Sum).
- Style: tick "Stacked bars". Title: Headcount by location.

### 5.4 Drill-down table
- Insert > Table.
- Dimensions: Person ID, Role, Type, Vendor, Location, Cost Line.
- Metrics: Planned Cost CHF, Actual Cost CHF, Variance CHF, Variance %.
- Sort: Variance % descending. Rows per page: 15.
- Style > Conditional formatting: Variance % greater than 0.05, red text.

### 5.5 Check before grouping
Each item's Date range dimension must be Month.

### 5.6 Group the month block
Select the date control, the 4 scorecards, the bar chart and the table. Right-click > Group (Ctrl+G or Cmd+G).
Now the date control filters only this block. The trend chart in step 6 keeps its own date range.

## Step 6. The trend block (10 min)

### 6.1 Plan vs actual by month
- Insert > Combo chart. Place it outside the group.
- Dimension: Month (Year Month). Sort: Month ascending.
- Metrics, in this order: Actual Sustainment CHF, Actual Program CHF, Planned Cost CHF.
- Style: series 1 and 2 as Bars, series 3 as Line. Tick "Stacked bars".
- Default date range: Custom, 1 Jan 2026 to 31 Oct 2026.
- Title: Spend vs plan by month (stacked bars = actual, line = plan).

### 6.2 YTD scorecard
- Insert > Scorecard, outside the group. Metric: Variance CHF. Label: YTD variance.
- Default date range: Custom, 1 Jan 2026 to 31 Oct 2026.
- Add a second one with Variance % if there is room.

## Step 7. Page filters (3 min)

Insert > Drop-down list, two times, outside the group. These filter the whole page.
- Control field: Location
- Control field: Type

Place them next to the date control.

## Step 8. QA check (5 min)

Your numbers must match this list. If one does not, fix it before you share the report.

| Check | Expected |
|---|---|
| Headcount, Oct 2026 | 47 |
| External share, Oct 2026 | 40.4% (19 of 47) |
| Spend this month, Oct 2026 | CHF 472,843 |
| Variance vs plan, Oct 2026 | +2.7% (CHF +12,463) |
| YTD variance, Jan to Oct | CHF +45,482 (+1.0%) |
| Headcount by location, Oct | Kuala Lumpur 20, Hyderabad 15, Basel 12 |
| Filter Basel + External, Jul to Oct | +15.0% over plan |
| Filter Basel + External, Jan to Jun | about -0.3% (on plan) |
| Monthly variance Jan to Jun | between -0.3% and 0.0% |
| Monthly variance Jul to Oct | between +2.4% and +3.2% |

Headcount changes built into the data, so you can explain them:
- April: 2 planned internal hires in Kuala Lumpur (46 to 48).
- September: 1 external contractor in Hyderabad rolled off (48 to 47).

## Step 9. Share (2 min)

1. Click Share > Manage access > "Anyone with the link can view".
2. Copy the link. Test it in an incognito window.
3. Add the link to the README in this repo.

---

## Out of scope for v1 (your v2 answer in the interview)

- Cost category split: salary, contractor fees, benefits, training, travel
- Forecast to year end, and full-year plan vs forecast
- FX: local currency to CHF
- Capacity scenarios: what happens to cost if work shifts from Basel to Kuala Lumpur
- Automated monthly refresh from source systems
