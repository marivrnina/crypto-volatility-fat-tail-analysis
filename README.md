# Fat-Tail Analysis of Cryptocurrency Returns (Bitcoin & Ethereum)

## Overview
This project studies the distribution of daily log returns for Bitcoin (BTC) and Ethereum (ETH) and tests whether they follow a normal distribution. Using historical price data, the analysis shows that both assets exhibit **fat tails, skewness, and strong deviations from normality**, which has important implications for risk management and volatility modeling.

---

## Data
- **Assets:** Bitcoin (BTC), Ethereum (ETH)  
- **Frequency:** Daily data  
- **Period:**
  - BTC: September 2010 – September 2025 (5,479 observations)
  - ETH: March 2019 – September 2025 (2,108 observations)
- **Variables used:**
  - Date  
  - Close price

**Summary Statistics (Price Levels)**

**Bitcoin:**
- Mean: $18,385.49
- Std Dev: $27,711.88
- Min: $0.06
- Max: $123,374.00

**Ethereum:**
- Mean: $1,885.44
- Std Dev: $1,289.15
- Min: $116.18
- Max: $4,796.78

---

## Methodology
The analysis follows a structured statistical workflow to assess distributional properties and tail behavior of cryptocurrency returns.

### 1. Data Preparation
- Data sorted chronologically by date
- Close prices converted to numeric format
- Combined dataset created for the overlapping period (2019 onwards)

### 2. Calculation of Daily Log Returns
Daily log returns are computed using the standard formula:

$$r_t = \log\left(\frac{P_t}{P_{t-1}}\right)$$

This transformation stabilizes variance and allows for meaningful statistical comparison across different price levels.

### 3. Descriptive Statistics of Log Returns
For both BTC and ETH log returns since 2019, the following statistics were calculated:

| Statistic | BTC | ETH |
|-----------|-----|-----|
| **Mean** | 0.0011 | 0.0016 |
| **Std Dev** | 0.0347 | 0.0475 |
| **Skewness** | -1.5581 | 1.3678 |
| **Kurtosis** | 26.3440 | 32.5315 |
| **Min** | -0.5181 | -0.3872 |
| **1%** | -0.0982 | -0.1294 |
| **5%** | -0.0493 | -0.0695 |
| **95%** | 0.0533 | 0.0699 |
| **99%** | 0.0973 | 0.1174 |
| **Max** | 0.1728 | 0.7432 |

**Key Observations:**
- Both assets show positive mean returns (BTC: 0.11%, ETH: 0.16% daily)
- ETH exhibits higher volatility (4.75% vs 3.47% daily)
- **Significant skewness**: BTC is negatively skewed (-1.56), indicating asymmetry with extreme negative returns; ETH is positively skewed (1.37)
- **Extreme kurtosis**: Both assets show excess kurtosis far exceeding 3 (BTC: 26.34, ETH: 32.53), confirming fat tails and leptokurtic distributions

### 4. Normality Testing
To formally assess whether returns follow a Gaussian distribution, four statistical tests were applied:

**Test Results:**

| Test | BTC Statistic | BTC p-value | ETH Statistic | ETH p-value |
|------|---------------|-------------|---------------|-------------|
| **Kolmogorov–Smirnov** | 0.091 | 0.0 | 0.086 | 0.0 |
| **Jarque–Bera** | 61,448.320 | 0.0 | 93,064.898 | 0.0 |
| **D'Agostino** | 1,052.630 | 0.0 | 1,024.931 | 0.0 |
| **Anderson–Darling** | 41.712 | — | 37.456 | — |

**Test Interpretations:**
- **Kolmogorov–Smirnov**: Measures the maximum gap between the cumulative distribution of the data versus a normal distribution
- **Jarque–Bera**: Tests for normality based on skewness and kurtosis; extremely high values indicate very strong deviation from normality
- **D'Agostino**: Uses skewness and kurtosis separately to test normality
- **Anderson–Darling**: Focuses on the tails (extreme values) to detect departures from normality

All four normality tests strongly reject the null hypothesis of normality (p-values ≈ 0.0). This confirms that both BTC and ETH returns are not normally distributed, primarily due to fat tails and extreme volatility clustering.

