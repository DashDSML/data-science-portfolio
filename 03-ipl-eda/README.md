# IPL Match Analysis — Exploratory Data Analysis & Hypothesis Testing
### Dushyant Singh Taggar | Undergraduate Engineer

---

## Overview

This project uses IPL match data from 2008 to 2019 to test whether things that feel important in cricket — winning the toss, choosing to field — are actually statistically meaningful or whether they just feel that way because of how the sport is talked about.

The dataset has 756 matches, one row per match. The analysis moves from a standard data interrogation through EDA and into three formal hypothesis tests, each chosen based on the variable types involved rather than applied arbitrarily.

---

## Objectives

- Perform structured exploratory data analysis on match outcomes, team performance and toss behaviour across 12 IPL seasons
- Select the correct statistical test for each question based on whether the variables are categorical or continuous
- Interpret results in plain terms and assess whether commonly held beliefs about T20 cricket hold up statistically

---

## Dataset

**Source:** IPL Complete Dataset 2008-2019 (Kaggle)
**File used:** `matches.csv` — one row per match with toss, result and margin information
**Size:** 756 matches, 18 columns
**Target questions:** toss outcome, toss decision, win margins

---

## Methodology

### 1. Data Cleaning
- Matches with no result or a tie (13 rows) are filtered out before analysis since they have no meaningful outcome
- `umpire3` is dropped — missing for 637 of 756 rows with no analytical value
- `city` nulls are identified as Dubai matches played abroad and left as is

### 2. Exploratory Data Analysis
- Total wins by team across all seasons
- Matches played per season with notes on expansion and the 2009 South Africa edition
- Toss decision trends by season — whether the preference for fielding has shifted over time
- Win margin distributions for batting first wins (runs) and chasing wins (wickets) separately

### 3. Correlation Heatmap
Engineered two binary columns — `toss_won_match` and `chose_field` — and examined correlations with `win_by_runs` and `win_by_wickets`. The negative correlation between the two win columns is structural: they cannot both be nonzero in the same match.

### 4. Hypothesis Testing

Three questions, three tests. The test type was chosen based on variable types before looking at the data.

| Test | Question | Variable Types | Test Used |
|---|---|---|---|
| 1 | Does winning the toss improve your chances of winning? | Categorical vs Categorical | Chi-square |
| 2 | Does choosing to field after the toss help? | Categorical vs Categorical | Chi-square |
| 3 | Do top teams win by larger margins batting first? | Continuous vs Continuous | t-test |

---

## Key Results

| Test | p-value | Conclusion |
|---|---|---|
| Toss win vs match win | > 0.05 | Not significant |
| Toss decision vs match win | < 0.05 | Significant |
| Top teams vs others, win by runs | > 0.05 | Not significant |

Winning the toss does not significantly affect match outcome. The toss winner won about 52% of matches which looks above chance but is not large enough to rule out random variation at this sample size.

The decision made after winning the toss does matter. Teams that chose to field won 56% of those matches compared to 46% for teams that chose to bat. This difference is statistically significant and consistent with how T20 tactics have evolved — by 2017 and 2018 fielding first is the overwhelming choice after winning the toss.

Top teams like Mumbai Indians and Chennai Super Kings win more matches overall but when they win batting first the margin in runs is not significantly different from other teams. Dominance shows up in consistency, not in the size of individual wins.

---

## Why the toss decision matters more than the toss itself

Winning the toss just gives you the choice. The data says fielding first is the better choice. The value of the toss is entirely in what you do with it — which is why the first test comes back insignificant and the second does not.

---

## Limitations & Honest Assessment

- The dataset covers 2008 to 2019 only — conclusions may not hold for more recent seasons where pitch and rule conditions have changed
- The t-test for win margins compares only batting first wins, so it does not capture dominance when teams are chasing — a fuller analysis would need a way to put runs and wickets on the same scale
- Several factors that plausibly affect outcomes (pitch type, home advantage, player availability) are absent from the data

---

## Technical Stack

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation and cleaning |
| `numpy` | Numerical operations |
| `seaborn` / `matplotlib` | Visualisation |
| `scipy.stats` | Chi-square test, independent samples t-test |

---

## Repository Structure

```
data-science-portfolio/
└── IPL_EDA.ipynb    ← Full analysis notebook
```

---

## About

Third/fourth year Engineering undergraduate with a focus on applied statistical methods. This project was built independently as part of a self-directed data science portfolio. The dataset was chosen because cricket is something I actually follow — the hypothesis tests were a way of checking whether the intuitions you build up watching the sport are real.

*— Dushyant Singh Taggar*
