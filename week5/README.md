# HealthConnect Clinic — Baseline No-Show Prediction Model (Data Science Track)

**AnalystLab Africa Experience Lab — Week 5: Data Preparation, Feature Engineering & Baseline Model**

## Project Overview

Week 5 moves the HealthConnect Data Science track from problem definition (Week 4) into
practical implementation: preparing the appointment data for modelling, engineering new
features, defining a train/test strategy, and training/evaluating the first baseline
classification model for predicting patient no-shows.

## Repository Structure

```
.
├── README.md
├── HealthConnect_Week5_Baseline_Model.ipynb   # Main notebook (data prep, EDA, features, model, evaluation)
├── Week5_Project_Summary.docx                  # Required concise Week 5 summary
├── data/
│   ├── HealthConnect_Appointment_Data.csv       # Original dataset, untouched
│   └── HealthConnect_Data_Dictionary.csv        # Variable definitions
└── figs/                                        # Saved copies of all 9 notebook visualizations (PNG)
```

## What Week 5 Covers

- **Week 4 review & re-verification:** the Cancelled-exclusion decision was re-checked with
  fresh evidence rather than simply repeated; the previously open `waiting_time_minutes`
  leakage question was resolved (excluded from the baseline model).
- **Data preparation:** missing value handling, categorical encoding (label/ordinal/one-hot as
  appropriate to each field), and removal of leakage/irrelevant fields.
- **Data exploration with visual evidence:** 9 visualizations, each tied to a specific
  preprocessing, feature-engineering, or modelling decision.
- **Feature engineering:** three new features — `no_show_rate`, `long_lead_time`,
  `is_first_visit` — each justified by evidence from the EDA.
- **Train/test strategy:** `GroupShuffleSplit` grouped on `patient_id`, to prevent the same
  patient's appointments appearing in both training and test sets.
- **Baseline models:** Logistic Regression (primary, interpretable baseline) and Random Forest
  (comparison), evaluated on accuracy, precision, recall, F1, confusion matrix, and ROC-AUC.

## Results

| Metric | Logistic Regression | Random Forest |
|---|---|---|
| Accuracy | 63.0% | 63.4% |
| Precision | 0.624 | 0.629 |
| Recall | 0.656 | 0.650 |
| F1-score | 0.640 | 0.640 |
| ROC-AUC | 0.678 | 0.677 |

Majority-class baseline: 50.0% accuracy — both models clear it meaningfully. `booking_lead_days`
and `distance_to_clinic_km` are the strongest predictors, confirming Week 4's initial
assessment. The engineered `no_show_rate` outranks the raw `previous_no_shows` count it was
derived from in feature importance, validating that engineering decision with evidence.

## Key Decisions

| Decision | Reasoning |
|---|---|
| Cancelled excluded from target | Re-verified with data: Cancelled patients' `previous_no_shows` behavior (0.418) resembles Attended (0.457) far more than No-Show (0.641) |
| Positive class (1) = No-Show | The clinic needs advance warning of who's at risk of missing an appointment, not confirmation of expected attendance |
| `waiting_time_minutes` excluded | Unresolved leakage risk — has values even for No-Show records; excluded conservatively pending stakeholder confirmation |
| Train/test split grouped by `patient_id` | Patients average ~3 appointments each; a random split would leak the same patient across both sets |

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Jupyter Notebook

## Cross-Track Collaboration

This week's feature-level findings are directly reusable by the Data Analytics track as
candidate KPI definitions or EDA talking points, since both tracks are analyzing the same
underlying appointment behavior from different angles.

## Next Step

Week 6: fairness/error-rate evaluation across `gender` and `age_group`, hyperparameter tuning,
and a business-defined trade-off between false negatives and false positives to guide model
selection.
