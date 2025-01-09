Project Title: Retail Sales Data Analysis Using SQL
Project Objective:
This project aims to analyze retail sales data using SQL queries to uncover meaningful business insights. The analysis includes cleaning the data, exploring key metrics, and addressing specific business queries such as customer trends, product category performance, and time-based sales patterns.

Database Schema
sql
Copy code
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(15),
    quantiy INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
Key Tasks and Solutions
1. Data Cleaning
Purpose: To ensure the data is consistent and reliable for analysis.

sql
Copy code
-- Identify missing values in specific columns
SELECT * FROM retail_sales WHERE transactions_id IS NULL;

-- Identify all rows with any NULL values
SELECT * FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR gender IS NULL
   OR category IS NULL
   OR quantiy IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;

-- Delete rows with NULL values
DELETE FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR gender IS NULL
   OR category IS NULL
   OR quantiy IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
2. Data Exploration
Key metrics like total sales, unique customers, and categories are computed to establish foundational insights.

sql
Copy code
-- Total number of sales
SELECT COUNT(*) AS total_sales FROM retail_sales;

-- Number of unique customers
SELECT COUNT(DISTINCT customer_id) AS total_customers FROM retail_sales;

-- Categories available in the data
SELECT DISTINCT category FROM retail_sales;
3. Business Queries
Q1: Retrieve sales made on a specific date ('2023-05-15').

sql
Copy code
SELECT * FROM retail_sales
WHERE sale_date = '2023-05-15';
Q2: Transactions in 'Clothing' category with quantity > 4 during Nov-2022.

sql
Copy code
SELECT * FROM retail_sales
WHERE category = 'Clothing' 
  AND quantiy > 4
  AND sale_date BETWEEN '2022-11-01' AND '2022-11-30';
Q3: Total sales by category.

sql
Copy code
SELECT category, SUM(total_sale) AS net_sales
FROM retail_sales
GROUP BY category;
Q4: Average age of customers who purchased from the 'Beauty' category.

sql
Copy code
SELECT ROUND(AVG(age), 2) AS average_age
FROM retail_sales
WHERE category = 'Beauty';
Q5: Transactions with total_sale > 1000.

sql
Copy code
SELECT * FROM retail_sales
WHERE total_sale > 1000;
Q6: Total transactions by gender and category.

sql
Copy code
SELECT gender, category, COUNT(transactions_id) AS total_transactions
FROM retail_sales
GROUP BY gender, category
ORDER BY gender, category;
Q7: Average sales for each month and identifying the best-selling month.

sql
Copy code
SELECT 
    EXTRACT(YEAR FROM sale_date) AS year, 
    EXTRACT(MONTH FROM sale_date) AS month, 
    AVG(total_sale) AS avg_sale
FROM retail_sales
GROUP BY year, month
ORDER BY avg_sale DESC;
Q8: Top 5 customers based on total sales.

sql
Copy code
SELECT customer_id, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
Q9: Unique customers per category.

sql
Copy code
SELECT category, COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
Q10: Total sales by product category.

sql
Copy code
SELECT category, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY category
ORDER BY total_sales DESC;
Q11: Average age of customers by category.

sql
Copy code
SELECT category, AVG(age) AS average_age
FROM retail_sales
GROUP BY category
ORDER BY average_age DESC;
Q12: Total sales by gender.

sql
Copy code
SELECT gender, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY gender;
Q13: Monthly total sales for 2023.

sql
Copy code
SELECT EXTRACT(MONTH FROM sale_date) AS month, SUM(total_sale) AS total_sales
FROM retail_sales
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY month
ORDER BY month;
Q14: Month with the highest total sales in 2023.

sql
Copy code
SELECT EXTRACT(MONTH FROM sale_date) AS month, SUM(total_sale) AS total_sales
FROM retail_sales
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY month
ORDER BY total_sales DESC
LIMIT 1;
Q15: Daily total sales.

sql
Copy code
SELECT sale_date, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY sale_date
ORDER BY sale_date;
Q16: Transactions in 'Electronics' by customers aged 30-40.

sql
Copy code
SELECT * FROM retail_sales
WHERE category = 'Electronics' AND age BETWEEN 30 AND 40;
Q17: Total sales by gender and category.

sql
Copy code
SELECT gender, category, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY gender, category;
Q18: Transaction with the highest total sale.

sql
Copy code
SELECT * FROM retail_sales
ORDER BY total_sale DESC
LIMIT 1;
Q19: Total transactions per month in 2023.

sql
Copy code
SELECT EXTRACT(MONTH FROM sale_date) AS month, COUNT(transactions_id) AS total_transactions
FROM retail_sales
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY month
ORDER BY month;
Insights and Deliverables
Key Insights: Identified top-performing categories, peak sales months, and customer demographics.
Visualizations: Suggestions for converting these queries into Power BI visualizations include sales heatmaps, customer demographic distributions, and monthly sales trend charts.
This SQL project is a comprehensive approach to understanding retail sales data and provides actionable insights for business decision-making.






