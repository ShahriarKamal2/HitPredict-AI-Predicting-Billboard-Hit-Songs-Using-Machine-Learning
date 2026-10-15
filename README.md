# 🎵 Hit Song Predictor

A machine-learning project that investigates whether the audio and structural
characteristics of a song can be used to predict whether it will become a hit.

The project combines exploratory data analysis, data visualization,
classification modelling, model comparison and explainable AI using SHAP.

---

## 📌 Project Overview

What makes a song a hit?

This project explores that question using historical Spotify audio features
and Billboard hit labels from songs released between the 1960s and 2010s.

The main objective is to answer:

> Can the musical characteristics of a song be used to predict whether it
> will become a hit?

The project first examines differences between hit and non-hit songs through
exploratory data analysis and then evaluates several machine-learning
classification algorithms.

The final model is interpreted using Random Forest feature importance and SHAP
to identify which audio characteristics influence hit predictions.

---

## 📊 Dataset

The project uses the **Spotify Hit Predictor Dataset (1960–2019)** available
on Kaggle.

Dataset:
https://www.kaggle.com/datasets/theoverman/the-spotify-hit-predictor-dataset

The dataset contains approximately **41,000 songs** across six decades.

### Target Variable

- `0` = Non-Hit
- `1` = Hit

The dataset is balanced, with approximately equal numbers of hit and non-hit
songs.

### Main Audio Features

The modelling stage uses:

- Danceability
- Energy
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Liveness
- Valence
- Tempo
- Chorus hit
- Number of song sections
- Song duration
- Musical key
- Mode
- Time signature

Track name, artist name and Spotify URI were excluded from the main predictive
model so that the model focuses on musical characteristics rather than artist
identity.

---

## 🔎 Exploratory Data Analysis

The EDA investigates:

- Class distribution
- Hit vs non-hit audio characteristics
- Feature distributions
- Correlations between audio characteristics
- Relationships between features
- Changes in hit-song characteristics across decades

Several clear patterns emerged.

Hit songs tended to have:

- Higher danceability
- Higher energy
- Higher loudness
- Higher valence
- Lower acousticness
- Much lower instrumentalness
- Slightly shorter average duration

Tempo showed relatively little difference between hits and non-hits.

The analysis also showed that the characteristics of successful songs changed
substantially between the 1960s and 2010s.

---

## 🤖 Machine-Learning Models

Five classification approaches were evaluated:

1. Dummy Classifier
2. Logistic Regression
3. Decision Tree
4. Random Forest
5. XGBoost

The dataset was divided into:

- **80% training data**
- **20% testing data**

A stratified split was used to maintain the balanced hit/non-hit distribution
in both datasets.

Numerical features were standardized, while categorical features such as key,
mode and time signature were one-hot encoded using a Scikit-learn pipeline.

---

## 📈 Model Performance

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest | **0.7828** | **0.7539** | 0.8397 | **0.7945** | **0.8639** |
| XGBoost | 0.7785 | 0.7441 | **0.8489** | 0.7931 | 0.8607 |
| Decision Tree | 0.7389 | 0.6847 | 0.8854 | 0.7722 | 0.8069 |
| Logistic Regression | 0.7178 | 0.6854 | 0.8052 | 0.7405 | 0.7939 |
| Dummy Classifier | 0.5000 | 0.0000 | 0.0000 | 0.0000 | 0.5000 |

---

## 🏆 Final Model

**Random Forest** was selected as the final model.

Final test performance:

- **Accuracy:** 78.28%
- **Precision:** 75.39%
- **Recall:** 83.97%
- **F1-score:** 79.45%
- **ROC-AUC:** 86.39%

XGBoost achieved slightly higher recall, but Random Forest achieved the best
overall combination of accuracy, precision, F1-score and ROC-AUC.

---

## 🧠 Model Explainability

Two explainability methods were used:

### Random Forest Feature Importance

The most influential features were:

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

### SHAP Analysis

SHAP analysis was used to understand both feature importance and the direction
of influence on predictions.

Important patterns included:

- Higher **instrumentalness** generally pushed predictions toward Non-Hit.
- Higher **acousticness** generally pushed predictions toward Non-Hit.
- Higher **danceability** generally pushed predictions toward Hit.
- Higher **energy** generally contributed toward Hit predictions.
- Higher **loudness** generally contributed toward Hit predictions.
- Tempo had relatively little influence on predictions.

These findings were broadly consistent with the exploratory data analysis.

SHAP was also used to explain an individual song prediction, showing which
features pushed the model toward Hit or Non-Hit.

---

## 📁 Repository Structure

```text
hit-song-predictor/
│
├── notebooks/
│   ├── 01_EDA_Data_Visualization.ipynb
│   └── 02_Hit_Song_Modelling.ipynb
│
├── outputs/
│   ├── README.md
│   ├── model_comparison_results.csv
│   └── random_forest_feature_importance.csv
│
├── models/
│   ├── README.md
│   └── hit_song_random_forest.pkl
│
├── README.md
├── requirements.txt
└── .gitignore
