# MySQL-Global-Electronics-Retailer
This project analyses sales, profit, and customer trends using MySQL. The dataset covers various categories, subcategories, and store performances over multiple years.

# Data Background
The dataset includes:
•	Product categories and subcategories
•	Store performance
•	Customer purchase behavior
•	Regional distribution of sales
•	Annual sales and profit trends

# SQL Queries Used

# Customers Table
select*
From Customers;

# Order Number, Order Date, Delivery Date, Quantity, Currency Code
Select `Order Number`, `Order Date`, `Delivery Date`, `Quantity`, `Currency Code`
From Sales;

# Count Distinct Name
Select Count(distinct Name)
from customers;

# Cities of Italy
SELECT City
FROM customers
where Country = 'Italy';

# Home Appliances and Computers
select*
from products
where Category = 'Home Appliances' or 'Computers';

# State-wise Count of StoreKey
select State, Count(StoreKey)
from stores
Group by State
order by Count(StoreKey) Desc;

# Average Quantity
SELECT Avg(Quantity) from sales;

# Count_of_customers in Italian Cities
select City, Count(Name) as count_of_customers
from customers
where Country = 'Italy'
Group by City
Order by count_of_customers Desc
Limit 25;

# City wise Count of Customers in Italy
Select Country, City, count(Name) as Count_of_Customers
from customers
where Country = 'Italy'
Group by City
Having Count_of_Customers>2
Order by Count_of_Customers Desc;

# Product-Wise Quantity
Select ProductKey, count(Quantity) as Quantity_Count
From sales
group by ProductKey
order by Quantity_Count Desc;

# Count_of_Quantity Categorized
Select `Order Number`, count(Quantity) as Count_of_Quantity,
CASE
WHEN count(Quantity) < 2 then 'Low'
WHEN Count(Quantity) Between 3 and 5 then 'Medium'
ELSE 'High'
END
FROM sales
group by `Order Number`
order by Count_of_Quantity Desc;

# Joining
Select*
from sales
Join products on sales.ProductKey = products.ProductKey
Join customers on sales.CustomerKey = customers.CustomerKey
Join stores on sales.StoreKey = stores.StoreKey
Join exchange_rates on sales.`Order Date` = exchange_rates.Date;
