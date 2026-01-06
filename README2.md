# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Первушин Дмитрий`

### Задание 1.

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

### Решение 1.

Создал docker-compose:

```
version: '3.8'

services:
  mysql:
    image: mysql:8.0
    container_name: mysql_docker
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: test_db
```

```
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'temp';
SELECT User FROM mysql.user;
```
![Решение1](https://github.com/Divan4eg/database_hw/blob/main/img/5.png)

```
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';
SHOW GRANTS FOR 'sys_temp'@'localhost';
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'temp';
```
![Решение1](https://github.com/Divan4eg/database_hw/blob/main/img/6.png)

```
docker cp /home/pda/sakila.sql mysql_docker:/tmp/sakila.sql
```
В консоли mysql
```
USE test_db;
SOURCE /tmp/sakila.sql;
```
![Решение1](https://github.com/Divan4eg/database_hw/blob/main/img/7.png)

### Задание 2.

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц.

### Решение 2.

![Решение2](https://github.com/Divan4eg/database_hw/blob/main/img/8.png)
https://github.com/Divan4eg/database_hw/blob/main/img/task2.ods


