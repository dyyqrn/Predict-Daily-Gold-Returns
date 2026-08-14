# Gold Price Return Prediction (2010–2025)

## Project Overview

This project tests whether machine learning can predict the daily price movement (daily percentage return) of PT Antam gold in Indonesian Rupiah (IDR) using only past price patterns and technical history.

## Problem Challenge

High Noise, Low Signal: Stock and commodity prices are tricky to predict on a daily basis because daily changes are mostly random noise.

Cheating Risks (Data Leakage): When building price prediction models, it is very easy to accidentally give the model future information by mistake (example: using today's price average to predict today's return), leading to fake "perfect" results.

## Solution Approach

- Daily Percentage Changes (Log Returns): Instead of raw gold prices the dataset was converted into daily log returns to make the data stationary and stable for machine learning.
- Strict Anti-Leakage Rules: All technical features (past daily price lags and rolling averages) were explicitly shifted back by 1 step (shift(1)) so models only look at data available yesterday.
- Fair Time Split: Data from 2010–2022 was used for training, and unseen future data from 2023–2025 was kept strictly for realistic testing.

## Models Used

1. Naive Baseline Model: A simple baseline model that always guesses 0 return (no price change) for every single day.

2. Linear Regression: A standard statistical model to test simple linear relationships.

3. Random Forest Regressor: A flexible tree-based model designed to catch complex, non-linear price patterns.

## Model Performance (Test Set)

| Model | Accuracy Score (R2) | Avg Error (MAE) | Total Error (RMSE) | Direction Guess (Up/Down) |
| --- | --- | --- | --- | --- |
| Naive Baseline (Predict 0) | N/A | 0.004707 | 0.007161 | N/A |
| Linear Regression | -0.0480 | 0.005029 | 0.007287 | 37.36% |
| Random Forest Regressor | -0.0250 | 0.004829 | 0.007207 | 39.87% |

## Key Findings
1. The Simple Guess Won: Simply predicting zero return (the Naive Baseline) had lower overall error than both machine learning models.
2. Negative Scores ($R^2$): Both Linear Regression and Random Forest performed slightly worse than guessing the average daily change.
3. Directional Guessing: The models only got the direction (Up or Down) right around 37%–39% of the time, which is below a simple coin flip (50%).

## Technical Insights

- The Market is Efficient: Past price trends alone do not hold enough secret clues to predict tomorrow's gold price. This aligns with the Weak-Form Efficient Market Hypothesis (EMH).

- What Mattered Most: Feature analysis showed that 7-day average price volatility and 90-day long-term memory were the strongest predictors, but still not strong enough on their own.

## Conclusion

While the machine learning models successfully trained on 12 years of historical data, relying purely on past price trends (technical analysis) isn't enough to beat a simple zero-change benchmark. Real-world daily gold prices in IDR behave very close to a random walk when looking strictly at price history.

## Tech Stack

- Language: Python
- Data Prep: Pandas, NumPy
- Machine Learning: Scikit-learn
- Data Visualization: Matplotlib, Seaborn

## Future Improvements

To build a model that can beat the baseline, future versions need real-world economic context instead of just past prices:

1. Global Economic Data: Add USD to IDR exchange rates, US interest rates (Fed Rate), and domestic inflation figures.
2. Market Sentiment & News: Use NLP (Natural Language Processing) to analyze financial news headlines and market sentiment scores.
3. Advanced Models: Try specialized volatility models (GARCH) and gradient boosting frameworks (LightGBM/XGBoost).
