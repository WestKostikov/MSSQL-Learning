# MSSQL-Learning
 Solving SQL tasks from the online data analytics course

Запросы к заданиям по модулю сортировки и функции для работы со строками:
Задание 1. 

Напишите SQL-запросы, которые выводят следующие данные:
По городу с самым большим населением. 
select top 1 * from skill_cities order by population DESC
По городу с самым маленьким населением. 
select top 1 * from skill_cities order by population ASC
По самому малонаселённому городу страны с идентификатором country_id=10. 
select top 1 * from skill_cities where country_id=10 order by population ASC
По самому населённому городу страны с идентификатором country_id=4. 
select top 1 * from skill_cities where country_id=4 order by population DESC
Список всех столиц, упорядочив вывод по убыванию населения.
select * from skill_cities where is_capital=1 order by population DESC

Задание 2. 

