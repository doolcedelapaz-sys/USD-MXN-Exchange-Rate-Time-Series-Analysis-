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
