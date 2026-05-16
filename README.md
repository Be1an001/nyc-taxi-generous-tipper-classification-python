# NYC Taxi Generous Tipper Classification (Python)

This is an individual Python machine learning portfolio project that rebuilds an Automatidata-inspired taxi tipping scenario using official NYC Open Data.

The project predicts whether a credit-card yellow taxi trip ended with a generous tip, defined as a tip rate of 20 percent or higher. I kept the project focused on a clear applied ML workflow: public data access, data cleaning, feature engineering, model comparison, evaluation, and honest limitations.

## Project Type / Status / Tools

- **Project type:** Applied machine learning / Python analytics portfolio project
- **Status:** Reproducible portfolio notebook and report, not a production system
- **Main tools:** Python, pandas, NumPy, requests, scikit-learn, XGBoost, matplotlib, Colab
- **Main notebook:** [`notebooks/01-automatidata-portfolio-project.ipynb`](notebooks/01-automatidata-portfolio-project.ipynb)
- **Exported script view:** [`scripts/01-automatidata-portfolio-project.py`](scripts/01-automatidata-portfolio-project.py)

## Business Problem

The original Automatidata classroom scenario focused on non-tippers. I did not want to keep that framing for a public portfolio project because it can raise fairness concerns.

In this version, the target is reframed as **generous tipping**:

- `1` = tip rate >= 20 percent
- `0` = tip rate < 20 percent

This keeps the project useful as a tip-behavior analysis example while avoiding language that directly profiles riders as "bad customers." The result should be understood as a portfolio prototype for decision-support thinking, not as a dispatch rule or production taxi system.

## Project Objective

The goal was to rebuild the Automatidata-inspired workflow into a public, reviewable project that can:

- pull taxi trip data from the official NYC Open Data API
- filter to trips where recorded tips are more reliable
- create a clear generous-tipping target
- engineer time, fare, trip, and location features
- compare baseline and tree-based classification models
- explain model results with a confusion matrix and permutation importance
- document limitations clearly

## Dataset and Scope

This project uses the official **2017 Yellow Taxi Trip Data** from NYC Open Data.

The raw dataset is not uploaded to this repository. The notebook and script pull a manageable public-data sample from the Socrata CSV endpoint.

Main data details:

- Source: official NYC Open Data
- Pull method: monthly API chunks from the Socrata CSV endpoint
- Public-data sample used in this project: **180,000 rows**
- Final filtered modeling sample: **116,748 credit-card trips**
- Raw API fields pulled first: **13**
- Final modeling inputs before one-hot encoding: **21**
- Target share: about **52.7 percent generous-tip trips**

The model only represents the filtered credit-card subset. Cash trips are excluded because cash tips are not recorded as consistently in the trip table.

More detail is available in [`data/README.md`](data/README.md).

## My Role / Contribution

This was an individual portfolio rewrite based on the Google Advanced Data Analytics Automatidata scenario.

The original course project provided the business theme and learning structure. For this public version, I rebuilt the data access, notebook workflow, feature engineering, model comparison flow, evaluation summary, static figures, report, and GitHub documentation.

See [`contribution-note.md`](contribution-note.md) for the contribution boundary.

## Methodology

Main workflow:

- pull selected 2017 yellow taxi fields from the official NYC Open Data API
- clean trip records and remove rows outside basic validity rules
- keep only credit-card trips
- create `tip_percent` and the `generous` target
- engineer time, fare, trip, speed, round-up, and grouped location features
- split the data into train, validation, and test sets
- compare Logistic Regression, Random Forest, and XGBoost
- tune tree-based models with `RandomizedSearchCV`
- select the final model by validation F1
- evaluate the selected model once on the holdout test set
- review the confusion matrix and permutation importance

## Key Findings

- XGBoost had the strongest validation F1 in this project, but the margin over Random Forest was narrow.
- The final XGBoost model reached **76.54 percent test F1**, with **69.87 percent precision**, **84.63 percent recall**, and **72.69 percent accuracy**.
- The test result stayed close to validation performance, which suggests the sampled setup was reasonably stable for a portfolio project.
- The model captured many actual generous-tip trips, but false positives were still meaningful.
- `vendorid` was much stronger than the other variables in permutation importance, so it should be treated as a possible proxy pattern rather than a causal driver.
- The result suggests predictive signal in this sampled credit-card trip dataset, not a production-ready model for all taxi trips.

## Visual Highlights

These selected static figures are kept in [`outputs/figures`](outputs/figures).

### One-page executive summary

![Automatidata executive summary](outputs/figures/automatidata-updated-executive-summary.png)

This figure summarizes the project setup, metrics, and next-step ideas in one page.

### XGBoost test confusion matrix

