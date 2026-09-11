````markdown
# Flipkart E-Commerce Sales, Returns & Customer Analytics

## 📊 Data Analyst Portfolio Project

An end-to-end **E-Commerce Data Analytics project** built using Python, SQL, and Power BI to analyze sales performance, profitability, customer behavior, product performance, returns, and regional trends.

> **Dataset Note:** This project uses a **simulated Flipkart-style e-commerce dataset** created for portfolio and educational purposes. It does not contain proprietary Flipkart customer or transaction data.

---

## 🚀 Project Overview

E-commerce businesses generate large volumes of transactional data. Converting this data into actionable business insights can help organizations improve:

- Sales performance
- Profitability
- Customer retention
- Product strategy
- Return management
- Regional performance
- Operational efficiency

This project demonstrates a complete analytics workflow, starting from **data generation and cleaning in Python**, followed by **SQL analysis and exploratory data analysis**, and finally an interactive **Power BI business intelligence dashboard**.

---

## 🎯 Business Objectives

The main objectives of this project are:

1. Analyze overall sales and profitability.
2. Identify high-performing categories and products.
3. Analyze monthly sales trends.
4. Understand customer purchasing behavior.
5. Identify repeat and loyal customers.
6. Analyze product and category return rates.
7. Identify major return reasons.
8. Compare sales and profitability across Indian states and regions.
9. Analyze the relationship between discounts and profitability.
10. Build an interactive executive dashboard for business decision-making.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Data generation, cleaning & analysis |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Faker | Synthetic customer data generation |
| Matplotlib | Data visualization |
| SQLite | SQL-based analytics |
| SQL | Business analysis & KPI queries |
| Power BI | Interactive dashboard |
| DAX | Measures & calculations |
| GitHub | Project version control |

---

# 📁 Project Workflow

```text
Synthetic Data Generation
        ↓
Data Cleaning & Validation
        ↓
Feature Engineering
        ↓
SQL Business Analysis
        ↓
Exploratory Data Analysis
        ↓
Star Schema Data Modeling
        ↓
DAX Measures
        ↓
Power BI Dashboard
        ↓
Business Insights & Recommendations
````

---

# 📦 Dataset

The project contains approximately:

* **50,000 orders**
* **12,000 customers**
* **6 major product categories**
* Multiple Indian states and regions
* Order data covering **2024–2025**

### Major Dataset Fields

```text
Order_ID
Customer_ID
Product_ID
Order_Date
Customer_Name
Age
Gender
City
State
Region
Category
Sub_Category
Product_Name
Quantity
Unit_Price
Discount_Percent
Sales_Amount
Cost_Amount
Profit
Payment_Method
Order_Status
Delivery_Days
Return_Flag
Return_Date
Return_Reason
Refund_Amount
Return_Cost
Customer_Rating
Net_Sales
Net_Profit
```

---

# 🧹 Data Cleaning & Preparation

Data quality checks were performed using Python and Pandas.

### Cleaning activities included:

* Duplicate order detection
* Missing value analysis
* Data type validation
* Negative value detection
* Quantity validation
* Discount validation
* Customer age validation
* Customer rating validation
* Delivery time validation
* Return-date validation
* Sales calculation validation
* Profit calculation validation
* Standardization of column names

Example:

```python
df_clean.columns = (
    df_clean.columns.str.strip()
    .str.lower()
    .str.replace(" ", "_")
)
```

---

# ⚙️ Feature Engineering

Additional analytical features were created:

```text
Order Year
Order Month
Order Month Name
Order Quarter
Order Year-Month
Profit Margin
Return Rate
```

These features were used for time-series analysis and Power BI reporting.

---

# 🗄️ SQL Analysis

SQLite was used to perform business-oriented SQL analysis.

### Key SQL analyses included:

* Overall sales and profit
* Monthly sales trends
* Category performance
* Product performance
* Top customers
* State performance
* Return rate by category
* Return reasons
* High-sales/high-return products
* Payment method analysis
* Order status analysis

Example business question:

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

# 📊 Exploratory Data Analysis

Python-based EDA was performed to identify important business patterns.

### Analyses included:

* Sales trend analysis
* Category sales and profit
* Top-performing products
* State-level performance
* Return-rate analysis
* Return-reason analysis
* Customer ratings
* Discount vs. profit
* Customer purchase frequency
* Customer segmentation

---

# 👥 Customer Segmentation

Customers were classified based on purchasing frequency.

### Customer Segments

| Segment  | Definition                    |
| -------- | ----------------------------- |
| One-Time | Purchased once                |
| Repeat   | Purchased more than once      |
| Loyal    | Frequent/high-value customers |

This segmentation helps identify customers who may benefit from:

* Loyalty programs
* Personalized offers
* Retention campaigns
* Cross-selling
* Upselling

---

# 🧩 Power BI Data Model

A **Star Schema** was implemented in Power BI.

### Fact Table

```text
Fact_Orders
```

### Dimension Tables

```text
Dim_Customer
Dim_Product
Dim_Geography
Dim_Date
```

### Model Structure

```text
             Dim_Customer
                  │
                  │
