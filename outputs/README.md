# Outputs

This folder keeps selected static visuals for the public portfolio version of the project.

These files are supporting artifacts for the notebook, report, and README. They are not screenshots of a deployed dashboard or app.

## Files

| File | Purpose |
|---|---|
| [`figures/automatidata-updated-executive-summary.png`](figures/automatidata-updated-executive-summary.png) | One-page project summary |
| [`figures/xgboost-test-confusion-matrix.png`](figures/xgboost-test-confusion-matrix.png) | Final XGBoost holdout test confusion matrix |
| [`figures/xgboost-permutation-importance.png`](figures/xgboost-permutation-importance.png) | Permutation importance for the selected model |
| [`../reports/automatidata-portfolio-report-cheng-liu.pdf`](../reports/automatidata-portfolio-report-cheng-liu.pdf) | Portfolio PDF report |
| [`../walkthrough/project-walkthrough.md`](../walkthrough/project-walkthrough.md) | Project walkthrough |

## Figure Notes

### Updated executive summary

![Automatidata executive summary](figures/automatidata-updated-executive-summary.png)

This one-page summary gives a quick overview of the business problem, methods, metrics, and next-step ideas.

### XGBoost test confusion matrix

![XGBoost test confusion matrix](figures/xgboost-test-confusion-matrix.png)

This figure shows the final model's test-set classification counts. The model captures many actual generous-tip trips, but false positives are still meaningful and should be discussed carefully.

### XGBoost permutation importance

![XGBoost permutation importance](figures/xgboost-permutation-importance.png)

This figure shows model reliance patterns. `vendorid` is much stronger than the other variables in this run, which is useful for interpretation but should not be treated as causal evidence.

## Local Artifacts

Local reruns may also write optional CSV summaries in the repository root:

- `validation_results.csv`
- `test_results.csv`
- `permutation_importance.csv`

These files are gitignored local helper outputs and are not the main saved outputs for this repository.
