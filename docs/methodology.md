# Methodology

## 1. Data Source

The project uses monthly Telecom Subscription Data published by the
Telecom Regulatory Authority of India (TRAI).

**Coverage:** January 2024 – July 2026

**Primary source:** Annexure-II — Wireless (Mobile) Subscriber Base

The analysis covers 22 Licensed Service Areas (LSAs).

---

## 2. Data Consolidation

Monthly TRAI reports were consolidated into a single analytical dataset.

The final dataset contains:

- 4,356 rows
- 8 columns
- 31 monthly periods

The analytical grain is:

**Period × LSA × Operator**

---

## 3. Data Validation

The consolidated dataset was checked for:

### Duplicate records

Period × LSA × Operator was used as the analytical key.

**Duplicate records found: 0**

### Subscriber values

Subscriber counts were checked for invalid negative values.

### Missing previous-month values

Previous-month subscriber values were checked before calculating
month-on-month metrics.

### Zero previous-month values

Growth was not calculated when the previous-month subscriber value was
zero because percentage growth would not be meaningful.

---

## 4. Derived Metrics

### Net Addition

Net addition was recalculated as:

`Current Subscribers − Previous Month Subscribers`

### Monthly Growth %

Monthly growth was recalculated as:

`(Current Subscribers − Previous Month Subscribers) / Previous Month Subscribers × 100`

The recalculated metric was used as the analytical source of truth
instead of relying on the original derived growth field.

### LSA Operator Market Share

For LSA-level analysis:

`Operator Subscribers within LSA / Total Subscribers within LSA × 100`

The resulting operator shares were checked to ensure they reconciled
to approximately 100% within each LSA-period combination.

---

## 5. December 2025 Reporting Revision

The December 2025 TRAI report contained a revised November 2025
subscriber baseline.

### Original November 2025 total

**1,173,881,921**

### Revised November baseline used by December report

**1,236,957,678**

### December 2025 subscriber count

**1,244,196,237**

Using the revised baseline:

`1,244,196,237 − 1,236,957,678 = 7,238,559`

Therefore, the December report's own month-on-month increase was
approximately **7.24M**.

Using the original November figure directly would create an apparent
increase of approximately **70.3M** in the published series.

### Handling approach

The project:

- Preserved the original November value
- Included December 2025 in the analysis
- Used the revised November baseline for December's own month-on-month calculation
- Retained the original November value for auditability
- Did not interpret the apparent ~70.3M published-series increase as
  normal month-on-month subscriber growth

---

## 6. Power BI Model

The Power BI report uses:

**Fact_Telecom** as the main fact table

**Dim_Date** as the date dimension

Relationship:

`Dim_Date[Date] → Fact_Telecom[period]`

Cardinality:

**1 → many**

The date dimension was also used to maintain chronological month
sorting and dynamic period filtering.

---

## 7. Dashboard Analysis

The Power BI report contains three pages:

### Page 1 — India Telecom Market Overview

Focuses on national subscriber trends, operator share, monthly
additions, and LSA distribution.

### Page 2 — Operator Competitive Intelligence

Focuses on operator subscriber trends, market-share movement,
subscriber changes, and operator comparison.

### Page 3 — LSA Geographic Intelligence

Focuses on subscriber distribution, operator market share by LSA,
LSA subscriber changes, and geographic concentration.

---

## 8. Interactivity

The dashboard uses dynamic DAX measures and slicers to allow analysis
by:

- Period
- LSA
- Operator

The same calculations therefore respond to the selected filter context
rather than relying only on static values.

---

## 9. Analytical Principles

The analysis distinguishes between:

- Absolute subscriber change
- Percentage growth
- Market share
- Percentage-point share change

Market-share change is expressed in **percentage points (pp)** rather
than percentage growth.

The project also avoids treating missing current-period observations
for historical operator series as zero without validation.
