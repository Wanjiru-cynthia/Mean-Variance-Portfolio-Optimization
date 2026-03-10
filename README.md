# Mean-Variance Portfolio Optimization

## Overview
This project implements Markowitz Mean-Variance Optimization on a 
10-stock portfolio across 5 sectors. We find the optimal portfolio 
weights that maximize the Sharpe Ratio and visualize the Efficient 
Frontier across 10,000 simulated portfolios.

## Portfolio Components
| Ticker | Company | Sector |
|--------|---------|--------|
| MSFT | Microsoft | Technology |
| GOOGL | Alphabet | Technology |
| JPM | JPMorgan Chase | Finance |
| GS | Goldman Sachs | Finance |
| JNJ | Johnson & Johnson | Healthcare |
| PFE | Pfizer | Healthcare |
| AMZN | Amazon | Consumer |
| BRK-B | Berkshire Hathaway | Diversified |
| TGT | Target | Retail |
| WMT | Walmart | Retail |

## Methodology

### Data
Five years of daily closing prices (2019–2024) sourced via yfinance 
(1,509) trading days per stock. Period captures COVID crash, 2022 
rate hike cycle, and post-pandemic recovery.

### Expected Returns
Mean historical annual returns calculated using PyPortfolioOpt's 
`mean_historical_return()` — annualized from daily returns.

### Risk Model
Sample covariance matrix estimated from historical returns using 
PyPortfolioOpt's `sample_cov()` — captures pairwise correlations 
across all 10 stocks (10×10 matrix).

### Optimization
Portfolio weights optimized using PyPortfolioOpt's 
`EfficientFrontier` — maximizing the Sharpe Ratio subject to:
- Weights sum to 1
- No short selling (all weights ≥ 0)
- Risk-free rate = 5.0%

### Efficient Frontier
10,000 randomly weighted portfolios simulated to map the full 
risk-return tradeoff space. Each portfolio's Sharpe Ratio 
color-coded from purple (low) to yellow (high).

## Results

### Expected Annual Returns by Stock
| Ticker | Expected Return |
|--------|----------------|
| MSFT | 28.37% |
| GS | 25.24% |
| GOOGL | 24.10% |
| WMT | 21.46% |
| AMZN | 19.31% |
| JPM | 19.28% |
| TGT | 15.39% |
| BRK-B | 14.34% |
| JNJ | 4.82% |
| PFE | -3.12% |

### Optimal Portfolio (Maximum Sharpe Ratio)
| Metric | Value |
|--------|-------|
| Expected Annual Return | 24.45% |
| Annual Volatility | 19.83% |
| Sharpe Ratio | 0.98 |

## Interpretation & Recommendations
- The optimizer heavily favored **MSFT, GS and WMT** — high 
  return stocks with favorable risk-adjusted profiles
- **PFE** received zero allocation — its -3.12% expected return 
  made it impossible to justify inclusion in an optimized portfolio
- **WMT** received meaningful allocation despite lower returns 
  than MSFT — its defensive low-volatility profile reduced overall 
  portfolio risk, improving the Sharpe Ratio
- A Sharpe Ratio of **0.98** reflects the drag of underperforming 
  healthcare stocks (PFE, JNJ) in the universe — removing them 
  is expected to push the Sharpe Ratio above 1.2
- The 2019–2024 period includes significant stress events — 
  COVID crash, 2022 rate hike selloff, Pfizer post-pandemic 
  collapse — making these results conservative relative to 
  a normalized market environment

## Tools
Python
NumPy 
Pandas  
yfinance 
PyPortfolioOpt  
Matplotlib


## Author
Cynthia Wanjiru | MS Quantitative Finance | Washington University in St Louis
