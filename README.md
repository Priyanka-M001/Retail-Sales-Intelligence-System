# Retail Sales Intelligence System


## What this project is about

Most analytics projects stop at charts. This one goes a layer deeper — I built a proper data warehouse with a star schema, loaded it into SQL, wrote 15+ analytical queries, and connected Power BI on top. The goal was to treat a retail dataset the way a business would actually want to use it: structured for querying, not just visualising.

---

## Dashboard Preview

![Dashboard](dashboard.png)

---

## What I found

- **$2.35M total revenue** across 4 years (2015–2018)
- **19.8% YoY growth** in 2018 — the strongest year on record
- **Technology** is the highest-revenue category at $884K, followed by Furniture ($750K) and Office Supplies ($722K)
- **West region leads** with 32% revenue share; South lags at 17%
- **Top customer (Sean Miller)** contributed $25,074 — top 10 customers represent a significant retention opportunity
- Sales consistently spike toward Q4 — November and December are peak months

---

## What I actually did

**ETL pipeline (Python / Pandas)**
- Standardised all column names to snake_case
- Parsed order_date and ship_date with mixed format handling
- Removed rows with invalid or missing order dates
- Built a full star schema:
  - `dim_date` — year, month, quarter, month name
  - `dim_customer` — customer ID, name, segment
  - `dim_product` — product ID, category, sub-category, product name
  - `dim_region` — country, city, state, postal code, region
  - `fact_sales` — all foreign keys + sales measure
- Generated surrogate keys for each dimension table
- Replaced natural keys with surrogate keys in the fact table
- Exported all 5 tables as CSVs for SQL ingestion

**SQL analysis (PostgreSQL)**
- Created all 5 tables with primary and foreign key constraints
- Total revenue, revenue by year, month, region, category, and segment
- Top 10 customers by revenue using RANK() window function
- Top product per category using PARTITION BY + RANK()
- YoY revenue growth using LAG() CTE
- Running cumulative revenue over time
- 5 reusable views created for BI layer connection

**Dashboard (Power BI)**
- Total revenue KPI with YoY growth indicator
- Revenue by year (line chart)
- Revenue by region (donut chart)
- Revenue by category (bar chart)
- Monthly sales trend
- Top 10 customers by revenue
- Insights and recommendations panel
---

## Tech stack

| Tool | Purpose |
|------|---------|
| Python (Pandas) | ETL and star schema construction |
| PostgreSQL | Data warehouse and SQL analysis |
| Power BI | Dashboard and reporting |

---

## Files

```
├── data_preparation.py    # Full ETL script
├── sales_analysis.sql     # All SQL queries and table creation
├── dim_customer.csv       # Customer dimension table
├── dim_date.csv           # Date dimension table
├── dim_product.csv        # Product dimension table
├── dim_region.csv         # Region dimension table
├── fact_sales.csv         # Fact table with surrogate keys
└── dashboard.png          # Dashboard screenshot
```
