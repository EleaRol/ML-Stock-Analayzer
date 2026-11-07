# ML Stock Analyzer

Forecasting the next 5 days of volatility of the SPY ETF with simple machine learning models.

## What is this project?

This project compares a few machine learning models to find out which one predicts better how much the stock market will move over the next 5 trading days (one market week).

The market is represented by SPY, an ETF (a fund traded on the stock exchange) that follows the S&P 500 index. The value we predict is the **realized volatility** of SPY: how much its price actually moved, measured with the standard deviation of daily returns and expressed as a yearly percentage.

Note that this is _not_ the VIX. The VIX shows how much volatility the market _expects_ in the future, while this project predicts the volatility that _really happens_.

## Why does it matter?

Volatility is one of the most common ways to measure risk. Knowing whether the market is likely to be calm or turbulent in the coming days helps us understand how risky investing could be and how fast conditions can change.

## Data

The data are daily SPY prices downloaded with the `yfinance` library, from January 2010 to October 2026 (about 4,200 usable days after cleaning). The data files are not stored in this repository: the notebook downloads them when you run it.

## Disclaimer

This is a beginner project, made as part of my first year of an Artificial Intelligence degree, and it was developed with the help of Claude Code. It is for learning and research only and it is **not financial advice**. You are free to use and change the code, for example to test other tickers.