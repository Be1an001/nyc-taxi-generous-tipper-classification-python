# Project Walkthrough

## Project Overview

This project is my public portfolio rewrite of the Automatidata project from the Google Advanced Data Analytics program.

The analysis uses official NYC Open Data and rebuilds the workflow in Colab. The main task is to predict whether a credit-card yellow taxi trip ended with a tip rate of 20 percent or higher.

Related project files:

- [Notebook version](../notebooks/01-automatidata-portfolio-project.ipynb)
- [Exported Python script view](../scripts/01-automatidata-portfolio-project.py)
- [Portfolio PDF report](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Data note](../data/README.md)
- [Contribution note](../contribution-note.md)

## Business Problem

The original classroom scenario focused on non-tippers. I changed that framing for this public version because directly profiling non-tippers can raise fairness concerns.

The target in this repository is **generous tipping**:

- `1` = tip rate >= 20 percent
- `0` = tip rate < 20 percent

This keeps the project useful as a tip-behavior analysis example while making the framing more responsible. It should still be treated as a portfolio prototype, not as an operational taxi decision system.

## Dataset and Scope

The project uses the official **2017 Yellow Taxi Trip Data** from NYC Open Data.

In this version, the notebook and exported script pull data directly from the official API instead of relying on local course CSV files.

Main data setup:

- public-data sample pulled: **180,000 rows**
- filtered modeling sample: **116,748 credit-card trips**
- original API fields pulled first: **13**
- final modeling inputs before one-hot encoding: **21**
- positive class share: about **52.7 percent generous-tip trips**

More source details are in [data/README.md](../data/README.md).

## Methodology

The workflow was:

1. pull selected trip fields from the official NYC Open Data API
2. clean the trip records
3. keep only credit-card trips
4. create the generous-tipping target
5. engineer time, fare, trip, speed, round-up, and grouped location features
6. split the data into train, validation, and test sets
7. compare Logistic Regression, Random Forest, and XGBoost
8. tune the tree-based models with `RandomizedSearchCV`
9. choose the final model by validation F1
10. evaluate once on the holdout test set
11. review the result with a confusion matrix and permutation importance

## Selected Code Examples

### Official data pull

```python
API_ENDPOINT = "https://data.cityofnewyork.us/resource/biws-g3hs.csv"

selected_columns = [
    "vendorid",
    "tpep_pickup_datetime",
    "tpep_dropoff_datetime",
    "passenger_count",
    "trip_distance",
    "ratecodeid",
    "pulocationid",
    "dolocationid",
    "payment_type",
    "fare_amount",
    "tip_amount",
    "tolls_amount",
    "total_amount"
]
```

This API workflow makes the project easier to review publicly because it does not depend on private course CSV files.

### Target and feature engineering

```python
df["tip_percent"] = np.round(
    df["tip_amount"] / (df["total_amount"] - df["tip_amount"]), 3
)
df["generous"] = (df["tip_percent"] >= 0.20).astype(int)

df["speed_mph"] = df["trip_distance"] / (df["duration_minutes"] / 60)
df["round5_ratio"] = (
    (np.ceil(df["fare_amount"] / 5) * 5) - df["fare_amount"]
) / df["fare_amount"]
```

The model uses trip, time, fare, speed, round-up, and grouped location features. The tip amount itself is used to create the target, not as a model input.

## Visual Highlights

### XGBoost test confusion matrix

![XGBoost test confusion matrix](../outputs/figures/xgboost-test-confusion-matrix.png)

The confusion matrix shows that the model captures many actual generous-tip trips, but false positives are still meaningful.

### XGBoost permutation importance

![XGBoost permutation importance](../outputs/figures/xgboost-permutation-importance.png)

Permutation importance shows that `vendorid` and fare-related variables were much stronger than the other variables in this run. This is useful for interpretation, but it is not causal evidence.

### One-page executive summary

![Automatidata executive summary](../outputs/figures/automatidata-updated-executive-summary.png)

The one-page summary gives a quick overview of the project setup, metrics, and limitation notes.

## Results

Final selected model: **XGBoost**

Main results:

- Validation F1: **76.58 percent**
- Test F1: **76.54 percent**
- Precision: **69.87 percent**
- Recall: **84.63 percent**
- Accuracy: **72.69 percent**

The model comparison showed that XGBoost and Random Forest were very close. XGBoost was selected because it had the strongest validation F1, but the margin was narrow.

## Interpretation

The result suggests that this sampled credit-card trip dataset contains useful predictive signal for generous tipping.

The strongest model reliance pattern came from `vendorid`, followed by fare-related variables. This should be interpreted carefully because a strong feature importance value does not explain why tipping happened and may reflect proxy patterns in the sampled data.

## Limitations

- The project uses a public-data sample, not the full 2017 taxi trip table.
- The model only represents filtered credit-card trips.
- Cash-trip tipping behavior is outside the model scope.
- The model should not be treated as a production dispatch or rider decision system.
- Permutation importance should not be interpreted as causality.
- No real TLC adoption, deployment, dashboard, SQL layer, GenAI component, or MLOps workflow is confirmed in this repository.
- Reruns depend on the NYC Open Data API and unpinned package versions.

## Conclusion

This project is best understood as an applied machine learning portfolio project. It shows how I rebuilt a guided classroom scenario into a public workflow using official open data, ethical target reframing, feature engineering, model comparison, and clear limitation notes.

## Related Files

- [Notebook version](../notebooks/01-automatidata-portfolio-project.ipynb)
- [Exported Python script view](../scripts/01-automatidata-portfolio-project.py)
- [Portfolio PDF report](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Data note](../data/README.md)
- [Outputs note](../outputs/README.md)
- [Scripts note](../scripts/README.md)
- [Contribution note](../contribution-note.md)
