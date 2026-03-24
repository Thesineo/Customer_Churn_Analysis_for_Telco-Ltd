# Customer Churn Analysis
### End-to-end data science project — Python · SQL · Machine Learning · Power BI

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat-square&logo=python)
![SQL](https://img.shields.io/badge/SQL-SQLite-003B57?style=flat-square&logo=sqlite)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Model-red?style=flat-square)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=flat-square&logo=powerbi)
![Status](https://img.shields.io/badge/Status-In%20Progress-green?style=flat-square)

---

## Overview

This project builds a complete customer churn prediction pipeline for a telecom company using the IBM Telco Customer Churn dataset (7,043 customers, 21 features). The goal is to identify which customers are at risk of leaving and understand the key drivers behind churn — delivering actionable insights through machine learning and an interactive Power BI dashboard.

This mirrors a real-world data analyst/scientist workflow: raw data → cleaning → SQL analysis → ML modelling → business dashboard.

---

## Business Problem

Telecom companies lose millions annually to customer churn. Acquiring a new customer costs 5–7× more than retaining an existing one. By predicting which customers are likely to churn before they leave, the business can intervene with targeted retention offers — saving revenue and improving customer lifetime value.

**Key questions this project answers:**
- What is the overall churn rate and which segments are most at risk?
- Which factors most strongly predict churn?
- Which specific customers should the retention team contact first?

---

## Project Structure

```
customer-churn-analysis/
├── data/                        # Raw and processed data (not tracked by git)
│   ├── churn_cleaned.csv
│   ├── churn_summary.csv
│   └── churn_predictions.csv
├── notebooks/
│   ├── 01_eda.ipynb             # Exploratory data analysis
│   ├── 02_sql.ipynb             # SQL analysis with SQLite
│   └── 03_model_comparison.ipynb  # ML model training & comparison
├── sql/
│   └── queries.sql              # All SQL queries documented
├── .gitignore
└── README.md
```

---

## Dataset

**IBM Telco Customer Churn** — publicly available via Kaggle

- 7,043 customer records
- 21 features including contract type, tenure, monthly charges, internet service and support options
- Target variable: `Churn` (Yes / No)
- Churn rate: **26.5%**

[Download from Kaggle →](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data cleaning & EDA | Python, pandas, matplotlib, seaborn |
| Data storage & querying | SQLite, SQL (window functions, views, CASE WHEN) |
| Machine learning | scikit-learn, XGBoost, LightGBM |
| Explainability | Feature importance, correlation analysis |
| Visualisation | Power BI (slicers, KPI cards, drill-through) |
| Version control | Git, GitHub |

---

## Project Phases

### Phase 1 — Exploratory Data Analysis
- Loaded and inspected 7,043 rows across 21 columns
- Fixed data quality issue: `TotalCharges` stored as object instead of numeric
- Analysed churn distribution, numerical feature distributions and categorical breakdowns
- Identified class imbalance: 73% retained vs 27% churned

**Key findings:**
- Churned customers average **18 months** tenure vs **38 months** for retained customers
- Churned customers pay **~$15/month more** on average
- Customers without **TechSupport** churn significantly more

### Phase 2 — SQL Analysis
- Loaded cleaned data into a SQLite database using Python
- Wrote analytical queries using `CASE WHEN`, `GROUP BY`, `ROUND` and window functions
- Created reusable summary views for Power BI consumption

**Queries written:**
- Overall churn rate calculation
- Churn rate by contract type, internet service and tenure bucket
- `RANK() OVER (PARTITION BY ...)` to rank customers by monthly charges within contract groups
- High-risk customer segment identification
- Aggregated summary view for dashboard use

**Top SQL finding:** Month-to-month contract customers churn at **43%** vs only **3%** for two-year contracts.

### Phase 3 — Machine Learning Model Comparison
Three models trained and compared head-to-head:

| Model | Accuracy | AUC Score | F1 (Churn) |
|---|---|---|---|
| Logistic Regression | ~81% | ~0.84 | ~0.60 |
| Random Forest | ~85% | ~0.88 | ~0.65 |
| **XGBoost** | **~87%** | **~0.91** | **~0.69** |

**Best model: XGBoost**

Top churn drivers identified:
1. Contract type (month-to-month)
2. Tenure (short tenure = higher risk)
3. Monthly charges (higher charges = higher risk)
4. Internet service type (Fiber optic)
5. Absence of TechSupport

Every customer was scored with a churn probability and assigned to a risk segment: **Low / Medium / High risk** — exported for Power BI.

### Phase 4 — Power BI Dashboard *(in progress)*
- KPI cards: total churn rate, high-risk customer count, average monthly charges
- Churn breakdown by contract type, tenure group and internet service
- Customer risk segment distribution
- Slicers: filter by contract type, risk segment and internet service

---

## How to Run This Project

**1. Clone the repository**
```bash
git clone https://github.com/Thesineo/customer-churn-analysis.git
cd customer-churn-analysis
```

**2. Create a virtual environment**
```bash
python3 -m venv venv
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm jupyter ipykernel
```

**4. Download the dataset**

Download from [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) and place `WA_Fn-UseC_-Telco-Customer-Churn.csv` in the `data/` folder.

**5. Run notebooks in order**
```
01_eda.ipynb → 02_sql.ipynb → 03_model_comparison.ipynb
```

---

## Results Summary

> By applying XGBoost with SHAP-informed feature selection, the model identifies **high-risk customers with 87% accuracy and an AUC of 0.91**. The top retention strategy recommendation: target month-to-month customers in their first 12 months with tenure-based loyalty incentives and tech support upgrades — this segment represents 43% churn risk and the highest revenue loss exposure.

---

## What I Learned

- End-to-end data pipeline design from raw CSV to deployed model
- Real-world SQL skills: window functions, CTEs, views and analytical aggregations
- Handling class imbalance in ML with `class_weight` and threshold tuning
- Model comparison methodology: why AUC and F1 matter more than accuracy for imbalanced data
- Translating ML outputs into business recommendations, not just metrics

---

## Project Status

- [x] Phase 1 — EDA with Python & pandas
- [x] Phase 2 — SQL analysis with SQLite
- [x] Phase 3 — Model comparison (Logistic Regression, Random Forest, XGBoost)
- [ ] Phase 4 — Power BI dashboard (in progress)

---

## Connect

Built by **Aniket Nerali**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin)](https://linkedin.com/in/yourprofile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat-square&logo=github)](https://github.com/Thesineo)
