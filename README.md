# National Walkability Index Analysis

Binary classification of U.S. Census block groups as **Walkable** or **Not Walkable** using the EPA Smart Location Database. Four machine learning models are built, tuned, and compared across 91,090 observations.

---

## Project Overview

The U.S. Environmental Protection Agency (EPA) rates the walkability of every Census block group in the country. This project converts that rating into a binary outcome and builds classification models to predict it — while identifying which neighborhood characteristics matter most.

**The important class is Non-Walkable (0)**, since correctly identifying areas that lack walkability has the most practical value for urban planning and policy decisions.

---

## Dataset

- **Source:** [EPA Smart Location Database](https://www.epa.gov/smartgrowth/national-walkability-index-user-guide-and-methodology)
- **Original size:** 220,740 Census block groups
- **After cleaning:** 91,090 (block groups with no nearby transit removed)
- **Split:** 80% training / 20% test

### Predictors

| Variable | Description |
|---|---|
| D1D | Activity Density — concentration of housing and jobs |
| D2B_E5MIX | Employment Mix — diversity of job types |
| D3B | Street Connectivity — ratio of intersections to street segments |
| D4A | Distance to Transit — distance to nearest public transit stop |

### Target Variable
- `Walkability` — binary: **0 = Not Walkable**, **1 = Walkable**

---

## Models

| Model | Test Accuracy | Test Sensitivity (Non-Walkable) |
|---|---|---|
| KNN (Original) | 0.850 | 0.495 |
| KNN (Normalized) | 0.894 | 0.659 |
| Decision Tree (Pruned) | 0.927 | 0.446 |
| Random Forest | 0.937 | 0.490 |
| **Bagged Tree** | **0.939** | **0.513** |

**Recommended model: Bagged Tree** — highest test accuracy (0.939) with a reasonable sensitivity for the important class. If identifying Non-Walkable areas is the sole priority, Normalized KNN offers the strongest test sensitivity (0.659).

---

## Key Findings

- **Street Connectivity (D3B)** is the most influential predictor across all models
- **Employment Mix (D2B_E5MIX)** is consistently the second most important
- **Activity Density (D1D)** has the least influence on walkability prediction
- A profile built from the mean values of all predictors is classified as **Walkable** with 100% model confidence, suggesting the average U.S. Census block group in this dataset tends to be walkable

---

## Files

```
national-walkability-analysis/
├── walkability_analysis.ipynb   ← Full analysis and code
├── report/
│   └── walkability_report.pdf   ← Original project write-up
└── README.md
```

> **Note:** The raw dataset is not included in this repository. It can be downloaded directly from the [EPA website](https://www.epa.gov/smartgrowth/national-walkability-index-user-guide-and-methodology).

---

## Tools & Libraries

- Python, Pandas, NumPy
- Scikit-learn (KNN, Decision Tree, BaggingClassifier, RandomForestClassifier, GridSearchCV, StandardScaler)
- Matplotlib, Seaborn
