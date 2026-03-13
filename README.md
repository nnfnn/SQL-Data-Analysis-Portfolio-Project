Retail Sales Analysis using SQL
Project Overview

Project Title: Retail Sales Analysis
Skill Level: Beginner
Tools Used: SQL, PostgreSQL / MySQL

This project demonstrates how SQL can be used to analyze retail sales data and generate business insights. The goal of the project is to practice key SQL concepts such as database creation, data cleaning, exploratory data analysis (EDA), and answering real business questions using SQL queries.

The dataset contains retail transaction details including customer demographics, product categories, sales quantity, and revenue. By analyzing this data, meaningful insights about customer behavior and sales performance can be identified.

Project Objectives

The main objectives of this project are:

Database Setup
Create a retail sales database and define the required table structure.

Data Cleaning
Identify missing or null values and remove incomplete records to maintain data quality.

Exploratory Data Analysis (EDA)
Explore the dataset to understand customer distribution, product categories, and transaction patterns.

Business Analysis
Use SQL queries to answer business questions and extract actionable insights from the data.

Database Setup

The first step is creating a database and a table to store retail sales information.

CREATE DATABASE p1_retail_db;

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

This table stores information related to each retail transaction including product category, customer details, quantity purchased, and total sales amount.

Data Exploration and Cleaning

Before performing analysis, the dataset was explored to understand its structure and ensure data quality.

Total Records in Dataset
SELECT COUNT(*) FROM retail_sales;
Total Unique Customers
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
Unique Product Categories
SELECT DISTINCT category FROM retail_sales;
Check for Missing Values
SELECT *
FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
Remove Records with Missing Values
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

Data cleaning ensures that further analysis is based on accurate and complete information.

Data Analysis and Business Questions

The following SQL queries were used to analyze the dataset and answer different business questions.

1. Retrieve All Sales Made on a Specific Date
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
2. Transactions for Clothing Category in November 2022 with Quantity Greater Than 4
SELECT *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND quantity >= 4;
3. Total Sales for Each Product Category
SELECT 
    category,
    SUM(total_sale) AS net_sales,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
4. Average Age of Customers Buying Beauty Products
SELECT
    ROUND(AVG(age),2) AS avg_customer_age
FROM retail_sales
WHERE category = 'Beauty';
5. Transactions Where Sales Value Exceeds 1000
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
6. Number of Transactions by Gender in Each Category
SELECT
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
7. Best Selling Month Each Year Based on Average Sales
SELECT
    year,
    month,
    avg_sale
FROM
(
SELECT
    EXTRACT(YEAR FROM sale_date) AS year,
    EXTRACT(MONTH FROM sale_date) AS month,
    AVG(total_sale) AS avg_sale,
    RANK() OVER(
        PARTITION BY EXTRACT(YEAR FROM sale_date)
        ORDER BY AVG(total_sale) DESC
    ) AS rank
FROM retail_sales
GROUP BY 1,2
) AS ranked_sales
WHERE rank = 1;
8. Top 5 Customers Based on Total Sales
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
9. Number of Unique Customers per Category
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
10. Sales Distribution by Time of Day
WITH hourly_sales AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END AS shift
FROM retail_sales
)

SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
Key Insights

Some insights obtained from the analysis include:

Retail transactions are distributed across multiple product categories such as Clothing and Beauty.

Certain transactions have significantly higher sales values, indicating premium purchases.

Sales vary across different months, helping identify potential seasonal trends.

Customer purchase behavior differs across time periods such as morning, afternoon, and evening.

A small group of customers contribute significantly to total sales.

Project Summary

This project demonstrates the use of SQL for:

Database creation and table design

Data cleaning and validation

Exploratory data analysis

Business-driven data analysis

It highlights how SQL can be used to transform raw transactional data into meaningful insights that can support business decision-making.

How to Use This Project

Clone the repository from GitHub.

Create the database using the provided SQL script.

Import the dataset into the retail_sales table.

Run the analysis queries to explore the data and generate insights.

Author

Muhammed Nifan

This project is part of my Data Analyst portfolio, where I showcase skills in SQL, data analysis, and business insight generation.
