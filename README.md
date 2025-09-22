Natural Gas Price Estimation & Forecasting

This project estimates and forecasts natural gas prices using statistical decomposition.
The approach captures both trend and seasonality, extrapolates prices 12 months into the future, and interpolates daily prices so that users can query the estimated price for any date between Oct 2020 – Sep 2025.

🔹 Dataset

Source: Simulated monthly snapshots of natural gas market prices.
Period: October 2020 → September 2024.
Each record = end-of-month price.

🔹 Methodology
Data Preparation
Converted Dates to datetime format and set as index.
Ensured monthly frequency (asfreq('M')).
Log-transformed prices for stability.
Seasonal Decomposition

Split series into:

Trend – long-term upward drift.
Seasonal – repeating annual cycle (winter peaks, summer troughs).
Residual – noise/unexplained variation.

Forecasting (12 months ahead)

Applied a seasonal naïve approach:
Used the average trend from the last 12 months as baseline.
Repeated the most recent seasonal cycle.
Generated forecasted monthly log-prices, then converted back to actual prices.

Daily Interpolation

Implemented estimate_price("YYYY-MM-DD") function.
Interpolates between monthly log-prices to estimate daily prices.
Ensures smoothness and positivity.



from src.estimator import estimate_price
import pandas as pd

# Example queries
print(estimate_price("2023-07-15", full_df))  # Historical mid-month date
print(estimate_price("2025-05-15", full_df))  # Forecasted mid-month date
