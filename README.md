# S&P 500 Sector Portfolio Optimisation

An empirical application of Mean-Variance Optimisation (MVO) to S&P 500 sector-level portfolios, comparing equal-weighted benchmarks against portfolios that maximise the Sharpe ratio using the Critical Line Algorithm and Ledoit-Wolf covariance shrinkage.

## Motivation

Naive equal-weighting is a common baseline in portfolio construction, but it ignores the covariance structure of returns. This project tests whether formal optimisation — finding the portfolio weights that maximise risk-adjusted return — systematically improves on equal-weighting across all eleven S&P 500 sectors over a 25-year sample.

## Methods

**Mean-Variance Optimisation (Markowitz, 1952)**
Given a set of assets with expected returns and a covariance matrix, MVO finds the portfolio on the efficient frontier that maximises the Sharpe ratio — return per unit of risk. The optimal portfolio is identified using a 2% risk-free rate.

**Critical Line Algorithm (CLA)**
Markowitz's original algorithm for tracing the efficient frontier exactly. More numerically stable than generic solvers and correctly handles corner solutions where optimal weights are zero.

**Ledoit-Wolf Covariance Shrinkage**
The sample covariance matrix is a poor estimator when the number of assets is large relative to the number of observations — a common problem in equity portfolios. Ledoit-Wolf shrinks the sample covariance towards a structured target, producing a better-conditioned matrix that reduces estimation error and leads to more stable, less concentrated portfolio weights.

## Structure

1. **Data import** — S&P 500 constituents scraped from Wikipedia; daily adjusted prices via Yahoo Finance (1999–present). Stocks with less than 99% data coverage are dropped.

2. **Equal-weighted analysis** — for each sector: individual asset return and risk charts, daily portfolio returns with extreme loss markers, 30-day rolling annualised volatility.

3. **Portfolio optimisation** — CLA efficient frontier with Ledoit-Wolf covariance; optimal Sharpe ratio weights; volatility comparison, cumulative return comparison and Value at Risk (5th percentile) comparison between equal-weighted and optimised portfolios.

4. **Summary** — risk-return scatter across all sectors for both equal-weighted and optimised portfolios.

## Key Questions

- Does Ledoit-Wolf optimisation systematically reduce portfolio volatility relative to equal-weighting?
- Which sectors benefit most from optimisation, and which are already close to efficient under equal-weighting?
- How does tail risk (VaR) compare between the two approaches?

## Tools

- **Python**: pandas, numpy, matplotlib, yfinance, PyPortfolioOpt
- **Methods**: Mean-Variance Optimisation, Critical Line Algorithm, Ledoit-Wolf shrinkage, Value at Risk
- **Data**: S&P 500 via Wikipedia + Yahoo Finance (1999–present)

## Connection to Companion Analyses

This project complements the [Shiller CAPE & Market Regimes](../Shiller-PE-Ratio) and [US Treasuries](../US-Treasuries-Analysis) analyses. Where those focus on macroeconomic predictors of market returns, this project operates at the portfolio construction level — taking expected returns and risk as given and asking how to allocate optimally across assets.
