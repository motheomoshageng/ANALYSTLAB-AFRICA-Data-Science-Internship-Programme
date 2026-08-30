# HealthConnect Clinic — No-Show Prediction (Data Science Track)

**AnalystLab Africa Experience Lab — Week 4: Problem Understanding**

## Project Overview

HealthConnect Clinic wants to use data and AI to reduce missed appointments and improve the
patient support experience. This is the Data Science track's Week 4 contribution: defining the
machine learning problem precisely and assessing whether the provided appointment data can
actually support a no-show prediction solution — before any model is built.

## Repository Structure

```
.
├── README.md
├── HealthConnect_Week4_ML_Problem_Definition.ipynb   # Main notebook (data assessment, problem definition, executed with outputs)
├── Week4_Project_Summary.docx                          # Required concise Week 4 summary
├── data/
│   ├── HealthConnect_Appointment_Data.csv               # Original dataset (5,000 records, untouched)
│   └── HealthConnect_Data_Dictionary.csv                # Variable definitions
└── figs/                                                # Saved copies of notebook visualizations (PNG)
```

## What Week 4 Covers

- **Problem type:** Binary classification — predict `is_no_show` (No-Show vs. Attended) using
  information available at or before the time an appointment is booked.
- **Target variable definition:** `Cancelled` appointments (5.3% of data) are explicitly excluded
  from the primary model — a cancellation is a known-in-advance, patient-initiated action, not
  the silent missed-appointment problem the business scenario describes.
- **Data quality assessment:** confirmed `reminder_channel` missingness is structurally expected
  (not a gap), found `previous_appointments`/`previous_no_shows` do **not** behave as genuine
  chronological running totals (42.3% of consecutive same-patient pairs decrease), and flagged
  `waiting_time_minutes` as a potential leakage risk pending stakeholder confirmation.
- **Feature assessment:** `previous_no_shows`, `booking_lead_days`, and `distance_to_clinic_km`
  all show strong, monotonic relationships with no-show rate; several categorical features
  (reminder channel, age group, appointment type/day/time, gender) show weak signal but are
  retained as candidates.
- **Initial modelling approach:** patient-grouped train/test split (to avoid the same patient
  appearing in both sets — patients average ~3 appointments each), Logistic Regression as an
  interpretable baseline vs. a tree-based ensemble, evaluated on recall/precision/ROC-AUC rather
  than raw accuracy.

## Key Findings

| Finding | Why It Matters |
|---|---|
| `previous_no_shows`, `booking_lead_days`, `distance_to_clinic_km` are strong predictors | Clear, monotonic relationships with no-show rate found directly in the raw data, before any modelling |
| `previous_appointments`/`previous_no_shows` are not true running totals | Confirmed empirically; must be treated as synthetic proxies, not real patient history, for this exercise |
| `waiting_time_minutes` has an unresolved leakage risk | Present even for No-Show/Cancelled records; excluded from the v1 feature set pending confirmation |
| Patients repeat ~3x on average in the dataset | Requires a patient-grouped train/test split, not a naive random split |

## Tools

Python · Pandas · NumPy · Matplotlib · Seaborn · Jupyter Notebook

## Next Step

Week 5 (Analysis & Solution Design): resolve the `waiting_time_minutes` question, decide the
imputation approach for small-missingness fields, run fuller statistical validation of candidate
features, and build the first baseline models.
