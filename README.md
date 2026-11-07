# ML Stock Analyzer

Forecasting the next 5 days of volatility of the SPY ETF with simple machine learning models.

> **This is a demo.** It is my first-year student project in Artificial Intelligence, built in collaboration with Claude Code. More professional projects will come later.

## What is this project?

This project compares a few machine learning models to find out which one predicts better how much the stock market will move over the next 5 trading days (one market week).

The market is represented by SPY, an ETF (a fund traded on the stock exchange) that follows the S&P 500 index. The value we predict is the **realized volatility** of SPY: how much its price actually moved, measured with the standard deviation of daily returns and expressed as a yearly percentage.

Note that this is _not_ the VIX. The VIX shows how much volatility the market _expects_ in the future, while this project predicts the volatility that _really happens_.

## Why does it matter?

Volatility is one of the most common ways to measure risk. Knowing whether the market is likely to be calm or turbulent in the coming days helps us understand how risky investing could be and how fast conditions can change.

## Data

The data are daily SPY prices downloaded with the `yfinance` library, from January 2010 to October 2026 (about 4,200 usable days after cleaning). The data files are not stored in this repository: the notebook downloads them when you run it.

## Method

- **Target:** the realized volatility of the next 5 trading days (annualized).
- **Features:** the realized volatility of the last 1, 5 and 21 days (`rv_1`, `rv_5`, `rv_21`), all calculated only with past data to avoid look-ahead bias.
- **Models:**
    - A **baseline** that simply uses `rv_21` as the prediction.
    - **Linear regression** (the HAR idea: recent volatility predicts future volatility).
    - **Random forest** (200 trees, `min_samples_leaf=20`, not tuned).
- **Evaluation:** walk-forward validation with `TimeSeriesSplit` (5 splits, 5-day gap). Each model always trains on the past and is tested on the period that comes after it. The gap avoids overlap between the target windows of the training and test data.
- **Metric:** MAE (mean absolute error). Lower is better.

## Results

Average MAE over the 5 test periods (2012 to 2026):

|Model|Average MAE|Improvement over baseline|
|---|---|---|
|Baseline (`rv_21`)|0.0604|n/a|
|Linear regression (HAR)|0.0537|about 11%|
|Random forest|0.0564|about 6.5%|

Linear regression beat the baseline in all 5 periods and the random forest in 4 of 5. Linear regression was better than the random forest in 3 of the 5 periods, so the difference between them is small. The hardest period for every model was 2018 to 2021, which includes the COVID crash.

## Limitations

- Only one asset (SPY) and only three features were tested.
- The random forest was not tuned, so the comparison is not completely fair.
- Five test periods are not enough to be sure that one model is always better.
- Only one metric (MAE) was used.

## How to run it

```bash
git clone https://github.com/EleaRol/ML-Stock-Analayzer.git
cd ML-Stock-Analayzer
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

Then open `AddSpy.ipynb` and run the cells in order.

## Disclaimer

This project is for learning and research only and it is **not financial advice**. You are free to use and change the code, for example to test other tickers.

## Credits

Made by Rolando (EleaRol) as a first-year Artificial Intelligence student, in collaboration with Claude Code, who acted as a mentor and explained each step while I wrote the code.