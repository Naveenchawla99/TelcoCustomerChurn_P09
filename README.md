# p09: linear vs random forest vs gradient boosting on Telco churn

Metric (fixed in R1 before any fit): recall at the top 10% of predicted churn scores.

## Data
IBM Telco Customer Churn sample data (7,043 rows, 19 features + `Churn`), as distributed on Kaggle:
https://www.kaggle.com/datasets/blastchar/telco-customer-churn
The CSV is **not** included. Download it and save it as `Telco-Customer-Churn.csv` next to the notebooks;
if the file is absent the notebooks fall back to OpenML dataset id 42178 (this copy may be preprocessed).
**Licence:** check the terms on the Kaggle page before redistributing; I have not verified them.

## Files
- `scratch.ipynb`: R3, forest and squared-loss boosting built from scikit-learn trees, with agreement checks
- `comparison.ipynb`: R1, R2, R4, R5, R6, R7, runnable top to bottom
- `decision.md`: R8 and the R5 limitations

## Seeds
Train/test split and R2 CV folds: 42. R5 paired folds: 7. Searches, forests, trees, permutation importance: 0.

