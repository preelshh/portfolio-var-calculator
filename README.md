# Portfolio VaR Calculator

Monte Carlo simulation for calculating portfolio Value at Risk and Conditional VaR.

[Live Demo](https://portfolio-var-calculator-9urfrqnkqxcvpcbvvf5eex.streamlit.app/)

## What is this?

If you have a portfolio of stocks, VaR tells you: "with 95% confidence, you won't lose more than $X tomorrow."

This tool uses Monte Carlo simulation to generate thousands of possible scenarios and calculate risk metrics.

## The Math

Portfolio returns are modeled using Geometric Brownian Motion:

S(t) = S(0) * exp[(μ - σ²/2)t + σ√t * Z]

where:
- S(t) is the portfolio value at time t
- μ is the expected return (drift)
- σ is volatility
- Z ~ N(0,1) is a random shock from the standard normal distribution

For each simulation, we sample Z and compute the portfolio return. After running 10,000+ simulations, we sort the outcomes and find the 5th percentile worst case - that's the VaR at 95% confidence.

CVaR (Conditional VaR) goes further and calculates the expected loss given that we're already in the worst 5% of scenarios.

## Why Monte Carlo over Parametric?

Parametric VaR assumes returns are normally distributed, which underestimates tail risk. Real markets have fat tails: crashes happen more often than normal distributions predict. Monte Carlo doesn't assume any distribution, so it captures these extreme events better.

## Features

- Real-time stock data via yfinance
- Adjustable confidence levels and time horizons
- Comparison between Monte Carlo and Parametric VaR
- Interactive visualizations of the return distribution

## Run Locally
```bash
pip install -r requirements.txt
streamlit run app.py
```

## Tech Stack

Python, Streamlit, NumPy, Scipy, yfinance
