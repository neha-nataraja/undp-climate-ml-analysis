# UNDP People's Climate Vote 2024 — Predictive Modelling & Country Clustering

**COMP5122M: Data Science — Coursework 1 (Part I & II)**
MSc Data Science & Analytics, University of Leeds (2025/26)
Group name: Persian — Shreya Pradeepkumar Arakeri, **Neha B N Belagarahalli Nataraja**, Druvitha Handrangi Kumaraswamy
Module leader: Dr. Duygu Sarikaya

## What this is

An analysis of the UNDP People's Climate Vote 2024 — the world's largest public
opinion survey on climate policy, spanning 73 countries and combining demographic and
attitudinal responses. The project has two parts: **Part I** used Tableau to explore
public support for a rapid transition from fossil fuels to renewable energy, broken
down by age group and country. **Part II** (this repo's code) extends that with
Python-based machine learning: predicting which respondent groups show strong support
for strengthening climate commitments, and clustering countries into typologies based
on climate attitudes.

**My contribution:** I built the full Part II Python analysis in this repo — data
preparation, feature engineering, model comparison, and the country clustering —
independently within the group. The project was submitted as a group coursework
(Persian), alongside Part I's Tableau visualisations.

## Approach

- **Data preparation:** removed aggregate "All Ages"/"Global" rows, pivoted from long
  to wide format by Country × Age group (287 groups), producing 73 feature columns
  from weighted-mean survey responses
- **Target:** derived from the "strengthen climate commitments" question, using a
  median split for a balanced binary classification (~24% high support, ~76% lower)
- **Features:** split explicitly into demographic (country, age, education — 74
  features) and attitudinal (climate worry, urgency, policy preference — 70 features)
  to test which category actually drives predictions
- **Models compared:** Logistic Regression, Random Forest, Gradient Boosting — evaluated
  with balanced accuracy, F1, ROC AUC, and 5-fold cross-validation
- **Clustering:** K-means on country-level aggregated attitudes, with silhouette
  analysis to select k, visualised via PCA

## Results

| Model | Balanced Accuracy | F1 | ROC AUC |
|---|---|---|---|
| Logistic Regression | 0.90 | 0.90 | 0.93 |
| Random Forest | 0.83 | 0.83 | 0.96 |
| Gradient Boosting | 0.80 | 0.80 | 0.93 |

**Key finding:** attitudinal features vastly outweigh demographic features in
predicting support for stronger climate commitments — attitudes about urgency and
global cooperation dominate feature importance, while demographic factors (country,
age, education) contribute comparatively little. This suggests climate communication
strategy should focus on shifting perceptions rather than targeting specific
demographic groups.

**Clustering:** k=2 was the optimal number of country clusters (silhouette ≈ 0.21),
splitting nations into a larger group of developing/emerging economies with lower
climate-support scores and a smaller group of higher-income nations (including France,
Germany, Japan, the UK, and the US) showing stronger support for strengthening
commitments — a pattern that held up across regional analysis, though with meaningful
within-region variation.

## Tech stack

Python · pandas · scikit-learn (LogisticRegression, RandomForestClassifier,
GradientBoostingClassifier, KMeans, PCA) · matplotlib · seaborn · Tableau (Part I)

## Files

- `unpd_climate_analysis.ipynb` — Part II Python analysis (modelling + clustering)
- `Peoples_Climate_Vote_Database_2024.csv` — source dataset (UNDP/University of Oxford, 2024)
- `model_comparison.csv`, `clustering_metrics.csv`, `feature_importance.csv`, `country_clusters.csv` — output tables
- Figures: feature importance, confusion matrix, ROC curve, clustering elbow/silhouette, PCA cluster visualisation, hierarchical dendrogram, regional cluster analysis

## Reference

United Nations Development Programme and University of Oxford, "Peoples' Climate Vote 2024," UNDP, New York, NY, USA, Jun. 2024.
