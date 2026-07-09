# Customer Churn Analysis and Retention Strategy — SQL + Python EDA on Relational Subscription Data

## Executive Summary
This project analyzes customer churn for a subscription-based service by integrating data from three relational tables (customer profiles, subscription details, and support interactions) stored in a SQLite database. Using SQL for extraction and Python (Pandas, Seaborn, Matplotlib) for cleaning, feature engineering, and exploratory analysis, the project identifies which customer segments churn most and quantifies the relationship between support escalations and churn.

**Note on scope:** This project uses a small, structured demonstration dataset (21 customers across 3 relational tables) designed to practice and showcase a full SQL-to-Python analytics workflow — data extraction, cleaning, feature engineering, KPI calculation, and visualization — rather than to produce statistically generalizable business conclusions. All figures below are accurate for this dataset.

**Key outcome:** Escalated support complaints show a strong positive correlation (76.7%) with churn — the clearest actionable signal in the data.

## Business Problem
Subscription businesses lose recurring revenue every time a customer cancels. Understanding *which* customers are likely to churn — by plan, acquisition channel, geography, and support experience — allows a business to prioritize retention efforts where they matter most, rather than treating all customers identically. This project builds the analytical foundation (KPIs, segment-level churn rates, and driver correlations) needed to support that kind of retention prioritization.

## Project Objectives
- Consolidate customer, subscription, and support data from a relational database into a single analysis-ready dataset
- Calculate core churn and retention KPIs
- Quantify churn rate across plan type, geography, and acquisition channel
- Measure the relationship between customer support escalations and churn
- Segment customers into churn-risk tiers
- Visualize churn patterns to support business interpretation

## Dataset Information
- **Source:** SQLite database (`customer_churn_.db`) with 3 tables
- **Tables:** `customer` (21 rows, 8 columns), `subscription` (21 rows, 11 columns), `support` (9 rows, 6 columns)
- **Final merged dataset:** 21 customers × 22 columns
- **Key fields:** plan type (Basic/Standard/Premium), contract type (Monthly/Annual), subscription/acquisition type (Organic/Paid/Referral), monthly charges, CLTV, churn score, cancellation date, escalation flag, CSAT score
- **Target variable:** `churn_flag` (derived from presence of a cancellation date)

## Tech Stack
| Category | Tools |
|----------|-------|
| Language | Python |
| Database | SQLite |
| Libraries | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| IDE | Jupyter Notebook |

## Project Workflow
```
SQLite Database (3 tables)
        ↓
SQL Extraction
        ↓
Data Cleaning & Standardization
        ↓
Table Merging (Customer + Subscription + Support)
        ↓
Feature Engineering (churn_flag, tenure, age, churn_risk)
        ↓
KPI Calculation
        ↓
Exploratory Data Analysis & Visualization
        ↓
Insights & Recommendations
```

## Data Cleaning
- Removed columns with no analytical value: `interests` (mostly null), `pincode` (100% null), `col_1` (100% null)
- Standardized inconsistent categorical labels (`Men`/`Women` → `Male`/`Female`)
- Imputed missing `country` values using a `state → country` lookup
- Converted all date fields (`dob`, `subscription_start_date`, `renewal_date`, `cancellation_date`, `complaint_date`) to proper datetime types
- Identified and resolved duplicate support records per customer, retaining the most recent interaction while preserving total complaint count as a feature
- Merged all three tables into a single customer-level analytical dataset via left joins on `customerid`

## Exploratory Data Analysis
**Questions investigated:**
- What is the overall churn and retention rate?
- Does churn vary by plan type, geography, or acquisition channel?
- Is there a relationship between support escalations and churn?
- How does churn relate to tenure, revenue, and monthly charges?

**Charts created:** monthly churn trend, churn rate by plan type, by state, by subscription/acquisition type, by escalation status, by gender, by contract type, a correlation heatmap across encoded features, a pairplot, and a categorical plot of monthly charges by plan type split by gender and churn-risk tier.

