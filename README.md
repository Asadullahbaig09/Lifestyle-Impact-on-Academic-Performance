# Lifestyle Impact on Academic Performance

A data science project that investigates how various lifestyle factors — such as study habits, sleep patterns, physical activity, social interactions, and stress levels — influence students' academic performance (GPA).

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Technologies Used](#technologies-used)
- [Key Features](#key-features)
- [Results](#results)
- [How to Run](#how-to-run)

## Overview

This project analyzes the `student_lifestyle_dataset.csv` dataset to uncover relationships between lifestyle habits and GPA. It covers the full data science pipeline: exploratory data analysis, feature engineering, statistical hypothesis testing, and predictive modeling.

## Dataset

The dataset (`student_lifestyle_dataset.csv`) contains student-level records with the following features:

| Feature | Description |
|---|---|
| `Student_ID` | Unique identifier for each student |
| `Study_Hours_Per_Day` | Daily hours spent studying |
| `Extracurricular_Hours_Per_Day` | Daily hours on extracurricular activities |
| `Sleep_Hours_Per_Day` | Daily hours of sleep |
| `Social_Hours_Per_Day` | Daily hours spent socializing |
| `Physical_Activity_Hours_Per_Day` | Daily hours of physical activity |
| `Stress_Level` | Categorical stress level (Low, Moderate, High) |
| `GPA` | Grade Point Average (target variable) |

## Project Workflow

### 1. Exploratory Data Analysis (EDA)
- Summary statistics and dataset inspection (`shape`, `info`, `describe`)
- Distribution analysis with histograms and KDE plots
- Count plots for categorical features (Stress Level)
- Correlation heatmap of numeric features
- Scatter plots of GPA vs. lifestyle features (colored by Stress Level)
- Boxplots by Stress Level and outlier detection

### 2. Feature Engineering
- **Total Activity Hours**: Sum of extracurricular and physical activity hours
- **Free Time Hours**: Remaining hours after accounting for study, sleep, activities, and social time
- **Is_Stressed**: Binary encoding of stress (Low → 0, Moderate/High → 1)
- Duplicate row removal

### 3. Data Preprocessing
- Label encoding for `Stress_Level`
- Outlier detection via z-scores and capping with IQR method
- Standard scaling of numeric features

### 4. Model Training & Evaluation
Two regression models are trained and compared across multiple train-test split ratios (80-20, 70-30, 60-40):

| Model | Description |
|---|---|
| **Linear Regression** | Baseline linear model |
| **Random Forest Regressor** | Ensemble model with 100 estimators |

Evaluation metrics: **Mean Squared Error (MSE)** and **R² Score**.

### 5. Statistical Analysis & Hypothesis Testing
- **F-test (`f_regression`)**: Tests statistical significance of each predictor
- **Variance Inflation Factor (VIF)**: Detects multicollinearity among features
- **Highly Correlated Feature Removal**: Drops features with correlation > 0.9
- **ANOVA Test**: Evaluates overall model significance (full model vs. mean-only baseline)

## Technologies Used

- **Python 3**
- **Pandas** — Data manipulation
- **NumPy** — Numerical computation
- **Matplotlib & Seaborn** — Data visualization
- **Scikit-learn** — Machine learning (Linear Regression, Random Forest, preprocessing, evaluation)
- **SciPy** — Statistical tests (t-test, z-scores, F-distribution)
- **Statsmodels** — VIF calculation and advanced statistical modeling

## Key Features

- End-to-end analysis from raw data to predictive models
- Comprehensive EDA with multiple visualization types
- Engineered features capturing lifestyle–performance interactions
- Robust outlier handling using both z-score detection and IQR capping
- Statistical hypothesis testing to validate predictor significance
- Multicollinearity diagnostics with VIF and correlation filtering
- Model comparison across different data split strategies

## Results

Held-out performance on 2,000 students (80-20 split, `random_state=42`):

| Model | MSE | R² |
|---|---|---|
| Linear Regression | 0.0424 | 0.546 |
| Random Forest | 0.0508 | 0.455 |

R² stays at 0.52–0.55 (Linear Regression) and 0.44–0.46 (Random Forest) across the 70-30 and 60-40 splits. The full model is significant by ANOVA (F ≈ 214, p < 0.001).

- Study hours is the dominant predictor (≈59% of Random Forest feature importance). Social time, physical activity and stress level are also significant in the univariate F-tests, while sleep and extracurricular hours are not.
- Linear Regression slightly outperforms Random Forest, which suggests the relationships are mostly linear.
- GPA-derived features (GPA category, GPA ratios) are excluded on purpose: they leak the target and inflate R² to ~0.99.

## How to Run

1. **Clone the repository** and navigate to the project folder.
2. **Install dependencies**:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy statsmodels
   ```
3. **Place the dataset** (`student_lifestyle_dataset.csv`) in the project root directory.
4. **Open and run** `Project.ipynb` in Jupyter Notebook, JupyterLab, or VS Code.

## Author

Asad Ullah Baig
