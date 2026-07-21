# Customer Churn Analysis

End-to-end churn analysis project using SQL and Python — from raw relational data to business-ready insights on why customers leave and where revenue is at risk.

## 📌 Overview

This project analyzes customer churn by combining data from three sources: customer demographics, subscription details, and support/complaint history. The goal was to quantify churn, identify its key drivers, and surface high-impact segments the business should prioritize for retention.

## 🗂️ Data Sources

Data was pulled from a SQLite database (`customer_churn.db`) with three tables:

| Table | Description |
|---|---|
| `db_customer` | Customer demographics — country, state, gender, DOB |
| `db_subscription` | Subscription details — plan type, contract type, charges, cancellation info, churn score |
| `db_support` | Support interactions — complaints, escalations, CSAT scores |

## 🛠️ Tools & Libraries

- **Python** — Pandas, NumPy
- **SQL / SQLite** — data extraction and querying
- **Matplotlib, Seaborn** — visualization and correlation analysis
- **Jupyter Notebook**

## 🧹 Data Cleaning & Preparation

- Merged 3 relational tables on `customerid` into a single unified dataset
- Fixed data types (converted date columns to `datetime`)
- Standardized inconsistent categorical values (e.g., "Men"/"Women" → "Male"/"Female")
- Imputed missing `country` values using state-country mapping derived from existing data
- Resolved duplicate records in the support table (customers with multiple complaints) by retaining the latest interaction while preserving total complaint counts
- Engineered a binary `churn_flag` from cancellation data to serve as the core analysis label

## 📊 Key Findings

| Metric | Value |
|---|---|
| **Overall Churn Rate** | 28.57% |
| **Retention Rate** | 71.43% |
| **ARPU (Avg. Revenue per User)** | ₹18.85 |
| **Avg. Customer Tenure** | ~1,498 days |
| **Revenue at Risk (from churned users)** | ₹73.94K |
| **Escalation Rate** | 19.05% |
| **Avg. Complaints per User** | 0.43 |
| **Correlation: Escalations vs. Churn** | 0.77 (strong positive) |

**Churn by Plan Type:**

| Plan Type | Churn Rate | Users | Total Revenue |
|---|---|---|---|
| Basic | 60.00% | 5 | ₹52.95K |
| Standard | 22.22% | 9 | ₹123.91K |
| Premium | 14.29% | 7 | ₹218.93K |

**Insight:** Basic plan subscribers churn at more than 4x the rate of Premium subscribers, making it the highest-priority segment for retention efforts. Support escalations show a strong correlation (0.77) with churn, indicating that unresolved or escalated complaints are a significant churn driver — improving first-contact resolution could meaningfully reduce churn.

## 📈 Visualizations

The notebook includes:
- Monthly churn trend (time series)
- Churn rate by plan type and by state
- Correlation heatmap across churn drivers
- Pairplot and categorical plots for multi-dimensional comparisons

## 🚀 How to Run

1. Clone this repository
   ```bash
   git clone https://github.com/yourusername/customer-churn-analysis.git
   cd customer-churn-analysis
   ```
2. Install dependencies
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
3. Open the notebook
   ```bash
   jupyter notebook Churn_Analysis.ipynb
   ```
   *(Ensure `customer_churn.db` is in the same directory)*

## 📁 Repository Structure

```
customer-churn-analysis/
├── Churn_Analysis.ipynb        # Main analysis notebook
├── customer_churn.db           # SQLite source database
├── exported_churn_data.csv     # Cleaned, merged dataset
└── README.md
```

## 🔮 Potential Next Steps

- Build a predictive churn model (logistic regression / random forest) using `churn_score` and engineered features
- Segment revenue-at-risk by state and subscription type for deeper prioritization
- Set up automated monthly churn tracking / dashboard

---
*Note: This project uses a small sample dataset for demonstration purposes.*