**Patterns observed:**
- Churn is heavily concentrated in the **Basic** plan and among **Referral**-acquired customers
- Several states show 0% churn while others (Karnataka, Meghalaya) show high churn — though with very small per-state sample sizes, so this should be read as directional, not statistically robust
- Escalated support cases are strongly associated with churn

## Key Insights
- **Overall churn rate is 28.57%**, with a retention rate of 71.43%
- **Basic plan customers churn at 60%**, compared to 22.22% for Standard and only 14.29% for Premium — churn risk decreases as plan tier increases
- **Referral-acquired customers churn at 83.33%**, far higher than Paid (16.67%) or Organic (0%) customers — the acquisition channel appears strongly linked to retention quality
- **Support escalations correlate with churn at 76.7%** — the strongest quantified relationship in the dataset
- **Average revenue per user (ARPU) is $18.85/month**, with $73.94 in monthly recurring revenue currently at risk from already-churned customers
- **Escalation rate across all customers is 19.05%**

## Business Recommendations
1. Investigate why Referral-acquired customers churn at a disproportionately high rate (83.33%) — the referral incentive or onboarding experience for this channel may need review
2. Prioritize retention intervention for Basic plan subscribers, who show the highest churn rate (60%) of any plan tier
3. Treat support escalation as an early-warning signal — given the 76.7% correlation with churn, escalated cases should trigger proactive retention outreach
4. Monitor churn by acquisition channel and plan type as ongoing KPIs, since both showed the clearest separation in this analysis

## Project Structure
```
customer-churn-analysis/
├── README.md
├── data/
│   └── customer_churn_.db
├── notebooks/
│   └── churn_analysis.ipynb
├── images/
│   ├── 01_monthly_churn_trend.png
│   ├── 02_churn_by_plan_type.png
│   ├── 03_churn_by_state.png
│   ├── 04_churn_by_subscription_type.png
│   ├── 05_churn_by_escalations.png
│   ├── 06_churn_by_gender.png
│   ├── 07_churn_by_contract_type.png
│   ├── 09_correlation_heatmap_final.png
│   ├── 10_pairplot.png
│   └── 11_catplot_plan_charges_by_risk.png
├── reports/
│   └── exported_churn_data.csv
├── requirements.txt
└── LICENSE
```

## Installation
```bash
pip install pandas numpy matplotlib seaborn
```

## How to Run
1. Clone the repository
2. Place `customer_churn_.db` in the `data/` folder
3. Open `notebooks/churn_analysis.ipynb` in Jupyter
4. Run all cells sequentially — the notebook connects to the SQLite database, cleans and merges the tables, then computes KPIs and generates visualizations

## Results
The analysis identified plan type, acquisition channel, and support escalation history as the clearest churn signals in this dataset, with escalations showing the strongest measured relationship (76.7% correlation). These findings point to concrete, testable retention actions rather than requiring further modeling to be useful.

## Future Improvements
- Replicate the segment-level churn aggregations as native SQL queries (GROUP BY/JOIN) rather than doing all aggregation in Pandas, to more directly demonstrate SQL proficiency
- Incorporate `cltv` (Customer Lifetime Value), which exists in the source data but is not yet analyzed
- Build a cohort/retention curve using `subscription_start_date` and `cancellation_date`
- Fix the complaint-rate calculation to be derived from data rather than hardcoded
- Add a Power BI or Tableau dashboard for stakeholder-facing reporting
- Test the analysis against a larger, real-world dataset to validate whether the observed patterns hold at scale

## Skills Demonstrated
| Skill | Demonstrated |
|--------|--------------|
| SQL (data extraction from relational DB) | ✓ |
| Multi-table joins & data integration | ✓ |
| Data cleaning & standardization | ✓ |
| Feature engineering | ✓ |
| KPI calculation | ✓ |
| Correlation analysis | ✓ |
| Data visualization (Matplotlib/Seaborn) | ✓ |
| Predictive modeling | ✗ (not attempted in this version) |

