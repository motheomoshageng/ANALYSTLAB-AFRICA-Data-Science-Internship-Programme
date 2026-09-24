# HealthConnect Clinic — No-Show Prediction (Data Science Track)

**AnalystLab Africa Experience Lab — Final Project Portfolio (Weeks 4-8)**

## Project Overview

HealthConnect Clinic, a fictional healthcare provider, wanted to know whether data could help
predict which patients are likely to miss appointments, so staff could intervene proactively.
This repository documents the full Data Science track journey — from problem definition through
a tested, honestly-limited final model — across an 8-week structured internship program.

## The Journey

| Week | Stage | What Happened |
|---|---|---|
| **Week 4** | Problem Definition | Defined the ML problem as binary classification; decided to exclude `Cancelled` appointments from the target (a cancellation is known in advance, unlike a silent no-show); flagged `waiting_time_minutes` as a possible leakage risk |
| **Week 5** | Baseline Model | Built Logistic Regression and Random Forest baselines (~63% accuracy); implemented a **patient-grouped** train/test split, since patients appear ~3x each in the data |
| **Week 6** | Error Analysis & Improvement | Found a severe accuracy cliff (38.9%) for patients travelling 30-50km; engineered a targeted `lead_distance_interaction` feature; tuned a Random Forest that improved recall to 0.677 on a single test split |
| **Week 7** | Rigorous Testing | Re-tested Week 6's claims under cross-validation — found the real improvement was smaller (+0.010 recall) but consistent across all folds; **discovered a previously-unknown fairness gap**: patients 65+ (24.6% of all data) have the lowest recall of any segment |
| **Week 8** | Final Integration | Consolidated the full evidence trail into a final, documented model with explicit strengths, weaknesses, and scope of safe use |

## Repository Structure

```
.
├── README.md
├── HealthConnect_Week8_Final_Model_Documentation.ipynb   # Final capstone notebook
├── Week8_Video_Script.docx                                 # Script/talking points for the required individual video
├── data/
│   ├── HealthConnect_Appointment_Data.csv                   # Original dataset, untouched
│   └── HealthConnect_Data_Dictionary.csv                    # Variable definitions
└── figs/                                                    # Final ROC curve and feature importance charts
```

*(Weekly notebooks and reports for Weeks 4-7 are available in their respective submission
archives — this repository's Week 8 notebook consolidates and reproduces their key findings.)*

## Final Model

A tuned Random Forest classifier predicting `is_no_show`, trained on 13 features including two
engineered specifically in response to error analysis: `no_show_history_level` (binned prior
no-show history) and `lead_distance_interaction` (booking lead time × distance to clinic).

**Cross-validated performance:**

| Model | Accuracy | Recall | ROC-AUC |
|---|---|---|---|
| Week 5 Baseline (Random Forest) | 0.626 | 0.649 | 0.677 |
| **Final Candidate** | **0.631** | **0.659** | **0.679** |

## What This Model Can and Cannot Do

**Can:** rank patients by relative no-show risk, to help staff prioritize reminders or outreach.

**Cannot:** make automated decisions without human review; provide precise risk percentages
(calibration doesn't support that level of trust); be safely deployed for the clinic's 65+
patient population without first addressing the documented fairness gap.

## Key Findings Worth Knowing

- **`booking_lead_days`, `distance_to_clinic_km`, and prior no-show history** are the most
  consistent predictors across every week of testing — clinically sensible, not a fragile
  artifact of one dataset split.
- **The engineered `lead_distance_interaction` feature is the model's 2nd most important
  feature overall**, validating that Week 6's targeted engineering decision was well-founded.
- **The most significant finding of the entire project** wasn't a modelling result — it was a
  fairness gap discovered by insisting on a larger-sample fairness check in Week 7, affecting
  the clinic's single largest patient age group.

## Limitations (Full List)

| Limitation | Status |
|---|---|
| `waiting_time_minutes` leakage risk | Unresolved — excluded throughout |
| `previous_appointments`/`previous_no_shows` not true running totals | Data-generation issue, mitigated via binning |
| 30-50km distance blind spot | Partially mitigated (38.9%→44.4%), not fully resolved |
| First-time patient risk underprediction | Unresolved |
| Calibration not meaningfully improved | Unresolved — mitigated by ranking-only recommended use |
| **Age-fairness gap (65+ patients)** | **Unresolved, escalated to stakeholders** |
| Fully synthetic dataset | Applies to every finding in this project |

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Jupyter Notebook

## Cross-Track Collaboration

Throughout Weeks 6-8, this track exchanged findings with a Data-Analytics-style segment
validation role — documented transparently as self-performed within an individual track
submission where no live counterpart was available, rather than presented as a team exchange
that didn't occur.
