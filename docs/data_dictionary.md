# Data Dictionary

The final analytical dataset contains 4,356 rows and 8 columns.

## Dataset Grain

One row represents:

**Period × LSA × Operator**

## Fields

| Field | Description |
|---|---|
| `period` | Month-end reporting date |
| `lsa` | Licensed Service Area (telecom circle) |
| `operator` | Telecom operator label |
| `previous_month_subscribers` | Subscriber count for the previous month used for comparison |
| `subscriber_count` | Current-month wireless subscriber count |
| `net_addition` | Difference between current and previous-month subscribers |
| `monthly_growth_pct` | Month-on-month subscriber growth percentage |
| `market_share_pct` | Operator subscriber share within the corresponding LSA and period |

## Derived Metrics

### Net Addition

`Current Subscribers − Previous Month Subscribers`

### Monthly Growth %

`(Current Subscribers − Previous Month Subscribers) / Previous Month Subscribers × 100`

Monthly growth is not calculated where the previous-month subscriber value is zero or unavailable.

### Market Share %

`Operator Subscribers / Total Subscribers within the same LSA and Period × 100`

## Data Coverage

**January 2024 – July 2026**

## Geographic Coverage

**22 Licensed Service Areas (LSAs)**

## Operator Coverage

The dataset contains six current operators, with **BSNL (VNO's)** appearing as a historical operator series in earlier periods.
