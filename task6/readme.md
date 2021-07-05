Task #6 - database:

1. Развернуть в облаке контейнер с базой данных SQL (MySQL or PostgreSQL)
2. Заполнить базу данных. Сделать две таблицы:
	Students (ID; Student; StudentId);
	Result (ID; StudentId; Task1; Task2; Task3; Task4);

3. Написать запрос который по вашей фамилии будет находить информацию по выполненным заданиям и выводить результат на экран.
4. Сделайте dump базы данных, удалите существующую и восстановите из дампа.
5. Написать Ansible роль для развертывания SQL или noSQL базы данных. Креды не должны храниться в GitHub.


----

The sequence is following:

docker exec -it some-postgres bash -u postgres		# starting postges container
createdb mydb						# database creation
\l+							# list databases to see new one, can be run outside of database
psql mydb						# use new database
mydb=# 							# expected output

-------->
CREATE TABLE Students (
Student            varchar(80),
StudentId        int
);
CREATE TABLE						# expected output if succeed
SELECT * FROM Students;					# see the empty table

CREATE TABLE Result (
StudentId        int,
Task1            varchar(80),
Task2           varchar(80),
Task3           varchar(80),
Task4           varchar(80),
Task5           varchar(80)
);
CREATE TABLE						# expected output if succeed

-------->
INSERT INTO 
    Students (StudentId, Student)
VALUES
('1','Ivan Ivanov'),
('2','Petro Petrov'),
...
('n','John Smith');

-------->
INSERT INTO 
   Result (StudentId, Task1, Task2, Task3, Task4, Task5)
VALUES
('1',	'Done',	'Done+extra',	'Done+extra',	'Done+extra',	'Done'),
('2',	'Done+extra',	'Done+extra',	'Done+extra',	'Done+extra',	'Done+extra'),
...
('n',	'Done',	'Done+extra',	'Done+extra',	'Done+extra',	'Done+extra');



SELECT * FROM Students;					# see both filled tables
SELECT * FROM Result;					#

SELECT Task1, Task2, Task3, Task4, Task5		# the request should be formed as shown.
FROM Students						#
INNER JOIN Result USING(StudentId)			# StudentId field exists in both tables
WHERE Students.student = 'Дмитрий Мошна';		# 

# sample output:
task1 |     task2     | task3 | task4 |     task5     
-------+---------------+-------+-------+---------------
 Done  | not_completed | Done  | Done  | not_completed
(1 row)

# Backup-restore process include the steps:
pg_dump mydb > /home/postgres/mydbdump;			# should be run in bash inside the container

DROP DATABASE mydb WITH (FORCE);			# "WITH (FORCE)" can be omitted, but my database was in "busy" state all the time

createdb mydb						# need to create database to fill in the data

psql mydb < /home/postgres/mydbdump			# restore process
