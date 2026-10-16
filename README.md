# Chicago Transportation Congestion & Capital Investment Prioritization

**A data-driven infrastructure capital strategy case study using Python, geospatial analytics, multi-criteria decision analysis, and constrained optimization.**

## Overview

How should a city prioritize transportation investments when congestion, roadway safety, transit needs, and limited capital funding compete for resources?

This project develops a hypothetical five-year, **$250 million transportation capital program** for Chicago. It translates transportation performance data into a corridor-level investment prioritization framework, evaluates potential infrastructure interventions, and tests how budget limits, spending constraints, and cost uncertainty affect capital allocation.

The objective is to demonstrate how engineering analysis and data-driven decision support can inform infrastructure investment strategy, capital planning, and program delivery.

> **Disclaimer:** This is an independent, hypothetical planning case study—not an official City of Chicago or Chicago Department of Transportation (CDOT) capital plan. Scoring weights, intervention costs, budget limits, and implementation schedules are illustrative assumptions.

## Business Problem

Transportation agencies must allocate finite capital budgets across projects with different needs, costs, and delivery requirements. Prioritizing solely by congestion or safety can overlook important trade-offs involving transit exposure, investment scale, affordability, and implementation timing.

This project addresses five questions:

1. Which transportation corridors should receive further investment consideration?
2. How can congestion, safety, and transit exposure be combined in a transparent prioritization framework?
3. Which infrastructure interventions are appropriate for different corridor needs?
4. What portfolio can fit within a constrained capital budget?
5. How do cost uncertainty, reserve requirements, and near-term spending limits change the recommended portfolio?

## Methodology

### 1. Congestion Analytics

Analyzed Chicago Traffic Tracker observations beginning in June 2024 to characterize corridor-level congestion.

- Established segment-level baseline speeds.
- Calculated percentage slowdown relative to baseline conditions.
- Evaluated average slowdown and the frequency of significant slowdown.
- Applied data-quality filters to improve the reliability of comparisons.
- Aggregated component-level results into investment-corridor priorities.

Congestion served as the initial screening mechanism for identifying candidate corridors.

### 2. Roadway Safety Analysis

Integrated crash data with roadway component geometries to estimate crash concentrations.

- Spatially associated crashes with candidate components.
- Calculated crashes per mile as a comparative safety indicator.
- Aggregated crash counts and roadway lengths at the investment-corridor level.
- Consolidated appropriate bidirectional components to reduce double-counting.

Crashes per mile is used as a screening indicator, not as a complete measure of crash severity, exposure-adjusted risk, or expected safety benefits.

### 3. Transit Exposure Analysis

Integrated CTA bus route geometries with 2025 route-level ridership data.

- Used projected coordinate systems for spatial analysis.
- Applied a 25-meter route buffer to evaluate spatial coverage.
- Used a 25% component-coverage threshold as an illustrative rule for identifying substantially serving routes.
- Aggregated qualifying route ridership at the corridor level, deduplicating route IDs within each corridor.

The resulting metric, **transit ridership exposure**, is a comparative proxy based on qualifying routes' ridership. It does not represent actual boardings attributable to an individual corridor.

### 4. Multi-Criteria Prioritization

Combined congestion, safety, and transit exposure into a transparent scoring framework.

| Criterion | Preliminary weight |
|---|---:|
| Roadway safety | 40% |
| Transit ridership exposure | 35% |
| Congestion | 25% |

Percentile-based scores were used to compare corridors. Higher-priority candidates were supplemented with targeted safety- or transit-led corridors to capture additional investment opportunities.

These weights and screening rules are project assumptions intended for scenario testing, not adopted agency policy.

### 5. Intervention Planning

Developed an illustrative intervention library to connect corridor needs to potential investment strategies.

| Intervention | Illustrative scope | Relative capital intensity |
|---|---|---|
| I1 — Operational optimization | Signal optimization and coordination | Low |
| I2 — Transit priority | Transit signal priority and bus-priority improvements | Low–medium |
| I3 — Intersection safety | Intersection redesign, turn-lane, and pedestrian-safety improvements | Medium |
| I4 — Corridor modernization | Multimodal corridor reconstruction and geometric improvements | High |
| I5 — Transit corridor investment | Dedicated transit treatments and broader bus-priority corridor improvements | High |

Preliminary cost ranges were assigned to intervention categories to support capital allocation and scenario analysis.

### 6. Capital Allocation and Scenario Analysis

Applied constrained optimization to select candidate projects under capital and policy constraints.

The analysis evaluated:

- A $250 million total program budget.
- A $25 million explicit reserve.
- A maximum of $120 million in spending during Years 1–3.
- A five-year implementation horizon.
- A policy scenario requiring at least nine Tier 1 projects.
- Low-, midpoint-, and high-cost estimates.

