# Twiga Trails Safaris: Insights

Source: `twiga_trails_report.pbix` (star schema with 12 tables, 25 DAX measures, 7 report pages).
Period: bookings made Jan 2023 to Dec 2025 (13,890 bookings). All amounts are in USD, as in the model.
Revenue, Gross Profit and Travellers exclude cancelled bookings, matching the model's `[Net Revenue]`, `[Gross Profit]` and `[Travellers]` measures.

Headline numbers (all years): Net Revenue 122.9M, Gross Profit 42.5M, Gross Margin 34.6%, Cancellation Rate 9.4%, NPS 35.0, Avg Rating 4.13.
Year on year, Net Revenue was 29.8M (2023), 39.7M (2024) and 53.4M (2025). Gross Margin rose from 30.5% to 34.2% to 37.1%.

---

## Insight 1: Move bookings from OTAs to direct and cut OTA cancellations

**Question:**
Which sales channels create the most profit per dollar of revenue, and where are we losing revenue to cancellations?

**Evidence (measure, period, comparison, visual):**
- Measures: `[Net Revenue]`, `[Gross Margin %]`, `[Cancellation Rate]`, `[Commission]`. Period: 2023–2025. Comparison: by `Agents[Channel]`.
- Visuals: the "Cancellation Rate by Channel" column chart and the agent table (Net Revenue, Commission %, Gross Margin %) on the *Channels & Customers* page.

| Channel | Net Revenue (USD) | Gross Margin % | Cancellation Rate |
|---|---|---|---|
| Direct | 44.3M | 42.2% | 7.2% |
| Corporate | 14.8M | 38.4% | 6.9% |
| Tour Operator | 33.6M | 30.1% | 7.4% |
| OTA | 30.1M | 26.5% | 14.9% |

- OTAs pay 14–17% commission, which is 15.3% of their revenue, against 0% for Direct.
- OTA cancellation is about double every other channel, and it stayed at 14.7% in 2025.
- Direct's share of revenue grew from 34.2% (2023) to 37.9% (2025), while OTA's share stayed flat at about 24.5%.

**Interpretation:**
OTAs bring about a quarter of revenue at the lowest margin, and they cancel twice as often. Commission explains much of the margin gap. If OTA cancellations matched the other channels (7.3%), we would have kept about 305 more bookings, worth about 2.9M USD of booked value over three years (about 1M a year).

**Limitation or alternative explanation:**
OTAs may bring price-sensitive or "browsing" guests who book speculatively, so some of those bookings might never have happened direct. Part of the margin gap is also contractual: free-cancellation terms and commission rates are set by OTA policy. Cancelled bookings carry no commission in the model, so OTA's true cost may be understated. The data does not show cancellation reasons.

**Recommended action:**
1. Raise direct-website visibility for the packages OTAs sell best (Luxury).
2. Offer a small direct-booking perk, such as a free airport transfer, that costs less than the 15% commission.
3. Negotiate a deposit or tighter cancellation window with the three OTAs (TrekHub, WildPass, BushTrip.travel). Start with BushTrip.travel, which has the lowest margin at 24.3%.

**How we will measure the result:**
Track `[Cancellation Rate]` for OTA, with a target of 10% or lower within 12 months. Track OTA share of `[Net Revenue]`, aiming to move from 25% to 20%. Track overall `[Gross Margin %]`, aiming to move from 37.1% (2025) upward. Review quarterly on the *Channels & Customers* page, filtered by `Date[Year]`.

---

## Insight 2: Reprice family trips, because children cost full price to serve but pay half

**Question:**
Why do family bookings earn far less profit per dollar than every other segment?

**Evidence (measure, period, comparison, visual):**
- Measures: `[Net Revenue]`, `[Gross Profit]`, `[Gross Margin %]`, `[Tour Cost]`. Period: 2023–2025. Comparison: by `Customers[Segment]`.
- Visuals: the "Revenue by Region & Segment" bar chart and the Segment × Region revenue table on the *Channels & Customers* page.

| Segment | Net Revenue (USD) | Gross Margin % |
|---|---|---|
| Group | 35.6M | 37.8% |
| Family | 30.2M | **22.1%** |
| Couple | 26.9M | 39.7% |
| Corporate | 24.2M | 38.5% |
| Solo | 5.9M | 39.6% |

- Family is the second-largest segment by revenue, but its margin is about 16 points below the others.
- Tour Cost is 69.9% of revenue for Family, against 52–54% for the other segments.
- Family margin is low in every category: Budget 21%, Mid-Range 20%, Luxury 23%.
- Every family booking includes children, and about half of all family travellers are children.
- In the booking data, a child adds exactly 50% of the unit price to the net amount, but `Packages[CostPerPaxUSD]` is charged per traveller at full cost.
- Revenue per traveller is 2,321 USD for Family, against about 3,000 for Couple, Corporate and Solo.

