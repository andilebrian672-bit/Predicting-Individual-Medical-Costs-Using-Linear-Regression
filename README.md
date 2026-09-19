# Predicting Individual Medical Costs Using Linear Regression

---

## 📋 Overview

This project builds a **Linear Regression** model to predict individual medical
insurance costs (`charges`) from demographic and lifestyle features. It covers
the full machine-learning pipeline: exploratory data analysis, preprocessing,
feature encoding, model training, and evaluation.

The goal is to identify the strongest drivers of medical cost and demonstrate
the utility of simple, interpretable models in health analytics.

---

## 📊 Dataset

- **Source:** `data/insurance.csv`
- **Records:** 1,338 individuals
- **Features:** 6 predictors + 1 target

| Feature    | Type        | Description                                              |
|------------|-------------|----------------------------------------------------------|
| `age`      | Integer     | Age of the primary beneficiary                           |
| `sex`      | Categorical | `male` / `female`                                        |
| `bmi`      | Continuous  | Body Mass Index                                          |
| `children` | Integer     | Number of children covered by health insurance           |
| `smoker`   | Categorical | `yes` / `no`                                             |
| `region`   | Categorical | `northeast`, `southeast`, `southwest`, `northwest`       |
| `charges`  | Continuous  | **Target** — individual medical costs billed (USD)       |

---

## 🔍 Approach

### 1. Data Pre-processing
- Checked for missing values — none found
- **Label encoding** for binary variables: `sex` (female=0, male=1), `smoker` (no=0, yes=1)
- **One-hot encoding** for `region` (dropped first column to avoid the dummy-variable trap)
- **StandardScaler** applied to all features (mean = 0, SD = 1)
- **80/20 train–test split**

### 2. Exploratory Data Analysis (EDA)
- Summary statistics for all variables
- Correlation matrix heatmap
- Distribution plots: gender, smoker status, age, charges
- Boxplot of medical costs by gender
- Regression line of age vs. charges

### 3. Model
- **Algorithm:** Linear Regression (`sklearn.linear_model.LinearRegression`)
- **Justification:** Target is continuous; linear regression provides a simple,
  interpretable baseline well-suited to this task.

### 4. Evaluation Metrics
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (R²)

---

## 📈 Results

### Key EDA Findings

| Correlation with `charges` | Value |
|----------------------------|-------|
| `smoker`                   | **0.79** ← strongest |
| `age`                      | 0.30  |
| `bmi`                      | 0.20  |

Smoking status is by far the most significant predictor, followed by age and BMI.

### Model Performance

| Metric | Value |
|--------|-------|
| **MSE**  | 36,705,783 |
| **RMSE** | $6,059 |
| **R²**   | **0.78** |

The model explains **78% of the variance** in medical charges — a solid fit for
a first-pass linear model. It performs well for low-to-medium costs but
**underpredicts the most extreme high-cost cases** ("super-utilizers"), a known
challenge in healthcare cost modelling.

![Actual vs Predicted](images/actual_vs_predicted.png)
*Actual vs. predicted medical costs — points cluster along the ideal line for low/medium costs but diverge at the high end.*

---
