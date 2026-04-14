# Economic Resilience: Does Renewable Energy Buffer Oil Price Shocks?

## Project Overview
Recent geopolitical tensions have highlighted the critical vulnerability of oil-importing nations to sudden disruptions in global energy markets. As energy transitions accelerate globally, policymakers increasingly justify clean energy investments not only for environmental sustainability but also for national economic security. 

This project investigates whether renewable energy adoption serves as a structural, macroeconomic buffer against oil price shocks. By analyzing panel data across multiple nations, this study aims to determine if a higher share of renewable energy reduces a country's exposure to price volatility and mitigates its subsequent impact on economic growth.

## Primary Research Question
Does renewable energy adoption buffer the impact of oil price fluctuations on economic growth across oil-importing countries over time?

## Data Sources and Features
The analysis is based on a merged panel dataset spanning from 2000 to 2020, focusing strictly on net oil-importing countries. The final dataset consists of 1,473 observations across 91 countries.

* **Global Data on Sustainable Energy (IEA / World Bank):** Provided the annual renewable energy share in total final energy consumption, GDP growth rates, and GDP per capita.
* **Brent Crude Oil Prices:** Daily historical prices were aggregated into annual averages to calculate year-on-year percentage changes, representing the global oil price shock variable.
* **World Bank Open Data:** Provided energy import dependency metrics, measuring the percentage of energy consumption sourced from foreign imports.

## Methodology
The analytical workflow is divided into two primary Jupyter Notebooks to maintain a clean structure:

1. **Data Collection and Cleaning (Data_Cleaning.ipynb)**
   * Transformed World Bank data from wide to long format.
   * Engineered new features, including annualized oil price percentage changes.
   * Merged multi-source datasets utilizing 'Country' and 'Year' as primary keys.
   * Filtered the dataset strictly for net energy importers to ensure the validity of the research scope.

2. **Visualization and Statistical Analysis (Visualization_and_Analysis.ipynb)**
   * **Exploratory Data Analysis (EDA):** Analyzed variable distributions, correlation matrices, and group-wise comparative statistics.
   * **Hypothesis Testing:** Conducted Pearson and Spearman rank-order correlation tests to identify initial linear and monotonic relationships.
   * **Econometric Modeling:** Implemented an Ordinary Least Squares (OLS) Fixed-Effects Panel Regression Model. The model controls for GDP per capita and energy import dependency, alongside Country and Year fixed effects. An interaction term (`oil_price_change * renewable_share`) was introduced to explicitly test the buffering hypothesis.

## Key Findings
The Fixed-Effects Regression Model yielded an R-squared value of 0.447, with several highly significant statistical findings:

* **Oil Price Impact:** Fluctuations in oil prices significantly impact GDP growth across the observed countries (Pearson r=0.237, p < 0.001).
* **Renewable Energy and Growth:** There is a baseline positive correlation between a higher renewable energy share and GDP growth (Pearson r=0.171, p < 0.001).
* **The Buffering Effect (Core Finding):** The interaction term between oil price change and renewable share is statistically significant (p < 0.001). This confirms the central hypothesis: renewable energy successfully acts as a macroeconomic buffer. Countries with higher proportions of renewable energy in their mix experience notably less economic volatility during periods of severe oil price shocks.
* **Import Dependency:** Energy import dependency exhibits a negative rank-order correlation with economic growth (Spearman r=-0.163, p < 0.001), reinforcing the economic risk of high external energy reliance.

## Repository Structure
* `/Data_Cleaning.ipynb` - Script for data ingestion, preprocessing, and merging.
* `/Visualization_and_Analysis.ipynb` - Script containing the EDA and formal statistical testing.
* `/final_dataset.csv` - The cleaned and merged panel dataset used for final modeling.

## Future Work
Following the formal statistical testing, future iterations of this project plan to incorporate Machine Learning methodologies. Algorithms such as Random Forest and XGBoost will be applied to predict GDP growth resilience, utilizing SHAP (SHapley Additive exPlanations) values to extract deeper insights into feature importance and non-linear interactions.

## How to Run
1. Clone this repository to your local machine or Google Colab environment.
2. Ensure you have the required Python dependencies installed: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`.
3. Execute `Data_Cleaning.ipynb` to process the raw data and output `final_dataset.csv`.
4. Execute `Visualization_and_Analysis.ipynb` to reproduce the descriptive statistics, visualizations, and regression models.
