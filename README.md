# E-Commerce Sales Data Processing & Reporting Pipeline
 
An end-to-end **data processing and reporting project** built with Python, SQL, and Power BI. It covers data ingestion, validation, transformation, SQL-based aggregation, star schema data modeling, and a reporting layer for sales, returns, customer, and regional analytics.
 
> **Dataset Note:** This project uses a **simulated Flipkart-style e-commerce dataset** created for portfolio and educational purposes. It does not contain proprietary Flipkart customer or transaction data.
 
---
 
## Project Overview
 
Raw transactional data is only useful once it is ingested, validated, cleaned, and modeled correctly. This project builds that full flow on **50,000+ order records and 12,000 customer records**:
 
- Ingest raw order and customer data into Python
- Validate data quality and fix defects
- Transform and enrich the data with derived features
- Load the cleaned data into a relational database (SQLite)
- Aggregate business KPIs with SQL
- Model the data as a star schema
- Serve the data to a Power BI dashboard using DAX measures
---
 
## Pipeline Workflow
 
```text
Data Ingestion (raw CSV)
        ↓
Data Validation & Quality Checks
        ↓
Data Cleaning & Transformation
        ↓
Feature Engineering
        ↓
Load to Relational Database (SQLite)
        ↓
SQL Aggregation & KPI Queries
        ↓
Star Schema Data Modeling
        ↓
DAX Measures
        ↓
Power BI Reporting Layer
```
 
---
 
## Technology Stack
 
| Technology | Purpose |
|---|---|
| Python | Ingestion, validation, transformation |
| Pandas | Data manipulation and cleaning |
| NumPy | Numerical operations |
| Faker | Synthetic customer data generation |
| Matplotlib | Data profiling and visualization |
| SQLite | Relational storage and SQL analysis |
| SQL | Extraction, aggregation, KPI queries |
| Power BI | Reporting dashboard |
| DAX | Measures and calculations |
| Git / GitHub | Version control |
 
---
 
## Dataset
 
* **50,000+ orders**
* **12,000 customers**
* **6 product categories**
* Multiple Indian states and regions
* Order data covering **2024–2025**
### Fields
 
```text
Order_ID, Customer_ID, Product_ID, Order_Date, Customer_Name, Age, Gender,
City, State, Region, Category, Sub_Category, Product_Name, Quantity,
Unit_Price, Discount_Percent, Sales_Amount, Cost_Amount, Profit,
Payment_Method, Order_Status, Delivery_Days, Return_Flag, Return_Date,
Return_Reason, Refund_Amount, Return_Cost, Customer_Rating, Net_Sales,
Net_Profit
```
 
---
 
## Data Validation & Quality Checks
 
Data quality checks were implemented with Python and Pandas before any analysis or loading:
 
| Check | Purpose |
|---|---|
| Duplicate order detection | Remove repeated order records |
| Missing value analysis | Find and handle nulls |
| Data type validation | Ensure correct types per column |
| Negative value detection | Catch invalid amounts |
| Quantity and discount validation | Enforce valid ranges |
| Customer age and rating validation | Enforce valid ranges |
| Delivery time validation | Catch impossible delivery days |
| Return-date validation | Return date must not precede order date |
| Sales and profit calculation validation | Recompute values and compare with stored values |
| Column name standardization | Consistent schema |
 
Example:
 
```python
df_clean.columns = (
    df_clean.columns.str.strip()
    .str.lower()
    .str.replace(" ", "_")
)
```
 
### Data Quality Results
 
Fill in these numbers from your own notebook output:
 
| Metric | Count |
|---|---|
| Raw records | [add] |
| Duplicate records removed | [add] |
| Records with missing values | [add] |
| Records failing range checks | [add] |
| Final clean records | [add] |
 
---
 
## Data Transformation & Feature Engineering
 
Derived fields created for time-series analysis and reporting:
 
```text
Order Year, Order Month, Order Month Name, Order Quarter,
Order Year-Month, Profit Margin, Return Rate
```
 
---
 
## SQL Layer
 
The cleaned data was loaded into **SQLite** and queried with SQL to extract, filter, and aggregate business metrics:
 
* Overall sales and profit
* Monthly sales trends
* Category and product performance
* Top customers
* State performance
* Return rate by category and return reasons
* High-sales / high-return products
* Payment method and order status analysis
Example:
 
```sql
SELECT
    category,
    SUM(sales_amount) AS total_sales,
    SUM(profit) AS total_profit
FROM orders
GROUP BY category
ORDER BY total_sales DESC;
```
 
---
 
## Customer Segmentation
 
| Segment | Definition |
|---|---|
| One-Time | Purchased once |
| Repeat | Purchased more than once |
| Loyal | Frequent / high-value customers |
 
---
 
## Data Model (Star Schema)
 
A **star schema** was implemented in Power BI.
 
**Fact table:** `Fact_Orders`
**Dimension tables:** `Dim_Customer`, `Dim_Product`, `Dim_Geography`, `Dim_Date`
 
```text
             Dim_Customer
                  │
Dim_Product ─── Fact_Orders ─── Dim_Geography
                  │
              Dim_Date
```
 
Relationships (one-to-many):
 
