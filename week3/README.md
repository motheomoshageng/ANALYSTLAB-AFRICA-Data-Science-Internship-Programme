# Heart Disease Prediction — Advanced Analysis, Statistical Validation & Feature Engineering

**AnalystLab Africa — Data Science Internship, Week 3**

## Project Overview

This is the Week 3 continuation of the Heart Disease Prediction project. It builds directly on the Week 2 cleaned dataset — no cleaning steps are repeated — and adds advanced exploratory data analysis, statistical hypothesis testing, further feature engineering, feature evaluation, and a refined final modelling dataset for Week 4.

Full narrative and evidence are in the notebook and the five accompanying reports (below).

## Repository Structure

```
.
├── README.md
├── requirements.txt
├── AnalystLab_Week3_Advanced_Analysis.ipynb        # Main notebook (all steps, executed with outputs)
├── Project_Continuity_Summary.docx                  # Part 1 deliverable
├── Statistical_Analysis_Summary.docx                 # Part 3 deliverable (4 tests, full write-up)
├── Feature_Engineering_and_Evaluation_Report.docx    # Parts 4 & 5 deliverables
├── Business_Insights_and_Recommendations_Report.docx # Part 7 deliverable (3 pages)
├── Data_Dictionary.docx                              # Updated data dictionary
├── heart.csv                                         # Original raw dataset (from Week 2)
├── data/
│   ├── heart_week2_cleaned.csv                        # Input: Week 2 cleaned dataset (917 rows, 15 cols)
│   └── heart_final_modelling_dataset.csv              # Output: Week 3 final modelling dataset (917 rows, 22 cols)
└── figs/                                              # Saved copies of all 16 notebook visualizations (PNG)
```

## What's New Since Week 2

| Area | Week 3 Addition |
|---|---|
| EDA | 16 additional visualizations: advanced distribution analysis (skewness), bivariate and multivariate analysis, group comparisons, target-variable analysis |
| Statistics | 4 hypothesis tests: Mann-Whitney U (Oldpeak), Welch's T-Test (MaxHR), Chi-Square (ChestPainType), Kruskal-Wallis (Cholesterol by ST_Slope) — all with full H0/H1, test statistic, p-value, decision, and business implication |
| Feature engineering | 3 new features: `MaxHR_Pct`, `RiskFactor_Count`, `Cholesterol_log` |
| Feature evaluation | Correlation, Variance Inflation Factor (manual, via linear regression R²), mutual information, and Random Forest importance — used to drop `HR_Reserve`, `MaxHR_Pct`, and raw `Cholesterol` as redundant |
| Final dataset | `data/heart_final_modelling_dataset.csv` — refined 22-column dataset ready for Week 4 modelling |

## Key Findings

- Oldpeak, MaxHR, and ChestPainType are all **statistically significantly** associated with heart disease status (p < 0.001 in all three tests).
- Cholesterol differs significantly across ST_Slope groups (p = 0.010), though the practical difference between group medians is modest.
- The engineered `RiskFactor_Count` composite score is the single strongest predictor found so far, by both mutual information and Random Forest importance.
- `HR_Reserve` and `MaxHR_Pct` were found to be near-exact mathematical restatements of `Age` and `MaxHR` (confirmed via Variance Inflation Factor) and were removed to avoid redundant signal.

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · SciPy · Scikit-learn · Jupyter Notebook

(No `statsmodels` dependency — Variance Inflation Factor was computed manually via `sklearn.linear_model.LinearRegression` R².)

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook AnalystLab_Week3_Advanced_Analysis.ipynb
```

## Next Step

Week 4: Machine Learning Model Development, Evaluation & Business Recommendations, using `data/heart_final_modelling_dataset.csv` as the modelling input.
