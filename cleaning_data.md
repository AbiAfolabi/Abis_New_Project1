What issues will you address by cleaning the data?

i) overestimation / inaccurate reporting due to duplicate data
ii) Inability to perform aggregates if data format is wrong e.g. numbers imported as strings
iii) incorrect calculations when null values are included.





Queries:
Below, provide the SQL queries you used to clean your data.

'''
ALL_SESSIONS TABLE
i) Updated country column containing values '(not set)' to NULL
'''
UPDATE all_sessions
SET country = CASE
    WHEN country = '(not set)' THEN 'NULL'
    ELSE country
    END;

'''
ii) Updated city column containing values '(not set)' to NULL
'''

UPDATE all_sessions
SET city = CASE
    WHEN city = '(not set)' THEN 'NULL'
    ELSE city
    END;

'''
iii) Updated city column containing values '(not available in demo dataset)' to NULL
'''

UPDATE all_sessions
SET city = CASE
    WHEN city = 'not available in demo dataset' THEN 'NULL'
    ELSE city
    END;



'''
ANALYTICS TABLE
i) Divided the exaggerated unit_cost by 1,000,000 to get the accurate unit_cost of procucts.
'''

UPDATE analytics
SET unit_price = unit_price/1000000

'''
ii) Updated blank cells in the columns userid, unit_sold, bounces & revenue to 'NULL' using the codes below:
'''

UPDATE analytics
SET userid = CASE
    	       WHEN userid = '' THEN 'NULL'
    	       ELSE userid
   	       END;

UPDATE analytics
SET units_sold = CASE
   	      WHEN units_sold = '' THEN 'NULL'
    	ELSE units_sold
    	END;



UPDATE analytics
SET bounces = CASE
    	       WHEN bounces = '' THEN 'NULL'
    	       ELSE bounces
       	       END;

UPDATE analytics
SET revenue = CASE
WHEN revenue = '' THEN 'NULL'
ELSE revenue
END;
