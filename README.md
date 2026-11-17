# botswana-food-inflation-early-warning
Early warning system for Botswana food price inflation: does machine learning beat simple persistence?

# Early Warning System for Food Price Inflation in Botswana

**Does machine learning beat simple persistence?**

A two-stage regression and classification approach, benchmarked against direct classification,
using regional and global economic indicators.

BIDA Research and Innovation group project, Botswana Accountancy College.

## Overview

Botswana imports much of its food, so food prices follow shocks from outside the country, and
official inflation figures are published only after prices have already risen. This project
builds and tests an early warning system that:

1. **Stage 1:** forecasts Botswana's monthly food price inflation 1, 2 and 3 months ahead.
2. **Stage 2:** converts each forecast into a risk category (below, within or above) using the
   Bank of Botswana's 3 to 6 percent inflation objective range.

Linear Regression, Random Forest and XGBoost are compared with a naive "last value" forecast.
Direct classifiers are used as a benchmark for the two-stage approach.

## Main findings

- No model was significantly more accurate than the naive last-value forecast at 1, 2 or 3
  months (Diebold-Mariano tests).
- One-month test RMSE: naive 1.68, Linear Regression 1.63, XGBoost 1.71, Random Forest 1.76.
- Botswana's own past inflation accounts for 99.3% of the Random Forest's importance, so food
  inflation is highly persistent.
- Regional food inflation, Brent crude oil and the Baltic Dry Index gave no reliable gain
  beyond Botswana's own history.
- Threshold alerts flagged 93.5% of months above 6%, although the naive rule did almost as well.
  The contribution is a transparent alert tool and an honest test, not a more accurate forecaster.

## Method

- **Data:** monthly, 2001 to 2023 (276 observations after dropping 2000, which has no valid
  year-on-year inflation).
- **Inputs:** Botswana's lagged food inflation [lags 0 to 2, confirm], Brent crude oil price,
  and monthly Baltic Dry Index measures [average, volatility, range, momentum, confirm].
- **Split:** chronological. Training 2001 to 2014, validation 2015 to 2018 (model and feature set
  selection), test 2019 to 2023 (the last 60 months).
- **Evaluation:** 60-month expanding-window rolling forecast, with RMSE, MAE and R squared for
  regression, and accuracy, precision, recall, F1 and confusion matrices for classification.
- **Statistical test:** Diebold-Mariano test of each model against the naive forecast.
- **Risk categories:** below 3%, 3 to 6%, and above 6%, following the Bank of Botswana's
  objective range (an assumption when applied to food inflation).

## Repository contents

| Path | Description |
|------|-------------|
| `[food_inflation_early_warning.ipynb]` | The full analysis, from data preparation to results |
| `data/README.md` | Where the data came from (raw data not included) |
| `outputs/` | Figures, metric tables and prediction files saved by the notebook |
| `reports/` | Final report and poster [add after marking] |
| `requirements.txt` | Python libraries used |

## Data

Five datasets were supplied: a regional food price panel (Botswana, Kenya, Namibia, South Africa,
Zimbabwe), a Botswana consumer price file, the Botswana policy interest rate, Brent crude oil
prices and the daily Baltic Dry Index. Source: [hackathon organisers / lecturer, add publishers
and access dates]. The raw files are not included in this repository [because of the data terms,
confirm].

Data decisions:

- **Zimbabwe** was excluded from the main models. Its series does not match its documented
  hyperinflation history, and including it destabilised Linear Regression.
- **The policy rate** was excluded. The supplied series is a constant 12% for about 18 years,
  while the Bank of Botswana published 7.5% in 2014, so it is inconsistent with published rates.
- **The consumer price file** was not used because it holds index levels, not inflation rates.

## How to run

1. Put the data files in `data/raw/` (file names are listed in `data/README.md`).
2. Install the libraries: `pip install -r requirements.txt`
3. Open the notebook and run all cells from the top.

Random seeds are set in the notebook, so results should be reproducible [confirm].

## Limitations

- The test period is short (60 months) and includes COVID-19 and the 2022 price shock, so
  statistical power is limited. A non-significant result means no difference could be shown, not
  that the models are equal.
- The 3 to 6% range is the Bank's range for overall inflation, and applying it to food is an
  assumption.
- No verified policy rate series was available, so monetary policy is not represented.
- The study covers Botswana only, and the data end in 2023.

## Team

[Sebaga Modumedi], [Thobo Maikano], [Thero Tsahabadira], [Bame Laetsang, [Tanaka Moloi]

Supervisor: [Mr Mavuna Sebapalo]

## References

See the final report for the full reference list.

