

---

# Sales Insights Data Analysis Project

## Project Overview
This project focuses on analyzing sales data to help the company understand its sales trends and make informed decisions. A Power BI dashboard was created to visualize key insights, with the aim of potentially increasing revenue by 7% in the next quarter.

## Table of Contents
- [Project Phases](#project-phases)
- [Technologies Used](#technologies-used)
- [Key Highlights](#key-highlights)
- [SQL Analysis](#sql-analysis)
- [Power BI Analysis](#power-bi-analysis)
- [Conclusion](#conclusion)

## Project Phases
1. **Requirement Gathering** - Identifying business needs and determining relevant metrics for sales analysis.
2. **Data Collection** - Gathering sales data from company databases.
3. **Data Processing** - Cleaning and structuring the data for effective analysis.
4. **Data Modeling** - Building data models to facilitate Power BI visualizations.
5. **Dashboard Building** - Designing a Power BI dashboard for interactive data exploration.
6. **Deployment** - Publishing the dashboard for use by stakeholders.

## Technologies Used
- **SQL** - Data extraction and transformation.
- **Power BI** - Data visualization and dashboard creation.

## Key Highlights
- Designed a Power BI dashboard to visualize sales trends and provide actionable insights.
- Enabled users to track sales patterns, allowing for informed business decisions.
- Projected revenue increase of at least 7% based on insights from the dashboard.

---

## SQL Analysis

Below are the SQL queries used to analyze the data:

### 1. Show all customer records
```sql
SELECT * FROM customers;
```

### 2. Show total number of customers
```sql
SELECT COUNT(*) FROM customers;
```

### 3. Show transactions for the Chennai market (market code for Chennai is `Mark001`)
```sql
SELECT * FROM transactions WHERE market_code = 'Mark001';
```

### 4. Show distinct product codes sold in Chennai
```sql
SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
```

### 5. Show transactions where the currency is US dollars
```sql
SELECT * FROM transactions WHERE currency = 'USD';
```

### 6. Show transactions in 2020 by joining with the date table
```sql
SELECT transactions.*, date.* 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020;
```

### 7. Show total revenue in the year 2020
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
  AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
```

### 8. Show total revenue in January 2020
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
  AND date.month_name = 'January' 
  AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
```

### 9. Show total revenue in 2020 for Chennai
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
  AND transactions.market_code = 'Mark001';
```

---

## Power BI Analysis

### Formula to Create `norm_amount` Column
The following formula is used to create a new column, `norm_amount`, in Power BI. It normalizes the sales amount based on the currency:

```plaintext
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount] * 75 else [sales_amount], type any)
```

This formula assumes a conversion rate of 1 USD = 75 INR.

---

## Conclusion
This project demonstrates how data analysis and visualization can provide valuable business insights. The Power BI dashboard created here effectively showcases sales trends, enabling data-driven decision-making. The analysis suggests that leveraging these insights can increase revenue by approximately 7% in the coming quarter. Future improvements could include integrating real-time data and predictive analytics to further enhance the dashboard’s utility.

---
