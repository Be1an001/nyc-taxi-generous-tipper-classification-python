# NYC Taxi Generous Tipper Classification (Python)

Public portfolio rewrite of the Automatidata project using official NYC Open Data, Colab, and XGBoost to predict generous tipper trips.

## Project overview

This is my updated public version of the Automatidata classroom project from the Google Advanced Data Analytics program.

I rebuilt the workflow so it can run directly in Colab with official NYC Open Data instead of local course CSV files. The main task is to predict whether a credit-card yellow taxi trip ended with a tip rate of 20% or higher.

I kept the project simple to read and easy to rerun. My goal for this repo is to show the business problem, the data workflow, the model comparison, and the main limits in a clean portfolio format.

## Project files

- [Portfolio PDF report](reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Notebook version](notebooks/01-automatidata-portfolio-project.ipynb)
- [Python script version](scripts/01-automatidata-portfolio-project.py)
- [Project walkthrough](walkthrough/project-walkthrough.md)
- [Data note](data/README.md)
- [Scripts note](scripts/README.md)
- [Outputs note](outputs/README.md)
- [Contribution note](contribution-note.md)

## Business problem

The original Automatidata scenario focused on non-tippers, but that framing can raise fairness concerns.

In this version, I changed the target to **generous tipping**. I defined the target as:

- `1` = tip rate >= 20%
- `0` = tip rate < 20%

This keeps the project useful for revenue-related analysis while being more responsible than directly profiling riders as non-tippers.

## Dataset

This project uses the official **2017 Yellow Taxi Trip Data** from NYC Open Data.

I did **not** upload raw CSV files to this repo. Instead, the notebook and script pull data directly from the official API.

Main dataset notes:

- Source: official NYC Open Data
- Pull method: monthly API chunks from the Socrata CSV endpoint
- Raw public-data slice used in this project: **180,000 rows**
- Final filtered modeling sample: **116,748 credit-card trips**
- Raw API fields pulled first: **13**
- Final modeling inputs before one-hot encoding: **21**

More details are in [data/README.md](data/README.md).

## Methods

Main workflow:

- pull data from the official API
- clean the trip records
- keep only credit-card trips
- engineer time, fare, trip, and location features
- split data into train / validation / test
- compare Logistic Regression, Random Forest, and XGBoost
- select the final model by validation F1
- evaluate once on the test set
- review confusion matrix and permutation importance

Selected engineered features:

- `pickup_hour`, `pickup_day`, `pickup_month`
- `am_rush`, `daytime`, `pm_rush`, `nighttime`
- `duration_minutes`, `speed_mph`
- `fare_bin`, `distance_bin`
- `round5_ratio`, `round10_ratio`
- grouped pickup and dropoff locations

## Main results

The final model was **XGBoost**, selected by a very small validation margin over Random Forest.

Main metrics:

- Validation F1: **76.58%**
- Test F1: **76.54%**
- Precision: **69.87%**
- Recall: **84.63%**
- Accuracy: **72.69%**
- Positive class share: **52.7%**

My main read is that the result is stable enough for a portfolio project, but it should still be presented as an **analysis prototype**, not a production dispatch rule.

## Key visuals

### One-page executive summary
![Automatidata executive summary](outputs/figures/automatidata-updated-executive-summary.png)

### XGBoost test confusion matrix
![XGBoost test confusion matrix](outputs/figures/xgboost-test-confusion-matrix.png)

### XGBoost permutation importance
![XGBoost permutation importance](outputs/figures/xgboost-permutation-importance.png)

## What these results told me

- XGBoost and Random Forest were almost tied, so the final choice should be described as a narrow win.
- The test result stayed very close to validation, which supports the stability of this setup.
- `vendorid` is much stronger than the other features, so it may act as a proxy for rider or trip pattern differences.
- The model has usable signal, but it is better for portfolio demonstration and insight work than for a high-stakes decision system.

## Limits

- This repo uses a public-data sample, not the full 2017 table.
- The analysis only uses **credit-card trips** because tip values are more reliable there than in cash trips.
- The model still overpredicts some generous cases.
- Strong feature importance does not mean direct causality.

## How to run

1. Open the notebook in Colab or run the Python script locally.
2. Install packages from `requirements.txt`.
3. Run the notebook or script from top to bottom.
4. The code will pull the data from official NYC Open Data.
5. The model results and figures can then be reproduced.

## Why I made this version

I wanted to turn a guided classroom scenario into a cleaner public portfolio project.

Compared with the course setup, I changed these parts:

- direct NYC Open Data API access
- no dependency on local course CSV files
- train / validation / test split
- added extra engineered features
- added permutation importance
- wrote a GitHub-friendly report and walkthrough

## Reference note

This project was rewritten as an independent public portfolio notebook.

The original business scenario and learning structure were **referenced from the Google Advanced Data Analytics Automatidata project**, but the public workflow, data access method, feature engineering, model selection flow, and GitHub presentation were rebuilt for this version.