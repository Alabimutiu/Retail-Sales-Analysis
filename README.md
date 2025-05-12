# Retail-Sales-Analysis
Retail Sales Analysis SQL Project
Project Overview
Project Title: Retail Sales Analysis
Level: Beginner
Database: p1_retail_db

Project Overview: Retail Sales Data Analysis Using SQL
This project highlights core SQL skills used in data analysis, focusing on retail sales data. It involves setting up a relational database, performing exploratory data analysis (EDA), and writing SQL queries to answer targeted business questions. Key tasks include data cleaning, trend analysis, and deriving insights to support decision-making. Ideal for entry-level analysts, this project demonstrates a practical understanding of SQL in a business context and builds a strong foundation for more advanced analytical work.

Objectives
Key Components:
Database Setup: Designed and populated a relational retail sales database using provided sales data.
Data Cleaning: Identified and removed records with missing or null values to ensure data quality and accuracy.
Exploratory Data Analysis (EDA): Conducted initial analysis to explore data distribution, key variables, and overall structure.
Business Analysis: Wrote SQL queries to answer specific business questions, such as identifying top-performing products, analyzing sales trends, and evaluating regional performance.
Project Structure

1. Database Setup
Database Creation: The project starts by creating a database named p1_retail_db.
Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

CREATE DATABASE sql_project_p1;

CREATE TABLE retail_sales
(
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
2. Data Exploration & Cleaning

Total Records: Calculated the total number of entries in the dataset to understand its size.
Unique Customers: Identified the total number of distinct customers to gauge customer base size.
Product Categories: Extracted all unique product categories to understand the range of offerings.
Data Quality Check: Detected and removed records containing null or missing values to ensure clean, reliable data.

SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

3. Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:

**Write a SQL query to retrieve all columns for sales made on '2022-11-05:
***sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
***

**Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022:
***sql
SELECT *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantiy >= 4;
***
**Write a SQL query to calculate the total sales (total_sale) for each category.:
***sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
***

**Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:
***sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
***

**Write a SQL query to find all transactions where the total_sale is greater than 1000.:
***sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
***

**Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:
***sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    category,
    gender
ORDER BY 1
***

**Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
***sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1  
***

**Write a SQL query to find the top 5 customers based on the highest total sales :
***sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
***

**Write a SQL query to find the number of unique customers who purchased items from each category.:
***sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
***

**Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):
***sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
***

Findings
Key Insights:

Customer Demographics: The dataset captures a diverse customer base across various age groups, with purchases spanning multiple categories, including Clothing and Beauty.
High-Value Transactions: A number of transactions exceeded $1,000, highlighting segments of premium customer activity.
Sales Trends: Monthly sales analysis revealed fluctuations, helping to identify peak sales periods and seasonal trends.
Customer Behavior: Analysis pinpointed top-spending customers and highlighted the most popular product categories.
Reports Delivered:
Sales Summary Report: Provided a comprehensive overview of total sales, customer profiles, and category performance.
Trend Analysis Report: Uncovered monthly sales patterns and shifts, useful for forecasting and planning.
Customer Insights Report: Highlighted high-value customers and tracked unique customer counts across product categories.

Conclusion:
This project offers a hands-on introduction to SQL in a business context, covering essential tasks such as database setup, data cleaning, exploratory data analysis, and business-oriented querying. The insights derived support strategic decision-making by revealing sales patterns, customer preferences, and product performance across the retail landscape.


How to Use
Clone the Repository: Clone this project repository from GitHub.
Set Up the Database: Run the SQL scripts provided in the database_setup.sql file to create and populate the database.
Run the Queries: Use the SQL queries provided in the analysis_queries.sql file to perform your analysis.
Explore and Modify: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.
Author - Mutiu Sulaimon
This portfolio project showcases my proficiency in SQL, a key skill for data analyst positions.

Stay Updated and Join the Community
For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

YouTube: Subscribe to my channel for tutorials and insights
Instagram: Follow me for daily tips and updates
LinkedIn: Connect with me professionally
Discord: Join our community to learn and grow together
Thank you for your support, and I look forward to connecting with you!
