# Gold Price Return Prediction (2010–2025)

## Project Overview

This project aims to predict daily gold price log returns using machine learning models.
The dataset spans from 2010 to 2025 and includes historical gold prices with timestamps.

The objective is to evaluate whether lag-based technical features can explain future gold return movements.

## Problem Challenge

Initial modeling using raw gold prices resulted in:

1. Extremely high Train R² (~0.99)
2. Negative Test R² (~ -1.15)

This issue was caused by:

Non-stationary process

Gold price levels exhibit long-term trends and regime shifts, making raw price prediction unstable.

## Solution Approach

To address non-stationarity, the target variable was transformed into:

Log Return

This transformation stabilizes the mean and variance, improving generalization.

Steps:
1. Convert and sort datetime
2. Compute daily log returns
3. Create lag features (1, 2, 3, 7, 14, 30 days)
4. Add rolling mean and rolling volatility features
5. Apply time-based train-test split
6. Compare baseline and ensemble models

## Models Used

A. Baseline: Linear Regression

B. Ensemble: Random Forest Regressor

## Model Performance (Test Set)

### Linear Regression
R²    : 0.192	
MAE    : 0.00474	
RMSE    : 0.00640

### Random Forest	
R²    : 0.195
MAE    : 0.00460	
RMSE    : 0.00639 

## Key Findings
1. Random Forest slightly outperformed Linear Regression.
2. Performance difference is small, suggesting limited nonlinear structure in lag-based features.
3. Model captures general directional movement but underestimates extreme volatility spikes.
4. Proper handling of time-series stationarity significantly improved generalization.

## Technical Insights

This project demonstrates:

1. Handling of time-series non-stationarity
2. Prevention of data leakage via time-based split
3. Feature engineering for financial returns
4. Baseline model comparison
5. Overfitting reduction
6. Proper out-of-sample evaluation

## Conclusion

While predicting financial returns remains inherently noisy, the model explains approximately 19.5% of out-of-sample variance, indicating that lag-based return features contain predictive signal.

The project highlights the importance of:

1. Transforming non-stationary data
2. Comparing against simple baselines
3. Evaluating models using realistic time splits

## Tech Stack
1. Python
2. Pandas
3. NumPy
4. Scikit-learn
5. Matplotlib

## Future Improvements
1. Time series cross-validation
2. Additional macroeconomic features
3. Gradient boosting comparison
4. Feature importance analysis
