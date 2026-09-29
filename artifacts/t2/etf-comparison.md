# ETF Comparison — SPY, TLT, GLD (Annual Fees and Maximum Drawdown)

This report continues the T1 ETF-comparison plan by upgrading from the synthetic `etf_snapshot.csv` to the T2 ETF Data Pack of real daily price history.

## Source and Method Details

- **Input paths:** `data/t2/data_dictionary.md`, `data/t2/fund_info.csv`, `data/t2/daily_prices.csv`
- **Preparation date:** 2026-09-25 (T2 ETF Data Pack; retained source downloads recorded 2026-09-20)
- **Common drawdown period:** 2016-09-01 through 2026-08-31 (inclusive), 2,512 observations per ETF
- **Frequency and adjustment basis:** daily US market sessions; calculation uses `adjusted_close` (provider split- and dividend-adjusted prices) for every observation in the window
- **Fee disclosure details:**
  - SPY: 0.0945% — fund-information as-of date 2026-09-10; fee-specific effective date not stated; accessed 2026-09-25
  - TLT: 0.15% — current prospectus; specific date not stated in the fee panel; accessed 2026-09-25
  - GLD: 0.4% — not stated in the selected field; accessed 2026-09-25
- **Script:** `artifacts/t2/calculate_drawdown.py`
- **Command executed:** `python artifacts/t2/calculate_drawdown.py` (from repository root)
- **Input check result:** all checks passed (header columns; 7,536 rows; exactly SPY/TLT/GLD; unique ticker/date pairs; 2,512 rows per ETF; strictly ascending dates; window first/last 2016-09-01 and 2026-08-31; matching date sets across tickers; all close and adjusted_close values positive and finite)
- **Calculation method:** for each ticker, dates ascending, cumulative high from window start; `drawdown_t = (adjusted_close_t / high_t - 1) * 100`; maximum drawdown = minimum of these values; peak must be on or before trough; earliest-trough/earliest-peak tie rule; full precision kept internally, rounded only for display.

## 1. Comparison

| ETF | Annual expense ratio (%) | Calculated maximum drawdown (%) | Peak date | Trough date |
|---|---|---|---|---|
| SPY | 0.0945 | -33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | -48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | -26.40 | 2026-01-29 | 2026-07-16 |

## 2. Observation

GLD has the smallest drawdown loss (closest to zero) in this period: **-26.40%**, versus SPY **-33.72%** and TLT **-48.35%** on the displayed two-decimal results; there are no ties. These drawdowns were calculated from `adjusted_close` in `data/t2/daily_prices.csv`, not read from a precomputed snapshot; drawdowns are non-positive, so closer to zero means a smaller loss. Limitation: these maximum drawdowns are measured from daily adjusted closes within the fixed 2016-09-01 to 2026-08-31 window only, so they are not all-time drawdowns, do not capture intraday losses, and the fees above are current issuer disclosure snapshots (accessed 2026-09-25), not ten-year averages.

## 3. Agent Check (self-check by the agent)

- **ETF chosen:** GLD (the smallest-loss ETF from the observation).
- **Source rows re-read from `data/t2/daily_prices.csv`:**
  - 2026-01-29, GLD, close=495.8999938964844, adjusted_close=495.8999938964844 (peak)
  - 2026-07-16, GLD, close=364.9599914550781, adjusted_close=364.9599914550781 (trough)
- **Check command:** a small local Python check script (kept outside the repository) that re-reads the CSV, prints the two rows, and recomputes `(trough / peak - 1) * 100`.
- **Actual output:** `recomputed (trough/peak - 1)*100 = -26.404517857029663`; `display two decimals = -26.40%`; `match (two decimals): True`; `peak <= trough: True`; full-series GLD recheck: 2,512 rows processed, max drawdown -26.404517857029663 with the same peak 2026-01-29 / trough 2026-07-16 pair.
- **Comparison and result:** the recomputed value matches the report's displayed -26.40%, the peak (2026-01-29) is on or before the trough (2026-07-16), and the full-series method inspection (all dates, all adjusted_close values, cumulative highs, earliest-trough/earliest-peak tie rule) reproduces the reported pair. Observation rechecked against all three results: GLD -26.40% remains closest to zero, with no ties. No correction was needed.
- This check was performed by the agent as its own self-check; it is not an independent verification, and no student review of the data was performed.
