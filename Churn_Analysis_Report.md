# Customer Churn Analysis Report
**Dataset:** Churn_Modelling.csv · 10,000 customers · 3 geographies

---

## Executive Summary
- **Overall churn rate: 20.4%** (2,037 of 10,000 customers lost)
- Three factors dominate: **number of products, age group, and geography**
- Germany churns at 2× the rate of France and Spain — a regional outlier
- Customers with 3–4 products have near-total churn (83–100%)

---

## 01 · Exploratory Data Analysis

| Feature | Mean | Range | Notes |
|---|---|---|---|
| Age | 38.9 | 18 – 92 | Churners avg older |
| Credit Score | 650.5 | 350 – 850 | Minimal churn signal |
| Balance | $76,485 | $0 – $250K | 36.2% hold zero balance |
| Tenure | 5.0 yrs | 0 – 10 | Near-flat churn across all tenures |
| Est. Salary | $100,090 | $12 – $200K | No churn signal |
| Num Products | 1.53 | 1 – 4 | Strongest non-linear churn driver |

No missing values. Clean dataset, ready for modelling.

---

## 02 · Churn Rate by Segment

### Geography
| Country | Customers | Churned | Churn Rate |
|---|---|---|---|
| France | 5,014 | 810 | 16.2% |
| Germany | 2,509 | 814 | **32.4%** ⚠️ |
| Spain | 2,477 | 413 | 16.7% |

### Number of Products ← strongest driver
| Products | Customers | Churn Rate |
|---|---|---|
| 1 | 5,084 | 27.7% |
| 2 | 4,590 | **7.6%** ✅ (sweet spot) |
| 3 | 266 | **82.7%** 🔴 |
| 4 | 60 | **100.0%** 🔴 |

### Age Group
| Age | Churn Rate |
|---|---|
| 18–30 | 7.5% |
| 31–40 | 12.1% |
| 41–50 | 34.0% |
| 51–60 | **56.2%** 🔴 |
| 60+ | 24.8% |

### Other Dimensions
- **Gender:** Female 25.1% vs Male 16.5% (8.6pp gap)
- **Active Members:** Inactive 26.9% vs Active 14.3%
- **Has Credit Card:** 20.8% (no card) vs 20.2% (has card) — negligible difference

---

## 03 · Customer Segmentation

Risk-scored on 5 dimensions: age, products, activity, geography, gender.

| Segment | Count | Churn Rate | Churned |
|---|---|---|---|
| Critical Risk | 329 | **90%** | 296 |
| High Risk | 2,010 | **44%** | 882 |
| Medium Risk | 3,042 | 18% | 536 |
| Low Risk | 4,619 | 7% | 323 |

**Critical segment profile:** Inactive, 3–4 products, 40+ years old, Germany/Female overlap.

---

## 04 · Key Churn Factors (Ranked)

1. **Number of Products** — Non-linear explosion at 3–4 products. Impact: 92.4pp spread. 
2. **Age Group** — Linear rise to 51–60 peak. Correlation: +0.285 (highest).
3. **Geography** — Germany is 2× all others. Not explained by demographics alone.
4. **Inactivity** — Inactive customers are 88% more likely to churn than active ones.
5. **Gender** — Female churn 52% higher than male; consistent across all regions.
6. **Balance (non-zero)** — Higher balance correlates with slightly more churn (+0.119).
7. **Credit Score** — Minimal effect (−0.027 correlation).
8. **Tenure** — Surprisingly flat; long-tenured customers are not significantly safer.
9. **Has Credit Card** — Negligible (−0.007). Credit card ownership is not protective.

---

## Recommendations

| Priority | Action | Target Segment |
|---|---|---|
| 🔴 Immediate | Audit 3–4 product customers; consider proactive downsell | 326 customers |
| 🔴 Immediate | Germany retention program (pricing / service review) | 1,695 at-risk |
| 🟡 Short-term | Re-engagement campaign for inactive members 41–60 | ~1,800 customers |
| 🟡 Short-term | Cross-sell second product to 1-product holders (reduce from 27.7% → 7.6%) | 5,084 customers |
| 🟢 Medium-term | Female-specific retention offer or product improvement | 4,543 customers |
| 🟢 Medium-term | Age 51–60 loyalty program (highest risk cohort) | 797 customers |