**Interpretation:**
The margin gap comes from pricing. Children are billed at half price but cost the same as an adult to serve (park fees, vehicle seat, lodge room share). The more a family grows, the thinner the margin gets. This is structural, so it will not fix itself with growth.

**Limitation or alternative explanation:**
The model's cost is one flat `CostPerPaxUSD` for every traveller. In reality a child may cost less (shared room, lower park fee), so the true margin may be higher than reported. Family trips may also be a gateway to repeat business, which is not measured here. Cutting the family discount could reduce family bookings.

**Recommended action:**
1. Test a child price of 65–75% of the adult price, for example only on Luxury and Mid-Range packages, and keep 50% on Budget.
2. Introduce a family package with a fixed price that includes a vehicle and a shared room, so cost per traveller falls.
3. Ask finance to confirm the real child cost per traveller, so the model's margin can be corrected.

**How we will measure the result:**
Track `[Gross Margin %]` for `Customers[Segment] = "Family"`, with a target of 30% or higher within 12 months. Track Family booking count and `[Cancellation Rate]` to confirm demand is not falling. Track Family revenue per traveller, which should rise from about 2,321 USD. Compare quarter on quarter on the *Channels & Customers* page.

---

## Insight 3: Fix the guest experience on Budget packages before growing them

**Question:**
Are Budget packages worth the effort they take, and are they hurting our reputation?

**Evidence (measure, period, comparison, visual):**
- Measures: `[Avg Rating]`, `[NPS]`, `[Review Count]`, `[Net Revenue]`, `[Travellers]`. Period: 2023–2025. Comparison: by `Packages[Category]` and by package.
- Visuals: the review table and the Rating/NPS cards on the *Guest Experience* page. Also "Revenue by Safari Package" and "Revenue by National Park" on the *Packages & Parks* page.

| Category | Share of Travellers | Share of Net Revenue | Avg Rating | NPS |
|---|---|---|---|---|
| Luxury | 35% | 70% | 4.5 | 59.4 |
| Mid-Range | 35% | 24% | 4.2 | 37.1 |
| Budget | 30% | 5.5% | 3.7 | **6.7** |

- Budget packages carry 30% of travellers but only 5.5% of revenue and 5.4% of gross profit (2.3M USD).
- The five lowest-NPS packages are all Budget: Northern Tanzania Group Camping (0.7), Amboseli Kilimanjaro Views Camping (3.1), Tsavo Red Elephants Road Trip (7.6), Mara Express Camping (9.4) and Nakuru & Naivasha Budget Trail (9.7).
- In the review text, about 35% of Budget reviews mention a service failure (cramped vehicle, too many vehicles at sightings, poor communication before the trip, delayed pickup or accommodation not as advertised). For Luxury the figure is about 8%.
- Budget margin (33.9%) is in line with Mid-Range (33.3%), so the problem is experience and scale, not cost.

**Interpretation:**
Budget guests are a large group who rate us the lowest, and the complaints are about logistics rather than wildlife. Each Budget traveller is worth little revenue, so the cost of a poor experience (word of mouth, OTA ratings) is large compared with what these trips earn.

**Limitation or alternative explanation:**
Budget customers may simply expect more of what they pay for. NPS also falls with price, so some of this gap is expectation, not service. Only 49% of bookings have a review, and reviews exist only for completed trips, so unhappy guests who cancelled are not counted. Review text appears to come from a fixed set of phrases, so it shows themes rather than precise causes.

**Recommended action:**
1. Cap group size or vehicles per departure on Budget packages, so each guest gets a window seat. This addresses the cramped-vehicle complaints.
2. Send a pre-trip message with pickup time and driver details 7 days before travel. Budget lead time is only about 34 days, so start it at booking.
3. Review the five lowest-NPS Budget packages and decide whether to improve or retire each one. Start with Northern Tanzania Group Camping.
4. Do not spend extra marketing budget on Budget packages until NPS improves.

**How we will measure the result:**
Track `[NPS]` and `[Avg Rating]` for `Packages[Category] = "Budget"`, with a target NPS of 25 or higher and rating of 4.0 or higher within 12 months. Track the share of Budget reviews that mention vehicle, communication or pickup issues, with a target below 20%. Use the *Guest Experience* page, filtered by `Date[Year]`.

---

## Insight 4: Protect and sell the Migration Peak, and fill the Long Rains gap

**Question:**
When do guests actually travel, and how should we plan capacity and marketing around the seasons?

