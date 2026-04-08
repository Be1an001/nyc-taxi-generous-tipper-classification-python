# Outputs

This folder keeps selected portfolio visuals I used for the public version of the project.

## Files

- [Updated executive summary](figures/automatidata-updated-executive-summary.png)
- [XGBoost test confusion matrix](figures/xgboost-test-confusion-matrix.png)
- [XGBoost permutation importance](figures/xgboost-permutation-importance.png)
- [Portfolio PDF report](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Project walkthrough](../walkthrough/project-walkthrough.md)

These are preserved supporting figures for the portfolio presentation. Local reruns may also create CSV summaries in the repo root, but those local files are gitignored and are not the main outputs kept here.

## 1. Updated executive summary

![Automatidata executive summary](figures/automatidata-updated-executive-summary.png)

This is the quick one-page summary version. I use it as a fast screening asset for GitHub or portfolio review.

## 2. XGBoost test confusion matrix

![XGBoost test confusion matrix](figures/xgboost-test-confusion-matrix.png)

This figure shows the final test confusion matrix with integer counts.

Main read:
- the model captured many actual generous trips
- false positives are still meaningful
- the result is usable, but should be explained with clear limits

## 3. XGBoost permutation importance

![XGBoost permutation importance](figures/xgboost-permutation-importance.png)

This figure shows which variables mattered most in the final model.

Main read:
- `vendorid` is much stronger than the other variables
- fare-related variables also matter
- this is useful for interpretation, but not proof of causality
