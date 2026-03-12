# 🔴 Customer Churn Analysis

An end-to-end churn intelligence pipeline — from raw data through exploratory analysis, segmentation, factor ranking, and interactive visualizations — built with Python and vanilla HTML/JS.

---

## 📁 Project Structure

```
├── Churn_Modelling.csv           # Original raw dataset
├── Churn_Analysis.html           # Full EDA + analysis report (4 sections)
├── Churn_Visualizations.html     # Interactive visualization suite (3 sections)
├── Churn_Analysis_Report.md      # Written findings & recommendations
└── README.md                     # This file
```

---

## 📊 Dataset Overview

| Property | Value |
|---|---|
| Source | `Churn_Modelling.csv` |
| Rows | 10,000 customers |
| Columns | 14 features |
| Target | `Exited` (1 = churned, 0 = retained) |
| Missing values | None |
| Geographies | France, Germany, Spain |
| Date range | Cross-sectional (no time dimension) |

### Feature Reference

| Column | Type | Description |
|---|---|---|
| `CustomerId` | int | Unique customer identifier |
| `Surname` | string | Customer surname |
| `CreditScore` | int | Credit score (350–850) |
| `Geography` | string | France / Germany / Spain |
| `Gender` | string | Male / Female |
| `Age` | int | Customer age (18–92) |
| `Tenure` | int | Years with the bank (0–10) |
| `Balance` | float | Account balance in USD |
| `NumOfProducts` | int | Number of bank products held (1–4) |
| `HasCrCard` | binary | Owns a credit card (0/1) |
| `IsActiveMember` | binary | Active in last period (0/1) |
| `EstimatedSalary` | float | Estimated annual salary |
| `Exited` | binary | **Target** — churned (1) or retained (0) |

---

## 🔍 Analysis Tasks

### 1. Exploratory Data Analysis
- Distribution of all 13 features, split by churn status
- Age, credit score, and balance distributions (stacked bars)
- Cross-tabulations across geography, gender, products, and activity
- No data cleaning required — dataset was complete and consistent

### 2. Churn Rate Calculation

| Dimension | Lowest Rate | Highest Rate | Spread |
|---|---|---|---|
| Overall | — | — | **20.4%** |
| Geography | France 16.2% | Germany 32.4% | 16.2pp |
| Gender | Male 16.5% | Female 25.1% | 8.6pp |
| Age Group | 18–30 at 7.5% | 51–60 at 56.2% | 48.7pp |
| Num Products | 2 products at 7.6% | 4 products at 100% | 92.4pp |
| Activity | Active 14.3% | Inactive 26.9% | 12.6pp |
| Tenure | Year 7 at 17.2% | Year 0 at 23.0% | 5.8pp |

### 3. Customer Segmentation

Risk-scored on 5 dimensions: age, product count, activity status, geography, and gender.

| Segment | Customers | Churn Rate | Already Churned | Avg Age |
|---|---|---|---|---|
| Critical Risk | 329 | **90%** | 296 | 48.5 |
| High Risk | 2,010 | **44%** | 882 | 48.0 |
| Medium Risk | 3,042 | 18% | 536 | 39.7 |
| Low Risk | 4,619 | 7% | 323 | 33.7 |

### 4. Key Churn Factors (Ranked)

| Rank | Factor | Impact | Correlation | Notes |
|---|---|---|---|---|
| 1 | **Number of Products** | 92.4pp spread | −0.048* | Non-linear: 3–4 products = catastrophic |
| 2 | **Age Group** | 48.7pp spread | +0.285 | Strongest linear signal |
| 3 | **Geography** | 16.2pp spread | — | Germany is a structural outlier |
| 4 | **Active Member** | 12.6pp spread | −0.156 | Inactivity is a leading indicator |
| 5 | **Gender** | 8.6pp spread | — | Female consistently higher across all regions |
| 6 | **Balance** | 10.3pp spread | +0.119 | Non-zero balance slightly increases risk |
| 7 | **Credit Score** | 4.2pp spread | −0.027 | Minimal predictive power |
| 8 | **Tenure** | 5.8pp spread | −0.014 | Near-flat — loyalty alone does not protect |
| 9 | **Has Credit Card** | 0.6pp spread | −0.007 | Negligible |

