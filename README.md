# MSSQL-Learning
 Solving SQL tasks from the online data analytics course

Requests for tasks by sorting module and functions for working with strings:
Task 1. 

Write SQL queries that output the following data:
The city with the largest population.
select top 1 * from skill_cities order by population DESC
The city with the smallest population.
select top 1 * from skill_cities order by population ASC
By the most sparsely populated city in the country with an identifier country_id=10. 
select top 1 * from skill_cities where country_id=10 order by population ASC
By the most populated city in the country with an identifier country_id=4. 
select top 1 * from skill_cities where country_id=4 order by population DESC
List of all capitals, ordering the output in descending order of population.
select * from skill_cities where is_capital=1 order by population DESC

Task 2. 
Write and execute SQL queries in the test environment, which are obtained from the skill_customers table:
The following columns:

Column order	Output value	Column name
1	first_name	first_name
2	value length fields first_name	len_first_name
3	first_name value without trailing spaces	trim_first_name
4	Length of first_name field value without trailing spaces	len_trim_first_name
select first_name, 
len(first_name) length_first_name, 
trim(first_name) trim_first_name, 
len(trim(first_name)) length_trim_first_name
from skill_customers
Rows whose first_name column values do not contain trailing spaces. To create a selection condition, use the functions for calculating the length of a string and removing trailing spaces.
select * from skill_customers where len(first_name)=len(trim(first_name))
Rows whose first_name column values do not contain trailing spaces. To compose a selection condition, use the string comparison functions like or analogues.
select * from skill_customers where not first_name like ' %' and not first_name like '% '
Write and execute an SQL query in the test environment that receives the following columns from the skill_customers table:

Column order	Output value	Имя колонки
1	Column value stripped of leading and trailing spaces first_name	first_name
2	Column value stripped of leading and trailing spaces last_name	last_name
select trim(first_name) first_name, 
trim(last_name) last_name
from skill_customers 
Task 3. 
Write and execute a SQL query in the test environment that gets all rows from the skill_price table. Adjust the item_name field - the first letter should be uppercase, the rest should be lowercase. The field name must remain item_name.
select concat(upper(substring(item_name, 1, 1)), 
lower(substring(item_name, 2, len(item_name)-1))) item_name, 
price_rub, cnt from skill_price

Task 4.
A query that receives rows by condition: the last_name column contains the substring '[wrong]';
select last_name from skill_customers where charindex('[wrong]', last_name)>0
Execute the query with the condition from point 1, include in the selection one calculated column that contains the last_name field value without the '[wrong]' substring. The name of the column is saved - last_name. For calculations, use the substring function. Column values must not contain trailing spaces.
select trim(concat(
substring(last_name, 1, charindex('[', last_name)-1), 
substring(last_name, charindex(']', last_name)+1, len(last_name)))) last_name
from skill_customers where charindex('[wrong]', last_name)>0
Repeat the query from step 2, but use the replace function for calculations.
select trim(replace(last_name, '[wrong]', '')) last_name
from skill_customers where charindex('[wrong]', last_name)>0

MODULE 5. SELECT - Working with date and time

Task 1. Using the SELECT statement for a database, query the server's current time in two ways:
- using the CURRENT_TIMESTAMP function: 
select CURRENT_TIMESTAMP current_datatime
- using the getdate() function: 
select GETDATE() current_datatime

Task 2. 
Write a query that uses the CAST function to extract a date from the result of the CURRENT_TIMESTAMP function.
select CAST(CURRENT_TIMESTAMP as Date) _date
Write a query that uses the CAST function to extract time from the result of the CURRENT_TIMESTAMP function.
select CAST(CURRENT_TIMESTAMP as Time) _time
Write a query that uses the CONVERT function to extract a date from the result of the CURRENT_TIMESTAMP function.
select CONVERT(date, CURRENT_TIMESTAMP) _date
Write a query that uses the CONVERT function to extract time from the result of the CURRENT_TIMESTAMP function.
select CONVERT(time, CURRENT_TIMESTAMP) _time
Write a query on the skill_managers table that retrieves the following columns:

Column number	Column name	Value
1	last_transaction_dt	last_transaction_dt value as it is in the table
2	last_transaction_date	date extracted from the last_transaction_dt field using the CAST function
3	last_transaction_time	time extracted from the last_transaction_dt field using the CONVERT function
select last_transaction_dt, 
CAST(CURRENT_TIMESTAMP AS Date) last_transaction_date, 
CONVERT(time, CURRENT_TIMESTAMP) last_transaction_time
from skill_managers

Task 3. 
Write a query using the FORMAT function that converts the result of the CURRENT_TIMESTAMP function to a string containing a date in the YYYY-DD-MM format. Date appearance example: 2005-08-09.
select FORMAT(CURRENT_TIMESTAMP, 'yyyy-dd-MM') formated
Write a query using the FORMAT function that converts the result of executing the CURRENT_TIMESTAMP function into a string containing the time in the hh:mm:ss format. An example of the appearance of time: 18:31:42.
select FORMAT(CURRENT_TIMESTAMP, 'hh:mm:ss') formated
Write a query on the skill_managers table that retrieves the following columns:

Column number	Column name	Value
1	last_transaction_dt	last_transaction_dt value as it is in the table
2	last_transaction_date	the value of the last_transaction_dt field, formatted by the FORMAT function as YYYY-DD-MM
3	last_transaction_time	the value of the last_transaction_dt field formatted by the FORMAT function as hh:mm:ss

