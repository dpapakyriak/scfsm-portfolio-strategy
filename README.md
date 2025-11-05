# Sector-Calibrated Factor Scoring Model (SCFSM)

## Abstract
The **Sector-Calibrated Factor Scoring Model (SCFSM)** introduces a systematic framework for quantitative equity selection and portfolio construction.  
The model integrates sector-specific regression analysis, empirical factor benchmarking, and normalization techniques to identify assets with superior expected performance across global equity markets.  
It aims to generate positive risk-adjusted returns and outperform the MSCI ACWI benchmark while maintaining a diversified, sector-balanced exposure.

---

## Methodology

### 1. Investment Universe
The analysis begins with the top 50 weighted constituents of the MSCI Index, which collectively explain over 95% of total index variance.  
This ensures global diversification and liquidity while maintaining exposure to the dominant drivers of market performance.

Let the investment universe be represented by

\[
\mathcal{U} = \{ S_1, S_2, \dots, S_N \}
\]

where each \( S_i \) denotes a stock in the universe.

---

### 2. Data Collection and Factor Definition
Eighteen fundamental metrics are collected on a quarterly basis for each firm over the past ten years.  
These metrics cover valuation, profitability, leverage, and growth characteristics.

| Category | Example Metrics |
|-----------|----------------|
| Valuation | P/E, EV/EBIT, Price-to-Book |
| Profitability | ROA Surplus, ROE Surplus, Operating Margin |
| Growth | Earnings per Share, Market Value Growth |
| Leverage/Liquidity | Debt Ratio, Current Ratio, Quick Ratio |

Let \( X = [x_1, x_2, \dots, x_n] \) denote the vector of financial factors for each firm.

---

### 3. Sector-Specific Regression Estimation
Each sector \( s \) is modeled independently to account for its structural sensitivities.  
A cross-sectional regression relates sectoral returns to financial factors:

\[
R_{s,t} = \alpha_s + \sum_{i=1}^{n} \beta_{s,i} X_{i,t} + \varepsilon_{s,t}
\]

where  
- \( R_{s,t} \) is the return of sector \( s \) at time \( t \),  
- \( \beta_{s,i} \) is the estimated coefficient of factor \( i \) for sector \( s \),  
- \( \varepsilon_{s,t} \) is the residual error term.

Only statistically significant factors (\( p < 0.05 \)) are retained for subsequent scoring.  
This ensures that factor weights reflect the true explanatory power within each sector.

---

### 4. Benchmark Threshold Calibration
For each financial factor, benchmark thresholds are established using a combination of empirical quantiles and literature-based standards.  
Each stock is assigned a binary value depending on whether it exceeds the benchmark condition.

\[
B_i =
\begin{cases}
1, & \text{if } X_i \text{ satisfies benchmark condition} \\
0, & \text{otherwise}
\end{cases}
\]

### 5. Sectoral Normalization
To ensure comparability within sectors, a min–max normalization is applied to each metric:

\[
S_{i,j} = \frac{X_{i,j} - \min(X_i)}{\max(X_i) - \min(X_i)}
\]

This normalization process eliminates scale bias across industries and enables consistent scoring of companies across the global equity universe.

---

### 6. Factor Scoring and Aggregation
Each firm receives a composite factor score calculated as a weighted sum of normalized scores:

\[
F_j = \sum_{i=1}^{n} w_i \, S_{i,j}
\]

where \( w_i \) represents the weight of factor \( i \), derived from sector-specific regression coefficients \( \beta_{s,i} \), normalized to sum to unity.  

Stocks are ranked by \( F_j \) within each sector and globally to identify top candidates for portfolio inclusion.

---

### 7. Portfolio Construction
The top-ranked assets by \( F_j \) are included in the model portfolio.  
Weights may then be optimized under a Sortino ratio objective:

\[
\max_{w} \; \frac{E[R_p] - R_f}{\sigma_{d,p}}
\]

subject to

\[
\sum_i w_i = 1, \quad w_i \ge 0
\]

