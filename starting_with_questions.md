Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT country, city, SUM(totaltransactionrevenue) Revenue
FROM all_sessions
    WHERE totaltransactionrevenue IS NOT NULL
	GROUP BY country, city
ORDER BY Revenue desc



SELECT country, city, SUM(totaltransactionrevenue) Revenue
FROM all_sessions
    WHERE totaltransactionrevenue IS NOT NULL
	GROUP BY country, city
ORDER BY Revenue desc


Answer:
USA has the highest transaction revenue on the site. Names of the first city is not given. San Francisco is 2nd and Sunnyvale is the 3rd city on the list.



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT country, city, AVG(total_ordered) AS Average_ProductQuantity
FROM products p
JOIN sales_report sr
ON p.SKU = sr.productsku
JOIN all_sessions al
ON al.productSKU = sr.productsku
GROUP by country, city
ORDER BY Average_ProductQuantity desc



Answer:
Average number of products ordered in different cities (and countries) varies with Saudi Arabia and Czechia being the topmost. Although US is closely following Saudi Arabia and Czechia, there are several cities in the US where the average order quantity is very low. 



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

WITH Table1 AS (
SELECT country, v2ProductCategory, SUM(total_ordered) AS TotalProductQuantity
FROM products p
JOIN sales_report sr
ON p.SKU = sr.productsku
JOIN all_sessions al
ON al.productSKU = sr.productsku
GROUP by country, v2ProductCategory
ORDER BY TotalProductQuantity desc
), Table2 AS (
SELECT country, MAX(TotalProductQuantity) Max
FROM Table1
GROUP BY country 
ORDER BY Max desc
)
SELECT Table1.country, v2ProductCategory, Table2.Max
FROM Table1, Table2
WHERE Table1.country = Table2.country 
AND Table1.TotalProductQuantity = Table2.Max
ORDER BY Max desc



Answer:
Product categories in Home/Nest/Nest-USA is the highest purchases and customers are in the United States (21690), Sweden (112), Honduras (112), and Morocco (94). Home/Shop by Brand/YouTube/ product category is sought for by customers across the globe. Men's T-shirt are mostly purchaed in Asia, Africa and South Amerrica.




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
WITH Table1 AS (
SELECT country, v2ProductCategory, sr.name, SUM(total_ordered) AS TotalProductQuantity
FROM products p
JOIN sales_report sr
ON p.SKU = sr.productsku
JOIN all_sessions al
ON al.productSKU = sr.productsku
GROUP by country, v2ProductCategory, sr.name
ORDER BY TotalProductQuantity desc
), Table2 AS (
SELECT country, MAX(TotalProductQuantity) Max
FROM Table1
GROUP BY country 
ORDER BY Max desc
)
SELECT Table1.country, v2ProductCategory, Table1.name, Table2.Max
FROM Table1, Table2
WHERE Table1.country = Table2.country 
AND Table1.TotalProductQuantity = Table2.Max
ORDER BY name, max desc


Answer: The top selling product is the "Ballpoint LED Light Pen" mostly purchased in the US, Germany & Japan. Hardcover Journal is the next most purchased product from 20 countries in diffeent continents. "22 oz  Bottle Infuser" is a well known product too purchased from 17 countries.





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:


select country, city, SUM(totalTransactionRevenue)
totalTransactionRevenue
from all_sessions a
WHERE totalTransactionRevenue IS NOT null
GROUP BY city, country
order by totalTransactionRevenue desc


Answer:
~93% of total transaction revenue is generated from the United States. Only 5 countries are contributing to the revenue (United States, Israel, Australia, Canada & Switzerland). 






