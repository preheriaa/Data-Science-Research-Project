# Hybrid Optical Analysis
This repository contains code and analysis for evaluating communication performance using hybrid RF/FSO systems. The analysis includes:
1. Exploratory Data Analysis
- Histograms, boxplots, and time-series plots to study trends and outliers.
- Distribution check of weather conditions (SYNOPCode).

2. Feature Selection
- Wrapper-based selection using Random Forest importance.
- Dimensionality reduction based on RMSE and R² thresholding.

3. Model Development
- **Specific Models**: One Random Forest per SYNOPCode (7 total).
- **Generic Model**: Single model using all data.
- **Joint Models**:
  - RF ➝ FSO: Use RF prediction as a feature for FSO model.
  - FSO ➝ RF: Use FSO prediction as a feature for RF model.

4. Evaluation and Visualization
- RMSE & R² per weather condition and average
- Worst-case RMSE
- Pearson Correlation
- Normalised Entropy Ratio (Ieo/Heo)

