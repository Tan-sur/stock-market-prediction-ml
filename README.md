# Stock Market Prediction Using Machine Learning

A machine learning and time-series analysis project that studies historical stock market data, predicts future price movements, compares predictive models, and evaluates an explainable trading-signal strategy.

## Overview

This project investigates whether historical price and volume data can provide useful information about future market movements.

The initial implementation focuses on the **NIFTY 50 index** using historical data obtained through Yahoo Finance. It compares regression, classification, and time-series forecasting approaches using chronological evaluation.

The project also implements a rule-based BUY/HOLD/SELL signal layer and a backtesting framework to evaluate its historical performance against a buy-and-hold benchmark.

**This is an educational and experimental project, not a financial advisory system.** Predictions and historical backtest results do not guarantee future performance.

## Objectives

- Collect and analyze historical OHLCV market data.
- Perform exploratory data analysis and feature engineering.
- Predict the next trading day's closing price.
- Classify the next trading day's price direction.
- Compare different machine learning and time-series models.
- Generate explainable BUY/HOLD/SELL signals using predefined rules.
- Backtest the strategy and compare it with a buy-and-hold benchmark.
- Evaluate models using appropriate metrics while avoiding look-ahead bias.

## Dataset

- **Initial instrument:** NIFTY 50
- **Yahoo Finance ticker:** `^NSEI`
- **Data source:** Yahoo Finance via `yfinance`
- **Frequency:** Daily historical observations
- **Data fields:** Open, High, Low, Close, Volume

The initial study uses historical data beginning in 2015. The actual available date range and number of observations depend on the downloaded dataset.

## Technology Stack

- Python
- Google Colab and Jupyter Notebook
- pandas and NumPy
- Matplotlib and Seaborn
- yfinance
- scikit-learn
- statsmodels

## Feature Engineering

The project derives additional features from historical data:

| Feature | Purpose |
|---|---|
| MA_20 | 20-day moving average for short-term trend analysis |
| MA_50 | 50-day moving average for longer-term trend analysis |
| Daily_Return | Percentage change in closing price |
| Volatility | Rolling 20-day standard deviation of daily returns |

These features are calculated using historical observations available at the relevant prediction time.

## Models

### 1. Linear Regression

Predicts the next trading day's closing price using historical market features.

**Evaluation:** MAE, RMSE, and R².

### 2. Decision Tree Classifier

Classifies the next trading day's price movement as UP or DOWN.

**Evaluation:** Accuracy, precision, recall, and F1-score.

### 3. Random Forest Classifier

Uses an ensemble of decision trees to classify price direction and estimate class probabilities.

**Evaluation:** Accuracy, precision, recall, F1-score, and confusion matrix.

### 4. ARIMA

Uses autoregressive, differencing, and moving-average components to forecast a univariate time series.

**Evaluation:** MAE and RMSE, alongside a suitable naïve forecasting baseline.

## Exploratory Data Analysis

The notebook includes:

- Historical closing-price visualization
- Closing prices with moving averages
- Daily-return distribution
- Rolling volatility
- Feature correlation analysis
- Autocorrelation analysis
- Stationarity testing for time-series forecasting

Each visualization is intended to answer a specific analytical question rather than serve as decoration.

## BUY / HOLD / SELL Signal Layer

The project adds a transparent rule-based decision layer on top of Random Forest predictions.

Initial experimental rules:

- **BUY:** Predicted UP probability is at least 60%, closing price is above MA_20, and MA_20 is above MA_50.
- **SELL:** Predicted UP probability is at most 40%, closing price is below MA_20, and MA_20 is below MA_50.
- **HOLD:** Neither condition is satisfied.

The thresholds are initial experimental choices, not universally optimal trading parameters. Signals are not recommendations to buy or sell real securities.

The system also provides the reasons behind each signal.

## Backtesting

The strategy is evaluated using historical predictions and predefined decision rules.

The framework is designed to include:

- Chronological model evaluation
- Signals based only on information available at the decision time
- Strategy returns and cumulative returns
- Comparison against a buy-and-hold benchmark
- Transaction-cost assumptions
- Maximum drawdown, trade count, win rate, and Sharpe ratio where appropriate

Execution timing, transaction costs, and benchmark assumptions must be specified explicitly. Historical performance does not establish future profitability.

## Methodology and Data Leakage Prevention

Financial time-series data must be evaluated chronologically.

The project avoids random shuffling for time-dependent prediction tasks and separates training data from future test observations. Feature engineering, model fitting, and signal generation must not use future information unavailable at the time of prediction.

Where appropriate, time-series cross-validation can be used for model selection.

## Project Structure

```text
stock-market-prediction-ml/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── stock_market_prediction.ipynb
├── src/
│   └── README.md
├── results/
│   └── README.md
└── LICENSE
```

## Getting Started

### Option 1: Run in Google Colab

1. Open the notebook in the `notebooks/` directory.
2. Select **Open in Colab** if a Colab link is provided.
3. Run the setup and data-download cells.
4. Execute the notebook cells in order.
5. Review the evaluation metrics, plots, signals, and backtest results.

### Option 2: Run locally

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/stock-market-prediction-ml.git
cd stock-market-prediction-ml
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter:

```bash
jupyter notebook
```

Open the notebook in the `notebooks/` directory.

An internet connection is required to download data from Yahoo Finance. Data availability and download behavior may change.

## Results

Model metrics and backtesting results will be documented after the corresponding experiments have been executed and verified.

Results should include appropriate baselines, evaluation-period details, and the assumptions used for signal generation and backtesting. No model should be considered successful solely because it achieves a high score on one metric.

## Limitations

- Historical price and volume data may not capture all factors affecting financial markets.
- Financial time series are noisy and can change behavior over time.
- Price prediction and direction classification are different tasks and require different metrics.
- Incorrect validation can produce misleadingly optimistic results.
- Trading costs, slippage, and execution constraints can reduce strategy performance.
- Historical backtesting cannot guarantee future returns.

## Future Improvements

- Walk-forward validation and systematic hyperparameter tuning
- Feature importance and model interpretability
- More rigorous trading-cost and execution modeling
- Robustness testing across different market periods
- Testing on additional instruments and datasets
- Reproducible experiment tracking

## Disclaimer

This project is for educational and research purposes only. It does not provide investment advice, and it should not be used as the sole basis for financial decisions.

## Author

**Tanishh Suryavanshi**

Engineering student interested in Python, machine learning, data analysis, and financial technology.
