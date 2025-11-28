# MonteCarloOptionPricing
# 🎲 Monte Carlo Simulation: Portfolio Risk & Option Pricing

![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)
![Finance](https://img.shields.io/badge/Quantitative-Finance-green?style=for-the-badge&logo=cashapp)
![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

## 📖 Executive Summary

This project implements a sophisticated **Monte Carlo Simulation engine** designed for Quantitative Finance applications. It serves two primary purposes: **Portfolio Risk Assessment** and **Derivatives Valuation**.

By leveraging repeated random sampling, this tool approximates complex mathematical quantities that are difficult or impossible to solve analytically. The project moves from calculating downside risk metrics (VaR/CVaR) using historical correlations to pricing European Call Options using the **Risk-Neutral Valuation framework**.

---

## 🚀 Key Capabilities

### 1. Advanced Data Pipeline
* **Dynamic Ingestion**: Automatically downloads historical financial data using the `yfinance` API.
* **Asset Support**: Configured to handle a diverse basket of equities including **AAPL, TSLA, NVDA, MSFT, WMT, and JPM**.
* **Statistical Analysis**: Computes daily returns, mean returns, and full covariance matrices ($\Sigma$) to understand asset interdependencies.

### 2. Correlated Portfolio Simulation
* **Cholesky Decomposition**: Uses linear algebra to decompose the covariance matrix ($L$), allowing the generation of **correlated random shocks** ($Z$).
* **Path Generation**: Simulates **80,000 distinct price paths** over a 200-day horizon to generate a robust probability distribution of future portfolio values.

### 3. Quantitative Risk Metrics
* **Value at Risk (VaR)**: Calculates the maximum expected loss at a 95% confidence level.
* **Conditional Value at Risk (CVaR)**: Also known as Expected Shortfall, this measures the average loss in the worst-case scenarios (tail risk).

### 4. Risk-Neutral Option Pricing
* **Measure Change**: Adapts the simulation from the physical measure (historical drift) to the risk-neutral measure (drift = risk-free rate).
* **Drift Adjustment**: Replaces historical returns with the daily risk-free rate ($r/252$).
* **Discounting**: Implements continuous discounting ($e^{-rT}$) to determine the fair present value of European Call Options.

---

## 🛠️ Installation & Dependencies

To replicate this analysis, ensure your environment is set up with the necessary scientific computing libraries.

### Requirements
The project relies on the standard Python quantitative stack:
* `numpy`: For vectorization and matrix operations (Cholesky decomposition).
* `pandas`: For time-series data manipulation.
* `scipy`: For statistical functions.
* `matplotlib`: For visualizing price paths and distributions.
* `yfinance`: For market data extraction.

### Setup Command
```bash
pip install numpy scipy matplotlib pandas yfinance

### 📊 Theoretical Framework
The Monte Carlo Method
Originating in the 1940s at Los Alamos (Ulam, von Neumann, Metropolis), Monte Carlo simulation uses massive random sampling to estimate results. In this project, we model the evolution of stock prices as a stochastic process.

Mathematical Model: Portfolio Simulation
We assume the portfolio returns follow a multivariate normal distribution. To maintain the historical correlation between assets (e.g., if NVDA rises, AAPL might also rise), we use Cholesky Decomposition.
