# Retail Sales Analysis with SQL

<img src="https://github.com/user-attachments/assets/4cfee941-fe2f-40f4-b448-503a192ac619" width="745" height="490" />


![Reatil](https://github.com/user-attachments/assets/4cfee941-fe2f-40f4-b448-503a192ac619)


## Project Overview

**Project Title:** Retail Sales Analysis  
**Database:** `Retail Sales Analysis_utf.csv`

This project demonstrates SQL proficiency and analytical techniques commonly applied by data analysts. It involves creating a retail sales database, performing exploratory data analysis (EDA), and addressing business questions using SQL queries. The project extracts insights related to sales trends, customer behavior, and product performance.

---

## Objectives

- **Database Setup**: Create and populate a retail sales database.
- **Data Cleaning**: Identify and remove null or missing records.
- **Exploratory Data Analysis**: Understand the structure and distribution of the dataset.
- **Business Analysis**: Use SQL to answer business questions and derive actionable insights.

---

## Project Structure

```
Retail_Sales_Analysis/
│
├── data/
│   └── retail_sales_data.csv        # Raw retail sales data
│
├── queries/
│   ├── data_cleaning.sql            # SQL for cleaning the dataset
│   ├── exploratory_analysis.sql     # SQL for basic EDA
│   └── business_analysis.sql        # SQL queries answering key business questions
│
├── reports/
│   ├── sales_summary_report.md      # Overview of sales performance
│   ├── trend_analysis_report.md     # Monthly sales trends
│   └── customer_insights_report.md  # Customer segmentation and top customer insights
│
└── README.md                        # Project documentation
```

---

## 1. Database Setup

```sql
CREATE DATABASE Retail_Sales_Analysis_with_SQL;

CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

## 2. Data Exploration & Cleaning

```sql
-- Record Count
SELECT COUNT(*) FROM retail_sales;

-- Unique Customers
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;

-- Category Count
SELECT DISTINCT category FROM retail_sales;

-- Null Value Check
SELECT * FROM retail_sales
WHERE transactions_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR age IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR price_per_unit IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;

-- Delete rows with critical nulls
DELETE FROM retail_sales
WHERE quantity IS NULL
    OR price_per_unit IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;

-- Impute missing age with median
WITH MedianCTE AS (
    SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY age) AS median_age
    FROM retail_sales
    WHERE age IS NOT NULL
)
UPDATE retail_sales
SET age = (SELECT median_age FROM MedianCTE LIMIT 1)
WHERE age IS NULL;
```

---

## 3. Dataset Exploration

- Total number of sales
- Unique customer count
- Product category distribution

```sql
SELECT COUNT(*) AS total_sales FROM retail_sales;

SELECT COUNT(DISTINCT customer_id) AS total_customers FROM retail_sales;

SELECT category, COUNT(*) AS total_count
FROM retail_sales
GROUP BY category
ORDER BY total_count DESC;
```

---

## 4. Business Queries

This section includes SQL queries for:

- Daily and filtered transactions
- Category performance
- Customer behavior
- Retention analysis
- Shift-based order segmentation
- Monthly growth trends
- Customer segmentation

All SQL queries are available in `business_analysis.sql` and include:

- Sales made on specific dates
- Clothing category filters
- Top 5 customers by total sales
- Average age by product category
- Gender-wise transactions per category
- Monthly trends and best-performing periods
- Customer segmentation logic and percentages
- Lifetime value (CLV) calculation

---

## Findings

### Customer Demographics

- Broad age range with top activity in Clothing and Beauty.

### High-Value Transactions

- Purchases above $1,000 indicate premium customers.

### Sales Trends

- Fluctuations observed, peak sales in early months.
- No sales growth throughout the year, indicating stagnation.

### Customer Insights

- Top 10 customers showed high lifetime value (up to $38,440).
- Segments:
  - High Spender & Frequent Buyer (19.35%)
  - Frequent Buyer (29.03%)
  - High Spender (20.65%)
  - Standard Customer (30.97%)

### Product Performance

- Clothing and Electronics dominate in both volume and revenue.

### Growth Analysis

- Sales growth rate was stagnant at 0% in all months of 2022.
- Indicates need for improved marketing or operational adjustments.

  ![image](https://github.com/user-attachments/assets/ce7c2d64-6da0-4510-ba83-c697ee5c8a72)


---

## Conclusion

This project showcases how SQL can be effectively used to analyze retail data by:

- Cleaning and preparing structured datasets
- Extracting customer and sales insights
- Identifying growth gaps and business opportunities

Key recommendations include investing in high-performing categories, leveraging customer segmentation for marketing, and addressing sales stagnation.

---

## Author

**Project By:** Akash Singh  
**Email:** [akash.singh@georgebrown.ca](mailto:akash.singh@georgebrown.ca)  
**LinkedIn:** (https://www.linkedin.com/in/akash-singh-979745147)    
**Project File:** [https://github.com/Singhakash9/Retail-Sales-Analysis-with-SQL/blob/main/SQL%20Retail%20Sales%20Analysis.sql)
