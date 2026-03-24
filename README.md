# volatility-forecast-ml

# Volatility Forecasting with Machine Learning and Deep Learning

## Overview

This project studies the prediction of **5-day realized volatility** of the S&P 500 using a range of models:

* Linear Regression (baseline)
* XGBoost (nonlinear machine learning)
* LSTM (deep learning)

We implement a **rolling-window backtesting framework** to simulate realistic out-of-sample forecasting and evaluate model performance under different market regimes.

---

## Motivation

Volatility forecasting is central to many financial applications, including:

* Risk management
* Derivatives pricing
* Portfolio allocation

While complex machine learning models are increasingly popular, it remains unclear whether they consistently outperform simpler statistical models in noisy financial environments.

This project aims to provide a **systematic comparison between model complexity and predictive performance**.

---

## Data

* Asset: S&P 500 Index (^GSPC)
* Frequency: Daily
* Period: 2010–Present
* Source: Yahoo Finance

---

## Methodology

### Target Variable

We define **5-day realized volatility** as the standard deviation of future returns over a 5-day horizon.

### Features

* Lagged returns
* Squared returns (volatility proxy)
* Rolling volatility (5-day, 10-day)

---

### Models

#### 1. Linear Regression

A simple baseline model used for comparison.

#### 2. XGBoost

Captures nonlinear relationships and feature interactions.

#### 3. LSTM

A recurrent neural network designed to capture temporal dependencies in time series data.

---

### Rolling Window Backtest

To ensure realistic evaluation:

* Training window: 1000 observations
* Testing window: 100 observations
* Models are re-trained at each step

This setup avoids look-ahead bias and mimics real-world forecasting.

---

### Regime Analysis

We define volatility regimes based on training data:

* **High-volatility regime**: top 30% of volatility
* **Low-volatility regime**: remaining observations

Model performance is evaluated separately across regimes.

---

## Results

### Overall Performance (MSE)

| Model             | MSE          |
| ----------------- | ------------ |
| Linear Regression | **0.000030** |
| LSTM              | 0.000045     |
| XGBoost           | 0.000050     |

**Key observation:**
Linear Regression outperforms both XGBoost and LSTM.

---

### High-Volatility Regime

| Model             | MSE          |
| ----------------- | ------------ |
| Linear Regression | **0.000041** |
| LSTM              | 0.000068     |
| XGBoost           | 0.000071     |

* All models perform significantly worse
* Linear Regression remains the most robust

---

### Low-Volatility Regime

| Model             | MSE          |
| ----------------- | ------------ |
| Linear Regression | **0.000019** |
| LSTM              | 0.000020     |
| XGBoost           | 0.000023     |

* Performance improves across all models
* Differences between models are smaller

---

### Stability Analysis

* XGBoost and LSTM exhibit **higher variance in performance**
* Maximum errors are substantially larger for complex models
* Linear Regression is **more stable and less prone to extreme errors**

---

## Key Findings

* **Model complexity does not guarantee better performance**
  Linear Regression consistently outperforms more complex models

* **Volatility regimes significantly impact predictability**
  Errors increase sharply during high-volatility periods

* **Nonlinear and deep learning models are less stable**
  They exhibit higher variance and occasional large prediction errors

* **Evidence of overfitting in complex models**
  Limited data and noisy signals reduce the effectiveness of LSTM and XGBoost

---

## Interpretation

These findings suggest that:

* Financial time series exhibit **low signal-to-noise ratios**
* Simpler models are often more robust in noisy environments
* Increased model complexity may lead to overfitting without additional data or features

Overall, this project highlights the importance of **model parsimony in financial forecasting**.

---

## How to Run

```bash
pip install -r requirements.txt
```

Then open:

```
Volatility_Forecasting.ipynb
```

---

## Tech Stack

* Python
* Pandas / NumPy
* Scikit-learn
* XGBoost
* PyTorch

---

## Future Work

* Add GARCH benchmark models
* Hyperparameter tuning
* Incorporate macroeconomic features
* Explore Transformer-based architectures

---

## Author

Siqi Liu
MS Mathematics in Finance, NYU Courant