## Key Visualizations
| Image | Caption | Why it matters |
|---|---|---|
| `02_churn_by_plan_type.png` | Churn rate by plan type | Shows the clearest business signal: churn drops sharply as plan tier rises |
| `04_churn_by_subscription_type.png` | Churn rate by acquisition channel | Highlights the Referral-channel churn problem |
| `05_churn_by_escalations.png` | Churn rate by escalation status | Visualizes the strongest correlation in the dataset |
| `09_correlation_heatmap_final.png` | Correlation heatmap (ordinal-encoded) | Summarizes relationships between plan tier, contract type, churn score, and escalations |
| `01_monthly_churn_trend.png` | Monthly churn trend | Shows when cancellations occurred over time |

## Resume Description
**One-line description:**
Analyzed customer churn across a relational subscription database using SQL and Python, identifying plan type, acquisition channel, and support escalations as the strongest churn signals.

**Resume bullets (ATS-friendly, based only on work shown in the notebook):**
- Integrated customer, subscription, and support data from a SQLite database using SQL, merging three relational tables into a unified dataset for churn analysis
- Engineered churn, tenure, and customer-risk features in Python (Pandas) and calculated core retention KPIs including churn rate, ARPU, and revenue at risk
- Identified a 76.7% correlation between support escalations and customer churn through statistical analysis and correlation heatmaps, informing a proactive retention recommendation

## GitHub Topics
`customer-churn` `churn-analysis` `data-analytics` `sql` `python` `pandas` `eda` `data-cleaning` `data-visualization` `seaborn` `matplotlib` `sqlite` `retention-analysis` `business-analytics` `portfolio-project`

## Repository Naming

**10 options:**
1. customer-churn-sql-python-analysis
2. subscription-churn-analytics
3. churn-analysis-relational-data
4. customer-retention-eda
5. churn-driver-analysis
6. subscription-customer-churn-analysis
7. churn-analytics-sql-pandas
8. customer-churn-kpi-analysis
9. retention-risk-analysis
10. churn-segmentation-analysis

**Best name:** `customer-churn-sql-python-analysis` — immediately communicates the subject and the tech stack, which helps both human recruiters skimming your GitHub and any ATS-adjacent keyword scan.

## Portfolio Rating

| Category | Score /10 | Reasoning |
|---|---|---|
| Technical depth | 5 | Solid multi-table integration, feature engineering, and correlation analysis; no SQL analytical queries, no modeling |
| Business relevance | 6 | Real KPIs and one strong actionable insight (escalation correlation); limited by small dataset |
| Recruiter appeal | 4 | Currently reads as tutorial-following due to formatting/commenting style and lack of narrative |
| GitHub quality | 3 | No README, no markdown documentation, leftover flawed code exists in current notebook |
| Resume value | 5 | Usable bullets exist, but need the README/repo cleanup to back them up credibly |
| ATS friendliness | 6 | Right keywords are present in the underlying work (SQL, Python, EDA, churn); needs surfacing in title/README |

**Overall current state: ~4.5/10** for a public portfolio piece. **With the README, SQL queries, and documentation fixes above: ~7/10** — a credible, honest, entry-level analytics project.

## Final Review — What Still Reads as a Tutorial
- **Numbered code comments** (`#1 churn rate`, `#2 retention rate`...) — this is the single biggest tell. Replace with markdown section headers and your own explanatory text.
- **Zero markdown cells** — a portfolio notebook should read like a report, not a script. Add markdown between sections explaining what you're doing and why.
- **Hardcoded value** (`avg_complain = 0.33`) instead of a real calculation — fix this before publishing; it will look bad if anyone runs the notebook.
- **Leftover duplicate/exploratory code** (the flawed first heatmap, the commented-out `churn_by_plan` line) — clean these out; keep only the final, correct version of each analysis.
- **No written insights anywhere in the notebook itself** — the numbers exist, but nothing interprets them. Add 1–2 sentence takeaways after each KPI/chart.
- **No SQL analytical work shown** — since the data lives in SQLite, add 3–4 real `GROUP BY`/`JOIN` queries that replicate your Pandas aggregations directly in SQL. This is the fastest way to make the project look less like "loaded a table into Pandas" and more like a genuine SQL+Python analyst project.
