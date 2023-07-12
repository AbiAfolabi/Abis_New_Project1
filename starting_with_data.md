Question 1: What is the number of countries represented in the dataset?

SQL Queries:
SELECT DISTINCT(country)
FROM all_sessions

Answer: 
There are 136 distinct countries



Question 2: Write a query to show the amount of orders by countries and cities where amount of orders is greater than 1000.

SQL Queries:

SELECT country, city, SUM(total_ordered) AS QuantityOrdered
FROM sales_report sr
JOIN all_sessions al
ON sr.productsku = al.productsku
GROUP BY country, city
HAVING SUM(total_ordered) > 1000
ORDER BY country

Answer:

"Brazil"	"NULL"	2078
"Canada"	"Toronto"	2101
"Canada"	"NULL"	5260
"Czechia"	"NULL"	1358
"Denmark"	"NULL"	1261
"France"	"NULL"	1671
"Germany"	"NULL"	4620
"Hong Kong"	"Hong Kong"	1339
"India"	"NULL"	3324
"Ireland"	"Dublin"	1116
"Italy"	"NULL"	2165
"Japan"	"NULL"	3440
"Mexico"	"NULL"	1429
"Netherlands"	"NULL"	1837
"Singapore"	"NULL"	1306
"Spain"	"NULL"	1744
"Taiwan"	"NULL"	3350
"United Kingdom"	"London"	2174
"United Kingdom"	"NULL"	6114
"United States"	"New York"	8069
"United States"	"Salem"	1247
"United States"	"San Francisco"	6776
"United States"	"Mountain View"	19382
"United States"	"Chicago"	2765
"United States"	"NULL"	56219
"United States"	"Los Angeles"	3651
"United States"	"Sunnyvale"	4596
"United States"	"Palo Alto"	3566
"United States"	"San Jose"	3256
"United States"	"Austin"	1674
"United States"	"Santa Clara"	1764
"United States"	"Seattle"	2202



Question 3: Make a list of the 10 countries with highest number of pageviews and the respective number of views.

SQL Queries:
SELECT country, Count(pageviews) Views
FROM all_sessions
GROUP by country
ORDER BY Views desc
LIMIT 10

Answer:

"United States"	8727
"India"	719
"United Kingdom"	668
"Canada"	642
"Germany"	336
"Japan"	241
"Australia"	225
"France"	218
"Taiwan"	174
"Netherlands"	158



Question 4: Make a list of organic searches made in 2017.

SQL Queries:

SELECT channelgrouping, date
FROM all_sessions
WHERE date BETWEEN '2017-01-01' AND '2017-12-31'
AND channelgrouping = 'organic search'


Answer:

None


Question 5: From which countries and cities were customers that spent greater than 2000 seconds on the company's site in the first quater of 2017 (unit of time assumed to be seconds)

SQL Queries:

SELECT country, city
FROM all_sessions
WHERE date BETWEEN '2017-01-01' AND '2017-03-31'
AND timeonsite >  '2000'


Answer:

"Ireland"	"Cork"
"United States"	"NULL"
"Israel"	"Tel Aviv-Yafo"
"United States"	"NULL"
"Canada"	"NULL"
"United States"	"New York"
"United States"	"New York"
"Greece"	"Thessaloniki"
"Argentina"	"Buenos Aires"
"Canada"	"NULL"
"France"	"Villeneuve-d'Ascq"