# Twiga Trails Safaris: Power BI Dashboard

A Power BI project for **Twiga Trails Safaris**, a fictional Nairobi safari operator. I turned raw booking files (messy, duplicated and inconsistent) into a clean star-schema model, validated DAX measures and a 7-page interactive report. The aim was to give the CEO one trusted report instead of conflicting spreadsheets.

Built for the [LuxDevHQ Power BI Safari Workshop](https://github.com/LuxDevHQ/Data/tree/main/powerbi-safari-workshop). The source data is in that repository, not this one.

---

## Business Questions

- How much revenue and gross profit do we make, and how fast are they growing?
- Are we meeting finance's monthly revenue targets?
- When do customers book, and when do they travel?
- Which channels, packages, parks and regions drive performance?
- Which channels cancel the most?
- How satisfied are guests (ratings and NPS)?

## Project at a Glance

| Item | Detail |
|------|--------|
| Tool | Power BI Desktop (PBIP project format) |
| Data | 13,927 raw booking rows (2023 to 2025), 6,500 customers, 18 packages, 10 parks, 14 agents, 6,759 reviews |
| After cleaning | 13,890 bookings |
| Model | Star schema, 12 tables, 1 inactive relationship (travel date) |
| DAX | 25 measures |
| Report | 7 pages (5 main, 1 tooltip, 1 drill-through) |
| Security | Dynamic row-level security by sales region |
| Currency | USD |

## Data Preparation (Power Query)

All cleaning is done in Power Query, so the source files stay untouched and every step can be repeated.

- Combined the yearly booking CSVs with a **folder query**, so new files load automatically.
- Parameterised the source path (`DataFolder`) so the project is portable.
- Removed duplicate bookings by `BookingID` (13,927 down to 13,890 rows).
- Standardised status spellings (for example `Canceled` to `Cancelled`).
- Replaced blank discounts with 0 and blank agent IDs with the direct desk (`AG00`).
- Standardised customer country names (for example `USA` to `United States`) so every customer maps to a sales region.
- Skipped the non-tabular title rows at the top of the Customers sheet.
- Added helper columns: `Pax`, `NetAmountUSD` and `LeadTimeDays`.

## Data Model

Central fact table `Bookings`, surrounded by `Customers`, `Packages`, `Agents`, `Regions`, `Parks`, `Categories`, `Reviews`, `Targets` and a calculated `Date` table. The `Date` table has two relationships to `Bookings`: an active one on booking date and an inactive one on travel date, which is switched on with `USERELATIONSHIP` where needed.

## Business Rules

| Metric | Definition |
|--------|------------|
| Net amount | (Adults + 0.5 × Children) × Unit price × (1 − Discount) |
| Net revenue | Net amount on non-cancelled bookings, recognised on booking date |
| Gross profit | Net revenue − Tour cost − Commission |
| Cancellation rate | Cancelled bookings ÷ all bookings |
| NPS | % promoters (9 to 10) − % detractors (0 to 6) |

## Dashboard Pages

| Page | Question it answers |
|------|---------------------|
| Executive Overview | Are we growing and on target? |
| Seasonality & Demand | When do guests book and travel? |
| Channels & Customers | Who sells for us, and who cancels? |
| Packages & Parks | What are we selling, and where? |
| Guest Experience | Where do we disappoint guests? |
| Package Snapshot (tooltip) | Quick revenue and rating view on hover |
| Package Detail (drill-through) | Full view of one selected package |

**Interactivity:** synced Year and Sales Region slicers, drill-through, report tooltip, bookmarks and a field parameter to switch the trend metric.

## Security, Publishing and Refresh

- **Row-level security (RLS):** a static `Europe` role and a dynamic `Regional Manager` role (filtered by `USERPRINCIPALNAME()`), so each manager only sees customers from their own sales region. Tested with *View as*.
- **Published** to Power BI Service and tested with a Viewer account.
- **Scheduled refresh** configured on the semantic model (East Africa Time).
- **Folder-source test:** added the 2026 H1 bookings file to the bookings folder and refreshed. The new rows loaded without changing the model, which proves the pipeline is reusable.
- **Dashboard** with pinned KPI cards and a cancellation-rate alert.

## Screenshots

### Executive Overview
![Executive Overview](Screenshots/01-executive-overview.png)

### Seasonality & Demand
![Seasonality & Demand](Screenshots/02-seasonality-demand.png)

### Channels & Customers
![Channels & Customers](Screenshots/03-channels-customers.png)

### Packages & Parks
![Packages & Parks](Screenshots/04-packages-parks.png)

### Guest Experience
![Guest Experience](Screenshots/05-guest-experience.png)

### Package Detail (drill-through)
![Package Detail](Screenshots/06-package-detail.png)

### Package Snapshot (tooltip)
![Package Snapshot](Screenshots/07-package-snapshot.png)

## Headline Results (2023 to 2025)

| KPI | Value |
|-----|-------|
| Net Revenue | 122.9M |
| Gross Profit | 42.5M |
| Gross Margin | 34.6% |
| Cancellation Rate | 9.4% |
| NPS | 35.0 |
| Average Rating | 4.13 |

Net Revenue grew from 29.8M (2023) to 39.7M (2024) to 53.4M (2025), with Gross Margin rising from 30.5% to 37.1%.

## Key Insights

The full analysis, with evidence, limitations, recommended actions and success measures, is in **[insights.md](insights.md)**.

1. **Channels:** OTAs bring about a quarter of revenue at the lowest margin (26.5%) and cancel about twice as often (14.9%) as other channels.
2. **Family trips:** The second-largest segment, but only a 22.1% margin, because children pay half price while costing the same to serve.
3. **Budget packages:** 30% of travellers but 5.5% of revenue, with the lowest NPS (6.7).
4. **Seasonality:** The Migration Peak (Jul to Oct) earns about four times more per month than the Long Rains (Apr to May).
5. **Targets:** 2025 revenue finished within 1% of target, but monthly targets are badly phased and Budget misses most often.

## Repository Structure

```
├── twiga_trails_report.pbip            # Open this in Power BI Desktop
├── twiga_trails_report.Report/         # Report pages and visuals
├── twiga_trails_report.SemanticModel/  # Data model, relationships, DAX
├── insights.md                         # Business insights and recommendations
├── Screenshots/                        # Dashboard page screenshots
├── .gitignore
└── README.md
```

## How to Open

1. Install **Power BI Desktop** (Windows).
2. Enable **Power BI Project (.pbip) save option** under File > Options and settings > Options > Preview features, then restart.
3. Download the workshop data from the [LuxDevHQ repository](https://github.com/LuxDevHQ/Data/tree/main/powerbi-safari-workshop).
4. Clone this repository and double-click `twiga_trails_report.pbip`.
5. In Power Query, set the `DataFolder` parameter to the path of your local `data/` folder.

## Skills Demonstrated

- Data cleaning and profiling in Power Query (M)
- Star-schema modelling with active and inactive relationships
- DAX: time intelligence, `CALCULATE`, `SUMX`, `USERELATIONSHIP`, `RANKX`, variables
- Row-level security (static and dynamic) and Power BI Service publishing
- Scheduled refresh and reusable folder-based data pipelines
- Report design, interactivity and storytelling for business users
- Turning analysis into evidence-based recommendations

## Author

**Eric Mwangi**

[GitHub](https://github.com/EricMWaimiri)
