# Business Memo — D2C Customer Retention Readiness

**To:** Product, Marketing & Customer Support Leadership  
**From:** Data Intelligence Team  
**Date:** October 1, 2025  
**Re:** Pre-Campaign Findings — Critical Retention Intelligence  
**Classification:** Internal — Confidential

---

## Executive Summary

Our analysis of **2,400 customers** (snapshot: 30 September 2025) reveals a
**47.0% churn rate** in the subsequent 60-day window — representing
**1,127 customers at risk**. Before launching any retention campaign, the
following five concerns must be addressed operationally.

---

## Key Findings

### 1. Loyalty Programme is Under-Enrolled and Underperforming

- Only ~42% of customers are enrolled in the loyalty programme (Silver/Gold/Platinum).
- Customers WITHOUT loyalty tier churn at **48.3%** vs **45.1%**
  for enrolled customers — a significant protective effect.
- **Immediate action:** Accelerate loyalty enrolment campaigns before spending on discounts.

### 2. Web Inactivity is a Leading Churn Signal

- Customers with **zero web sessions in the last 30 days** churn at **66.3%**.
- Active web users churn at only **45.3%**.
- Many churned customers visited the site but did not convert (high cart abandonment).
- **Action:** Trigger re-engagement emails within 7 days of web inactivity.

### 3. Support Complaints are Not Being Resolved Effectively

- Customers with **3+ support tickets** churn at **34.9%** — nearly double the average.
- `product_reaction` and `refund_delay` ticket types show the highest churn correlation.
- Reopened tickets (customer complained, then complaint was reopened) are especially predictive.
- **Action:** Flag customers with 2+ tickets for proactive outreach before they churn.

### 4. Discount Dependency is Not Driving Long-Term Retention

- Customers receiving >40% average discount churn at **51.0%**,
  higher than customers with <10% discount (46.5%).
- This suggests discount-trained customers churn when discounts stop.
- **Action:** Shift from blanket discounts to value-based retention (loyalty points, early access).

### 5. Acquisition Channel Drives Long-Term Retention Quality

- Referral and Organic customers show the lowest churn rates.
- Marketplace-acquired customers show the highest churn risk.
- Instagram and Influencer-acquired customers are mid-risk but highly discount-sensitive.
- **Action:** Re-evaluate CAC spend on Marketplace; invest more in Referral programmes.

---

## Recommended Pre-Campaign Actions

| Priority | Action | Owner | Timeline |
|----------|--------|-------|----------|
| P1 | Enrol eligible customers in loyalty programme | CRM | Week 1 |
| P1 | Flag customers with 2+ open support tickets for proactive outreach | Support | Week 1 |
| P2 | Set up 7-day web-inactivity trigger email sequence | Marketing | Week 2 |
| P2 | Replace blanket discount campaigns with segment-specific offers | Marketing | Week 2 |
| P3 | Re-evaluate Marketplace acquisition budget vs. LTV | Marketing/Finance | Month 1 |
| P3 | Build cart-abandonment recovery flow (already seeing 30d data) | Product | Month 1 |

---

## Risks of Acting Without This Analysis

Launching a blanket discount campaign without segmentation would:
1. Cannibalize revenue from customers who would have purchased anyway (~58% base retention rate)
2. Train already-discount-dependent customers to expect even deeper discounts
3. Miss the true high-risk segment (inactive, high-complaint customers) who need relationship repair, not discounts

---

## Data Limitations to Note

- ~58% of customers have no loyalty tier — this field is critical and should be collected at signup
- Web event data covers only the last 30 days; longer windows would improve signal quality
- Support ticket sentiment scores are model-generated and should be validated against manual labels

---

*This memo is based on automated analysis of the customer dataset. All figures are from the
September 30, 2025 snapshot. For model-based churn scoring, refer to the Part 3 model outputs.*