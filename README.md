# USD/MXN Exchange Rate Time Series Analysis duraing Crisis (2008-2024)
## Overview
This project develops a macro-financial forecasting framework for the USD/MXN exchange rate using  GARCH models in Python.

The objective is to evaluate how macroeconomic conditions and market risk indicators affect exchange rate dynamics and volatility over time.

The analysis combines exchange rate data with domestic and international macroeconomic variables to capture both economic fundamentals and financial market sentiment.

## Research Question
How do macroeconomic indicators and financial risk factors influence the behavior and volatility of the USD/MXN exchange rate?

Specifically, this project investigates whether variables such as inflation, interest rates, oil prices, industrial activity, and market uncertainty improve forecasting performance when incorporated into ARIMAX-GARCH models.

## Dataset

Study Period

January 2008 – December 2024

The primary analysis uses observations covering the period from 2008 to 2024.

For data engineering purposes, Mexican CPI data was collected beginning in 2007 to facilitate temporal alignment and forward-filling procedures during the preprocessing stage.

## Variables

| Variable            | Description                         | Source        |
| ------------------- | ----------------------------------- | ------------- |
| USD/MXN             | Mexican Peso exchange rate          | Yahoo Finance |
| VIX                 | Market volatility index             | Yahoo Finance |
| Oil Prices (WTI)    | Global oil benchmark                | FRED          |
| Fed Funds Rate      | U.S. monetary policy rate           | FRED          |
| Banxico Rate        | Mexican policy interest rate        | Banxico API   |
| Industrial Activity | Mexican industrial production index | FRED          |
| CPI                 | Mexican Consumer Price Index        | FRED          |


## 📥 Data Collection

| Category | Variable | Source | Frequency |
|-----------|-----------|-----------|-----------|
| Exchange Rate | USD/MXN Exchange Rate | Yahoo Finance | Daily |
| Market Risk | VIX Index | Yahoo Finance | Daily |
| Commodities | WTI Crude Oil Prices | FRED | Daily |
| Monetary Policy | Fed Funds Rate | FRED | Monthly |
| Monetary Policy | Banxico Interest Rate | Banxico API | Daily / Policy Updates |
| Economic Activity | Industrial Production Index (Mexico) | FRED | Monthly |
| Inflation | Consumer Price Index (Mexico) | FRED | Monthly |

## 3 types of forecasting (Chapter 4)
The analytical forecast shows a gradual increase in expected volatility from 0.4775 to 0.4952 over the five-day horizon. This behavior reflects the high persistence estimated in the GARCH model and indicates that volatility shocks are expected to remain relevant in the short run.

The simulation forecast, based on 1,000 Monte Carlo paths, yields results almost identical to the analytical forecast. This close agreement suggests that the model's theoretical dynamics adequately capture the evolution of volatility and that simulation uncertainty is relatively small.

The bootstrap forecast, which resamples historical standardized residuals, produces slightly more irregular forecasts. Unlike the analytical and simulation methods, the bootstrap approach incorporates historical shock patterns directly from the data, resulting in small fluctuations across forecast horizons. Nevertheless, the overall forecast level remains very close to the other two approaches.

Overall, the similarity of the three forecasts provides strong evidence that the estimated GARCH(1,1) specification delivers stable and reliable short-term volatility predictions for the USD/MXN exchange rate.

## Chapter 1 — Model Variables and Macroeconomic Indicators
| Component | Equation |
|-----------|----------|
| Dependent Variable | $USDMXN_t$ |
| CPI Inflation Rate | $\pi_t=\frac{CPI_t-CPI_{t-1}}{CPI_{t-1}}\times100$ |
| Exchange Rate Change | $\Delta S_t=S_t-S_{t-1}$ |

## Chapter 2 — Data Cleaning and Transformation

| Component | Equation |
|-----------|----------|
| Forward Fill | $x_t=x_{t-1}$ |
| Backward Fill | $x_t=x_{t+1}$ |
| Linear Interpolation | $x_t=x_0+\frac{t-t_0}{t_1-t_0}(x_1-x_0)$ |
| Simple Return | $R_t=\frac{P_t-P_{t-1}}{P_{t-1}}$ |
| Log Return | $r_t=\ln\left(\frac{P_t}{P_{t-1}}\right)$ |

## Chapter 3 — Exploring Financial Time Series Data

