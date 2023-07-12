# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of this project is to:
1. Get familiar and comfortable with creating databases and tables.

2. Import data into tables with their appropriate data type.

3. Clean, transform and validate data using appropriate update & transformation codes.

4. Write SQL to query tables (single or multiples by joining) to retrieve information.

5. Perform aggregates on data.


## Process
1. Created the e-commerce database in pgAdmin.

2. Created 5 tables for the 5 datafiles provided: all_sessions, analytics, products, sales_by_sku and sales_report'.

3. Imported the data files into thier respective tables.

4. Performed QA tests for completeness, uniqueness and consistency of the data.

5. Updated (cleaned) data columns where necessary based on the QA tests.

6. Validated data.


## Results
~94% of transactions was by US customers.

~40% of transactions was by referral.

High page views did not translate into transactions.

Nest(R) products are the most purchased.


## Challenges 
Data import failed many times and took about half of available time to complete the project.

Lots of nulls in the data set leading to various assumptions which does not give the true picture of the company's sales.

Same column names in different tables can be confusing e.g. fullvisitorid in all_sessions and analytics tables are not reconcilable with the current formatting.

Meaning of columns not clear since there is no data definition documenation provided.

## Future Goals
 Perform more QA test on the dataset.

 Fill up or eliminate columns that have no informations (all blanks) from the tables.

 Calculate percentages of the revenue contributions from the different countries and cities.
 
 Propose marketing strategies to get countries that are not contributing to revenue on board.
 


