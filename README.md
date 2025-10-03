# Monte Carlo Value-at-Risk (VaR) and Expected Shortfall (ES) for a Multi-Asset Portfolio

This repository contains a concise, single-notebook implementation of **portfolio risk estimation** using **Monte Carlo simulation**, **parametric (normal) VaR**, **Expected Shortfall (ES)**, and a simple **backtest**. The portfolio includes representative ETFs for US equities, developed ex-US equities, emerging market equities, and US bonds. Historical data are downloaded with **yfinance** and daily P&L is simulated under both **log-return** and **arithmetic-return** assumptions.

---

## Project Overview
- Build a diversified **equity–bond** portfolio with user-specified tickers and weights  
- Download and clean historical price data (adjusted close)  
- Compute **log** and **arithmetic** returns and estimate mean/covariance  
- Run **Monte Carlo** simulations to obtain the P&L distribution  
- Compute **VaR** and **ES** at a configurable confidence (default 95%)  
- Compare **Monte Carlo VaR** to **parametric (normal) VaR**  
- **Backtest** the parametric VaR on historical returns (breach count & rate)  
- (Optional) Run a **correlation shock** scenario to probe sensitivity

**Key Findings (from the default example run):**  
- Monte Carlo and parametric VaR estimates are closely aligned (~£14.8k, 1-day, 95%)  
- ES(95%) is around £18.6k for the same setup  
- Backtesting shows a breach rate near 4% with 95% VaR, consistent with expectations

---

## Repository Structure
    notebooks/
      Portfolio_VaR_ES.ipynb        # Single notebook with data load, simulation, VaR/ES, backtest, and scenario
    assets/                         # Output Figure
    README.md
    requirements.txt
    LICENSE

---

## Quickstart
Clone and set up a virtual environment, then launch Jupyter.

    git clone https://github.com/joshdpaterson/portfolio-var-es
    cd portfolio-var-es
    python -m venv .venv
    source .venv/bin/activate        # Windows: .venv\Scripts\activate
    pip install -r requirements.txt
    jupyter notebook

Open the single notebook in the `notebooks/` directory and run the cells top-to-bottom.

---

## Example Workflow (Portfolio_VaR_ES.ipynb)
- Define **tickers** and **weights** (must sum to 1) and set capital, horizon, and confidence level  
- Download prices with **yfinance**, compute daily returns, inspect volatilities and correlations  
- Choose the **return model** (log or arithmetic) and estimate μ and Σ  
- Draw shocks with **Cholesky** to simulate multi-asset returns → portfolio P&L  
- Report **mean**, **volatility**, **VaR**, and **ES** from the simulated distribution  
- Compute **parametric VaR** using normal approximation and compare to Monte Carlo  
- **Backtest** the parametric VaR on historical portfolio returns (breaches & breach rate)  
- (Optional) Apply a **correlation shock** to explore sensitivity of VaR

---

## Technical Stack
- **Python**: numpy, pandas, matplotlib  
- **Data**: yfinance (adjusted close prices)  
- **Stats/Sim**: numpy RNG + Cholesky for correlated draws; NormalDist for z-scores  
- **Notebook**: single Jupyter notebook for a reproducible end-to-end workflow

---

## Results (Default Example Summary)
- Simulated mean daily return ≈ 0.04%  
- Simulated daily volatility ≈ 0.93%  
- **VaR (95%, 1-day, Monte Carlo)** ≈ **£14,800**  
- **ES (95%, 1-day, Monte Carlo)** ≈ **£18,600**  
- **Parametric VaR (95%, 1-day)** ≈ **£14,800** (very close to MC)  
- Backtest breaches ≈ **4%** of days, consistent with a 95% VaR

> These figures depend on tickers, weights, lookback window, and current market data; re-running will produce updated numbers.

---

## License
MIT — see `LICENSE`.

---

## Contact
Open an issue if you have questions about the notebook, methodology, or extending the workflow (e.g., different assets, horizons, or confidence levels).
