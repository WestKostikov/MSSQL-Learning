# MSSQL-Learning
 Solving SQL tasks from the online data analytics course

������� � �������� �� ������ ���������� � ������� ��� ������ �� ��������:
������� 1. 

�������� SQL-�������, ������� ������� ��������� ������:
�� ������ � ����� ������� ����������. 
select top 1 * from skill_cities order by population DESC
�� ������ � ����� ��������� ����������. 
select top 1 * from skill_cities order by population ASC
�� ������ �������������� ������ ������ � ��������������� country_id=10. 
select top 1 * from skill_cities where country_id=10 order by population ASC
�� ������ ���������� ������ ������ � ��������������� country_id=4. 
select top 1 * from skill_cities where country_id=4 order by population DESC
������ ���� ������, ���������� ����� �� �������� ���������.
select * from skill_cities where is_capital=1 order by population DESC

������� 2. 