The optimization objective maximizes the sum of corridor priority scores subject to the specified constraints. Because these scores are not monetized benefits, the result should be interpreted as a **priority-score-based portfolio**, not a measured benefit-maximizing investment program.

## Illustrative Results

The selected scenario produced the following portfolio:

| Metric | Result |
|---|---:|
| Investment corridors selected | 11 |
| Total midpoint project cost | $222.5M |
| Explicit capital reserve | $25.0M |
| Total midpoint commitment | $247.5M |
| Remaining budget capacity | $2.5M |
| Tier 1 corridors selected | 9 |
| Tier 2 corridors selected | 2 |
| Years 1–3 scheduled spending | $32.375M |
| Years 1–3 spending cap | $120.0M |

The selected projects' five-year spending profiles reconcile to their midpoint costs under the assumed phasing approach.

### Cost Sensitivity

| Scenario | Project cost | Reserve | Total commitment | Variance from $250M cap |
|---|---:|---:|---:|---:|
| Low estimate | $145M | $25M | $170M | +$80M |
| Midpoint estimate | $222.5M | $25M | $247.5M | +$2.5M |
| High estimate | $300M | $25M | $325M | −$75M |

*Positive variance indicates remaining budget capacity; negative variance indicates a funding shortfall.*

The high-cost scenario exceeds the program cap by $75 million, demonstrating that a portfolio affordable at midpoint estimates may not remain affordable under cost escalation or adverse project-level estimates.
![alt text](<images/corridor allocation list .png>)
![alt text](<images/capital program cost sensitivity.png>)
A separate scenario requiring at least nine Tier 1 corridors was infeasible with a $200 million net project budget after reserving $25 million from a $225 million total budget. This illustrates the trade-off between policy requirements and available funding.
![alt text](<images/scheduled annual capital allocation.png>)
## Key Takeaways

- **Prioritization requires multiple perspectives.** Congestion alone does not capture safety burdens or the potential importance of transit-served corridors.
- **Screening and investment selection are different decisions.** A high-priority corridor must still be evaluated for intervention suitability, scope, cost, and delivery feasibility.
- **Capital constraints materially affect outcomes.** The selected portfolio changes when minimum Tier 1 requirements, reserve levels, and spending limits are introduced.
- **Cost uncertainty is a strategic risk.** The high-cost scenario requires a contingency response, scope adjustments, project deferrals, or additional funding.
- **Phasing assumptions matter.** The illustrative schedule satisfies the spending cap mathematically, but actual delivery would require project-readiness, engineering, utility, procurement, and construction assessments.

## Tools & Technologies

- **Python:** Data processing and analytical workflows
- **Pandas / NumPy:** Data cleaning, aggregation, scoring, and scenario analysis
- **GeoPandas / Shapely:** Geospatial data integration and spatial analysis
- **NetworkX / spatial indexing:** Connectivity analysis and component construction
- **SciPy:** Constrained optimization
- **Power BI:** Transportation congestion visualization and exploratory analysis

## Data Sources

The analysis draws on publicly available transportation datasets, including:

- Chicago Traffic Tracker — Historical Congestion Estimates
- Chicago roadway centerline and street geometry data
- Roadway crash data
- Chicago Transit Authority (CTA) Bus Routes
- CTA Bus Ridership — Monthly Day-Type Averages

Dataset coverage, temporal alignment, spatial joins, and data-quality limitations affect the interpretation of the results. Refer to the project notebook for the specific processing steps and assumptions.

## Limitations & Next Steps

This framework is intended to support preliminary screening and capital strategy—not replace engineering design, safety studies, or formal agency project selection.

Potential next steps include:

- Validate corridor boundaries, project scopes, and candidate interventions with agency stakeholders.
- Refine project-level cost estimates and quantify escalation and contingency requirements.
- Improve safety analysis using crash severity and exposure-adjusted measures.
- Refine transit exposure estimates with corridor-level service and ridership attribution.
- Incorporate project readiness, utility coordination, procurement, and delivery dependencies into the schedule.
- Develop measurable outcome estimates, such as crash reduction, travel-time savings, reliability improvements, and transit performance.
- Test alternative scoring weights, reserve levels, and policy constraints through sensitivity analysis.

## Repository Structure

```text
chicago-transportation-capital-strategy/
├── README.md
├── notebooks/
│   └── transportation_capital_strategy.ipynb
└── outputs/
    └── capital program cost sensitivity.png
    └── corridor allocation list.png
    └── scheduled annual capital allocation.png

```

*Adjust the repository structure above to match the files actually committed to GitHub.*

## Author

Civil engineering and infrastructure professional exploring the intersection of **transportation planning, capital strategy, program management, and data-driven decision support**.

This project demonstrates an end-to-end workflow from raw transportation data to investment prioritization, constrained capital allocation, and strategic recommendations.