Dim_Product ─── Fact_Orders ─── Dim_Geography
                  │
                  │
              Dim_Date
```

Relationships:

```text
Dim_Customer[customer_id]
        1 ─────── *

Fact_Orders[customer_id]


Dim_Product[product_id]
        1 ─────── *

Fact_Orders[product_id]


Dim_Geography[geography_id]
        1 ─────── *

Fact_Orders[geography_id]


Dim_Date[Date]
        1 ─────── *

Fact_Orders[order_date]
```

---

# 📈 Power BI Dashboard

The Power BI report contains five analytical pages.

## 1️⃣ Executive Overview

Provides a high-level view of business performance.

### KPIs

* Total Sales
* Net Sales
* Total Profit
* Net Profit
* Total Orders
* Total Customers
* Return Rate
* Average Order Value

### Visuals

* Monthly Sales Performance
* Sales by Category
* Top Products
* State Performance
* Order Status
* Interactive slicers

---

## 2️⃣ Sales & Product Intelligence

Analyzes product and category performance.

### Key Metrics

* Sales
* Profit
* Profit Margin
* Units Sold

### Analysis

* Revenue by Category
* Profit by Category
* Product Performance
* Discount vs Profit
* Top Products
* Category profitability

---

## 3️⃣ Customer Intelligence

Analyzes customer purchasing behavior.

### Key Metrics

* Total Customers
* Repeat Customers
* Repeat Customer Rate
* Average Order Value

### Analysis

* Customer Segments
* Top Customers
* Purchase Frequency
* Customer Value
* Repeat customer behavior

---

## 4️⃣ Returns Intelligence

Focuses on product returns and their financial impact.

### Key Metrics

* Returned Orders
* Return Rate
* Total Refunds
* Total Return Cost

### Analysis

* Return Reasons
* Return Rate by Category
* Products with High Return Rates
* Sales vs Return Rate
* Financial impact of returns

---

## 5️⃣ Geographic Intelligence

Analyzes business performance across India.

### Analysis

* State-level Sales
* State-level Profit
* Regional Sales
* Regional Profit
* State Return Rate
* Regional performance comparison

---

# 🧮 DAX Measures

Important Power BI measures created in the project include:

```DAX
Total Sales =
SUM(Fact_Orders[sales_amount])
```

```DAX
Net Sales =
SUM(Fact_Orders[net_sales])
```

```DAX
Total Profit =
SUM(Fact_Orders[profit])
```

```DAX
Net Profit =
SUM(Fact_Orders[net_profit])
```

```DAX
Total Orders =
DISTINCTCOUNT(Fact_Orders[order_id])
```

```DAX
Total Customers =
DISTINCTCOUNT(Fact_Orders[customer_id])
```

```DAX
Units Sold =
SUM(Fact_Orders[quantity])
```

```DAX
Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Orders]
)
```

```DAX
Returned Orders =
CALCULATE(
    [Total Orders],
    Fact_Orders[return_flag] = 1
)
```

```DAX
Return Rate =
DIVIDE(
    [Returned Orders],
    [Total Orders]
)
```

```DAX
Total Refunds =
SUM(Fact_Orders[refund_amount])
```

```DAX
Total Return Cost =
SUM(Fact_Orders[return_cost])
```

```DAX
Profit Margin =
DIVIDE(
    [Total Profit],
    [Total Sales]
)
```

```DAX
Repeat Customers =
COUNTROWS(
    FILTER(
        VALUES(Dim_Customer[customer_id]),
        CALCULATE(
            DISTINCTCOUNT(Fact_Orders[order_id])
        ) > 1
    )
)
```

```DAX
Repeat Customer Rate =
DIVIDE(
    [Repeat Customers],
    [Total Customers]
)
```

---

# 💡 Key Business Insights

The analysis can be used to identify:

### 📈 Sales

* Monthly sales trends and seasonality
* Best-performing product categories
* Top revenue-generating products
* High-value customer segments

### 💰 Profitability

* Most profitable categories
* Products generating strong margins
* Impact of discounts on profit
* Difference between gross and net profitability

### 👥 Customers

* One-time vs repeat customers
* Customer purchase frequency
* High-value customers
* Customer retention opportunities

### 🔄 Returns

* Categories with higher return rates
* Major return reasons
* Products with high sales but high returns
* Financial impact of refunds and return costs

### 🌎 Geography

* Top-performing states
* Regional sales contribution
* Regional profitability
* Geographic return patterns

---

# 📌 Business Recommendations

Based on the analytical framework, businesses can consider:

### 1. Improve Customer Retention

Develop loyalty programs and personalized campaigns for repeat and high-value customers.

### 2. Optimize Discounts

Avoid excessive discounting on products where discounts significantly reduce profit margins.

### 3. Reduce Product Returns

Investigate products and categories with unusually high return rates and identify the underlying causes.

### 4. Improve Product Strategy

Prioritize high-revenue and high-margin products while reviewing low-performing products.

### 5. Regional Optimization

Focus marketing and inventory strategies on high-performing regions while investigating underperforming markets.

### 6. Monitor Net Profit

Track refunds and return costs alongside sales to understand the true financial performance of the business.

---

# 📂 Project Structure

```text
flipkart-ecommerce-sales-customer-analytics/
│
├── data/
│   ├── raw/
│   └── cleaned/
│
├── notebooks/
│   └── ecommerce_analysis.ipynb
│
├── sql/
│   └── ecommerce_analysis.sql
│
├── powerbi/
│   └── ecommerce_dashboard.pbix
│
├── images/
│   └── dashboard_screenshots/
│
├── README.md
│
└── requirements.txt
```

---

# 📋 Requirements

Install the required Python libraries:

```bash
pip install pandas numpy matplotlib faker
```

SQLite is used for SQL analysis.

---

# ▶️ How to Run the Project

### Step 1 — Clone the repository

```bash
git clone https://github.com/<your-username>/flipkart-ecommerce-sales-customer-analytics.git
```

### Step 2 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 3 — Open the notebook

Open:

```text
notebooks/ecommerce_analysis.ipynb
```

### Step 4 — Run the Python workflow

The notebook covers:

```text
Data Generation
      ↓
