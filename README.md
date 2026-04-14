# 🌍 Economic Resilience: Does Renewable Energy Buffer Oil Price Shocks?

## 📌 Project Overview
Recent geopolitical tensions have highlighted the vulnerability of oil-importing nations to sudden disruptions in global energy markets. This project investigates whether **renewable energy adoption serves as a structural buffer against oil price shocks**, reducing a country's exposure to price volatility and its subsequent impact on economic growth. 

Understanding this relationship is increasingly urgent for policymakers seeking to justify clean energy transitions not just for environmental reasons, but as a matter of national economic resilience.

## 🎯 Research Question
*Does renewable energy adoption buffer the impact of oil price fluctuations on economic growth across oil-importing countries over time?*

## 📊 Data Sources
The project utilizes a panel dataset spanning from **2000 to 2020**, combining three main sources:
1. **[Global Data on Sustainable Energy](https://www.kaggle.com/)**: Provides annual renewable energy share, GDP growth, and GDP per capita.
2. **[Brent Crude Oil Prices](https://www.kaggle.com/)**: Daily prices aggregated to annual averages and year-on-year percentage changes.
3. **[World Bank Open Data](https://data.worldbank.org/)**: Energy import dependency (measuring the share of energy consumption sourced from imports).

*Note: The final dataset was filtered to include only net oil-importing countries (91 countries, 1,473 observations).*

## 🛠️ Methodology & Project Structure
The analysis is conducted in Python using Jupyter Notebooks/Google Colab, split into two main phases:

* **1. Data Collection and Cleaning (`Data_Cleaning.ipynb`)**
  * Reshaping World Bank data from wide to long format.
  * Aggregating daily oil prices to annual percentage changes.
  * Merging datasets on 'Country' and 'Year'.
  * Filtering for net energy importers (`energy_import_pct > 0`).

* **2. Visualization and Analysis (`Visualization_and_Analysis.ipynb`)**
  * **EDA:** Correlation matrices, variable distributions, and group comparisons.
  * **Hypothesis Testing:** Pearson and Spearman correlation tests.
  * **Statistical Modeling:** Fixed-Effects Panel Regression Model (OLS) including an interaction term (`oil_price_change * renewable_share`) to test the buffering effect.

## 📈 Key Findings
Based on our Fixed-Effects Panel Regression Model (R² = 0.447):

* **H1 (Supported):** Oil price changes significantly affect GDP growth (Pearson r=0.237, p<0.001).
* **H2 (Supported):** Renewable energy share positively affects GDP growth (Pearson r=0.171, p<0.001).
* **H3 (Supported - Core Finding):** Renewable energy successfully acts as a buffer against oil price impacts. The interaction term (`renewable_x_oil`) is statistically significant (p<0.001), indicating that countries with higher renewable energy shares experience less economic volatility during oil price shocks.
* **H4 (Partially Supported):** Energy import dependency shows a negative rank-order relationship with GDP growth (Spearman r=-0.163, p<0.001).

## 🚀 How to Run
1. Clone this repository.
2. Ensure you have the required libraries installed: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`.
3. Run `Data_Cleaning.ipynb` to generate the `final_dataset.csv`.
4. Run `Visualization_and_Analysis.ipynb` to view the EDA and regression models.
