# Titanic Survival Prediction — EDA & Logistic Regression
### Dushyant Singh Taggar | Undergraduate Engineer

---

## Overview

This project investigates whether passenger survival on the Titanic can be predicted from biographical and ticketing data. The problem is framed as a **binary classification task** — the target variable `survived` takes values 0 or 1 — and solved using Logistic Regression with rigorous statistical validation at each stage.

The analysis is structured to mirror a real applied research workflow: beginning with data interrogation, moving through assumption testing, feature selection grounded in correlation theory, and concluding with model evaluation using both standard and information-theoretic metrics.

---

## Objectives

- Perform structured exploratory data analysis to understand feature distributions and their relationship to survival
- Validate statistical assumptions before and after modelling (normality, multicollinearity, feature redundancy)
- Build an interpretable binary classifier and evaluate it beyond simple accuracy
- Demonstrate that feature selection decisions can be grounded in statistical theory rather than trial and error

---

## Dataset

**Source:** Seaborn's built-in Titanic dataset (`sns.load_dataset('titanic')`)  
**Size:** 891 passengers, 15 features  
**Target:** `survived` (0 = Did not survive, 1 = Survived)

---

## Methodology

### 1. Exploratory Data Analysis
- Distribution analysis of continuous features (`age`, `fare`) and categorical features (`sex`, `pclass`, `embarked`)
- Survival rate breakdowns by demographic and ticketing variables
- Missing value assessment and imputation strategy

### 2. Feature Engineering
| Feature | Description |
|---|---|
| `sex_encoded` | Binary encoding of passenger sex |
| `embarked_encoded` | Ordinal encoding of port of embarkation |
| `family_size` | `sibsp + parch + 1` — total family aboard |
| `is_alone` | Binary flag: `family_size == 1` |

### 3. Statistical Assumption Testing
- **Shapiro-Wilk Test** — normality check on continuous features
- **Point-Biserial Correlation** — measuring association between binary features and the survival target, with p-values reported for each
- **Variance Inflation Factor (VIF)** — multicollinearity detection across all model features

### 4. Feature Selection — McFadden's Pseudo R²
Features were added sequentially in descending order of correlation strength. At each step, McFadden's Pseudo R² was computed:

```
McFadden's R² = 1 − (log-likelihood of model / log-likelihood of null model)
```

This approach directly quantifies the marginal information gain of each additional feature — equivalent in spirit to adjusted R² in OLS regression — and identifies the point of diminishing returns.

### 5. Model Training & Evaluation
- **Model:** Logistic Regression (`sklearn`, L2 penalty, `lbfgs` solver, `max_iter=1000`)
- **Split:** Stratified train/test split
- **Metrics:** Accuracy, Precision, Recall, F1-score, Confusion Matrix, Classification Report

---

## Key Results

| Feature | Point-Biserial r | p-value |
|---|---|---|
| `sex_encoded` | −0.543 | < 0.0001 |
| `is_alone` | −0.203 | < 0.0001 |
| `embarked_encoded` | −0.168 | < 0.0001 |

- **Model Accuracy: ~80%** — consistent with published benchmarks on this dataset
- `sex_encoded` and `pclass` together account for the majority of the model's explanatory power
- McFadden's R² plateaus after three features, indicating additional variables spend degrees of freedom without meaningful predictive gain

---

## Limitations & Honest Assessment

- The dataset is a **census, not a random sample** — statistical inference is bounded to this voyage and cannot be generalised to a broader population
- **Omitted variable bias** is likely: lifeboat proximity, deck positioning, and social connections aboard correlate with both predictors and survival but are absent from the data
- Logistic Regression assumes **linearity in the log-odds** — this was not formally tested and represents a modelling assumption worth revisiting with more flexible classifiers

---

## Technical Stack

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation and cleaning |
| `numpy` | Numerical operations |
| `seaborn` / `matplotlib` | Visualisation |
| `scikit-learn` | Model training, preprocessing, evaluation |
| `scipy.stats` | Point-biserial correlation, Shapiro-Wilk test |
| `statsmodels` | Logit model, VIF computation |

---

## Repository Structure

```
data-science-portfolio/
└── TitanicLogReg+EDA.ipynb    ← Full analysis notebook
```

---

## About

Third/fourth year Engineering undergraduate with a focus on applied statistical methods and machine learning. This project was built independently as part of a self-directed learning programme in data science.

*— Dushyant Singh Taggar*
