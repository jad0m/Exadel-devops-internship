Task #6 - database:

1. Развернуть в облаке контейнер с базой данных SQL (MySQL or PostgreSQL)
2. Заполнить базу данных. Сделать две таблицы:
	Students (ID; Student; StudentId);
	Result (ID; StudentId; Task1; Task2; Task3; Task4);

3. Написать запрос который по вашей фамилии будет находить информацию по выполненным заданиям и выводить результат на экран.
4. Сделайте dump базы данных, удалите существующую и восстановите из дампа.
5. Написать Ansible роль для развертывания SQL или noSQL базы данных. Креды не должны храниться в GitHub.