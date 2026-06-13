# Iris Dataset - Principal Component Analysis
### Dushyant Singh Taggar | Undergraduate Engineer

---

## Overview

The Iris dataset has 150 flowers from three species with four measurements each. The question this notebook asks is whether all four measurements are actually necessary or whether most of the information is concentrated in fewer directions.
This is a dimensionality reduction problem. PCA finds the directions in the data that carry the most variation and lets you project everything onto those. If two directions are enough to capture 95%+ of the variance you can go from a 4-dimensional dataset to a 2D plot without losing much. I studied PCA in my MML course and wanted to run it on a real dataset to see if the theory holds up.

---

## What the analysis covers

The notebook starts with a standard look at the data - distributions by species, summary statistics, missing values. Before running PCA it checks correlations between the four features, because highly correlated features are not carrying independent information and PCA should be able to compress them. The data is then standardised (mean subtracted, divided by standard deviation for each feature) so PCA treats all features equally regardless of scale. PCA is applied, the explained variance per component is computed, and the loadings are examined to understand what each component actually represents. The final section projects the data onto two dimensions and runs a one way ANOVA to confirm the species separation in the reduced space is statistically significant and not just a visual artefact.

---

## Key Results

| Component | Variance Explained | Cumulative |
|---|---|---|
| PC1 | 72.96% | 72.96% |
| PC2 | 22.85% | 95.81% |
| PC3 | 3.67% | 99.48% |
| PC4 | 0.52% | 100% |

Two components account for 96% of the total variance. The remaining two are not worth keeping. PC1 is essentially a size axis - it loads heavily on petal length, petal width and sepal length, all of which are correlated with each other at r = 0.87 to 0.96. PC2 captures sepal shape, specifically the contrast between sepal width and sepal length independent of overall size. The 2D projection cleanly separates Setosa from the other two species and the ANOVA on PC1 scores returns a p-value essentially equal to zero, confirming the separation is real.

---

## Why the features compress so well

Petal length and petal width have a correlation of 0.96. They are measuring the same thing. Because of this the dataset that looks four dimensional is effectively two dimensional - most of what varies across the 150 flowers varies along a single size axis. PCA makes this visible.

---

## Tools used

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `seaborn` / `matplotlib` | Visualisation |
| `scikit-learn` | PCA, StandardScaler |
| `scipy.stats` | One way ANOVA (f_oneway) |

---

## About

Third/fourth year Engineering undergraduate. This project was built to apply PCA from coursework to a real dataset and examine whether the theoretical guarantees about variance compression hold in practice.

*— Dushyant Singh Taggar*
