# Data Science Portfolio
### Dushyant Singh Taggar | Undergraduate Engineer

---

## Overview

Three independent projects built to develop and demonstrate applied data science skills. Each project was chosen to cover a different part of the stack — classification, dimensionality reduction, and statistical inference — and each one was built with a real dataset rather than a toy example.

The work spans supervised learning, unsupervised learning, and hypothesis testing. All notebooks are written to be readable: the reasoning behind each decision is explained in the notebook itself, not just the code.

---

## Projects

### [01 — Titanic Survival Prediction | EDA & Logistic Regression](./01-titanic-survival/README.md)

Binary classification problem. The question is whether survival on the Titanic can be predicted from passenger data — sex, class, age, fare, family situation. The answer is yes, to about 80% accuracy, which matches published benchmarks on this dataset.

What makes this more than a standard Titanic notebook is the statistical groundwork before the model is touched. The analysis distinguishes between Pearson and point-biserial correlation depending on whether the feature is continuous or binary, runs VIF to check for multicollinearity, and uses McFadden's Pseudo R² to track exactly how much each additional feature contributes to the model — the logistic regression equivalent of adjusted R² in OLS. The log-loss function is derived from first principles and tied back to maximum likelihood estimation over a Bernoulli distribution.

Sex and passenger class dominate. McFadden's R² plateaus after three features. Additional variables spend degrees of freedom without meaningful gain.

**Key tools:** `pandas`, `scikit-learn`, `scipy.stats`, `statsmodels`

---

### [02 — Iris PCA | Dimensionality Reduction & Variance Analysis](./02-iris-pca/README.md)

Dimensionality reduction problem. The Iris dataset has four features but they are not carrying four independent pieces of information. Petal length and petal width correlate at r = 0.96. Because of this, PCA compresses 96% of the total variance into just two components.

The notebook works through the full PCA pipeline — standardisation with justification for why it is necessary, explained variance computation, loading analysis to interpret what each principal component actually represents, and a 2D projection with species coloured. PC1 is a size axis. PC2 captures sepal shape independent of size. A one-way ANOVA on PC1 scores confirms the species separation in the reduced space is statistically significant and not a visual artefact.

The mathematical explanation of PCA — principal components as directions of maximum variance, eigenvalues as the proportion of variance explained — is written out in the notebook rather than treated as a black box.

**Key tools:** `pandas`, `scikit-learn`, `scipy.stats`, `matplotlib`

---

### [03 — IPL Match Analysis | EDA & Hypothesis Testing](./03-ipl-eda/README.md)

Statistical inference problem. 756 IPL matches from 2008 to 2019. The question is whether things that feel important in cricket — winning the toss, choosing to field — are actually statistically meaningful.

Three hypothesis tests are run, each chosen based on the variable types before looking at results. Toss outcome vs match outcome is categorical vs categorical so chi-square is used. Win margins for two groups of teams is continuous vs continuous so a t-test is used. The choice of test is explained in the notebook at each step.

Results: winning the toss does not significantly affect match outcome (p > 0.05). The decision made after the toss does — teams that chose to field won 56% of those matches vs 46% for teams that batted (p < 0.05). Top teams do not win by significantly larger margins than others when batting first; their dominance is in consistency, not margin size.

**Key tools:** `pandas`, `scipy.stats`, `seaborn`, `matplotlib`

---

## What these projects cover together

| Area | Project |
|---|---|
| Binary classification | 01 — Titanic |
| Model assumption testing | 01 — Titanic |
| Dimensionality reduction | 02 — Iris PCA |
| Variance decomposition | 02 — Iris PCA |
| Hypothesis testing (chi-square) | 03 — IPL |
| Hypothesis testing (t-test) | 03 — IPL |
| Exploratory data analysis | All three |
| Statistical correlation analysis | All three |

---

## Repository Structure

```
data-science-portfolio/
├── README.md                          ← You are here
├── 01-titanic-survival/
│   ├── TitanicLogReg+EDA.ipynb
│   └── README.md
├── 02-iris-pca/
│   ├── IrisPCA.ipynb
│   └── README.md
└── 03-ipl-eda/
    ├── IPL_EDA.ipynb
    └── README.md
```

---

## About

Third/fourth year Engineering undergraduate. These projects were built independently as a self-directed data science portfolio. The goal was to go beyond running functions and understand what the methods are actually doing — why you standardise before PCA, why log-loss is the right objective for logistic regression, why the chi-square test is appropriate for categorical variables and the t-test is not. That reasoning is written into each notebook.

*— Dushyant Singh Taggar*
