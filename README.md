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


