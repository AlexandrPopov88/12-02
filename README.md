# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Попов Адександр`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

![1-3](https://github.com/user-attachments/assets/4cd92690-ca8a-4aba-9db5-171f136b5003)


1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

![1-5](https://github.com/user-attachments/assets/be1895d5-68d3-434a-a7f1-49d8a53d9de6)


1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

![1-8](https://github.com/user-attachments/assets/8c90fc6f-13ff-4527-a689-0cb3b9ba89f1)


*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

#### ОТВЕТ (простыня со всеми запросами):
```
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.24-1_all.deb
sudo apt install -y mysql-server
mysql -u root -p 
mysql> select User,Host from mysql.user;
mysql -u root -p
mysql> grant ALL PRIVILEGES on *.* to 'sys_temp'@'%' with GRANT option;
mysql> show grants for 'sys_temp'@'%';
mysql -u sys_temp -p
alter user 'sys_temp'@'%' IDENTIFIED with mysql_native_password by '12345678';
wget -c https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
mysql -u sys_temp -p
mysql>show databases;
mysql>create database SakilaDB;
mysql>show databases;
mysql>use SakilaDB;
mysql>show tables;
mysql>source sakila-schema.sql;
mysql>source sakila-data.sql;
mysql>show tables;
mysql>exit
mysql -u sys_temp -p
mysql>show databases;
mysql>use SakilaDB;
mysql>show tables;
mysql>exit
```


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

```
Название таблицы             | Название первичного ключа
actor                        | actor_id
actor_info                   | 
address                      | address_id
category                     | category_id
city                         | city_id
country                      | country_id
customer                     | customer_id
customer_list                | 
film                         | film_id
film_actor                   | actor_id, film_id
film_category                | film_id, category_id
film_list                    | 
film_text                    | film_id
inventory                    | inventory_id
language                     | language_id
nicer_but_slower_film_list   | 
payment                      | payment_id
rental                       | rental_id
sales_by_film_category       | 
sales_by_store               | 
staff                        | staff_id
staff_list                   | 
store                        | store_id
```





## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*
