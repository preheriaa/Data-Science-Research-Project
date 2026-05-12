# Hybrid RF/FSO Communication Channel Model

Predicting signal attenuation in hybrid Radio Frequency / Free-Space Optical (RF/FSO) communication systems using machine learning. This project models how weather conditions degrade wireless signal quality — a practical problem in the design of reliable outdoor communication links.

## Problem Statement

Hybrid RF/FSO systems combine two wireless technologies to improve reliability: FSO offers high bandwidth but is sensitive to weather (fog, rain, turbulence), while RF is more weather-resilient but lower bandwidth. Accurately predicting channel attenuation under different weather conditions helps engineers design systems that switch between channels at the right time.

This project builds a Random Forest regression model to predict channel attenuation from weather and environmental features, and evaluates it on both synthetic and empirical data.

## Dataset

- **File:** `RFLFSODataFull.csv`
- **Key features:** weather condition codes (SYNOP), atmospheric variables, channel measurement data
- **Target:** Channel attenuation values for RF/FSO links

## Project Structure

```
├── a1909636_hybrid_optical.ipynb          # Main analysis notebook
├── modified_a1909636_hybrid_optical.py    # Standalone Python script
├── a1909636_Data_Science_Project_A.pdf    # Full project report
└── RFLFSODataFull.csv                     # Dataset
```

## Methodology

### 1. Exploratory Data Analysis
- Distribution plots for all features to understand data shape
- Boxplots to identify outliers in each variable
- Correlation heatmap to understand feature relationships
- Ensured SYNOP weather codes were correctly typed as integers

### 2. Data Balancing
- Applied resampling (`sklearn.utils.resample`) to address class imbalance in weather condition categories
- Compared model performance on original vs. balanced data

### 3. Predictive Modelling
- **Model:** Random Forest Regressor
- **Train/test split:** standard holdout
- **Evaluation metrics:** RMSE and R²
- **Analysis:** Compared synthetic data performance vs. empirical data performance to understand model generalisation

### 4. Comparative Analysis
- Investigated performance differences between synthetic and real-world empirical datasets
- Documented insights in a detailed project report

## Key Findings

- Weather condition codes (SYNOP) are strong predictors of channel attenuation
- The model generalises better to empirical data when trained on balanced datasets
- Synthetic data can introduce bias that reduces real-world applicability — a key consideration in telecom modelling

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

# Run as a script
python modified_a1909636_hybrid_optical.py

# Or open the notebook
jupyter notebook a1909636_hybrid_optical.ipynb
```

> Update the dataset path in the notebook/script to point to your local `RFLFSODataFull.csv`.

## Author

**Prashant Shrestha**  
Master of Science in Data Science — University of Adelaide (2025)  
[LinkedIn](https://linkedin.com/in/preheria)