select last_transaction_dt last_transaction_dt, 
FORMAT(CURRENT_TIMESTAMP, 'yyyy-dd-MM') last_transaction_date, 
FORMAT(CURRENT_TIMESTAMP, 'hh:mm:ss') last_transaction_time
from skill_managers 

Task 4. 
Write a query using the YEAR function that extracts the year from the result of the CURRENT_TIMESTAMP function in number format.
select year(current_timestamp) year
Write a query using the MONTH function that extracts the month from the result of the CURRENT_TIMESTAMP function in number format.
select month(current_timestamp) month
Write a query using the DAY function that extracts a day from the result of the CURRENT_TIMESTAMP function in number format.
select day(current_timestamp) day
Write a query using the DATEPART function that extracts an hour from the result of the CURRENT_TIMESTAMP function in number format.
select datepart(hour, current_timestamp) hour
Write a query using the DATEPART function that extracts minutes from the result of the CURRENT_TIMESTAMP function in number format.
select datepart(minute, current_timestamp) minute

Task 5. 

Getting a list of managers, consisting of the following columns:
Manager's name.
Last name of the manager.
Manager's year of birth (name the column year_of_born).

Include in the sample managers who had the last transaction at 22:00 or later.
select first_name, last_name, 
datepart(year, birth_date) year_of_born
from skill_managers 
where datepart(hour, last_transaction_dt)>=22

Getting a list of managers, consisting of the following columns:
Manager's name.
Last name of the manager.
The date of the last transaction in the form: day in the format 1-31 (without the first zero) and the English name of the month separated by a space, name the column dt.
Include managers who were born in the summer in the sample, and sort the entire list by last name (in ascending order).
select first_name, last_name, 
FORMAT(last_transaction_dt, 'd MMMM') dt
from skill_managers 
where month(birth_date) in (6,7,8) order by last_name

MODULE 6. SELECT - Working with date and time (Part 2)

Task 1. 
Table rows in which the manager's birthday (birth_date column) matches November 25, 1989.
select * from skill_managers where birth_date='1989-11-25' 
Table rows in which the manager's birthday (birth_date column) corresponds to November 25, 1989 or July 14, 1997.
select * from skill_managers where birth_date='1989-11-25' or birth_date='1997-07-14'
Table rows whose last transaction date (last_transaction_dt column) matches the timestamp 2020-03-10 15:07:11 or 2020-05-11 17:28:26.
select * from skill_managers 
where last_transaction_dt='2020-03-10 15:07:11' 
or last_transaction_dt='2020-05-11 17:28:26'
Table rows whose last transaction (column last_transaction_dt) was made on September 1, 2020.
select * from skill_managers 
where cast(last_transaction_dt as Date) = '2020-09-01'Table rows whose last transaction (column last_transaction_dt) was made at 16:54:30.
select * from skill_managers 
where cast(last_transaction_dt as Time) = '16:54:30'

Task 2. 
Table rows in which the manager's birthday (birth_date column) is greater than or equal to 1989-11-25.
select * from skill_managers 
where birth_date>='1989-11-25'
Table rows in which the manager's birthday (birth_date column) is between two dates: 1989-11-25 and 1997-07-14. Range boundaries must be included in the sample.
select * from skill_managers 
where birth_date>='1989-11-25'
and birth_date<='1997-07-14'
Table rows whose last transaction dates (last_transaction_dt column) start with the timestamp 2020-03-10 15:07:11.
select * from skill_managers 
where last_transaction_dt>='2020-03-10 15:07:11'
Table rows whose last transaction date (last_transaction_dt column) falls within the range between timestamps 2020-03-10 15:07:11 and 2020-05-11 17:28:26. Range boundaries must be included in the sample.
select * from skill_managers 
where last_transaction_dt>='2020-03-10 15:07:11'
and last_transaction_dt<='2020-05-11 17:28:26'
Table rows whose last transaction (column last_transaction_dt) falls between March 10, 2020 and May 11, 2020. Transactions that fall within the days that the range is specified must be included in the selection.
select * from skill_managers 
where CAST(last_transaction_dt as Date)>='2020-03-10'
and CAST(last_transaction_dt as Date)<='2020-05-11'

Task 3. Compile and execute three SQL queries to the skill_operation table, requesting rows according to certain selection conditions by the date specified in three columns: year - year, month - month, day - day.

All lines from 2020-08-20. Conditions must be specified for each column (year, month, day) separately.
select * from skill_operation where year=2020 and month=08 and day=20
All rows whose date (consisting of the year, month, day column values) matches the number 2020-08-20.
select * from skill_operation 
where DATEFROMPARTS(year, month, day)='2020-08-20' 
All rows whose date (consisting of the year, month, day column values) falls between 2020-08-20 and 2020-08-26. Range boundaries should not be included in the sample.
select * from skill_operation 
where DATEFROMPARTS(year, month, day)>'2020-08-20' 
and DATEFROMPARTS(year, month, day)<'2020-08-26'
In paragraphs 2 and 3 in Microsoft SQL Server, the conditions must be specified using the DATEFROMPARTS function

Task 4.Compose and execute two SQL queries of the following form:
select * from skill_events where CAST(expression as date)='2020-08-20'
The expression must use the dt_bad_string column and functions:
Only the replace function.
select * from skill_events where 
cast(
replace(replace(replace(dt_bad_string,' year ','-'),' month ','-'),' day','')
as date)='2020-08-20'
Microsoft SQL Server: concat function that uses substring functions and others (if needed).
select * from skill_events where 
cast(
concat(
substring(dt_bad_string,1,4),
'-',
substring(dt_bad_string,11,2),
'-',
substring(dt_bad_string,19,2)
)
as date)='2020-08-20'

