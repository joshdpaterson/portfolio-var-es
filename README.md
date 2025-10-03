# Portfolio VaR & ES Analysis

This repository contains the code from my project on quantifying portfolio downside risk using Value-at-Risk (VaR) and Expected Shortfall (ES). It uses historical ETF data, Monte Carlo simulation, and a parametric normal approximation to estimate potential losses, and validates results through a simple backtest.

The project involved: collecting and cleaning ETF price data (SPY, EFA, IEMG, AGG); computing log and arithmetic returns with proper alignment of tickers and weights; estimating mean returns and covariance matrices; running large-scale Monte Carlo simulations (200k+ paths) with Cholesky decomposition; calculating VaR and ES at 95% confidence for a £1M portfolio; performing a backtest of historical VaR breaches to check calibration; and stress-testing diversification by applying correlation-shock scenarios. Relevance: practical quantitative risk management, statistical modeling, and reproducible financial analysis in Python.

---

## Repository Structure

notebooks/
  portfolio_var_es.ipynb     — Main notebook (simulation, VaR/ES, backtests)
assets/                      — Example plots (P&L histograms, correlation matrices)
requirements.txt             — Python dependencies
README.md
LICENSE

---

## Quickstart

Clone the repository and set up a virtual environment:

$ git clone https://github.com/joshdpaterson/portfolio-var-es
$ cd portfolio-var-es
$ python -m venv .venv
$ source .venv/bin/activate    (Windows: .venv\Scripts\activate)
$ pip install -r requirements.txt
$ jupyter notebook

Open notebooks/portfolio_var_es.ipynb and run the cells in order. The notebook will download data, run simulations, and generate risk metrics.

---

## Project Overview

Data Preparation — Fetches adjusted close prices via yfinance (2015–present); computes log returns (for modeling) and arithmetic returns (for realized P&L); validates alignment between tickers, weights, and covariance matrices.

Monte Carlo Simulation — Generates correlated return scenarios with Cholesky decomposition; supports both log-return and arithmetic-return models; produces a simulated distribution of portfolio P&L.

Risk Metrics — Value-at-Risk (VaR): worst loss not exceeded with 95% probability. Expected Shortfall (ES): average loss in the worst 5% of cases. Both are computed from the simulated distribution and compared with a parametric normal approximation.

Backtesting — Compares historical portfolio returns to the parametric 95% VaR; reports breach rate (e.g., ~4% vs expected 5%, slightly conservative).

Stress Testing — Applies a correlation shock that blends off-diagonal correlations toward a target (e.g., ρ = 0.25 or ρ = 0.9) to explore diversification breakdowns when markets move together.

---

## Technical Stack

Python (numpy, pandas, matplotlib); yfinance for historical data; Jupyter Notebooks for reproducibility; Monte Carlo methods and basic risk statistics.

---

## Key Concepts

Log vs arithmetic returns; label-safe portfolio math to avoid misalignment; multivariate normal simulation via Cholesky; VaR vs ES (quantile vs tail mean); backtesting breach rates; correlation shocks as a simple systemic-risk stress test.

---

## Results (Example)

For a portfolio of 50% SPY, 20% EFA, 15% IEMG, 15% AGG: daily volatility ≈ 0.93%; 1-day 95% VaR ≈ £14,800 (≈1.48% of £1M capital); ES ≈ £18,600; parametric VaR closely matches Monte Carlo; backtest breaches ≈ 4% vs theoretical 5%; lowering equity–equity correlations (ρ → 0.25) reduces VaR, while raising correlations increases VaR.

---

## Reproducibility Notes

Default alpha = 95%, horizon = 1 day; weights sum to 1 (0.50, 0.20, 0.15, 0.15); data window 2015–present; fixed random seed for reproducible Monte Carlo.

---

## License

MIT License — see LICENSE.

---

## Contact

Questions or ideas for extensions? Please open an issue or reach out.
