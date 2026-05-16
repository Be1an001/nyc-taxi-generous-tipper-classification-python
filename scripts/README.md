# Scripts Note

This folder keeps the code-side companion file for the project.

## Files

- [`../notebooks/01-automatidata-portfolio-project.ipynb`](../notebooks/01-automatidata-portfolio-project.ipynb) is the main runnable notebook.
- [`01-automatidata-portfolio-project.py`](01-automatidata-portfolio-project.py) is an exported Python script view of the same workflow.

## Notebook vs. Script

The notebook is the best file for reviewing the project step by step. It includes markdown explanations, stored outputs, model results, and visualizations.

The Python script is easier to scan quickly on GitHub. It is useful as a code reference, but the notebook remains the primary runnable version.

## Main Workflow in the Code

- pull official NYC Open Data by API
- clean the trip data
- keep only credit-card trips
- engineer the generous-tipping target and modeling features
- split data into train, validation, and test sets
- compare Logistic Regression, Random Forest, and XGBoost
- select the final model by validation F1
- evaluate the selected model on the holdout test set
- plot the confusion matrix and permutation importance

## Reproducibility Notes

Local reruns may write optional CSV summaries in the repository root:

- `validation_results.csv`
- `test_results.csv`
- `permutation_importance.csv`

These are local helper outputs and are gitignored. The project also depends on internet access to pull data from NYC Open Data.

## Related Files

- [`../reports/automatidata-portfolio-report-cheng-liu.pdf`](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [`../walkthrough/project-walkthrough.md`](../walkthrough/project-walkthrough.md)
- [`../data/README.md`](../data/README.md)
- [`../outputs/README.md`](../outputs/README.md)
- [`../requirements.txt`](../requirements.txt)
