# AlgoTrade AI 📈

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.55-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-ML-orange?style=for-the-badge)
![Plotly](https://img.shields.io/badge/Plotly-Visualisation-3D4DB7?style=for-the-badge&logo=plotly&logoColor=white)
![Yahoo Finance](https://img.shields.io/badge/Yahoo%20Finance-Live%20Data-6001D2?style=for-the-badge)

**A full-stack AI-powered algorithmic trading simulator combining supervised ML, reinforcement learning, portfolio optimisation, and advanced risk modelling — with live daily trading signals and explainable AI.**

[🚀 Live App](https://stockproject-cmy24zfxv2hsenglgjktrw.streamlit.app) · [📊 Features](#features) · [🛠️ Tech Stack](#tech-stack) · [⚡ Quick Start](#quick-start)

</div>

---

## Overview

AlgoTrade AI is a quantitative finance research platform built end-to-end in Python. It fetches live market data from Yahoo Finance, runs trained ML and RL models to generate trading signals, and presents everything through an interactive Streamlit dashboard with eight analytical pages.

The platform is designed to demonstrate skills relevant to quant research, algorithmic trading, and ML engineering roles — covering the full pipeline from raw data ingestion to deployed web application.

---

## Features

### 📡 Daily Signal *(flagship feature)*
- Fetches live OHLCV data from Yahoo Finance up to yesterday's close — automatically every day
- Runs all three trained models (XGBoost, Random Forest, Logistic Regression) and displays **BUY / HOLD / SELL**
- **SHAP explainability** — bar chart showing exactly which feature influenced the prediction and by how much
- **AI reasoning cards** — plain English explanation of RSI, MACD, Bollinger Bands, MA crossovers, and model confidence
- 90-day candlestick chart with signal marked, MACD subplot, RSI subplot

### 🤖 ML Prediction Engine
- Three trained classifiers: XGBoost, Random Forest, Logistic Regression
- Price chart with BUY/SELL signal markers and probability band
- Real model evaluation metrics: Accuracy, Precision, Recall, ROC-AUC, F1
- Feature importance bar chart from trained model
- Confusion matrix
- Equity curve vs Buy & Hold

### 🧠 RL Agent
- Reinforcement learning trading agent (PPO-based momentum strategy)
- Portfolio vs Buy & Hold chart with trade markers
- Training reward curve
- Rolling 20-day portfolio returns
- Trade distribution and recent trades table

### 📊 Portfolio Overview
- Unified equity curve comparison: ML vs RL vs Buy & Hold
- Drawdown chart for both strategies
- Live quote panel (price, open, high, low, volume)
- Strategy metrics comparison table
- Signal indicators (RSI, MACD, BB Width, MA Cross)

### 💼 Portfolio Optimiser
- Modern Portfolio Theory with 1,000 random portfolio simulations
- Efficient frontier scatter plot coloured by Sharpe ratio
- Max Sharpe and Min Volatility portfolios highlighted
- Optimal weight allocation donut chart
- Correlation matrix heatmap
- Individual stock return and volatility cards

### ⚠️ Risk VaR
- Historical VaR, Parametric VaR, Monte Carlo VaR — all three methods
- Confidence level slider updates all three simultaneously
- Rolling 60-day VaR chart
- Daily return distribution histogram
- Realised vs EWMA predicted volatility

### 🎲 Monte Carlo Simulation
- Up to 5,000 Geometric Brownian Motion price paths
- Fan chart with 5th / 25th / 50th / 75th / 95th percentile bands
- Final value distribution histogram
- Scenario summary (Bear / Low / Base / High / Bull)
- Distribution stats: mean, std dev, skewness, kurtosis, tail probabilities

### 📋 Trade Log
- Full execution history for ML and RL strategies
- Real P&L calculated from actual BUY → SELL round trips (not simulated)
- Cumulative P&L chart with individual trade bars
- P&L distribution histogram
- Monthly breakdown bar chart
- Trade stats: win rate, avg win/loss, profit factor, best/worst trade

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.10+ |
| Dashboard | Streamlit |
| ML Models | scikit-learn, XGBoost |
| RL Agent | Momentum-based strategy (PPO architecture) |
| Data | Yahoo Finance via `yfinance` |
| Visualisation | Plotly |
| Explainability | SHAP |
| Numerical | NumPy, pandas |
| Deployment | Streamlit Community Cloud |

---

## Project Structure

```
StockProject/
│
├── data/
│   ├── raw/                    # OHLCV CSVs downloaded from Yahoo Finance
│   │   ├── AAPL.csv
│   │   ├── TSLA.csv
│   │   └── ...
│   ├── processed/              # Feature-engineered CSVs for model training
│   │   ├── AAPL_features.csv
│   │   └── ...
│   ├── data_loader.py          # Downloads raw data from Yahoo Finance
│   └── live_feed.py            # Fetches live data + computes features daily
│
├── ml_price_prediction/
│   ├── train_model.py          # Trains XGBoost, RF, Logistic Regression
│   ├── predict.py              # Generates signals from trained models
│   └── evaluation.py          # Model evaluation metrics
│
├── ml_strategy_rl/
│   ├── rl_agent.py             # DQN-based RL agent
│   ├── trading_environment.py  # Custom Gym-style trading environment
│   ├── q_learning_agent.py     # Q-learning baseline
│   ├── reward_functions.py     # Reward shaping
│   └── train_rl_agent.py       # RL training loop
│
├── backtesting/
│   ├── backtester.py           # Core backtesting engine
│   └── performance_metrics.py  # Sharpe, VaR, drawdown, win rate etc.
│
├── risk_management/
│   ├── var_model.py            # VaR calculations
│   ├── monte_carlo.py          # Monte Carlo simulation
│   ├── volatility_prediction.py
│   └── risk_controls.py
│
├── portfolio/
│   ├── allocation.py
│   └── portfolio_manager.py
│
├── models/                     # Trained .pkl model files
│   ├── xgb_model.pkl
│   ├── random_forest_model.pkl
│   └── logistic_model.pkl
│
├── signals/
│   └── trading_signals.csv
│
├── dashboard/
│   └── AlgoTradeAI/
│       └── trading_app/
│           ├── app.py                      # Home page
│           ├── utils.py                    # Shared theme, data loaders, sidebar
│           └── pages/
│               ├── Daily_Signal.py         # 📡 Live daily prediction
│               ├── ML_Prediction.py        # 🤖 ML model signals
│               ├── RL_Agent.py             # 🧠 RL trading agent
│               ├── Overview.py             # 📊 Portfolio overview
│               ├── Portfolio_Optimizer.py  # 💼 Efficient frontier
│               ├── Price_Indicators.py     # 📈 Technical analysis
│               ├── Risk_VaR.py             # ⚠️  Value at Risk
│               ├── Monte_Carlo.py          # 🎲 Price path simulation
│               └── Trade_Log.py            # 📋 Execution history
│
├── requirements.txt
└── README.md
```

---

## Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/Varsh24-hash/AI-trading.git
cd StockProject
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Download raw data
```bash
python data/data_loader.py
```

### 4. Train the models
```bash
python ml_price_prediction/train_model.py
```

### 5. Run the dashboard
```bash
streamlit run dashboard/AlgoTradeAI/trading_app/app.py
```

---

## Machine Learning Pipeline

### Feature Engineering
Six features are computed from raw OHLCV data — these match exactly between training and live inference:

| Feature | Description |
|---|---|
| `return_1d` | Previous day's percentage return |
| `MA_10` | 10-day simple moving average |
| `MA_50` | 50-day simple moving average |
| `volatility` | 10-day rolling annualised volatility |
| `volume_change` | Day-over-day volume percentage change |
| `RSI` | 14-period Relative Strength Index |

### Models
| Model | Use case |
|---|---|
| XGBoost | Primary signal — gradient boosted trees, handles non-linearity |
| Random Forest | Ensemble baseline — robust to overfitting |
| Logistic Regression | Linear baseline — interpretable coefficients |

All models are trained on an 80/20 time-series split (no data leakage).

### Signal Logic
```
Probability > 0.60  →  BUY
Probability < 0.40  →  SELL
Otherwise           →  HOLD
```

---

## Live Daily Signal

The daily signal feature is the key differentiator of this project. Unlike models trained on a fixed historical window, it:

1. Fetches 2 years of data from Yahoo Finance up to yesterday's close
2. Computes all 6 features on the fresh data
3. Runs the saved `.pkl` model — **no retraining required**
4. Generates a BUY / HOLD / SELL signal for tomorrow
5. Explains the decision using SHAP values and indicator analysis

This means the signal is always based on the most recent market data available, without any manual intervention.

---

## Supported Tickers

| Ticker | Company |
|---|---|
| AAPL | Apple Inc. |
| TSLA | Tesla Inc. |
| MSFT | Microsoft Corp. |
| GOOGL | Alphabet Inc. |
| AMZN | Amazon.com |
| NVDA | NVIDIA Corp. |
| META | Meta Platforms |
| JPM | JPMorgan Chase |
| V | Visa Inc. |
| WMT | Walmart Inc. |

---

## Performance Metrics

All strategy backtests report the following metrics:

- **Total Return** — cumulative portfolio growth
- **Annualised Return** — CAGR assuming 252 trading days
- **Volatility** — annualised standard deviation of daily returns
- **Sharpe Ratio** — excess return per unit of risk
- **Max Drawdown** — largest peak-to-trough decline
- **Win Rate** — percentage of profitable trading days
- **Calmar Ratio** — annualised return / max drawdown
- **Sortino Ratio** — downside-only risk-adjusted return
- **VaR (Historical / Parametric / Monte Carlo)** — daily loss limit at confidence level
- **CVaR / Expected Shortfall** — average loss beyond VaR threshold

---

## Deployment

The app is deployed on **Streamlit Community Cloud** and rebuilds automatically on every push to `main`.

Live URL: [https://stockproject-cmy24zfxv2hsenglgjktrw.streamlit.app](https://stockproject-cmy24zfxv2hsenglgjktrw.streamlit.app)

---

## Disclaimer

> This project is built for educational and research purposes only. It is not financial advice and should not be used to make real investment decisions. All backtested results are simulated and past performance does not guarantee future returns.

---

## Author

Built by **[Your Name]** as a quantitative finance and ML engineering portfolio project.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github)](https://github.com/YOUR_USERNAME)
