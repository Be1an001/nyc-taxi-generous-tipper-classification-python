# Scripts Note

This folder keeps the code side of the project.

## Files

- [Notebook version](../notebooks/01-automatidata-portfolio-project.ipynb)
- [Python script version](01-automatidata-portfolio-project.py)

## What is the difference?

### Notebook
The notebook is the main runnable version for Colab.  
It is the best file if someone wants to follow the project step by step.

### Python script
The Python file is the exported script version of the same workflow.  
It is easier to scan quickly on GitHub and useful for people who prefer a plain script view.

## Main workflow in the code

- pull official NYC Open Data by API
- clean the trip data
- keep only credit-card trips
- engineer target and features
- split into train / validation / test
- compare Logistic Regression, Random Forest, and XGBoost
- evaluate the final model
- plot the confusion matrix and permutation importance

## Related files

- [Portfolio PDF report](../reports/automatidata-portfolio-report-cheng-liu.pdf)
- [Project walkthrough](../walkthrough/project-walkthrough.md)
- [Data note](../data/README.md)
- [Outputs](../outputs/README.md)