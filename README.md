# README: Superstore_new.xlsx

## Overview

**Superstore_new.xlsx** is a retail analytics workbook based on the classic Superstore dataset. It contains four years of global order transaction data alongside a set of pre-built pivot table summaries and a dashboard sheet. The workbook is structured for exploratory data analysis, business intelligence reporting, and dashboard visualisation practice.

---

## File Structure

The workbook contains **11 sheets**, divided into three layers:

| Layer | Sheet(s) | Purpose |
|---|---|---|
| Raw Data | `Sheet1` | Full transactional dataset (51,290 rows) |
| Pivot Summaries | `Profit per Category`, `Sales per Region`, `Shipping Cost per Category`, `Sales per Sub Category`, `Sales per Category`, `Quantity per Sub-Category`, `Sales`, `Profit`, `Shipping Cost` | Aggregated pivot table outputs |
| Dashboard | `Dashboard` | Visual summary titled "SUPERSTORE ANALYSIS" |

---

## Raw Data — `Sheet1`

### Dimensions
- **Rows:** 51,290 order line items
- **Columns:** 24

### Columns Reference

| Column | Data Type | Description |
|---|---|---|
| Row ID | Integer | Unique row identifier |
| Order ID | Text | Order reference number |
| Order Date | Text (DD-MM-YYYY) | Date the order was placed |
| Ship Date | Text (DD-MM-YYYY) | Date the order was shipped |
| Ship Mode | Text | Shipping method used |
| Customer ID | Text | Unique customer identifier |
| Customer Name | Text | Full name of the customer |
| Segment | Text | Customer segment |
| City | Text | Delivery city |
| State | Text | Delivery state/province |
| Country | Text | Delivery country |
| Postal Code | Float | Postal/zip code (41,296 nulls — international orders) |
| Market | Text | Global market grouping |
| Region | Text | Sub-region within market |
| Product ID | Text | Unique product identifier |
| Category | Text | Top-level product category |
| Sub-Category | Text | Product sub-category |
| Product Name | Text | Full product name |
| Sales | Float | Revenue from the line item (USD) |
| Quantity | Integer | Number of units ordered |
| Discount | Float | Discount rate applied (0.0 – 0.85) |
| Profit | Float | Profit/loss on the line item (USD) |
| Shipping Cost | Float | Cost of shipping (USD) |
| Order Priority | Text | Order fulfilment priority level |

### Date Range
Orders span **1 January 2011 – 31 December 2014** (4 years).

### Key Categorical Values

**Markets (7):** US, APAC, EU, Africa, EMEA, LATAM, Canada

**Regions (13):** East, West, South, North, Central, Caribbean, Oceania, North Asia, Central Asia, Southeast Asia, Africa, EMEA, Canada

**Categories (3):** Technology, Furniture, Office Supplies

**Sub-Categories (17):** Accessories, Appliances, Art, Binders, Bookcases, Chairs, Copiers, Envelopes, Fasteners, Furnishings, Labels, Machines, Paper, Phones, Storage, Supplies, Tables

**Segments (3):** Consumer, Corporate, Home Office

**Ship Modes (4):** Same Day, First Class, Second Class, Standard Class

**Order Priorities (4):** Critical, High, Medium, Low

### Numeric Summary

| Metric | Min | Max | Mean | Notes |
|---|---|---|---|---|
| Sales | $0.44 | $22,638.48 | $246.49 | Wide spread; high-value outliers |
| Quantity | 1 | 14 | 3.5 | Most orders are small |
| Discount | 0% | 85% | 14.3% | Many orders at 0% discount |
| Profit | -$6,599.98 | $8,399.98 | $28.61 | Losses present; discounting drives negatives |
| Shipping Cost | $0.00 | $933.57 | $26.38 | Highly variable |

### Data Quality Notes
- **Postal Code** has 41,296 null values (~80.5% missing). This is expected — non-US orders do not use US-style postal codes.
- All other columns are fully populated with no missing values.
- Order Date and Ship Date are stored as **text strings** (DD-MM-YYYY format), not Excel date serials. These will need to be converted if used in time-series calculations.

---

## Pivot Summary Sheets

Each summary sheet is a pivot table extracted from the raw data. They are formatted with two blank rows at the top before the header row.

| Sheet | Rows | Columns | Aggregation | Grand Total |
|---|---|---|---|---|
| Sales per Category | Segment | Sum of Sales | By customer segment | $270,487.10 |
| Sales per Sub Category | Sub-Category | Sum of Sales | 17 product sub-categories | $270,487.10 |
| Sales per Region | Region | Sum of Sales | 13 global regions | $12,642,501.91 |
| Profit per Category | Segment | Sum of Profit | By customer segment | $43,695.98 |
| Shipping Cost per Category | Category | Sum of Shipping Cost | 3 product categories | $28,127.14 |
| Quantity per Sub-Category | Sub-Category | Sum of Quantity | 17 product sub-categories | 2,921 units |
| Sales | (Single value) | Sum of Sales | Total only | $270,487.10 |
| Profit | (Single value) | Sum of Profit | Total only | $43,695.98 |
| Shipping Cost | (Single value) | Sum of Shipping Cost | Total only | $28,127.14 |

> **Note:** The Sales, Profit, and Shipping Cost totals in the pivot sheets reflect a filtered or partial subset of the data, not the full 51,290-row dataset. If you need totals for the full dataset, calculate directly from `Sheet1`.

---

## Dashboard Sheet

The `Dashboard` sheet is titled **"SUPERSTORE ANALYSIS"** and contains visual elements built from the pivot summaries. It is not directly readable as tabular data — it is intended for visual presentation.


---

## Notes for Analysts

1. The pivot sheets use a subset of data. Always verify against `Sheet1` for full-dataset analysis.
2. Profit can be negative — this is real data reflecting discounting losses, not data errors.
3. The dataset covers global markets. Regional analysis should account for currency and market differences.
4. "Postal Code" nulls should be treated as expected missing data, not as data quality failures.

---

*Last updated: March 2026*
