# Домашнее задание к занятию "`Введение в SQL`" - `Тапилин Артём`

### Задание 1
![Создал учётную запись sys_temp](https://github.com/tapilin34/12-02-hw/blob/main/img/users-add.jpg)
![Добавил права пользователю](https://github.com/tapilin34/12-02-hw/blob/main/img/users-grant.jpg)
![Импортировал БД](https://github.com/tapilin34/12-02-hw/blob/main/img/db-import-diagram.jpg)
![Вывод в виде таблицы](https://github.com/tapilin34/12-02-hw/blob/main/img/db-import.jpg)

### Задание 2
![Таблица сопоставления полей](https://github.com/tapilin34/12-02-hw/blob/main/img/db-tables.jpg)

### Задание 3
Команда для отзыва прав на внесение, изменение и удаление данных из базы sakila.
REVOKE INSERT, UPDATE, DELETE ON sakila.* FROM 'sys_temp'@'%';
![Выполните запрос на получение списка прав для пользователя sys_temp](https://github.com/tapilin34/12-02-hw/blob/main/img/users-after-revoke.jpg)