| Component | Equation |
|-----------|----------|
| Correlation Coefficient | $\rho_{XY}=\frac{Cov(X,Y)}{\sigma_X\sigma_Y}$ |
| Sample Mean | $\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i$ |
| Sample Variance | $s^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2$ |
| Skewness | $Skew=\frac{1}{n}\sum\left(\frac{x_i-\bar{x}}{s}\right)^3$ |
| Kurtosis | $Kurt=\frac{1}{n}\sum\left(\frac{x_i-\bar{x}}{s}\right)^4$ |
| Jarque-Bera Test | $JB=\frac{n}{6}\left(S^2+\frac{(K-3)^2}{4}\right)$ |

## Chapter 4 — Volatility Modeling with GARCH(1,1)

| Component | Equation |
|-----------|----------|
| Zero Mean Process | $r_t=\varepsilon_t$ |
| Error Process | $\varepsilon_t=\sigma_t z_t$ |
| Student-t Innovations | $z_t\sim t_{\nu}$ |
| GARCH(1,1) Variance | $\sigma_t^2=\omega+\alpha\varepsilon_{t-1}^2+\beta\sigma_{t-1}^2$ |
| Estimated GARCH Model | $\sigma_t^2=0.0167+0.1122\varepsilon_{t-1}^2+0.8651\sigma_{t-1}^2$ |
| Volatility Persistence | $\alpha+\beta=0.9773$ |
| Long-Run Variance | $\sigma_{LR}^{2}=\frac{\omega}{1-\alpha-\beta}$ |

## Chapter 5 — Monte Carlo Simulation and Risk Analysis

| Component | Equation |
|-----------|----------|
| Monte Carlo Estimator | $E[X]\approx\frac{1}{N}\sum_{i=1}^{N}X_i$ |
| Cholesky Decomposition | $\Sigma=LL^{T}$ |
| Geometric Brownian Motion | $dS_t=\mu S_tdt+\sigma S_tdW_t$ |
| Discrete GBM | $S_{t+\Delta t}=S_te^{(\mu-\frac{1}{2}\sigma^2)\Delta t+\sigma\sqrt{\Delta t}Z}$ |
| Value-at-Risk (95%) | $VaR_{95}=\mu-1.645\sigma$ |
| Value-at-Risk (99%) | $VaR_{99}=\mu-2.326\sigma$ |
| Expected Shortfall | $ES_{\alpha}=E[X\mid X\le VaR_{\alpha}]$ |

## Chapter 6 — Stationarity and Time Series Diagnostics

| Component | Mathematical Representation |
|-----------|----------------------------|
| ADF Null Hypothesis | $H_0:$ Unit Root Exists |
| ADF Alternative Hypothesis | $H_1:$ Series is Stationary |
| ADF Regression | $\Delta y_t=\alpha+\beta t+\gamma y_{t-1}+\sum\delta_i\Delta y_{t-i}+\varepsilon_t$ |
| KPSS Null Hypothesis | $H_0:$ Series is Stationary |
| KPSS Alternative Hypothesis | $H_1:$ Series has Unit Root |
| Autocorrelation Function (ACF) | $\rho_k=\frac{Cov(X_t,X_{t-k})}{Var(X_t)}$ |
| Partial Autocorrelation Function (PACF) | $PACF(k)=Corr(X_t,X_{t-k}\mid X_{t-1},...,X_{t-k+1})$ |


## Recent USD/MXN News (June 2026)
1. Banxico Is Near the End of Its Rate-Cutting Cycle: Banxico lowered its benchmark interest rate to 6.50% in May 2026 but signaled that the easing cycle may be approaching its end. This is generally supportive for the peso because it helps preserve the interest-rate differential relative to the United States.
2. The U.S. Dollar Strengthened Over the Past Week: Recent U.S. economic data came in stronger than expected, leading markets to speculate that the Federal Reserve could maintain a more restrictive monetary stance for longer. This provided support for the U.S. dollar globally.
3. The Mexican Peso Remains Relatively Strong: The USD/MXN exchange rate has recently traded in a range of approximately 17.20 to 17.50, very close to the level you mentioned (17.47). Some analysts view 17.50 as an important resistance level.
4. Remittances and Peso Strength: The appreciation of the peso has reduced the purchasing power of remittances when converted into Mexican pesos, which has become a topic of recent economic analysis and discussion.


## Author
Dulce De La Paz Ortiz
Quant Finance and Economist 
Mexico City, Mexico 



