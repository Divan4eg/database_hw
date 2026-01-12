# Домашнее задание к занятию "`Репликация и масштабирование. Часть 1`" - `Первушин Дмитрий`

### Задание 1
На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

Ответить в свободной форме.

### Решение 1

Master-Slave:

Есть один главный сервер (Master), который принимает все записи, остальные серверы (Slave) только читают данные. Если Master выходит из строя, система временно перестаёт работать на запись.

Master-Master:

Все серверы равнозначны и могут как писать, так и читать данные, изменения синхронизируются между всеми серверами в обе стороны. При выходе из строя одного сервера остальные продолжают работать.

### Задание 2
Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.

### Решение 2

Создал 2 контейнера, связал одной сетью repl1. Прокинул файлы my.cnf.
![Решение2](https://github.com/Divan4eg/database_hw/blob/main/img/9.png)

На master
```
CREATE USER 'replica'@'%';
GRANT REPLICATION SLAVE ON *.* TO'replica'@'%';
FLUSH PRIVILEGES;
SHOW BINARY LOG STATUS;
```

На replica
```
CHANGE REPLICATION SOURCE TO SOURCE_HOST='master', SOURCE_USER='replica', RELAY_LOG_POS=773;
START REPLICA;
SHOW REPLICA STATUS\G;
```

Реплика запустилась.

![Решение2](https://github.com/Divan4eg/database_hw/blob/main/img/10.png)

Создаю записи, сразу вижу изменения.

![Решение2](https://github.com/Divan4eg/database_hw/blob/main/img/11.png)


