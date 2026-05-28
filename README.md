# Part 1 — Data Audit, EDA & Business Understanding

> **Project:** D2C Customer Churn Intelligence & Retention API  
> **Snapshot Date:** 2025-09-30 | **Target:** Churn in next 60 days

---

## Overview

This module performs a full data audit and exploratory analysis of a D2C personal-care brand's customer dataset, covering 2,400 customers across 7 data files. The goal is to understand churn patterns, identify data quality issues, and surface evidence-backed hypotheses before any model is built.

**Key Findings:**
- Overall 60-day churn rate: **47.0%** (1,127 of 2,400 customers)
- Customers with zero web sessions churn at **66.3%** vs 45.3% for active users
- Customers with 3+ support tickets show elevated churn vs. baseline
- Loyalty programme non-enrollment strongly correlates with churn risk
- 1,872 post-snapshot orders identified and flagged (must NOT be used as features)

---

## Folder Structure

```
part1_eda/
├── eda_audit.ipynb              # Main EDA script (runs all analysis)
├── outputs/
│   ├── data_quality_report.md   # Detailed data quality findings
│   └── business_memo.md         # Executive memo for stakeholders
├── charts/
│   ├── chart01_churn_distribution.png
│   ├── chart02_churn_by_demographics.png
│   ├── chart03_rfm_vs_churn.png
│   ├── chart04_support_vs_churn.png
│   ├── chart05_web_activity_vs_churn.png
│   ├── chart06_order_behavior.png
│   ├── chart07_hypotheses_evidence.png
│   └── chart08_campaigns_interventions.png
├── README.md
└── requirements.txt
```

---

## Setup & Run

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Place dataset CSVs in ../data/ (or update DATA_DIR in eda_audit.py)

# 3. Run the analysis
python eda_audit.py
```

All outputs (charts + markdown reports) are generated automatically.

---

## Dataset Used

| File | Rows | Purpose |
|------|------|---------|
| customers.csv | 2,400 | Customer profiles |
| orders.csv | 10,009 | Transaction history (pre + post snapshot) |
| support_tickets.csv | 1,921 | Support interactions |
| web_events_snapshot.csv | 2,400 | 30-day web/app activity |
| churn_labels.csv | 2,400 | Target variable + train/val/test split |
| rfm_modeling_snapshot.csv | 2,400 | Pre-engineered feature table |
| intervention_history.csv | 2,400 | Campaign history |

---

## Key Churn-Risk Hypotheses

| # | Hypothesis | Evidence |
|---|-----------|----------|
| H1 | Customers with 3+ support tickets have higher churn | Validated in chart04 |
| H2 | Web-inactive customers (0 sessions/30d) churn at 66.3% | Validated in chart05 |
| H3 | No loyalty enrolment → higher churn | ~3pp gap vs enrolled |
| H4 | High negative ticket sentiment → elevated churn | Validated in chart04 |
| H5 | Heavy discount users churn more | 51% vs 46.5% for low-discount users |

---

## Tech Stack

Python 3.11+ | pandas | numpy | matplotlib | seaborn

---

## Business Impact

Before this analysis, the brand had no systematic view of which customers were at risk or why. This module surfaces five actionable hypotheses that directly inform the retention strategy in Part 2.
