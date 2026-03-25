Retail Sales Analysis using SQL
Project Overview

Project Title: Retail Sales Analysis
Tools Used: SQL, PostgreSQL / MySQL

In this project, I used SQL to analyze retail sales data and generate meaningful business insights. My main goal was to strengthen my understanding of core SQL concepts such as database creation, data cleaning, exploratory data analysis (EDA), and solving real-world business problems using queries.

The dataset I worked on includes retail transaction details such as customer demographics, product categories, sales quantity, and revenue. By analyzing this data, I was able to identify patterns in customer behavior and evaluate overall sales performance.

Project Objectives

Through this project, I focused on:

Database Setup:
I created a retail sales database and defined the table structure.
Data Cleaning:
I identified missing/null values and removed incomplete records to ensure data accuracy.
Exploratory Data Analysis (EDA):
I explored the dataset to understand customer distribution, product categories, and transaction trends.
Business Analysis:
I wrote SQL queries to answer business questions and extract actionable insights.
Database Setup

I started by creating the database and table:

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

This table stores detailed information about each transaction, including customer details, product category, and sales amount.

Data Exploration and Cleaning

Before analysis, I explored and cleaned the dataset:

Checked total records:
SELECT COUNT(*) FROM retail_sales;
Counted unique customers:
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
Identified product categories:
SELECT DISTINCT category FROM retail_sales;
Checked for missing values:
SELECT *
FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
Removed incomplete records:
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

This ensured that my analysis was based on clean and reliable data.

Data Analysis & Business Questions

I used SQL queries to answer key business questions:

Retrieved sales for a specific date
Analyzed clothing transactions in a specific month
Calculated total sales per category
Found average age of customers buying beauty products
Identified high-value transactions (>1000)
Compared transactions by gender across categories
Determined best-performing months using ranking
Identified top 5 customers by total spending
Calculated unique customers per category
Analyzed sales distribution by time of day
Key Insights

From my analysis, I discovered:

Sales are distributed across multiple categories like Clothing and Beauty
Some transactions contribute significantly higher revenue (premium purchases)
Monthly sales trends indicate possible seasonality
Customer buying behavior varies across different times of the day
A small group of customers contributes a large portion of total sales
Project Summary

Through this project, I demonstrated my ability to:

Design and create databases using SQL
Perform data cleaning and validation
Conduct exploratory data analysis
Solve business problems using SQL queries

This project shows how I can transform raw data into meaningful insights that support business decision-making.

How to Use This Project
Clone the repository from GitHub
Create the database using the SQL script
Import the dataset into the retail_sales table
Run the queries to generate insights
Author

Muhammed Nifan

This project is part of my Data Analyst portfolio, where I showcase my skills in SQL, data analysis, and deriving business insights from data.
