# Reatail Sales Analysis SQL Project
## Project Overview
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyse retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. 
## Objective
- Create and populate a retail sales database with the provided sales data.
- Identify and remove any records with missing or null values.
- Perform basic exploratory data analysis to understand the dataset.
- Use SQL to answer specific business questions and derive insights from the sales data.
## Dataset
<a href="https://github.com/mamatha203/Reatail-Sales-Analysis-SQL-Project/blob/main/Retail%20Sales%20Analysis.csv">Dataset</a>
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
```
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
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```
## Schema
### 1.Write a SQL query to retrieve all columns for sales made on '2022-11-05?
```sql
select * 
from retail_sales 
where sale_date = '2022-11-05';
```
### 2.Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022?
```sql
select * 
from retail_sales
where category = 'Clothing' 
and 
to_char(sale_date,'yyyy-mm')='2022-11' and quantiy >= 4;
```
### 3.Write a SQL query to calculate the total sales,total orders for each category?
```sql
select category,
sum(total_sale)as Total_sales,
count(*)as total_orders
from retail_sales
group by category;
```
### 4.Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category?
```sql
select 
round(avg(age),2) as Average_age 
from retail_sales
where category = 'Beauty';
```
### 5.Write a SQL query to find all transactions where the total_sale is greater than 1000?
```sql
select * 
from retail_sales
where total_sale>=1000;
```
### 6.Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category?
```sql
select 
category,
gender,
count(transactions_id)as Total_transactions
from retail_sales
group 
by 1,2
order by 1;
```
### 7.Write a SQL query to calculate the average sale for each month. Find out best selling month in each year?
```sql
select 
yearname,
monthname,
Avg_sale
from
(
select
extract(year from sale_date) as Yearname,
extract(month from sale_date) as monthname,
avg(total_sale) as Avg_sale,
rank()over(partition by extract(year from sale_date) order by avg(total_sale) desc)as rank
from retail_sales
group by 1,2) as t1
where rank=1;
```
### 8.Write a SQL query to find the top 5 customers based on the highest total sales?
```sql
select customer_id,
sum(total_sale)as highest_sales
from retail_sales
group by 1
order by 2 desc
limit 5;
```
### 9.Write a SQL query to find the number of unique customers who purchased items from each category?
```sql
select 
category,
count(distinct customer_id) as unique_customer
from retail_sales
group by 1;
```
### 10.Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)?
```sql
with hourly_sale
as(
select *,
case
when extract(hour from sale_time)<12  then 'Morning'
when extract(hour from sale_time)between 12 and 17 then 'Afternoon'
else 'evening'
end as shift
from retail_sales
)
select shift,
count(*)as Total_orders 
from hourly_sale 
group by shift;
```
## Findings
- The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- Monthly analysis shows variations in sales, helping identify peak seasons.
- The analysis identifies the top-spending customers and the most popular product categories.
## Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.





