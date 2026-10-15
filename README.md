# 🎵 Hit Song Predictor

A machine-learning project that investigates whether the audio and structural characteristics of a song can be used to predict whether it will become a hit.

## Project Overview

This project uses the Spotify Hit Predictor Dataset (1960–2019) to explore whether musical characteristics can help predict hit status.

The workflow includes:
- Exploratory Data Analysis
- Data visualization
- Classification modelling
- Model comparison
- Random Forest feature importance
- SHAP explainability
- Individual-song explanation

## Dataset

Dataset: https://www.kaggle.com/datasets/theoverman/the-spotify-hit-predictor-dataset

The combined dataset contains 41,106 songs.

Target:
- `0` = Non-Hit
- `1` = Hit

## Features Used

- danceability
- energy
- key
- loudness
- mode
- speechiness
- acousticness
- instrumentalness
- liveness
- valence
- tempo
- time_signature
- chorus_hit
- sections
- duration_min

Artist, track name, URI, and decade were excluded from the main predictive model.

## Model Performance

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest | **0.7828** | **0.7539** | 0.8397 | **0.7945** | **0.8639** |
| XGBoost | 0.7785 | 0.7441 | **0.8489** | 0.7931 | 0.8607 |
| Decision Tree | 0.7389 | 0.6847 | 0.8854 | 0.7722 | 0.8069 |
| Logistic Regression | 0.7178 | 0.6854 | 0.8052 | 0.7405 | 0.7939 |
| Dummy Classifier | 0.5000 | 0.0000 | 0.0000 | 0.0000 | 0.5000 |

## Final Model

Random Forest was selected as the final model.

- Accuracy: **78.28%**
- Precision: **75.39%**
- Recall: **83.97%**
- F1-score: **79.45%**
- ROC-AUC: **86.39%**

## Explainability

Top Random Forest feature importances:

| Rank | Feature | Importance |
|---:|---|---:|
| 1 | Instrumentalness | 0.1641 |
| 2 | Acousticness | 0.1058 |
| 3 | Danceability | 0.1029 |
| 4 | Energy | 0.0808 |
| 5 | Loudness | 0.0726 |
| 6 | Speechiness | 0.0716 |
| 7 | Duration | 0.0705 |
| 8 | Valence | 0.0678 |

SHAP analysis showed that:
- Higher instrumentalness generally pushed predictions toward Non-Hit.
- Higher acousticness generally pushed predictions toward Non-Hit.
- Higher danceability generally pushed predictions toward Hit.
- Higher energy and loudness generally pushed predictions toward Hit.
- Tempo had relatively little influence.

## Repository Structure

```text
hit-song-predictor/
├── notebooks/
│   ├── 01_EDA_Data_Visualization.ipynb
│   └── 02_Hit_Song_Modelling.ipynb
├── outputs/
│   ├── README.md
│   ├── model_comparison_results.csv
│   └── random_forest_feature_importance.csv
├── models/
│   ├── README.md
│   
├── README.md
├── requirements.txt
└── .gitignore
```

## Technologies

Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, SHAP, Joblib, Google Colab, GitHub.

## Limitations

- Audio features alone do not determine commercial success.
- The dataset is artificially balanced.
- Musical trends changed across decades.
- The model captures associations, not causation.
- Extensive hyperparameter tuning was not completed.
- A random train/test split was used rather than temporal validation.
- The same held-out test set was used for model comparison and final selection.

## Future Improvements

- Hyperparameter tuning
- Temporal validation
- Probability calibration
- Artist and genre information
- Streaming and social-media features
- NLP features from lyrics
- Streamlit deployment

## Key Takeaway

Audio characteristics contain meaningful information about hit status, but no single feature determines commercial success. The strongest predictions come from combining multiple characteristics while recognizing that external factors also influence real-world outcomes.
