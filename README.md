# Financial Controlling Dashboard

### From month-end reporting to a forward-looking view

[View interactive dashboard in Power BI](https://app.powerbi.com/view?r=eyJrIjoiOWQ2NWZlZjItZTQxYi00MjY0LWE3ZDQtYmM2YzdkZGJjNDJhIiwidCI6ImVkOGYxNjczLTM4OTAtNGRiNC1hM2YwLTk3YWQ5NDI3Yzc0ZiIsImMiOjEwfQ%3D%3D) — public link, no Power BI account or sign-in required.

**How can a month close ahead of budget on every headline number, and still hide a cost line running over plan or a product whose margin is quietly eroding?**

This dashboard was built to answer that question for a Finance & Controlling audience: a two-page Power BI report that checks the current month against Budget, extends the view into a blended Actual + Forecast full-year outlook, and separates products that are genuinely improving in profitability from ones that are simply growing revenue.

> **The management flow:** Executive Overview signals whether the month is on track and where the Budget variance sits → P&L Analysis extends that into the full-year outlook, breaks revenue down by product and country, classifies products by growth-and-margin trend, and checks operating expense discipline by cost center.

## Business problem

Inventory, headcount and marketing spend all show up on the P&L as a single number for the month. That number can look healthy on average while individual lines move in opposite directions underneath it — and a report that only shows the current month can't say whether that pattern will hold for the rest of the year.

The business needs three questions answered every month:

- Is performance on track against Budget, and which P&L lines are actually driving the variance?
- Based on Actual results so far, where is the full year likely to land — not just where has it been?
- Which products are improving in profitability rather than just growing revenue, and is operating spend staying inside budget by cost center?

The dashboard was designed to answer the first two at a glance and give Controlling a specific, prioritized starting point for the third.

## Dataset

The report runs on a **sample financial-controlling dataset**, structured the way a mid-size company's P&L data typically is: Actual results, Budget, and Forecast, broken down by product, cost center and country.

| Scope | Detail |
|---|---|
| Scenarios | Actual (19,811 rows), Budget (2,880 rows), Forecast (480 rows) |
| Time coverage | January 2025 – December 2026 (24 months) |
| Products | 5 |
| Countries | 5 (Germany, France, Netherlands, Austria, Switzerland) |
| Cost centers | 7 (Production, Logistics, Admin, IT, Sales, Marketing, HR) |
| P&L line items | 9 (Revenue, COGS, Personnel, Logistics, Marketing, IT, Administration, Depreciation, Other Opex) |

**All figures are illustrative.** This is a synthetic dataset built to demonstrate the data model, DAX logic and report design — not a real company's numbers.

## Tools

**Microsoft Power BI Desktop** — Power Query (M) for data preparation, a star-schema semantic model, and DAX for every measure, bridge, and trend classification on the report. This write-up focuses on how the dashboard was used to reason through the business questions, not just how it was built.

## Analysis approach

1. **Check the month.** Compare Revenue, Gross Profit, Gross Margin and EBIT against Budget for the period selected.
2. **Explain the variance.** Bridge the EBIT and Gross Profit gap between Budget and Actual, line item by line item.
3. **Look past the current month.** Blend Actual with Forecast into one continuous full-year path, against the same months last year.
4. **Locate where revenue sits.** Break the period down by product and by country.
5. **Separate growth from profitability.** Classify each product by its own trend — revenue growth and margin movement together, not a single-period snapshot.
6. **Check spending discipline.** Compare Operating Expenses against Budget by cost center.

## Main insights

- **The month beat Budget, but not for one reason.** Revenue came in 19% ahead of Budget (+289.3K) and Gross Profit 55% ahead (+356.8K) — driven by both higher revenue and COGS landing 8% under Budget (-67.5K). Gross Margin reached 55.3%, 12.8pp ahead of target.
- **Opex told a mixed story underneath a favorable total.** Personnel and Logistics both ran slightly over Budget (+2%), while Marketing finished 5% under Budget yet grew faster month-over-month than any other line (+9.6%) — worth watching even though it isn't over budget yet.
- **Revenue is concentrated, not evenly spread.** The four largest-labelled products already cover roughly 90% of the period's revenue, and Germany alone accounts for over a third of the five countries shown.
- **Growth and margin don't move together for every product.** In the current period, four of five products carry a "Positive Momentum" signal (revenue and/or margin trending up over the last 3 months), but one shows no confirmed 2-month trend on either dimension — a different situation from simply "underperforming," and one a single revenue ranking would not surface.

## Dashboard walkthrough

### 1. Executive Overview — Is performance on track this month?

![Executive Overview page — KPI tiles for Revenue, Gross Profit, Gross Margin and EBIT bSI, budget-variance bridges, and a financial summary table](screenshots/01-executive-overview.png)

The top row compares the period against Budget on four measures: Revenue (2M, +289.3K vs Budget), Gross Profit (1M, +356.8K), Gross Margin (55.3%, +12.8pp) and EBIT bSI (294K, +354.8K). Each tile carries a small trend line so a favorable variance can be read alongside the direction it's been moving, not just its current value.

**The financial summary table: where exactly does the variance sit?**

Below the headline cards, every P&L line is shown against Prior Month, month-over-month change, and Budget in the same table. This is where the aggregate picture breaks apart: COGS finished under Budget (-8%) while Personnel and Logistics both ran slightly over (+2% each), and Marketing — despite finishing under Budget — grew faster month-over-month (+9.6%) than any other line. A single "beat Budget" headline would hide all three of those.

**The bridges: what actually moved EBIT and Gross Profit versus Budget?**

Two waterfall charts decompose the variance instead of only stating it. The EBIT bSIhowing which line items pushed the number up and which pulled it down. The Gross Profit bridge splits the same variance into a revenue effect (0.7M) and a margin effect (0.1M–0.2M), separating "we sold more" from "we sold more profitably."

**The product chart: is margin distributed the same way as revenue?**

A combination chart compares Gross Profit and Revenue (bars) against Gross Margin % (line) by product. The ranking doesn't line up cleanly — the product with the strongest revenue isn't automatically the one with the strongest margin. That gap is exactly what the Product Portfolio Matrix on the next page investigates on a trend basis rather than a single-period snapshot.

*Next question: the month beat Budget — but does that hold for the rest of the year, and which products are actually compounding that advantage?*

### 2. Full-Year Outlook (FYFC) — Where is the year heading, not just where has it been?

![P&L Analysis page — full-year Revenue and EBIT bSI outlook, revenue by product and by country, the Product Portfolio Matrix, and operating expenses versus budget by cost center](screenshots/02-pnl-analysis.png)

Two charts blend Actual months with Forecast months into one continuous line for Revenue and EBIT bSI, plotted against the same months last year (PY). The blending is what makes a partial year readable as a full-year outlook: once Actual d bridge walks from the Budget baseline through Revenue, COGS, Personnel, Logistics, Marketing, IT, Administration, Depreciation and Other Opex to the Actual total — sata stops, Forecast picks up the remaining months automatically, so the chart never shows a gap.

The harder modeling problem sits behind this chart, not on it: Forecast only fills months Actual hasn't reached yet, so summing Actual and Forecast directly is safe. Budget, elsewhere on the report, exists for all twelve months in parallel with Actual — so any Actual+Budget blended view instead needs an explicit "use Actual where it exists, otherwise Budget" rule, or it would double-count.

*Next question: where inside that number does the revenue actually sit?*

### 3. Revenue Mix — Which products and countries make up the number?

The donut chart breaks the period's revenue down by product: the four labelled slices (Product B 630K, Product A 422K, Product D 362K, Product C 236K) already account for around 90% of the total, with Product E the smallest remaining share. The bar chart does the same by country — Germany leads at 0.65M, more than double the smallest country shown (Switzerland, 0.22M).

Neither chart says whether that concentration is a risk or simply how the business is structured — but it sets up the question the Portfolio Matrix answers next: within that product mix, which ones are actually improving?

*Next question: beyond revenue share, which products are improving in profitability — not just size?*

### 4. Product Portfolio Matrix — Which products are compounding growth with better margins?

![Product Portfolio Matrix — five products plotted by 3-month revenue growth versus 3-month gross margin change, bubble size by revenue, color-coded by trend signal](screenshots/03-product-portfolio-matrix.png)

Every product is plotted on its own trend, not a single period: 3-month revenue growth on the x-axis against 3-month gross margin change on the y-axis, bubble size scaled to revenue. A product only counts as trending "up" or "down" if it moved in the same direction for two consecutive months against the month before — one strong month isn't enough to call a trend, which keeps the signal from reacting to noise.

| Signal | Color | Definition |
|---|---|---|
| Positive Momentum | 🟢 `#0F7B2B` | Revenue and/or Gross Margin trending up over the last 3 months |
| Negative Momentum | 🔴 `#B71C1C` | Revenue and/or Gross Margin trending down over the last 3 months |
| Diverging Trend | 🟠 `#BF360C` | Revenue and Gross Margin are moving in opposite directions |
| Stable | ⚪ `#616161` | Neither measure shows a confirmed 2-month consecutive trend |

In the current period, four of five products carry a Positive Momentum signal; the fifth (Product A) is Stable — a distinct case from "declining," and one worth a closer look precisely because it isn't sending a clear signal either way. The legend above is reproduced from a small definition table built into the model, so the color-coding stays explainable without needing separate documentation.

*Next question: with revenue and margin trends understood, is spending staying inside budget?*

### 5. Cost Governance — Is spending disciplined by cost center?

The same P&L Analysis page tracks Total Operating Expenses against Budget across every cost center — Production, Logistics, Admin, IT, Sales, Marketing, HR — sorted from largest to smallest, with the Budget line overlaid directly on the Actual bars. That layout is deliberate: a favorable network-level Opex total can still hide one specific department running over budget while another offsets it, and this is the chart built to catch that.

## Recommendations

| Priority | Recommended action | Intended benefit |
|---|---|---|
| Watch the Marketing growth rate | Marketing finished under Budget but grew faster month-over-month than any other opex line (+9.6%). Track it for a second month before it becomes a Budget miss. | Catches an emerging overspend before it shows up as a variance. |
| Review the "Stable" product signal | Product A currently shows no confirmed 2-month trend on either revenue growth or margin. | Flags it for a closer look instead of assuming "no signal" means "no issue." |
| Extend Forecast-blend validation to Opex | Confirm whether Operating Expense forecast months track a flat Budget-like assumption rather than the recent Actual trend — the same gap already found and corrected in COGS forecasting. | Keeps the full-year outlook consistent across every P&L line, not only Revenue and EBIT. |
| Investigate over-budget cost centers individually | Use the cost-center chart to identify which specific department sits above its Budget line, rather than relying on the network-level Opex total. | Targets corrective action instead of a blanket cost review. |
| Re-validate the trend signal each period | Every new Actual month shifts which products qualify for a 2-month confirmed trend. | Keeps the Portfolio Matrix's color-coding meaningful rather than static. |

## Technical approach

**Power BI Desktop · DAX · Power Query (M) · Star-schema semantic model**

- **Data model:** 15 tables and 16 relationships. Three scenario-based fact tables — Actual (19,811 rows), Budget (2,880 rows), Forecast (480 rows) — share one grain and join to Date, Account, Cost Center, Product and Region dimensions.
- **Measures:** 89 explicit DAX measures, organized by display folder (e.g. `Income Statement\FY FC vs PY`, `Income Statement\Product Matrix`) covering KPIs, budget bridges, blended scenarios, and trend classification.
- **Scenario blending — two different patterns:** Actual+Forecast blends with simple addition (`[Revenue] + [FC Revenue]`), since Forecast only fills months Actual hasn't reached. Actual+Budget instead requires conditional logic (`IF(NOT ISBLANK([Revenue]), [Revenue], [BU Revenue])`), because Budget holds a value for all twelve months and a simple sum would double-count.
- **Time intelligence:** trend measures anchor to `MIN(DimDate[Date])` — the report's selected month — and use `EDATE()` to reach back two months, with `CALCULATE(..., ALL(DimDate), YEAR(...)=..., MONTH(...)=...)` so the comparison rolls correctly across a year-end boundary instead of breaking in December/January.
- **Trend-signal logic:** a four-branch `SWITCH(TRUE(), ...)` where the two conflicting-trend branches are evaluated *before* the OR-based branches. Branch order is load-bearing here — the OR conditions alone can't distinguish "both trends improving" from "one improving while the other conflicts," so the conflict checks have to run first.
- **Supporting tables:** a small disconnected table drives the Portfolio Matrix legend text and colors, kept independent of the fact model so the definitions can be edited without touching DAX. Two ordered "bridge step" tables drive the EBIT and Gross Profit waterfall charts.
- **Report design:** 2 navigation pages — Executive Overview and P&L Analysis — deliberately kept separate so the "is this month on track" view doesn't compete for space with the forward-looking and diagnostic analysis.

## Assumptions and limitations

This is a monthly simulation with project-defined Budget targets. Scenario blending assumes Forecast and Actual months never overlap, and that Budget always exists in parallel with Actual — both hold in the current dataset, but either assumption would need revisiting if the data structure changed.

The Portfolio Matrix's trend signals require two consecutive months of movement in the same direction; a single strong or weak month does not change a product's classification. This makes the signal more stable but also slower to react to a genuine, sudden change.

This repository presents the dashboard, screenshots, and the analytical write-up above. The underlying data source and full DAX/Power Query source are not included, so the calculations cannot be independently reproduced from this repository alone.

---

Built by **Thi Diep Pham** — BI & Data Analyst · Power BI Developer
[phamdiep21994@gmail.com](mailto:phamdiep21994@gmail.com)