### 5. Visualization Techniques
Visual diagnostics were used to support statistical results:

- **Histograms with Normal Overlay**  
  Show empirical distribution shape compared to fitted normal distribution, revealing heavy tails and peaked centers

- **Box Plots**  
  Display outliers and extreme values in both positive and negative directions

- **Q–Q Plots (Quantile-Quantile Plots)**  
  Compare empirical quantiles against theoretical normal quantiles to illustrate deviations and tail thickness
  - Points lying on the diagonal line indicate normality
  - Deviations at the extremes confirm fat tails in both cryptocurrencies

---

## Key Findings

### Non-normal Returns
- BTC and ETH daily log returns are **not normally distributed**
- All normality tests (Kolmogorov–Smirnov, Jarque–Bera, D'Agostino, Anderson–Darling) strongly reject Gaussian assumptions with p-values ≈ 0

### Fat Tails (Leptokurtosis)
- Both assets exhibit **extreme excess kurtosis** (BTC: 26.34, ETH: 32.53)
- This implies a much higher probability of extreme events than predicted by normal distribution models
- The 1st and 99th percentiles show significant tail risk beyond normal expectations

### Skewness and Asymmetry
- **Bitcoin**: Negatively skewed (-1.56), indicating higher frequency and magnitude of extreme negative returns (crash risk)
- **Ethereum**: Positively skewed (1.37), indicating occasional extreme positive returns
- Asymmetric return distributions require different risk management approaches for upside vs downside

### Higher Volatility in Ethereum
- ETH shows 37% higher standard deviation than BTC (4.75% vs 3.47% daily)
- ETH exhibits more extreme maximum daily return (74.32% vs 17.28%)
- Both assets show volatility clustering typical of financial time series

### Model Risk
Risk models assuming normality (e.g., basic Value-at-Risk relying only on mean and variance) will severely:

- **Underestimate crash probability**: Fat tails mean extreme losses occur more frequently than normal models predict
- **Misprice downside risk**: Negative skewness in BTC means left-tail risk is particularly underestimated
- **Fail during market stress events**: Normal distribution fails to capture the clustering of extreme volatility during crises

---

## Practical Implications

### Why Normal Distribution Fails for Crypto
1. **Extreme events are not rare**: Kurtosis values of 26-32 indicate extreme returns occur far more often than the normal distribution predicts
2. **Asymmetric risk**: Skewness means upside and downside risks are fundamentally different
3. **Volatility clustering**: Crypto markets exhibit periods of calm followed by intense volatility, violating independence assumptions

### Alternative Modeling Approaches
To model cryptocurrency risk more realistically, heavy-tailed and flexible approaches are required:

- **Student's t-distribution**: Accommodates fat tails through degrees of freedom parameter
- **Extreme Value Theory (EVT)**: Specifically models the distribution of extreme returns
- **GARCH models**: Captures volatility clustering and time-varying risk
- **Historical simulation**: Uses actual empirical distribution without parametric assumptions
- **Non-parametric bootstrapping**: Resamples actual data to generate risk scenarios

These methods better capture tail risk and extreme volatility inherent in crypto markets.

### Risk Management Recommendations
1. **Do not rely on normal VaR**: Use historical or Monte Carlo VaR with fat-tailed distributions
2. **Stress testing**: Incorporate extreme scenarios beyond normal confidence intervals
3. **Tail risk hedging**: Use options or other derivatives to hedge against extreme moves
4. **Dynamic position sizing**: Adjust exposure based on realized volatility and market conditions
5. **Diversification limits**: Recognize that correlations may increase during extreme events

---

## Conclusion
The analysis confirms that Bitcoin and Ethereum returns exhibit **strong departures from normality**, characterized by:

- **Fat tails** (extreme excess kurtosis: 26-32)
- **Skewness** (asymmetric distributions: -1.56 for BTC, +1.37 for ETH)
- **Rejection of normality** across all statistical tests (p-values ≈ 0)

These findings highlight the **necessity of advanced statistical models** when performing risk assessment, portfolio construction, or volatility forecasting in cryptocurrency markets. Traditional risk models based on normal distribution assumptions will systematically underestimate tail risk and fail during periods of market stress, which are more frequent in crypto than in traditional asset classes.
