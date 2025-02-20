# SQL Project Ecommerce
## Project Overview
#### **Project's Titles** : `SQL Project E-commerce`
#### **Database** : `project_ecommerce`
#### **Tables** : `ecommerce_project5`
This project aims to demonstrate SQL skills and techniques in data analysis specifically to explore, clean, and analyze online sales data. The project consisted of setting up a online sales database, performing exploratory data analysis (EDA), and answering business questions through specific SQL queries.
## Project Objectives
#### 1) Set Up the Database :
Prepare a database for this project from previously available data
#### 2) Data Cleaning 
identify and delete null,missing values or duplicate data from database
#### 3) Exploratory Data Analysis (EDA) 
carry out data exploration to better understand the dataset
#### 4) Business Question Analysis
Using SQL queries to answer several business questions related to this retail sales project

## STRUCTURE 
### 1) DATABASE and TABLE SET UP
+ **Database Creation** : The first step to start this project is create the database entitled **`project_ecommerce`**
+ **Tables Creation** : The table used in this project is entitled **`ecommerce_project5`** which consists of several columns, such as product_id,product_name ,category ,price ,discount ,tax_rate ,stock_level,supplier_id,customer_age_group,customer_location,customer_gender ,shipping_cost ,shipping_method,return_rate ,seasonality,popularity_index

```sql
Create Database project_ecommerce;
Create table ecommerce_project5
(product_id varchar(10),
product_name varchar(100),
category varchar(50),
price numeric(10,2),
discount int,
tax_rate int,
stock_level int,
supplier_id varchar (100),
customer_age_group varchar(100),
customer_location varchar(100),
customer_gender varchar(100),
shipping_cost numeric(10,2),
shipping_method varchar(100),
return_rate numeric(10,2),
seasonality varchar(10),
popularity_index int
)
```
### 2) Check Is There Null Values 
**Cleaning Data** : Find the null values from dataset and remove them.
```sql
select* from ecommerce_project5;
select count(*) is null from ecommerce_project5;
```
## 3) EDA and Project's Insight
This process is carried out by answering several questions related to the dataset with the aim of deepening understanding regarding the dataset
### Task 1. Display all products with prices above 500 and discounts more than 10%
```sql
select product_name, category
from 
ecommerce_project5
where price >500 and discount > 10
group by product_name,category;
```
### Task 2.Take the 5 products with the highest return rate
```sql
select product_name, category, return_rate from ecommerce_project5
order by return_rate desc
limit 5;
```

### Task 3.Search for all products in the 'Electronics' category with less than 100 in stock.
```sql
select product_name,category,stock_level
from ecommerce_project5
where category ='Electronics' and stock_level <100;
```

### Task 4.count the number of products in each category
```sql
select count(*) as total_product,category
from ecommerce_project5
group by category
order by total_product desc;
```

### Task 5.Show average price and average discount for each category
```sql
select category, 
avg(price) as average_price,
avg(discount) as average_discount
from ecommerce_project5 
group by category;
```

### Task 6. Look for categories that have an average return rate of more than 4%
```sql
select category,avg(return_rate) as avg_return_rate
from ecommerce_project5
group by category
having avg(return_rate)>4;
```

### Taks 7.Look for suppliers who provide products at the highest prices
```sql
select supplier_id,product_name, category, price
from ecommerce_project5
where price =(select max(price) from ecommerce_project5);
```

### Task 8.display products with a return rate higher than the average return rate of all products.
```sql
SELECT return_rate, product_name, avg(return_rate) as avg_return_rate
from ecommerce_project5
where return_rate > (select avg(return_rate) from ecommerce_project5);
```
### Task 9. Create a new column to categorize products by price:
+ 'Low' for prices < 100
+ 'Medium' for prices 100 - 500
+ 'High' for prices > 500
```sql
select product_name, price,
CASE
	WHEN price < 100 then 'Low'
    WHEN price BETWEEN 100 AND 500 then 'Medium'
    ELSE 'High'
END as Price_category

from ecommerce_project5;
```

### Task 10. Use the Window Function to display product rankings based on popularity in each category.
```sql
select product_name, category, popularity_index,
	RANK() over(partition by category order by popularity_index desc) as rank_popularity
FROM ecommerce_project5;
```

### Task 11. Determine the best-selling products based on season
```sql
select product_name, category, seasonality, popularity_index
from
(select product_name, category, seasonality, popularity_index,
ROW_NUMBER() over(partition by category order by popularity_index desc) as row_popularity
from ecommerce_project5) ranked_product
where row_popularity = 1;
```
### Task 12. Analyze the Effectiveness of Discounts
+ Look for categories with the highest average return rates, but only for categories that provide an average discount of more than 10%.

```sql
select category, avg(discount) as avg_discount, avg(return_rate) as avg_return_rate
from ecommerce_project5
group by category
having avg(discount) > 10
order by avg_return_rate desc;
```

### Task 13.Customer Insights: Age and Gender Segmentation Analysis
+ Calculate total transactions per age group and gender, then sort by highest total transaction price.
```sql
select customer_age_group,customer_gender, sum(price) as total_price
from ecommerce_project5
group by 2,1
order by total_price desc;
```

## CONCLUSION
This project is a form of direct application of the use of SQL for data analysis which consists of creating databases and tables, cleaning data, exploring and analyzing data, and answering several business questions using SQL queries. Through this project, it is hoped that we can improve our ability to process data using SQL and can help businesses make better decisions.

## AUTHOR - PUTU ARISMADI
This project is one of the projects I worked on to enhance my data analysis and processing skills using SQL.
For more information about me or if you're interested in connecting, feel free to reach out to me via:
+ LinkedIn: [Connect me in Linkedin](https://www.linkedin.com/in/putu-arismadi-103223223/)
+ Instagram: [Follow me in Instagram](https://www.instagram.com/arismadi._?igsh=MTVzdDFsZzQyaHpwbQ==)




