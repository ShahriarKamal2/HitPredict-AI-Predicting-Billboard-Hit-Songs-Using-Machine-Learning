# 📊 Outputs

This directory contains generated results from the machine-learning stage of the Hit Song Predictor project.

## Files

### `model_comparison_results.csv`

Contains evaluation results for:
- Dummy Classifier
- Logistic Regression
- Decision Tree
- Random Forest
- XGBoost

Metrics include:
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Random Forest achieved the strongest overall result with a ROC-AUC of **0.8639**.

### `random_forest_feature_importance.csv`

Contains impurity-based feature importance values from the final Random Forest model.

Top features include:
- Instrumentalness
- Acousticness
- Danceability
- Energy
- Loudness

These importance values show which variables contributed most strongly to reducing prediction uncertainty in the Random Forest. They should not be interpreted as causal effects.

For directional interpretation, see the SHAP analysis in:

```text
notebooks/02_Hit_Song_Modelling.ipynb
```
