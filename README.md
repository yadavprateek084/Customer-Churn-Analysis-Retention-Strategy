# 📊 Customer Churn Analysis & Retention Strategy

### End-to-End SQL + Python Exploratory Data Analysis on Relational Subscription Data

<p align="center">

![Python](https://img.shields.io/badge/Python-3.11-blue?style=for-the-badge)
![SQL](https://img.shields.io/badge/SQLite-Database-green?style=for-the-badge)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-black?style=for-the-badge)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-blue?style=for-the-badge)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange?style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-EDA-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-success?style=for-the-badge)

</p>

<p align="center">
<img src="images/05_churn_by_escalations.png" width="850">
</p>

---

# 🚀 Overview

Customer churn directly impacts recurring revenue for subscription businesses. Identifying customers at risk of cancellation enables organizations to proactively improve customer experience and maximize retention.


This project demonstrates an **end-to-end Data Analytics workflow**, beginning with extracting data from a **relational SQLite database** using **SQL**, followed by **data cleaning, feature engineering, KPI analysis, exploratory data analysis (EDA), and business recommendations** using Python.

The project integrates customer profiles, subscription information, and customer support interactions to identify the major factors associated with churn.

> **Dataset Scope:**
> This project uses a structured demonstration dataset containing **21 customers across 3 relational tables**. The objective is to showcase practical SQL and Python analytics skills rather than produce statistically generalizable business conclusions.

---

# ✨ Project Highlights

* ✅ Extracted data from a relational SQLite database
* ✅ Joined **3 normalized tables** into a unified analytical dataset
* ✅ Cleaned and standardized messy business data
* ✅ Engineered customer-level analytical features
* ✅ Calculated key subscription business KPIs
* ✅ Built **10+ visualizations** using Matplotlib & Seaborn
* ✅ Identified customer segments with the highest churn risk
* ✅ Quantified the relationship between support escalations and churn
* ✅ Delivered actionable business recommendations

---

# 💼 Business Problem

Subscription-based businesses lose recurring revenue every time a customer cancels their subscription.

Instead of treating every customer equally, businesses need to identify:

* Which customers are most likely to churn
* Which customer segments generate the highest retention risk
* Which operational factors contribute most to customer loss

This analysis helps prioritize retention strategies by uncovering patterns across customer demographics, subscription plans, acquisition channels, and customer support interactions.

---

# 🎯 Project Objectives

* Extract data from multiple SQL tables
* Merge relational datasets into a customer-level analytical dataset
* Clean and standardize raw business data
* Engineer features for churn analysis
* Calculate business KPIs
* Analyze churn across customer segments
* Measure the relationship between customer support escalations and churn
* Visualize customer behavior
* Generate business recommendations

---

# 🛠️ Tech Stack

| Category      | Tools               |
| ------------- | ------------------- |
| Programming   | Python              |
| Database      | SQLite              |
| SQL           | SQLite Queries      |
| Libraries     | Pandas, NumPy       |
| Visualization | Matplotlib, Seaborn |
| IDE           | Jupyter Notebook    |

---

# 🗄 Database Schema

The project uses a relational SQLite database containing three normalized tables.

```
customer
│
├── Customer Information
│
subscription
│
├── Subscription Details
│
support
│
└── Customer Support Records
```

After SQL extraction and joins:

```
21 Customers
        │
        ▼
Merged Dataset

21 Rows × 22 Columns
```

---

# 🔄 Project Workflow

```
             SQLite Database
                    │
     ┌──────────────┼──────────────┐
     │              │              │
 Customer      Subscription     Support
     │              │              │
     └──────────────┼──────────────┘
                    │
            SQL Data Extraction
                    │
            Data Cleaning
                    │
        Feature Engineering
                    │
          Dataset Integration
                    │
          KPI Calculation
                    │
 Exploratory Data Analysis (EDA)
                    │
      Business Insights
                    │
 Business Recommendations
```

---

# 🗄 SQL Work

SQL was used to extract and prepare data from the relational database before analysis in Python.

### SQL Concepts Demonstrated

* SELECT
* WHERE
* LEFT JOIN
* ORDER BY
* Aggregate Functions
* Relational Database Querying

SQL Responsibilities:

* Extract customer records
* Retrieve subscription information
* Join multiple relational tables
* Validate merged records
* Prepare data for downstream analysis

---

# 🧹 Data Cleaning & Preparation

The dataset underwent several preprocessing steps before analysis.

### Cleaning Steps

* Removed columns containing little or no analytical value

  * `interests`
  * `pincode`
  * `col_1`

* Standardized inconsistent categorical values

```
Men → Male
Women → Female
```

* Converted date columns into datetime format

* Imputed missing country values using state-country mapping

* Removed duplicate support records while preserving complaint counts

* Merged all tables using customer IDs

---

# ⚙️ Feature Engineering

New analytical features created during preprocessing:

* `churn_flag`
* `customer_age`
* `subscription_tenure`
* `churn_risk`
* `complaint_count`
* `escalation_flag`

These engineered features enabled KPI calculations and segmentation analysis.

---

# 📈 Business KPIs

| KPI                             |      Value |
| ------------------------------- | ---------: |
| Customers                       |         21 |
| Database Tables                 |          3 |
| Final Dataset                   |    21 × 22 |
| Overall Churn Rate              | **28.57%** |
| Retention Rate                  | **71.43%** |
| Average Revenue Per User (ARPU) | **$18.85** |
| Monthly Revenue at Risk         | **$73.94** |
| Escalation Rate                 | **19.05%** |
| Escalation–Churn Correlation    |  **76.7%** |

---

# 📊 Exploratory Data Analysis

The following business questions were investigated:

* What is the overall churn rate?
* Which subscription plan experiences the highest churn?
* Does geography influence churn?
* Does acquisition channel affect retention?
* How do support escalations relate to churn?
* How do revenue and tenure vary across customer segments?


---

# 🔍 Key Insights

### 📌 Overall Customer Churn

* Overall churn rate: **28.57%**
* Retention rate: **71.43%**

---

### 📌 Plan Type

Basic Plan

* 60% churn

Standard Plan

* 22.22% churn

Premium Plan

* 14.29% churn

Higher-tier plans demonstrate significantly better customer retention.

---

### 📌 Acquisition Channel

Referral

* **83.33% churn**

Paid

* **16.67% churn**

Organic

* **0% churn**

Referral-acquired customers exhibit the highest churn risk.

---

### 📌 Customer Support

Support escalations demonstrate a **76.7% positive correlation** with churn, making escalation history the strongest churn indicator identified in this dataset.

---

### 📌 Revenue Metrics

* Average monthly revenue per customer: **$18.85**
* Monthly recurring revenue currently at risk: **$73.94**

---

# 💡 Business Recommendations

Based on the analysis:

### 1. Improve Basic Plan Retention

Basic subscribers show the highest churn rate and should be prioritized for retention campaigns.

---

### 2. Review Referral Program Quality

Investigate onboarding and incentive structures for referral customers, who churn at significantly higher rates.

---

### 3. Monitor Support Escalations

Escalated complaints should trigger proactive customer outreach, as they strongly correlate with churn.

---

### 4. Track Retention KPIs

Continuously monitor:

* Churn Rate
* Retention Rate
* Escalation Rate
* Revenue at Risk
* Acquisition Channel Performance



---

# 📚 Skills Demonstrated

* SQL Database Querying
* Relational Database Analysis
* Multi-table SQL Joins
* Data Cleaning
* Data Wrangling
* Feature Engineering
* Exploratory Data Analysis
* Business KPI Reporting
* Correlation Analysis
* Customer Analytics
* Data Visualization
* Business Storytelling

---

