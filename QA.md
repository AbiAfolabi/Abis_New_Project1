What are your risk areas? Identify and describe them.
1. Incomplete data - There are several columns in the data that are empty. Also rows of with missing information. This does not give the full picture and could lead to biased judgements.

2. Duplicates will lead to erroneous analysis and conclusions due to overestimation.

3. Inconsistent / unreasonable values - Some data values are out of expected range e.g. having negative values in quantity ordered.

4. Referential Integrity checked between tables failed. Same column names in different tables not matching. 


QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. checked for completeness of rows information in all the tables. There were several columns with blanks and null values. I did not attempt to fill in the blanks/nulls with values using any of the possible methods (mean, median, mode etc) because I do not have a detailed description of what the columns mean to guide my judgment.




2. Checked for duplicates quering for unique values e.g. below shows there were no duplicates in the producs and sales_by_sku tables

SELECT DISTINCT SKU
FROM products


SELECT DISTINCT productSKU 
FROM sales_by_sku

SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1;


3. Checked for unreasonable values like when order quantity or stocklevel in the products tabe is negative, where total_ordered is negative in the sales_by_sku table

SELECT * from products
WHERE orderedquantity < 0 OR stocklevel < 0

I would expect sentiment values to be between 0 and 1 (no negatives), however I found values less than 0. This requires investigation to know if the scale is between -1 and +1 with 0 being neutral.

SELECT * from products
WHERE sentimentscore < 0 OR sentimentscore > 1

SELECT * 
FROM sales_by_sku
WHERE total_ordered < 0

If total_ordered is 0, it could mean the product is not in demand and guide decisions on offering promotional sales on the products or discontinung stockup.

SELECT *
FROM sales_by_sku
WHERE total_ordered  = 0 

4. all_sessions and analytics table have fullvisitorid column but the formatting is different and there is no overlap when I use the INNER JOIN


SELECT an.fullvisitorid, al.fullvisitorid from all_sessions al
FULL OUTER JOIN analytics an
ON an.fullvisitorid = al.fullvisitorid
where al.fullvisitorid is not null
AND an.fullvisitorid is not null


Integrirty check between the tables failed. For example, below is SQL for referential integrity Check for "sales_by_sku" and "all_sessions" tables.

WITH CTE AS(
SELECT 'sales_by_sku' AS table_name, 
       COUNT(*) AS count_rows, 
       'productsku' AS key_name,
       COUNT(DISTINCT(productsku)) AS count_of_productsku
FROM sales_by_sku

UNION ALL

SELECT 'sales_report' AS table_name, --f
       COUNT(*) AS count_rows,    
       'sales_report' AS key_name,
       COUNT(DISTINCT(productsku)) AS count_of_productsku   
FROM sales_report 
            ), 
            
QA_raw AS(
SELECT COUNT(DISTINCT(count_of_productsku)) as test_result FROM cte
)


SELECT 'referential_integrity_check' AS qa_test_name,
       CASE
        WHEN test_result = 1 THEN 'pass'
        ELSE 'fail'
       END AS qa_result
FROM qa_raw; 



