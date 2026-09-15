# Superconductor Critical Temperature Prediction

Comparison of 6 regularized regression methods to predict superconductor critical temperature from 81 material-science features derived from atomic composition.

Dataset: UCI Superconductivty Data (Hamidieh, 2018) - 21,263 materials, 81 numeric predictors. https://archive.ics.uci.edu/dataset/464/superconductivty+data

## Result

| Model | RMSE (test, Kelvin) |
|---|---|
| Stepwise (AIC) | 18.12 |
| LASSO | 18.23 |
| PLS | 18.25 |
| Forward selection | 18.32 |
| PCR | 18.88 |
| Ridge | 19.02 |

With a standard deviation of ~34.3 K in the target variable, the best model (stepwise) reaches an approximate R-squared of 0.72 - a solid fit for a purely linear model.

## Why the comparison matters

With 81 highly correlated atomic-property predictors, this is a textbook case for comparing variable selection (stepwise, forward, LASSO) against pure shrinkage (Ridge) and dimensionality reduction (PCR, PLS). The result is clear: methods that select variables consistently beat Ridge, suggesting the effective dimensionality of the problem is lower than it appears.

## Methodology

Sample of 3,000 observations (2,500 train / 500 test) from the full 21,263, to keep training computationally manageable. Predictors standardized using training data only. All six models tuned via cross-validation. Compared by test RMSE.

## Reproducibility

The code in superconductivity_analysis.Rmd is fully reproducible: it downloads the public UCI data and runs end to end. Results independently verified before publishing to this repository.

## Stack

R, glmnet (Ridge/LASSO), pls (PCR/PLS), caret (preprocessing), ggplot2

---
Originally developed as part of my Statistical Learning coursework (Universidad de los Andes, Industrial Engineering); refined and independently verified for this repository.
