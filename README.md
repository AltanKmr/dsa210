# Economic Resilience: Does Renewable Energy Buffer Oil Price Shocks?

## Project Overview

Recent geopolitical tensions have highlighted the critical vulnerability of
oil-importing nations to sudden disruptions in global energy markets. As energy
transitions accelerate globally, policymakers increasingly justify clean energy
investments not only for environmental sustainability but also for national
economic security.

This project investigates whether renewable energy adoption serves as a
structural, macroeconomic buffer against oil price shocks. By analyzing panel
data across multiple nations, this study aims to determine if a higher share of
renewable energy reduces a country's exposure to price volatility and mitigates
its subsequent impact on economic growth.

## Primary Research Question

Does renewable energy adoption buffer the impact of oil price fluctuations on
economic growth across oil-importing countries over time?

## Data Sources and Features

The analysis is based on a merged panel dataset spanning from 2000 to 2020,
focusing strictly on net oil-importing countries. The final dataset consists of
**1,473 observations across 91 countries**.

- **Global Data on Sustainable Energy (IEA / World Bank):** Provided the annual
  renewable energy share in total final energy consumption, GDP growth rates,
  and GDP per capita.
- **Brent Crude Oil Prices:** Daily historical prices were aggregated into
  annual averages to calculate year-on-year percentage changes, representing
  the global oil price shock variable.
- **World Bank Open Data:** Provided energy import dependency metrics, measuring
  the percentage of energy consumption sourced from foreign imports

## Repository Structure

```
/
├── Data_Cleaning.ipynb               # Data ingestion, preprocessing, and merging
├── Visualization_and_Analysis.ipynb  # EDA and formal statistical testing
├── ML_Methods.ipynb                  # Machine learning models and predictions
├── final_dataset.csv                 # Cleaned and merged panel dataset
└── requirements.txt                  # Python dependencies
```

## Methodology

The analytical workflow is divided into three Jupyter Notebooks:

### 1. Data Collection and Cleaning (`dsa210.ipynb`)

- Transformed World Bank data from wide to long format.
- Engineered new features, including annualized oil price percentage changes
  and an interaction term (`renewable_share × oil_price_change`).
- Merged multi-source datasets using `country` and `year` as primary keys.
- Filtered the dataset strictly for net energy importers to ensure the validity
  of the research scope.
- **Exploratory Data Analysis (EDA):** Analyzed variable distributions,
  correlation matrices, and group-wise comparative statistics.
- **Hypothesis Testing:** Conducted Pearson and Spearman rank-order correlation
  tests to identify linear and monotonic relationships.
- **Econometric Modeling:** Implemented an Ordinary Least Squares (OLS)
  Fixed-Effects Panel Regression Model controlling for GDP per capita, energy
  import dependency, and country/year fixed effects. An interaction term
  (`oil_price_change × renewable_share`) was introduced to explicitly test the
  buffering hypothesis. This model achieved an **R² of 0.447**.

### 2. Machine Learning Methods (`ml_methods.ipynb`)

Four machine learning algorithms were applied to extend the statistical findings
into a predictive framework:

#### Random Forest Regressor
A 200-tree ensemble model trained to predict GDP growth. Key configuration:
`max_depth=15`, `min_samples_split=5`, `max_features='sqrt'`. Evaluated with
5-fold cross-validation and learning curve diagnostics. Gini-based feature
importance was extracted to rank predictor contributions.

#### XGBoost Regressor
An Extreme Gradient Boosting model (`n_estimators=300`, `learning_rate=0.05`,
`max_depth=5`) trained on the same feature set. Served as the second regression
engine for performance benchmarking against Random Forest.

#### K-Means Clustering
Unsupervised segmentation of countries based on their macro-energy profiles.
Optimal cluster count (K=3) was selected via the Elbow Method and Silhouette
Coefficient analysis. Results were projected into 2D using PCA for
visualization, revealing three structurally distinct country groups with
different economic resilience profiles.

#### Logistic Regression
A binary classification model predicting whether a country will experience
**economic expansion** (GDP growth > 0) or **contraction** (GDP growth ≤ 0).
Trained with L2 regularization and `class_weight='balanced'` to handle class
imbalance. Model performance was evaluated using ROC-AUC and Precision-Recall
curves. The trained model was subsequently used to score each country's
**probability of economic expansion**, enabling three strategic country
rankings:

- 🏆 **Green Growth Leaders** — high renewable share, highest expansion
  probability
- ⚠️ **Highly Vulnerable Importers** — high energy import dependency, highest
  contraction risk
- 🛢️ **Traditional Energy Giants** — energy-independent nations, ranked by
  macroeconomic resilience

## Key Findings

### Statistical Analysis

The Fixed-Effects Regression Model yielded an **R² of 0.447**, with several
highly significant results:

- **Oil Price Impact:** Oil price fluctuations significantly affect GDP growth
  (Pearson r = 0.237, p < 0.001). Confirmed by H1.
- **Renewable Energy and Growth:** Higher renewable share correlates positively
  with GDP growth (Pearson r = 0.171, p < 0.001). Confirmed by H2.
- **The Buffering Effect (Core Finding):** The interaction term between oil
  price change and renewable share is statistically significant (p < 0.001).
  Countries with a higher renewable share experience significantly less economic
  volatility during oil price shocks. Confirmed by H3.
- **Import Dependency:** Energy import dependency shows a negative rank-order
  correlation with growth (Spearman r = −0.163, p < 0.001). Partially
  confirmed by H4.

### Machine Learning Analysis

| Model | Task | Key Metric |
|-------|------|-----------|
| Random Forest | Regression (GDP growth prediction) | R², RMSE, MAE |
| XGBoost | Regression (GDP growth prediction) | R², RMSE, MAE |
| K-Means (K=3) | Clustering (country segmentation) | Silhouette Score |
| Logistic Regression | Classification (expansion vs contraction) | ROC-AUC, PR-AUC |

**Feature Importance (Random Forest):** Gini importance scores confirmed that
`oil_price_change` and `renewable_share` are the dominant predictors of GDP
growth, consistent with the statistical findings. The interaction term
`renewable_x_oil` ranked as a meaningful contributor, providing ML-based
evidence that the buffering relationship is not merely a linear artifact.

**Country Segmentation (K-Means):** Three country clusters emerged with
structurally distinct energy-economic profiles. The cluster with the highest
average renewable share demonstrated lower GDP growth variance during oil shock
years, visually confirming the buffering hypothesis at a population level.

**Classification Performance (Logistic Regression):** The model successfully
discriminated between expansion and contraction periods, with ROC-AUC and
Precision-Recall curves indicating meaningful predictive signal beyond a random
baseline. Country-level expansion probabilities produced an interpretable
strategic ranking aligned with the project's policy implications.

## Hypothesis Summary

| Hypothesis | Description | Verdict |
|-----------|-------------|---------|
| H1 | Oil price change affects GDP growth | ✅ Supported |
| H2 | Renewable share positively affects GDP growth | ✅ Supported |
| H3 | Renewable energy buffers oil price shocks on GDP | ✅ Supported |
| H4 | Energy import dependency negatively affects GDP growth | ⚠️ Partially supported |

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/AltanKmr/dsa210
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run notebooks in order:
   - `Data_Cleaning.ipynb`
   - `Visualization_and_Analysis.ipynb`
   - `ML_Methods.ipynb`

## Requirements

See `requirements.txt` for the full list. Key dependencies:

```
pandas, numpy, matplotlib, seaborn, plotly
scikit-learn, xgboost, statsmodels
```