> *Products shows a negative linear correlation because products 1 & 2 dominate volume. The effect at 3–4 is non-linear and highly significant.

---

## 📈 Deliverables

### `Churn_Analysis.html` — Full Report
A four-section dark analytical report with 12+ charts.

| Section | Content |
|---|---|
| 01 · EDA | Age/credit/balance distributions; 4 summary KPI cards |
| 02 · Churn Rates | Geography, products, age group, gender × geography breakdowns; active × age heatmap |
| 03 · Segmentation | Risk tier cards; segment volume vs churn bar; active × age grouped bar |
| 04 · Key Factors | Factor impact table with visual bars; correlation chart; tenure sparkline |

---

### `Churn_Visualizations.html` — Interactive Viz Suite
Three-section sticky-nav visualization page with 15+ charts and 6 heatmaps.

**Section 1 — Churn Distribution**
- Overall split donut (20.4% churn)
- Gender stacked bar
- Geography donut (Germany outlier highlighted)
- Products donut + inline percentage bars
- Active vs inactive donut with stat callouts
- Age group stacked bar (retained vs churned volumes)

**Section 2 — Tenure vs Churn**
- Churn rate line across years 0–10 with average reference line
- Volume stacked bar by tenure
- Multi-line: tenure × product count (3-product line hovers 65–100%)
- Multi-line: tenure × geography (Germany never drops below 27%)

**Section 3 — Heatmaps (6)**

| Heatmap | Key Finding |
|---|---|
| Age × Geography | Germany 51–60: **69.5%** — highest intersection in dataset |
| Age × Gender | Female 51–60: **65.2%** vs Male 47.5% |
| Geography × Activity | Inactive Germany: **41.1%** |
| Age × Products | 51–60 + 4 products: **100%** |
| Balance Band × Tenure | 1–50K balance, early tenure: **43.5%** |
| Credit Score × Age | Age dominates every credit band — score irrelevant |

---

## 💡 Key Recommendations

| Priority | Action | Target | Expected Impact |
|---|---|---|---|
| 🔴 Critical | Audit 3–4 product customers; consider proactive downsell to 2 | 326 customers | Reduce from 83–100% → ~8% |
| 🔴 Critical | Germany-specific retention program (pricing or service investigation) | ~1,695 at-risk | Align to France/Spain baseline |
| 🟡 High | Re-engagement campaign for inactive members aged 41–60 | ~1,800 customers | Close 12.6pp activity gap |
| 🟡 High | Cross-sell second product to 1-product holders | 5,084 customers | Reduce from 27.7% → 7.6% |
| 🟢 Medium | Female-targeted loyalty or product-fit improvement | 4,543 customers | Close 8.6pp gender gap |
| 🟢 Medium | Early life (Year 0–1) onboarding program — highest tenure churn | ~1,448 customers | Reduce new-customer dropout |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3 / pandas / numpy | Data analysis and segmentation |
| Chart.js 4.4.1 | All interactive charts |
| Vanilla HTML / CSS / JS | Report and visualization UI |
| Google Fonts (Syne, JetBrains Mono, IBM Plex family) | Typography |

---

## 🚀 How to Run

1. Open `Churn_Analysis.html` or `Churn_Visualizations.html` in any modern browser — no server, no dependencies.
2. Use the sticky navigation in `Churn_Visualizations.html` to jump between the three sections.
3. Hover any heatmap cell to see the exact churn percentage for that combination.
4. Hover any chart for detailed tooltips.

---

*Customer Churn Analysis · Churn_Modelling.csv · 10,000 records · 3 geographies*
