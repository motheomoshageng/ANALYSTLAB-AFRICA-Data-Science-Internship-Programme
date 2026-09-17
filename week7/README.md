# HealthConnect Clinic — Model Testing, Refinement & Validation (Data Science Track)

**AnalystLab Africa Experience Lab — Week 7: Testing, Refinement & End-to-End Validation**

## Project Overview

Week 7 systematically tests the Week 6 candidate model rather than repeating its comparison:
is the improvement real or a single-split artifact, did the targeted fix for a known blind
spot actually work, and is the model suitable for HealthConnect's use case once tested under
more rigorous conditions (cross-validation, edge cases, calibration, fairness at scale)?

## Repository Structure

```
.
├── README.md
├── HealthConnect_Week7_Testing_Validation.ipynb   # Main notebook (all tests, executed with outputs)
├── Week7_Project_Summary.docx                      # Required concise Week 7 summary
├── data/
│   ├── HealthConnect_Appointment_Data.csv           # Original dataset, untouched
│   └── HealthConnect_Data_Dictionary.csv            # Variable definitions
└── figs/                                            # Calibration curve visualization
```

## What Week 7 Tested — and Found

| Test | Result |
|---|---|
| Is the Week 6 recall improvement real? (5-fold grouped CV) | Yes, but smaller than the single-split suggested: +0.010 average (0.649→0.659), consistent across all 5 folds |
| Did the 30-50km distance fix actually work? (direct retest) | Partial fix: 38.9% → 44.4% accuracy — real improvement, but still below chance-level performance |
| Overfitting check | No meaningful overfitting (train/test gap = 0.031) |
| Edge case: first-time patients | Model systematically underpredicts their no-show risk (43.2% predicted vs. 52.3% actual) |
| Calibration (Brier score) | No meaningful improvement over baseline (0.225 vs. 0.226) |
| Fairness re-check at full scale (out-of-fold predictions, n=4,737) | **New finding:** 65+ patients (largest age group, ~24.6% of data) have the lowest recall of any segment (0.604) |

## Key Decisions

- **No further feature engineering applied to the distance segment** — the model isn't
  overfitting, so the remaining gap is treated as a data-volume limitation requiring more
  training data in that band, not a feature-design problem to keep patching.
- **The age-fairness finding is escalated, not silently fixed** — correcting it (e.g. per-group
  thresholds) trades off overall performance against equity across a real decision that needs
  stakeholder input, not a unilateral technical fix.
- **Model positioned as a risk-ranking tool, not a probability source** — since calibration
  didn't meaningfully improve, relative ranking is more trustworthy than a quoted percentage.

## Cross-Track Testing

The Week 6 `lead_distance_interaction` feature — built from a Data-Analytics-style segment
finding — was directly retested against the exact problem it was built to solve, closing the
Test → Finding → Action → Retest loop the Week 7 brief requires. Full documentation is in the
notebook's Cross-Track Testing section.

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Jupyter Notebook

## Next Step

Week 8: escalate the 65+ fairness finding to Project Management, confirm pipeline
compatibility with ML Engineering, and finalize the model's presentation with its tested
strengths and limitations both clearly documented.
