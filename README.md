# Singapore Bus Boarding Decision Analytics

## Project Overview

This project evaluates whether incorporating real-time crowd density information improves bus boarding decisions for commuters in Singapore. Using live data from the **Land Transport Authority (LTA) DataMall API**, the project simulates and tests two competing boarding policies across 1,097 peak-hour bus arrivals.

The analysis is structured in two phases — a counterfactual simulation (Phase 1) and a randomised A/B test (Phase 2) — culminating in a utility-based decision framework that models trade-offs between wait time and crowd discomfort.

---

## Business Problem

Singapore's public transport system is world-class, but commuter discomfort during peak hours remains a persistent pain point. When should a commuter board a crowded bus versus wait for the next one?

This project asks: **does giving commuters crowd density information lead to better boarding decisions, and at what cost?**

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python (Pandas, NumPy, SciPy) | Data processing, analysis, modelling |
| PostgreSQL | Data storage and SQL-based querying |
| LTA DataMall API | Real-time bus arrival and crowd data |
| Power BI | Dashboard and visualisation |

---

## Project Structure

```
├── Phase 1 — Counterfactual Simulation
│   ├── Rule-based group comparison
│   ├── Decision outcome matrix
│   ├── Threshold sensitivity analysis (7/10/12 min ETA)
│   └── Wait time penalty quantification
│
├── Phase 2 — Randomised A/B Test
│   ├── 50/50 random group assignment (n=1,097)
│   ├── Utility cost function (α = β = 0.2)
│   ├── Sigmoid boarding probability model
│   ├── Independent samples t-test
│   └── Power analysis
│
└── Dashboard (Power BI)
    ├── Phase 1 — Counterfactual page
    └── Phase 2 — A/B Testing page
```

---

## Key Findings

### Phase 1
- Crowd-aware policy reduced bad boarding decisions by **100%** (9.8% → 0%)
- Overall boarding rate cost: **−5 percentage points** (54% → 49%)
- Result stable across 7, 10, and 12-minute ETA thresholds
- 10-minute ETA confirmed as optimal operational cutoff

### Phase 2
- Group A (ETA only) mean boarding probability: **0.798**
- Group B (Crowd-aware) mean boarding probability: **0.729**
- Difference: **7.96 percentage points**
- T-statistic: **6.98** | P-value: **< 0.0001**
- Power analysis: minimum 241 rows required — study collected **4.5× the threshold**

---

## Analytical Conclusion

> A single boarding rule is suboptimal for all commuters. The ETA-only policy minimises wait time but exposes commuters to avoidable crowding. The crowd-aware policy improves comfort at a modest boarding rate cost. The optimal policy depends on individual commuter preference — modelled through a weighted utility function.

Singapore's high bus frequency means High crowd density is operationally rare. The policy benefit is most pronounced during peak hours and service disruptions — precisely when commuters need decision support most.

---

## Limitations and Next Steps

- Observed boarding behavior (EZ-Link tap-in data) unavailable from public API — boarding decisions are simulated using utility-based rules
- High density scenarios rare due to Singapore's transit efficiency
- Future work: apply framework to granular LTA boarding data if access were available; extend to Difference-in-Differences design using stops with/without crowd display boards

---

## Data Collection

- Source: LTA DataMall Bus Arrival v3 API
- Collection period: Peak hours (7:30–9:00am SGT  on weekdays)
- Bus stops: Multiple high-ridership Singapore stops
- Total peak-hour records: 1,097 after ETA filtering (0–30 minutes)