where  
- \( E[R_p] = w^T \mu \) is the expected portfolio return,  
- \( \sigma_{d,p} = \sqrt{E[\min(0, w^T R - R_f)^2]} \) is the downside deviation,  
- \( R_f \) is the risk-free rate.  

This produces a long-only, fully invested portfolio optimized for downside risk-adjusted performance.

---

## Mathematical Summary

| Symbol | Definition |
|:--|:--|
| \( R_{s,t} \) | Sectoral return at time \( t \) |
| \( X_i \) | Financial factor \( i \) |
| \( \beta_{s,i} \) | Sectoral factor loading |
| \( S_{i,j} \) | Normalized factor score for firm \( j \) |
| \( F_j \) | Aggregate factor score for firm \( j \) |
| \( w_i \) | Portfolio weight on asset \( i \) |
| \( R_p \) | Portfolio return |
| \( \sigma_{d,p} \) | Downside deviation |
| \( \text{Sortino} = \frac{E[R_p] - R_f}{\sigma_{d,p}} \) | Portfolio optimization objective |

---

## Empirical Results

| Rank | Ticker | Sector | Score |
|------|--------|--------|-------|
| 1 | META | Communication Services | 0.93 |
| 2 | LLY | Health Care | 0.90 |
| 3 | NOVO-B.CO | Health Care | 0.88 |
| 4 | HD | Consumer Discretionary | 0.87 |
| 5 | ASML.AS | Information Technology | 0.84 |
| 6 | LIN | Materials | 0.82 |
| 7 | WMT | Consumer Staples | 0.81 |
| 8 | XOM | Energy | 0.80 |
| 9 | BRK-B | Financials | 0.79 |
| 10 | GE | Industrials | 0.77 |
| 11 | MA | Financials | 0.76 |
| 12 | SHEL.L | Energy | 0.74 |
| 13 | NESN.SW | Consumer Staples | 0.73 |
| 14 | 9988.HK | Communication Services | 0.72 |
| 15 | 2330.TW | Information Technology | 0.71 |

The resulting portfolio demonstrates consistent exposure to firms exhibiting above-average profitability, strong balance sheets, and stable growth relative to their sectoral peers.

---

## Performance Evaluation
To assess portfolio efficiency, risk-adjusted performance is evaluated using the Sharpe and Sortino ratios, as well as alpha and volatility measures.

Let \( R_p \) and \( R_b \) denote the portfolio and benchmark returns, respectively.

\[
\text{Alpha} = E[R_p - R_b]
\]
\[
\text{Sharpe} = \frac{E[R_p] - R_f}{\sigma_p}
\]
\[
\text{Sortino} = \frac{E[R_p] - R_f}{\sigma_{d,p}}
\]

Drawdown and volatility analyses are used to evaluate downside protection and capital stability over time.  
The SCFSM model exhibits superior downside control relative to benchmark indices due to its sector-calibrated risk management mechanism.

---

## Discussion
The SCFSM provides a sector-aware approach to factor-based investing by decomposing return drivers at the industry level.  
This design improves upon generic multi-factor models by aligning factor exposure with sector-specific sensitivities, enhancing both interpretability and empirical robustness.  
The normalization and calibration mechanisms ensure that each factor’s contribution is comparable across industries and market conditions.

---

## References
- Sortino, F. A., & Van der Meer, R. (1991). *Downside Risk.* *Journal of Portfolio Management,* 17(4), 27–31.  
- Sharpe, W. F. (1966). *Mutual Fund Performance.* *Journal of Business,* 39(1), 119–138.  
- López de Prado, M. (2018). *Advances in Financial Machine Learning.* Wiley.  
- Fama, E. F., & French, K. R. (1993). *Common Risk Factors in the Returns on Stocks and Bonds.* *Journal of Financial Economics,* 33(1), 3–56.


---

## Author
Developed by **Dimitrios Papakyriakopoulos** as part of a research project on quantitative equity modeling and sector-specific factor analysis for systematic portfolio construction.

