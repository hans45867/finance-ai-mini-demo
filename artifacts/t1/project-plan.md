# T1 Project Plan — Finance AI Mini Demo

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes using illustrative ETF data:

- `SPY` — US equities
- `TLT` — long-term US Treasury bonds
- `GLD` — gold

The workflow is intended to support project versioning, AI-assisted analysis, verification, and agent collaboration in later tutorials.

## Available Data

The repository provides one fixed snapshot dataset, `data/etf_snapshot.csv`, containing one row per ETF with the following columns:

| Column | Meaning |
|---|---|
| `ticker` | Short identifier for the illustrative ETF |
| `asset_class` | Broad type of asset represented by the ETF |
| `expected_return_pct` | Illustrative annual return assumption (percent per year) |
| `volatility_pct` | Illustrative annual variability assumption (percent per year) |
| `max_drawdown_pct` | Illustrative largest peak-to-trough loss (percent; negative values represent losses) |
| `expense_ratio_pct` | Illustrative annual fund fee (percent per year) |

All values are synthetic teaching data and are not live or historical market observations. The dataset is deliberately small and fixed so no download or data-cleaning step is required.

## Expected Final Deliverable

The final deliverable will be a written analysis comparing SPY, TLT, and GLD on risk and return characteristics (expected return, volatility, maximum drawdown, and expense ratio), produced through a verifiable, reproducible workflow. This project plan itself, saved at `artifacts/t1/project-plan.md`, is the first step of that workflow.

## Three Project Milestones

1. **Project setup and planning (T1):** Write and save this project plan, establishing the goal, data, and scope.
2. **Data exploration and analysis:** Load `etf_snapshot.csv` and produce descriptive comparisons and simple visualizations of the three ETFs, following the documented data dictionary.
3. **Documentation and verification:** Finalize the analysis report, verify that results match the source data, and review the workflow for reproducibility.

Analysis in milestones 2 and 3 is planned work; it has not been completed yet.

## One Data Limitation

The dataset is synthetic teaching data, so it is not suitable for investment decisions: all numeric values are illustrative assumptions rather than current quotations, verified historical estimates, or forecasts. It also omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints.

## Next Action

Have the project plan reviewed and then save it with Git (the initial commit or an update of the working tree), without committing or pushing any changes on behalf of the student. After that, proceed to the next tutorial step, which will design a bounded analysis task using this repository.
