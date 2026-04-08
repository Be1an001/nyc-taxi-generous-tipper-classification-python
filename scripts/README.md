# Scripts Note

This folder keeps the code side of the project.

## Files

- [Notebook version](../notebooks/01-automatidata-portfolio-project.ipynb)
- [Exported Python script view](01-automatidata-portfolio-project.py)

## What is the difference?

### Notebook
The notebook is the main runnable version for Colab.  
It is the best file if someone wants to follow the project step by step.

### Python script
The Python file is an exported script view of the same workflow.  
It is easier to scan quickly on GitHub and useful as a companion code view, but the notebook is still the primary runnable version.

## Main workflow in the code

- pull official NYC Open Data by API
- clean the trip data
- keep only credit-card trips
- engineer target and features
- split into train / validation / test
- compare Logistic Regression, Random Forest, and XGBoost
- evaluate the final model
- plot the confusion matrix and permutation importance

## Small note on local artifacts

Local reruns may also write optional CSV summaries in the repo root:

- `validation_results.csv`
- `test_results.csv`
- `permutation_importance.csv`

These are local helper outputs and are gitignored in this repo.

## Related files

- [Portfolio PDF report](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Project walkthrough](../walkthrough/project-walkthrough.md)
- [Data note](../data/README.md)
- [Outputs](../outputs/README.md)
