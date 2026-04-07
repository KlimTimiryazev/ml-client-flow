# Customer Churn Prediction

> Course project for the **"Machine Learning"** discipline  
> Financial University under the Government of the Russian Federation  
> Topic: *Machine Learning for Customer Churn Prediction*

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Repository Structure](#repository-structure)
- [EDA — Key Findings](#eda--key-findings)
- [Work Plan](#work-plan)
- [Tech Stack](#tech-stack)

---

## Problem Statement

Binary classification: predict whether a customer will churn (churn = Yes/No) based on behavioral and payment features of their subscription.

Real-world application — early identification of high-risk customers to enable proactive retention.

---

## Dataset

`customer_subscription_churn_usage_patterns.csv` — 1000 records of subscription service customers.

| Feature | Type | Description |
|---|---|---|
| `user_id` | int | Identifier (dropped before training) |
| `signup_date` | date | Registration date |
| `plan_type` | categorical | Subscription plan: Basic / Premium |
| `monthly_fee` | float | Monthly payment (199 / 699 RUB) |
| `avg_weekly_usage_hours` | float | Average weekly usage time |
| `support_tickets` | int | Number of support requests |
| `payment_failures` | int | Number of failed payments (0–5) |
| `tenure_months` | int | Subscription duration in months |
| `last_login_days_ago` | int | Days since last login |
| `churn` | Yes / No | **Target variable** |

**Class balance:** ~57% No / ~43% Yes — no additional balancing required.

---

## Repository Structure

```
.
└── курсовая работа по ML/
    ├── отток клиентов.ipynb              # Main notebook
    ├── customer_subscription_churn_usage_patterns.csv
    └── ML_course_readmes/                # Course reference materials
```

---

## EDA — Key Findings

### Multicollinearity
`plan_type` and `monthly_fee` are perfectly collinear (Basic = 199 RUB, Premium = 699 RUB).  
**Decision:** drop `plan_type` before training — keep only `monthly_fee`.

### Most Informative Features (by correlation with churn)
| Feature | Observation |
|---|---|
| `last_login_days_ago` | Churned customers hadn't logged in for a long time — strong behavioral signal |
| `support_tickets` | High number of support requests correlates with churn |
| `payment_failures` | Payment issues are a clear predictor |

### Distributions
All numerical features are uniformly distributed; no anomalous values detected.

### Multicollinearity among remaining features
Absent (confirmed by correlation heatmap).

---

## Work Plan

- [x] Load and inspect data (`df.info`, `df.head`, `df.describe`)
- [x] EDA: distributions, correlations, boxplots vs target variable
- [ ] Preprocessing: drop `user_id`, `plan_type`; encode `churn`; extract features from `signup_date`; normalization
- [ ] Train baseline models (≥7 algorithms) with training time measurement
- [ ] Compare models by metrics (Accuracy, F1, ROC-AUC, training time)
- [ ] Hyperparameter tuning (GridSearchCV) for the best model
- [ ] Improvements: regularization, feature selection, ensembling
- [ ] Cross-validation (k-fold) for final performance evaluation

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-F7931E?logo=scikit-learn&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
