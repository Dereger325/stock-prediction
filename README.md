# NVIDIA Stock Price Prediction

## Problem
Predict NVIDIA's next-day closing price using historical price and volume data. 
Unlike retail sales forecasting where promotions and seasonality drive predictable 
patterns, stock prices are influenced by news, earnings, and macroeconomic events 
that are invisible to technical indicators.

## Dataset
NVIDIA (NVDA) historical data from Yahoo Finance, January 2020 to December 2024, 
covering 1,257 trading days. Features used: closing price, volume, and 
engineered technical indicators.

## Approach
Built 12 technical features including lag features (1, 2, 5, 10 days), rolling 
means and standard deviation (5, 20 days), momentum indicators, MA crossover, 
and volume ratio. Used walk-forward validation with 5 folds instead of random 
split — random splitting would allow the model to train on future prices, 
corrupting evaluation.

## Results

| Metric | Value |
|--------|-------|
| Baseline MAPE (random walk) | 2.46% |
| Model MAPE | 52.24% |
| Direction Accuracy | 42.34% |
| Random Direction Baseline | 50.00% |

## Key Finding
The model fails catastrophically on 2024 data because NVIDIA's AI-driven price 
surge represents a structural break — a new market regime the model was never 
trained on. Technical indicators assume the future resembles the past; when it 
doesn't, no amount of feature engineering or hyperparameter tuning can recover. 
External signals such as earnings sentiment, analyst estimates, and macro 
indicators would be required to detect regime changes before they happen.

## What Would Improve This Model
1. Sentiment features — NLP on earnings calls, news headlines
2. Macro features — interest rates, VIX (volatility index), sector ETF performance
3. Fundamental features — P/E ratio, revenue growth, analyst estimates
4. Ensemble with regime detection — classify market regime before predicting
5. Shorter prediction horizon — predict next hour instead of next day