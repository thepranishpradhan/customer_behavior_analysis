# Customer Shopping Behavior Analysis

End-to-end data analysis project covering the full pipeline: Python for data cleaning, PostgreSQL/SQL for business-question analysis, and Power BI for dashboard visualization.

## Overview

This project analyzes 3,900 customer shopping transactions to uncover patterns in spending behavior, product performance, and customer segments — turning raw transactional data into actionable business recommendations.

## Business Questions Answered

1. What are the top 5 highest-rated products by average customer review?
2. What are the top 3 best-selling products within each product category?
3. How does average purchase amount compare between standard and express shipping?
4. Do subscribers spend more than non-subscribers?
5. Is there a revenue difference between male and female customers?
6. Which customers use discounts while still spending above average (high-value discount users)?
7. How can customers be segmented by purchase behavior?

*(See `sql/customer_behavior_analysis.sql` for the full list of 10 queries with results, including a verification pass added after initial analysis.)*

## Dataset

- **Source**: Customer shopping behavior dataset
- **Size**: 3,900 rows, 18 columns
- **Data quality**: 37 missing values, isolated to the Review Rating column — imputed using category-level median, preserving distribution integrity
- **Key fields**: customer demographics, purchase amount, category, item purchased, review rating, subscription status, shipping type, discount usage, frequency of purchases

## Tools Used

| Tool | Purpose |
|---|---|
| Python (pandas) | Data cleaning, missing value imputation, feature engineering |
| SQLAlchemy | Loading cleaned data directly into PostgreSQL |
| PostgreSQL | Structured querying to answer business questions |
| Power BI | Interactive dashboard and visualization |

## Project Workflow

1. **Data Loading** — Imported the raw CSV using pandas.
2. **Initial Exploration** — Checked structure, data types, and summary statistics.
3. **Missing Data Handling** — Imputed 37 missing Review Rating values using the median rating within each product category.
4. **Feature Engineering** — Created `age_group` (via quantile binning) and `purchase_frequency_days` (mapping categorical frequency labels to numeric day counts).
5. **Database Integration** — Loaded the cleaned DataFrame directly into PostgreSQL using SQLAlchemy's `to_sql()`.
6. **SQL Analysis** — Answered 10 business questions using SQL: aggregate functions, CTEs, and window functions (`ROW_NUMBER() OVER (PARTITION BY ...)`) for top-N-per-group analysis.
7. **Dashboard** — Built an interactive Power BI dashboard on top of the query results.

## Key Findings

- **Revenue by gender**: Male customers generate significantly more total revenue than female customers ($157,890 vs. $75,191), but this is driven entirely by customer volume — there are more than twice as many male customers (2,652) as female (1,248). Average spend per customer is nearly identical ($59.54 male vs. $60.25 female), with female customers spending marginally more per transaction.
- **Top-rated products**: Gloves (3.86/5), Sandals (3.84/5), Boots (3.82/5), Hat (3.80/5), and Skirt (3.79/5) are the five highest-rated items by average customer review.
- **Shipping type**: Express shipping customers spend modestly more on average than standard shipping customers ($60.48 vs. $58.46 — about 3.5% higher), a real but small effect.
- **Subscription status**: Subscribers don't spend more per transaction than non-subscribers ($59.49 vs. $59.87) and contribute revenue proportionate to their customer share (27% of customers, 27% of revenue). Subscribers do show modestly more previous purchases (26.08 vs. 25.08 — about 4% higher).
- **Customer segmentation**: Segmenting by previous purchase count (New = 1, Returning = 2–10, Loyal = 11+) shows the base is overwhelmingly established: 79.9% of customers (3,116) are Loyal, 18.0% (701) are Returning, and only 2.1% (83) are genuinely New.
- **Best-sellers by category**: Top 3 items by order volume include Jewelry, Sunglasses, and Belt (Accessories); Blouse, Pants, and Shirt (Clothing); Sandals, Shoes, and Sneakers (Footwear); and Jacket and Coat (Outerwear).

## Repository Structure
├── data/
│ └── customer_behavior_analysis.csv
├── notebooks/
│ └── customer_behavior_analysis.ipynb
├── sql/
│ └── customer_behavior_analysis.sql
├── dashboard/
│ └── customer_behavior_analysis.pbix
├── presentation/
│ └── customer_behavior_analysis.pptx
├── report/
│ └── customer_behavior_analysis.docx
└── README.md

## Dashboard Preview
<img width="1128" height="634" alt="customer behavior dashboard powerbi" src="https://github.com/user-attachments/assets/29d3f5fd-3dcf-46ee-8f16-5b9ccef43036" />

## Author
**Pranish Pradhan** — Business Analyst
https://www.linkedin.com/in/mrpranishpradhan/ • pranish.pradhan.2024@gmail.com
