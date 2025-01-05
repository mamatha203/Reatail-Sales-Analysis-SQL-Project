# Reatail Sales Analysis SQL Project
## Project Overview
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyse retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. 
## Objective
- Create and populate a retail sales database with the provided sales data.
- Identify and remove any records with missing or null values.
- Perform basic exploratory data analysis to understand the dataset.
- Use SQL to answer specific business questions and derive insights from the sales data.
## Database setup
- The project starts by creating a database named retail_db.
- A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quanty sold, price per unit, cost of goods sold (COGS), and total sale amount.
 ```sql
 CREATE TABLE retail_sales
 (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantiy INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
 );

## Data Exploration & Cleaning
- Determine the total number of records in the dataset.
- Find out how many unique customers are in the dataset.
- Identify all unique product categories in the dataset.
- Check for any null values in the dataset and delete records with missing data.

```sql
SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantiy IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

## 1.Write a SQL query to retrieve all columns for sales made on '2022-11-05'?
```sql
SELECT * FROM RetailSales;