```text
Dim_Customer[customer_id]    1 ──── *  Fact_Orders[customer_id]
Dim_Product[product_id]      1 ──── *  Fact_Orders[product_id]
Dim_Geography[geography_id]  1 ──── *  Fact_Orders[geography_id]
Dim_Date[Date]               1 ──── *  Fact_Orders[order_date]
```
 
---
 
## Reporting Layer (Power BI)
 
The report has five pages.
 
1. **Executive Overview:** Total Sales, Net Sales, Total Profit, Net Profit, Total Orders, Total Customers, Return Rate, Average Order Value; monthly trend, category sales, top products, state performance, order status
2. **Sales & Product:** Sales, profit, profit margin, units sold; discount vs profit; category profitability
3. **Customer:** Repeat customers and rate, customer segments, top customers, purchase frequency
4. **Returns:** Returned orders, return rate, refunds, return cost; return reasons and return rate by category
5. **Geographic:** State and regional sales, profit, and return rate
---
 
## DAX Measures
 
```DAX
Total Sales = SUM(Fact_Orders[sales_amount])
```
 
```DAX
Net Sales = SUM(Fact_Orders[net_sales])
```
 
```DAX
Total Profit = SUM(Fact_Orders[profit])
```
 
```DAX
Net Profit = SUM(Fact_Orders[net_profit])
```
 
```DAX
Total Orders = DISTINCTCOUNT(Fact_Orders[order_id])
```
 
```DAX
Total Customers = DISTINCTCOUNT(Fact_Orders[customer_id])
```
 
```DAX
Units Sold = SUM(Fact_Orders[quantity])
```
 
```DAX
Average Order Value = DIVIDE([Total Sales], [Total Orders])
```
 
```DAX
Returned Orders =
CALCULATE([Total Orders], Fact_Orders[return_flag] = 1)
```
 
```DAX
Return Rate = DIVIDE([Returned Orders], [Total Orders])
```
 
```DAX
Total Refunds = SUM(Fact_Orders[refund_amount])
```
 
```DAX
Total Return Cost = SUM(Fact_Orders[return_cost])
```
 
```DAX
Profit Margin = DIVIDE([Total Profit], [Total Sales])
```
 
```DAX
Repeat Customers =
COUNTROWS(
    FILTER(
        VALUES(Dim_Customer[customer_id]),
        CALCULATE(DISTINCTCOUNT(Fact_Orders[order_id])) > 1
    )
)
```
 
```DAX
Repeat Customer Rate = DIVIDE([Repeat Customers], [Total Customers])
```
 
---
 
## Key Findings
 
Add 4 to 6 findings with real numbers from your dashboard, for example:
 
* Top category by sales: [category] with [value]
* Overall return rate: [value]%
* Repeat customer rate: [value]%
* Highest-sales state: [state]
---
 
## Project Structure
 
```text
flipkart-ecommerce-sales-customer-analytics/
├── data/
│   ├── raw/
│   └── cleaned/
├── notebooks/
│   └── ecommerce_analysis.ipynb
├── sql/
│   └── ecommerce_analysis.sql
├── powerbi/
│   └── ecommerce_dashboard.pbix
├── images/
│   └── dashboard_screenshots/
├── README.md
└── requirements.txt
```
 
---
 
## Requirements
 
```bash
pip install -r requirements.txt
```
 
`requirements.txt`:
 
```text
pandas
numpy
matplotlib
faker
```
 
---
 
## How to Run
 
1. Clone the repository:
```bash
git clone https://github.com/SivaPrasad110/flipkart-ecommerce-sales-customer-analytics.git
```
2. Install dependencies: `pip install -r requirements.txt`
3. Open `notebooks/ecommerce_analysis.ipynb` and run all cells. The notebook covers data generation, validation, cleaning, feature engineering, EDA, and SQL analysis.
4. Open `powerbi/ecommerce_dashboard.pbix` to explore the dashboard.
---
 
## Dashboard Preview
 
```markdown
![Executive Overview](images/dashboard_screenshots/executive_overview.png)
![Sales & Product](images/dashboard_screenshots/sales_product.png)
![Customer Intelligence](images/dashboard_screenshots/customer_intelligence.png)
![Returns Intelligence](images/dashboard_screenshots/returns_intelligence.png)
![Geographic Intelligence](images/dashboard_screenshots/geographic_intelligence.png)
```
 
---
 
## Skills Demonstrated
 
* **Data engineering fundamentals:** data ingestion, data validation, data cleaning, data transformation, data quality checks, data modeling (star schema)
* **Python:** Pandas, NumPy, Matplotlib, Faker, feature engineering
* **SQL:** extraction, filtering, aggregation, GROUP BY, KPI queries, trend analysis
* **Reporting:** Power BI, DAX, KPI cards, slicers, interactive dashboards
* **Practices:** technical documentation, Git and GitHub version control
---
 
## Future Improvements
 
* Rebuild the transformation step in **PySpark** and orchestrate it with **Apache Airflow** (see the related `ecommerce-etl-pipeline` repository once published)
* Add automated unit tests and row-count reconciliation checks
* Load curated tables into a cloud warehouse such as Snowflake
* Add pipeline logging and monitoring
* Customer Lifetime Value, RFM segmentation, and sales forecasting
---
 
## Author
 
**Mekala Siva Prasad**
Python | SQL | Data Processing | Power BI
[LinkedIn](https://www.linkedin.com/in/m-siva-prasad-7a5891315/) | [GitHub](https://github.com/SivaPrasad110)
