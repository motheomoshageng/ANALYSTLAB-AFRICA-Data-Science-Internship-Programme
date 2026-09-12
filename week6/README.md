# HealthConnect Clinic — Model Improvement, Error Analysis & Validation (Data Science Track)

**AnalystLab Africa Experience Lab — Week 6: Integration, Advanced Development & Validation**

## Project Overview

Week 6 does not repeat the Week 5 baseline — it analyzes *where and why* it fails, refines
features based on that specific evidence, develops improved models, and validates whether any
of them are a better candidate to carry into Week 7.

## Repository Structure

```
.
├── README.md
├── HealthConnect_Week6_Model_Improvement.ipynb   # Main notebook (error analysis, refinement, model comparison)
├── Week6_Project_Summary.docx                     # Required concise Week 6 summary
├── data/
│   ├── HealthConnect_Appointment_Data.csv          # Original dataset, untouched
│   └── HealthConnect_Data_Dictionary.csv           # Variable definitions
└── figs/                                           # Saved copies of notebook visualizations (PNG)
```

## What Week 6 Covers

- **Error analysis:** the Week 5 baseline's confusion matrix was broken into False Negatives
  (missed no-shows — the costly error) and False Positives, then validated against segments
  (distance, lead time, prior no-show count) to find *where* errors concentrate.
- **Key finding:** a sharp, previously-unknown accuracy cliff for patients travelling 30-50km
  (38.9% accuracy — worse than chance) — a more specific and actionable finding than Week 5's
  general "distance matters" conclusion.
- **Feature refinement:** two new features, each justified by a specific error-analysis
  finding — `no_show_history_level` (binned, addressing tiny sample sizes at high
  `previous_no_shows` values) and `lead_distance_interaction` (addressing the distance cliff).
- **Improved models:** a hyperparameter-tuned Random Forest (via `RandomizedSearchCV` with
  `GroupKFold`) and a Gradient Boosting Classifier, both trained on the refined feature set.
- **Fairness check:** model recall was compared across gender groups, per the fairness concern
  flagged as remaining work in Week 5.

## Results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Week 5: Logistic Regression | 0.630 | 0.624 | 0.656 | 0.640 | 0.678 |
| Week 5: Random Forest (baseline) | 0.634 | 0.629 | 0.650 | 0.640 | 0.677 |
| **Week 6: Random Forest (tuned + refined)** | **0.639** | 0.629 | **0.677** | **0.652** | **0.680** |
| Week 6: Gradient Boosting (refined) | 0.638 | 0.634 | 0.652 | 0.643 | 0.678 |

**Candidate model: Week 6 tuned Random Forest.** It improved recall — the metric that matters
most, since a missed no-show is the costlier error for HealthConnect — from 0.650-0.656 to
0.677, a genuine if modest gain. Gradient Boosting did not outperform it, suggesting the
current feature set's ceiling is closer to "better-tuned tree ensemble" than "different
algorithm entirely."

## Cross-Track Integration

Data-Analytics-style segment validation (documented transparently as self-performed, given no
live Data Analytics counterpart for this individual submission) directly shaped which features
were refined — a concrete change to the modelling approach, not just a shared observation. Full
documentation is in the notebook's Cross-Track Integration section.

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Jupyter Notebook

## Next Step

Week 7: re-run the fairness check with a larger sample, stress-test the candidate model on
edge cases, test probability calibration, confirm the `waiting_time_minutes` question with
stakeholders, and coordinate an end-to-end test with the ML Engineering track's pipeline.
