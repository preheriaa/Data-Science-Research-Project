# Hybrid RF/FSO Communication Channel Model

Predicting signal attenuation in hybrid Radio Frequency / Free-Space Optical (RF/FSO) communication systems using machine learning. This project models how weather conditions degrade wireless signal quality — a practical problem in the design of reliable outdoor communication links.

## Problem Statement

Hybrid RF/FSO systems combine two wireless technologies to improve reliability: FSO offers high bandwidth but is sensitive to weather (fog, rain, turbulence), while RF is more weather-resilient but lower bandwidth. Accurately predicting channel attenuation under different weather conditions helps engineers design systems that switch between channels at the right time.

This project builds and compares two Random Forest modelling strategies — condition-specific and generic — to predict FSO and RF channel attenuation from weather and environmental features.

## Dataset

- **File:** `RFLFSODataFull.csv`
- **Size:** ~91,000 rows across 7 SYNOP weather condition categories
- **Key features:** weather condition codes (SYNOP), atmospheric variables (humidity, temperature, visibility, wind, particulate, rain), distance, frequency
- **Targets:** `FSO_Att` and `RFL_Att` — channel attenuation in dB for FSO and RF links

## Project Structure

```
├── hybrid_rf_fso.ipynb     # Full pipeline: EDA, balancing, feature selection, modelling
└── RFLFSODataFull.csv      # Dataset
```

## Methodology

### 1. Exploratory Data Analysis
- Distribution plots for all features to understand data shape
- Boxplots to identify outliers in each variable
- Correlation heatmap to understand feature relationships
- Hourly trend analysis of FSO and RF attenuation
- Ensured SYNOP weather codes were correctly typed as integers

### 2. Data Balancing
- Dataset had significant class imbalance across SYNOP categories (e.g. 56,964 clear-sky vs 191 code-3 entries)
- Resampled each SYNOP category to the median count using `sklearn.utils.resample`:
  - Over-represented categories → down-sampled (without replacement)
  - Under-represented categories → over-sampled (with replacement)
- Balanced dataset: 12,012 rows across 7 conditions

### 3. Feature Selection (Backward Elimination)
- Iteratively removed the least important feature by Random Forest feature importance
- Recorded RMSE and R² at each step; identified cutoff where performance stabilised
- Selected features: FSO = 12 retained, RFL = 9 retained

### 4. Modelling — Two Strategies Compared
- **Specific Model:** separate Random Forest trained per SYNOP weather condition
- **Generic Model:** single Random Forest trained across all conditions (SYNOPCode included as feature)
- Both strategies evaluated with RMSE and R² per target

## Key Findings

- SYNOPCode (weather condition) is the strongest predictor of attenuation for both FSO and RF channels
- Condition-specific models achieve lower RMSE than the generic model, confirming that attenuation patterns differ meaningfully across weather types
- Data balancing improved model performance on rare weather conditions that were heavily under-represented
- Backward elimination reduced noise without hurting predictive accuracy
- FSO attenuation is harder to predict (higher RMSE) than RF, consistent with its greater sensitivity to atmospheric conditions

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core language |
| pandas, NumPy | Data manipulation |
| Matplotlib, Seaborn | Visualisation |
| scikit-learn | Random Forest, resampling, evaluation |

## How to Run

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn

# Open the notebook
jupyter notebook hybrid_rf_fso.ipynb
```

> **Note:** Ensure `RFLFSODataFull.csv` is in the same directory as the notebook. This notebook is compute-intensive (~10–20 min runtime) due to the large dataset and multiple Random Forest models.

## Author

**Prashant Shrestha**  
Master of Science in Data Science — University of Adelaide (2025)  
[LinkedIn](https://linkedin.com/in/preheria)