![XGBoost test confusion matrix](outputs/figures/xgboost-test-confusion-matrix.png)

The confusion matrix shows that the model captures many generous-tip trips but still produces a meaningful number of false positives.

### XGBoost permutation importance

![XGBoost permutation importance](outputs/figures/xgboost-permutation-importance.png)

Permutation importance shows model reliance patterns. It should not be treated as causal evidence about why riders tip.

## Model Evaluation Note

The final model was chosen using validation F1, then evaluated once on the holdout test set.

This matters because XGBoost and Random Forest were very close on validation performance. The final model should be described as a narrow validation win, not a large performance gap.

## Repository Structure

| Path | Purpose |
|---|---|
| [`notebooks/01-automatidata-portfolio-project.ipynb`](notebooks/01-automatidata-portfolio-project.ipynb) | Main Colab notebook and primary runnable analysis |
| [`scripts/01-automatidata-portfolio-project.py`](scripts/01-automatidata-portfolio-project.py) | Exported Python script view of the notebook workflow |
| [`reports/automatidata-portfolio-report-cheng-liu.pdf`](reports/automatidata-portfolio-report-cheng-liu.pdf) | Portfolio PDF report |
| [`walkthrough/project-walkthrough.md`](walkthrough/project-walkthrough.md) | Step-by-step project walkthrough |
| [`data/README.md`](data/README.md) | Data source, fields, and scope notes |
| [`outputs/README.md`](outputs/README.md) | Notes on saved portfolio figures |
| [`outputs/figures`](outputs/figures) | Static visual outputs used in the README and report |
| [`scripts/README.md`](scripts/README.md) | Notes on notebook and script usage |
| [`contribution-note.md`](contribution-note.md) | Course reference and individual contribution note |
| [`requirements.txt`](requirements.txt) | Python package list |

## How to Reproduce

The notebook is the main runnable version of the project.

1. Open [`notebooks/01-automatidata-portfolio-project.ipynb`](notebooks/01-automatidata-portfolio-project.ipynb) in Colab or a local notebook environment.
2. Install the packages listed in [`requirements.txt`](requirements.txt).
3. Run the notebook cells to pull the selected data fields from NYC Open Data.
4. Review the validation results, final test results, confusion matrix, and permutation importance in the notebook outputs.

Reproducibility notes:

- The project depends on internet access and the NYC Open Data API.
- The code includes an optional Socrata app-token field if retrieval is slow or rate-limited.
- Package versions are not pinned in `requirements.txt`, so exact rerun behavior may vary slightly over time.
- Local reruns may create `validation_results.csv`, `test_results.csv`, and `permutation_importance.csv` in the repo root. These are local helper outputs and are gitignored.

## Limitations

- This project uses a public-data sample, not the full 2017 taxi trip table.
- The analysis is limited to filtered credit-card trips because recorded tips are more reliable there than in cash trips.
- The model should not be used to make high-stakes decisions about riders or drivers.
- Permutation importance does not prove causality.
- `vendorid` may reflect proxy patterns that need more investigation before any operational interpretation.
- No real TLC adoption, production deployment, dashboard, SQL layer, GenAI component, or MLOps workflow is confirmed in this repository.
- API availability and unpinned package versions may affect future reruns.

## Future Improvements

- Add a filtering summary that shows how many rows are removed at each cleaning step.
- Add a small EDA section with one or two simple charts before modeling.
- Add threshold tuning to show the precision and recall tradeoff more clearly.
- Improve the confusion matrix labels so the class meanings are easier to read.
- Add a short model card that summarizes intended use, limitations, and fairness concerns.
- Pin package versions if exact reruns become more important.

## Related Files

- [`notebooks/01-automatidata-portfolio-project.ipynb`](notebooks/01-automatidata-portfolio-project.ipynb)
- [`scripts/01-automatidata-portfolio-project.py`](scripts/01-automatidata-portfolio-project.py)
- [`walkthrough/project-walkthrough.md`](walkthrough/project-walkthrough.md)
- [`data/README.md`](data/README.md)
- [`outputs/README.md`](outputs/README.md)
- [`outputs/figures/automatidata-updated-executive-summary.png`](outputs/figures/automatidata-updated-executive-summary.png)
- [`outputs/figures/xgboost-test-confusion-matrix.png`](outputs/figures/xgboost-test-confusion-matrix.png)
- [`outputs/figures/xgboost-permutation-importance.png`](outputs/figures/xgboost-permutation-importance.png)
- [`reports/automatidata-portfolio-report-cheng-liu.pdf`](reports/automatidata-portfolio-report-cheng-liu.pdf)
- [`scripts/README.md`](scripts/README.md)
- [`contribution-note.md`](contribution-note.md)
- [`requirements.txt`](requirements.txt)
