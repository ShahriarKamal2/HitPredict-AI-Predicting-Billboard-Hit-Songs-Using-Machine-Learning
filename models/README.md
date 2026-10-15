# 🤖 Models

This directory documents the final machine-learning model used in the **Hit Song Predictor** project.

## Final Model

The final selected model is a **Random Forest Classifier** implemented inside a Scikit-learn pipeline that includes both preprocessing and classification.

The trained binary model file (`.pkl`) is **not included in this repository**. This keeps the repository lightweight and avoids storing a large serialized model file.

The model can be recreated by running:

```text
notebooks/02_Hit_Song_Modelling.ipynb
```

from top to bottom.

## Model Performance

| Metric | Score |
|---|---:|
| Accuracy | 0.7828 |
| Precision | 0.7539 |
| Recall | 0.8397 |
| F1-score | 0.7945 |
| ROC-AUC | 0.8639 |

Random Forest achieved the strongest overall performance among the models evaluated.

## Models Compared

The project evaluated:

- Dummy Classifier
- Logistic Regression
- Decision Tree
- Random Forest
- XGBoost

Random Forest was selected because it achieved the best overall combination of accuracy, precision, F1-score, and ROC-AUC.

## Expected Input Features

The final model expects the following input features:

```text
danceability
energy
key
loudness
mode
speechiness
acousticness
instrumentalness
liveness
valence
tempo
time_signature
chorus_hit
sections
duration_min
```

The target variable should not be included when generating predictions.

## Preprocessing

The saved pipeline includes preprocessing for both numerical and categorical variables.

- Numerical features are standardized.
- `key`, `mode`, and `time_signature` are one-hot encoded.
- The preprocessing pipeline is fitted only on the training data to reduce data leakage.

## Recreating and Saving the Model

After running the modelling notebook, the trained pipeline can be saved locally using:

```python
import joblib

joblib.dump(
    random_forest_pipeline,
    "hit_song_random_forest.pkl"
)
```

It can later be loaded with:

```python
import joblib

model = joblib.load(
    "hit_song_random_forest.pkl"
)
```

## Generating Predictions

Example:

```python
prediction = model.predict(song_features)

hit_score = model.predict_proba(
    song_features
)[:, 1]
```

The `predict_proba()` output should be interpreted as a **model-estimated score/probability**, not as a calibrated real-world probability that a song will become commercially successful.

## Explainability

The final model was interpreted using:

- Random Forest impurity-based feature importance
- SHAP global feature importance
- SHAP beeswarm analysis
- Individual-song SHAP explanations

The most influential features included:

- Instrumentalness
- Acousticness
- Danceability
- Energy
- Loudness

Full explainability analysis is available in:

```text
notebooks/02_Hit_Song_Modelling.ipynb
```

## Note

The trained `.pkl` model is intentionally excluded from GitHub. Anyone who wants to reproduce the model can run the modelling notebook using the original dataset and generate the model locally.
