# Data Quality Report — D2C Churn Intelligence Project

> **Snapshot Date:** 2025-09-30 | **Generated:** Auto  
> **Author:** Capstone Submission, Part 1

---

## Executive Summary

The dataset covers **2,400 customers** across 7 files totalling ~26,600 rows.
Several intentional and real quality issues were identified. Key concerns include:
- Duplicate-like order records (`_DUP` suffix) requiring deduplication
- Missing loyalty tier (~58%) and skin type (~17%) in customers
- ~80 orders with null ratings
- Outlier order values up to ₹24,789
- **1,872 post-snapshot orders** that MUST NOT be used as model features

---

## 1. File-Level Summary

| File | Rows | Columns | Duplicate Rows | Null Columns |
|------|------|---------|----------------|--------------|
| customers | 2,400 | 9 | 0 | 2 |
| orders | 10,009 | 10 | 0 | 1 |
| support_tickets | 1,921 | 8 | 0 | 0 |
| web_events | 2,400 | 10 | 0 | 0 |
| churn_labels | 2,400 | 4 | 0 | 0 |

---

## 2. Column-Level Null Analysis

### customers

| Column | Dtype | Nulls | Null % | Unique Values |
|--------|-------|-------|--------|---------------|
| customer_id | str | 0 | 0.0% | 2400 |
| signup_date | datetime64[us] | 0 | 0.0% | 609 |
| city_tier | str | 0 | 0.0% | 3 |
| age_group | str | 0 | 0.0% | 4 |
| acquisition_channel | str | 0 | 0.0% | 6 |
| loyalty_tier | str | 1386 | 57.75% ⚠️ | 3 |
| preferred_category | str | 0 | 0.0% | 6 |
| skin_type | str | 401 | 16.71% ⚠️ | 5 |
| marketing_consent | str | 0 | 0.0% | 2 |

### orders

| Column | Dtype | Nulls | Null % | Unique Values |
|--------|-------|-------|--------|---------------|
| order_id | str | 0 | 0.0% | 10009 |
| customer_id | str | 0 | 0.0% | 2400 |
| order_date | datetime64[us] | 0 | 0.0% | 674 |
| category | str | 0 | 0.0% | 6 |
| quantity | int64 | 0 | 0.0% | 4 |
| gross_amount | float64 | 0 | 0.0% | 9514 |
| discount_pct | float64 | 0 | 0.0% | 71 |
| delivery_days | int64 | 0 | 0.0% | 11 |
| returned | int64 | 0 | 0.0% | 2 |
| rating | float64 | 80 | 0.8% | 5 |

### support_tickets

| Column | Dtype | Nulls | Null % | Unique Values |
|--------|-------|-------|--------|---------------|
| ticket_id | str | 0 | 0.0% | 1921 |
| customer_id | str | 0 | 0.0% | 1247 |
| ticket_date | datetime64[us] | 0 | 0.0% | 526 |
| issue_type | str | 0 | 0.0% | 7 |
| support_channel | str | 0 | 0.0% | 3 |
| resolution_hours | float64 | 0 | 0.0% | 525 |
| sentiment_score | float64 | 0 | 0.0% | 181 |
| reopened | int64 | 0 | 0.0% | 2 |

### web_events

| Column | Dtype | Nulls | Null % | Unique Values |
|--------|-------|-------|--------|---------------|
| customer_id | str | 0 | 0.0% | 2400 |
| snapshot_date | datetime64[us] | 0 | 0.0% | 1 |
| sessions_30d | int64 | 0 | 0.0% | 24 |
| product_views_30d | int64 | 0 | 0.0% | 101 |
| cart_adds_30d | int64 | 0 | 0.0% | 13 |
| wishlist_adds_30d | int64 | 0 | 0.0% | 7 |
| abandoned_carts_30d | int64 | 0 | 0.0% | 7 |
| email_opens_30d | int64 | 0 | 0.0% | 14 |
| campaign_clicks_30d | int64 | 0 | 0.0% | 7 |
| last_visit_days_ago | int64 | 0 | 0.0% | 61 |

### churn_labels

| Column | Dtype | Nulls | Null % | Unique Values |
|--------|-------|-------|--------|---------------|
| customer_id | str | 0 | 0.0% | 2400 |
| snapshot_date | datetime64[us] | 0 | 0.0% | 1 |
| churn_next_60d | int64 | 0 | 0.0% | 2 |
| split | str | 0 | 0.0% | 3 |

---

## 3. Specific Quality Issues

### 3.1 Duplicate-Like Order Records

- **12** orders have IDs ending in `_DUP`.
- These simulate real-world deduplication challenges.
- **Recommendation:** Drop `_DUP` records before aggregating order features.
- Treat as soft duplicates — they represent the same transaction entered twice.

### 3.2 Missing Values — `customers.loyalty_tier`

- **~1,386 (57.8%)** customers have no loyalty tier.
- This is not a data error — customers who never enrolled have a null.
- **Recommendation:** Impute as `'No Loyalty'` or create a binary `has_loyalty` flag.

### 3.3 Missing Values — `customers.skin_type`

- **~401 (16.7%)** customers did not provide skin type.
- **Recommendation:** Treat null as `'Not Provided'`. Do not impute with modal value.

### 3.4 Missing Ratings — `orders.rating`

- **~80** orders lack a customer rating.
- **Recommendation:** Use `rating.mean()` per customer for features; handle null at aggregation.

### 3.5 Outlier Gross Amounts

- Orders with `gross_amount > ₹2343` (p99): **82 records**
- Max value: ₹24789
- **Recommendation:** Cap at p99 for modeling features. Investigate if these are B2B orders or data entry errors.

### 3.6 Post-Snapshot Orders (Leakage Risk)**

- **1,872 orders** have `order_date > 2025-09-30`.
- These orders exist ONLY to define the churn label.
- **NEVER use post-snapshot orders as model features — this is the primary leakage risk.**

### 3.7 Join Coverage

- Customers with no orders in `orders.csv`: 0
- Customers with no support tickets: 1,153 (expected — not all customers raise tickets)
- Orphan order customer_ids not in customers.csv: 0
- Orphan ticket customer_ids not in customers.csv: 0

---

## 4. Data Treatment Recommendations

| Issue | Recommended Treatment | Priority |
|-------|----------------------|----------|
| `_DUP` orders | Drop before aggregation | **High** |
| `loyalty_tier` nulls | Encode as `'No Loyalty'` | **High** |
| `skin_type` nulls | Encode as `'Unknown'` | **Medium** |
| `rating` nulls | Use mean per customer; fillna(0) for no-order customers | **Medium** |
| Gross amount outliers | Cap at p99 for modeling | **Medium** |
| Post-snapshot orders | Strictly exclude; flag all post-2025-09-30 rows | **Critical** |

---

## 5. Data Integrity Score

| Dimension | Score | Notes |
|-----------|-------|-------|
| Completeness | 7/10 | loyalty_tier and skin_type have significant nulls |
| Consistency | 8/10 | Minor issues with outliers and duplicates |
| Accuracy | 9/10 | Timestamps valid; IDs consistent across files |
| Timeliness | 10/10 | Snapshot-based; leakage boundary clearly defined |
| Uniqueness | 8/10 | _DUP records require deduplication |