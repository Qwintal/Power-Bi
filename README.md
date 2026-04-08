# 📊 Superstore Sales Analysis — Power BI Dashboard

## Overview

This project analyzes retail sales data to uncover profitability issues, sales trends, and regional performance.
The dashboard is designed to answer a critical business question:

> **Are high sales actually translating into profit?**

The analysis reveals that revenue growth alone is misleading—several high-performing products are consistently loss-making.

---

## Live Dashboard

🔗 https://app.powerbi.com/view?r=eyJrIjoiNTQyYzkwYzAtMTIzNS00NmQwLThmZDEtNmU5ZGUzZmZjMTY4IiwidCI6ImQxZjE0MzQ4LWYxYjUtNGEwOS1hYzk5LTdlYmYyMTNjYmM4MSIsImMiOjEwfQ%3D%3D

---

## Dataset

* Source: Superstore dataset (Kaggle)
* Records: ~10,000 rows
* Time Period: 2014–2017
* Region: United States

### Additional Data

A secondary dataset was created to simulate regional sales targets.

---

## Data Preparation (Power Query)

To demonstrate real-world data issues, the dataset was intentionally dirtied before cleaning:

* Introduced null values (Postal Code)
* Added duplicate rows
* Mixed date formats
* Inconsistent text casing
* Added junk column

### Cleaning Steps

* Removed duplicates (Order ID level)
* Removed rows with null postal codes
* Standardized categorical fields (Title Case)
* Converted date formats to consistent type
* Dropped irrelevant columns

---

## Data Modeling (Star Schema)

A star schema was implemented for performance and scalability.

### Fact Table

* **Fact_Orders**: Sales, Profit, Quantity, Discount

### Dimension Tables

* Dim_Customer
* Dim_Product
* Dim_Date
* Dim_Ship
* Dim_Region

### Why Star Schema?

* Reduces redundancy
* Prevents incorrect aggregations
* Improves query performance
* Enables flexible slicing across dimensions

---

## Key DAX Measures

```DAX
Total Sales = SUM(Fact_Orders[Sales])
Total Profit = SUM(Fact_Orders[Profit])
Total Orders = DISTINCTCOUNT(Fact_Orders[Order ID])

Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)

Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(Dim_Date[Date])
)

YoY Sales Growth % =
DIVIDE(
    [Total Sales] - [Sales LY],
    [Sales LY],
    0
)
```

---

## Dashboard Structure

### 1. Executive Overview

* KPI Cards: Sales, Profit, Orders, Margin
* Monthly Sales & Profit Trends
* Category Contribution

---

### 2. Sales Performance Over Time

* Year-over-Year comparison
* Quarterly breakdown
* Monthly anomaly detection

---

### 3. Product & Category Analysis

* Top 10 products by revenue
* Profit margin by sub-category
* Sales vs Profit scatter plot
* Bottom 5 loss-making products

---

### 4. Regional & Customer Analysis

* Sales by state (map)
* Segment performance
* Profit by region
* Average order value

---

## Key Insights

### 1. High Sales ≠ High Profit

* Tables: **-11% profit margin**
* Bookcases: **-6% profit margin**
* These products generate revenue but consistently incur losses

👉 Recommendation:

* Increase pricing OR reduce cost OR discontinue

---

### 2. Strong Seasonality (Q4 Dominance)

* Q4 sales are **40–50% higher** than Q1/Q2
* Pattern is consistent across all years

👉 Recommendation:

* Shift marketing and inventory focus to Q4
* Reduce spend in low-conversion months (Q1)

---

## Key Takeaway

> Revenue is not a reliable performance metric without profitability context.
> This dashboard identifies where the business is scaling losses instead of profits.

---

## Tools Used

* Power BI Desktop
* Power Query (ETL)
* DAX (Data Analysis Expressions)
* Excel (data manipulation)

---

## Project Structure

```
Superstore-PowerBI-Dashboard/
│
├── pbix/
│   └── WSV_Lab.pbix
│
├── dataset/
│   ├── superstore_dirty.csv
│   └── regional_targets.csv
│
├── docs/
│   └── project_explanation.docx
│
└── README.md
```

---

## Limitations & Future Improvements

* No real-time data source (CSV-based)
* No Row-Level Security (RLS)
* No incremental refresh setup

### Future Enhancements

* Connect to SQL database
* Implement RLS for user-specific views
* Add forecasting models
* Optimize model for large-scale datasets

---

## Author

**Ankit Uniyal**
BSc Data Science

---