Data Cleaning
      ↓
Feature Engineering
      ↓
EDA
      ↓
SQL Analysis
```

### Step 5 — Open Power BI

Open:

```text
powerbi/ecommerce_dashboard.pbix
```

Load the prepared dimension and fact tables and explore the interactive dashboard.

---

# 📸 Dashboard Preview

Add your Power BI screenshots here:

```markdown
![Executive Overview](images/dashboard_screenshots/executive_overview.png)

![Sales & Product](images/dashboard_screenshots/sales_product.png)

![Customer Intelligence](images/dashboard_screenshots/customer_intelligence.png)

![Returns Intelligence](images/dashboard_screenshots/returns_intelligence.png)

![Geographic Intelligence](images/dashboard_screenshots/geographic_intelligence.png)
```

---

# 🎓 Skills Demonstrated

This project demonstrates practical skills in:

### Data Analytics

* Data cleaning
* Data validation
* Exploratory data analysis
* KPI development
* Business analysis

### Python

* Pandas
* NumPy
* Matplotlib
* Faker
* Feature engineering

### SQL

* Aggregations
* GROUP BY
* ORDER BY
* Filtering
* Business KPI analysis
* Trend analysis
* Customer analysis

### Power BI

* Data modeling
* Star schema
* DAX
* KPI cards
* Slicers
* Interactive dashboards
* Drill-through analysis
* Business storytelling

### Business Intelligence

* Sales analysis
* Profitability analysis
* Customer analytics
* Product analytics
* Returns analytics
* Geographic analytics

---

# 📊 Project Highlights

```text
50,000+ Orders
12,000 Customers
2024–2025 Transaction Period
6 Major Product Categories
Multiple Indian States & Regions
5-Page Power BI Dashboard
Star Schema Data Model
SQL Business Analysis
Python EDA
DAX KPI Measures
```

---

# 🔮 Future Improvements

Potential extensions include:

* Customer Lifetime Value (CLV)
* RFM customer segmentation
* Sales forecasting
* Return prediction
* Customer churn prediction
* Product recommendation system
* Advanced cohort analysis
* Automated Power BI refresh
* Real-time e-commerce analytics
* Machine learning-based demand forecasting

---

# 👨‍💻 Author

**Siva Prasad**

Data Analyst | Python | SQL | Power BI | Data Science

---

# ⭐ Project Purpose

This project was created as a **Data Analyst portfolio project** to demonstrate an end-to-end approach to transforming raw e-commerce data into actionable business insights using Python, SQL, and Power BI.

If you find this project useful, feel free to ⭐ the repository.

````

### Recommended `requirements.txt`

Create a file named **`requirements.txt`**:

```text
pandas
numpy
matplotlib
faker
````

### One important thing before pushing

Since your dataset is **simulated**, keep the wording **“simulated Flipkart-style dataset”** in the README. This makes the project professional and transparent rather than implying you had access to real Flipkart internal data.
