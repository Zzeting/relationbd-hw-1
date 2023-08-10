# Домашнее задание к занятию "`Базы данных`" - `Мамонтов Александр`


### Задание 1. 

Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

идентификатор, первичный ключ, serial,
фамилия varchar(50),
...
идентификатор структурного подразделения, внешний ключ, integer).


# Решение

Сотрудники (

id - сотрудника SMALLINT AUTO_INCREMENT PRIMARY KEY,
фамилия VARCHAR(100) not null,
имя, VARCHAR(100) not null,
отчество VARCHAR(100),
id - должности SMALLINT FOREIGN KEY,
id - подразделения SMALLINT FOREIGN KEY,  
оклад DECIMAL(10,2) not null,
дата найма DATE not null

);

Должности (
    
id - должности SMALLINT AUTO_INCREMENT PRIMARY KEY,
название VARCHAR(100) not null,

);

Тип_подразделения (

id - типа подразделения SMALLINT AUTO_INCREMENT PRIMARY KEY,
название VARCHAR(100) not null

);

Подразделение (

id - подразделения SMALLINT AUTO_INCREMENT PRIMARY KEY,
название VARCHAR(100) not null,
id - типа подразделения SMALLINT FOREIGN KEY,
id - адреса SMALLINT FOREIGN KEY

);

Адрес_филиала (

id - адреса SMALLINT AUTO_INCREMENT PRIMARY KEY,
адрес TINYTEXT not null

);

Проект (

id - проекта INT AUTO_INCREMENT PRIMARY KEY,
название VARCHAR(150) not null

);


Работа (

id - сотрудника,
id - проекта,
PRIMARY KEY (id - сотрудника, id - проекта)

);


### Задание 2

Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.


В данной таблице имеется 8 атрибутов, согласно формуле `n!/((n-r)! * (r)!)`, где `r - количество атрибутов в ключе`, а `n - количество атрибутов в отношении`, мы имеем 255 функциональных зависимостей, перечисление которых не имеет практической необходимости.

При удалении избыточных зависимоестей в данном случае достаточно использовать следующие правила Аксиомы Армстронга:
- Рефлексивность
- Пополнение
- Транзитивность