**Evidence (measure, period, comparison, visual):**
- Measures: `[Revenue By Travel Date]` and `[Travellers By Travel Date]` (these use the inactive `TravelStartDate` relationship), `[Avg Lead Time (days)]`. Period: all travel dates in the model. Comparison: by `Date[Season]`.
- Visuals: the Season × Category matrix and the "Revenue By Travel Date" line chart on the *Seasonality & Demand* page. Also "How Far Ahead Do Guests Book?" bar chart.

| Season (months) | Revenue by Travel Date (USD) | Share | Revenue per Month (USD) |
|---|---|---|---|
| Migration Peak (Jul–Oct) | 59.5M | 48% | 14.9M |
| Festive Peak (Dec–Jan) | 27.0M | 22% | 13.5M |
| Shoulder (Feb–Mar, Jun, Nov) | 29.6M | 24% | 7.4M |
| Long Rains (Apr–May) | 6.8M | 5.5% | 3.4M |

- Peak months earn about four times more per month than Long Rains.
- Luxury guests book far ahead (about 136 days on average), against about 69 days for Mid-Range and 34 days for Budget.
- Margin is also higher in peak seasons (about 37%) than in Long Rains or Shoulder (about 29%).

**Interpretation:**
The business depends on two peaks. Peak seasons are the most profitable, so capacity (vehicles, guides, lodge allocations) must be secured early, since Luxury guests book 4–5 months ahead. April and May are nearly empty, so they are the best place to add revenue.

**Limitation or alternative explanation:**
Bookings in the data end in Dec 2025, so travel dates in 2026 are only partly filled, and the totals above include those partial 2026 months. The Long Rains are a real weather limit, so demand may not recover easily. Lower margins in off-peak seasons may reflect discounting or lower prices, which this analysis has not tested.

**Recommended action:**
1. Open Migration Peak allocations earlier, 6 months ahead, for Luxury packages.
2. For Long Rains, create "green season" offers for Mid-Range and Budget packages, and launch them in January–February. The average lead time is about 80 days, so promotion for April–May travel needs to start then.

**How we will measure the result:**
Track `[Revenue By Travel Date]` for Long Rains, with a target of 8M USD or more, up from 6.8M. Track `[Travellers By Travel Date]` by season. Track Long Rains `[Gross Margin %]` so discounts do not erode profit, keeping it at 29% or higher. Review on the *Seasonality & Demand* page after each travel season.

---

## Insight 5: Revenue is meeting targets but not beating them, and the miss is timing

**Question:**
Are we on target, and where in the year do we fall short?

**Evidence (measure, period, comparison, visual):**
- Measures: `[Net Revenue]`, `[Revenue Target]`, `[Target Variance %]`, `[Revenue YoY %]`. Period: 2023–2025, by booking date. Comparison: actual against `Targets`.
- Visuals: the KPI card and the Net Revenue / Gross Profit line chart on the *Executive Overview* page.

| Year | Target (USD) | Actual (USD) | Variance | Revenue YoY % |
|---|---|---|---|---|
| 2023 | 30.3M | 29.8M | −1.5% | n/a |
| 2024 | 41.0M | 39.7M | −3.2% | +33.2% |
| 2025 | 53.7M | 53.4M | −0.6% | +34.4% |

- In 2025 the company came within 0.6% of target, but missed in 6 of 12 months.
- The biggest misses in 2025 were January (−9.6%) and December (−8.5%). The biggest beats were August (+7.6%) and April (+6.7%).
- By category in 2025, Luxury hit target (+0.1%), Mid-Range missed by 2.1% and Budget missed by 4.1% (below target in 10 of 12 months).
- The 2026 target is 60.8M USD, which is +14% on 2025 actuals, while revenue has been growing about 34% a year.

**Interpretation:**
Total revenue is close to plan, but the plan's monthly shape is wrong. Targets were too high for January and December and too low for April and August. Budget is the weakest against target. The 2026 target looks easy compared with recent growth, so it may not push the team.

**Limitation or alternative explanation:**
The model compares targets to revenue by booking date, not travel date, so a target may be missed in one month simply because guests booked earlier or later. Three years is a short history for setting monthly patterns. Growth may slow as the business gets bigger, so +14% may be reasonable.

**Recommended action:**
1. Re-phase the 2026 monthly targets using actual booking patterns (higher in May–August when most bookings are made, lower in January and December).
2. Agree a stretch target for 2026 above 60.8M USD, with Luxury and Direct as the main drivers.
3. Review Budget targets, either lowering them or backing them with a clear plan (see Insight 3).

**How we will measure the result:**
Track `[Target Variance %]` monthly, with a goal of every month within ±5% (in 2025, 4 of 12 months were outside that range). Track `[Revenue YoY %]` against the new stretch target. Review monthly on the *Executive Overview* page.

---