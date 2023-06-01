## Информация о проекте
Необходимо организовать систему учета для питомника, в котором живут
домашние и вьючные животные.

## Задание
1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).

![Task_1](/Kennel_account_system/Images/1.png)

2. Создать директорию, переместить файл туда.

![Task_2](/Kennel_account_system/Images/2.png)

3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.

![Task_3_1](/Kennel_account_system/Images/3-1.png)

![Task_3_2](/Kennel_account_system/Images/3-2.png)


4. Установить и удалить deb-пакет с помощью dpkg.

![Task_4](/Kennel_account_system/Images/4.png)


5. Выложить историю [команд](https://github.com/kremlik144/final_control_work/blob/main/Kennel_account_system/CommandsUbuntu.md) в терминале ubuntu

6. [Нарисовать диаграмму](https://github.com/kremlik144/final_control_work/blob/main/Kennel_account_system/Animal_diagram.drawio) в которой есть родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы.

![Task_6](/Kennel_account_system/Images/6.png)

7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”

```sql
CREATE DATABASE Human_friends;
```

8. Создать таблицы с иерархией из диаграммы в БД

```sql
USE Human_friends;
CREATE TABLE animal_classes
(
	Id INT AUTO_INCREMENT PRIMARY KEY, 
	Class_name VARCHAR(20)
);

INSERT INTO animal_classes (Class_name)
VALUES ('вьючные'),
       ('домашние');  


CREATE TABLE packed_animals
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO packed_animals (Genus_name, Class_id)
VALUES ('Лошади', 1),
       ('Ослы', 1),  
       ('Верблюды', 1); 
    
CREATE TABLE home_animals
(
	Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO home_animals (Genus_name, Class_id)
VALUES ('Кошки', 2),
       ('Собаки', 2),  
       ('Хомяки', 2); 

```

9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения

```sql
CREATE TABLE cats 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO cats (Name, Birthday, Commands, Genus_id)
VALUES ('Васька', '2016-05-09', 'кс-кс', 1),
	   ('Маська', '2016-06-10', 'можно', 1),  
	   ('Ириска', '2016-07-11', 'нельзя', 1); 


CREATE TABLE dogs 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO dogs (Name, Birthday, Commands, Genus_id)
VALUES ('Тузик', '2010-01-02', 'можно, нельзя, сидеть', 2),
	   ('Мурзик', '2011-02-03', 'лежать, сидеть, голос', 2),  
	   ('Биба', '2012-03-04', 'лапу, умри, фас', 2), 
	   ('Боба', '2013-04-05', 'рядом, лежать, голос', 2);


CREATE TABLE hamsters 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO hamsters (Name, Birthday, Commands, Genus_id)
VALUES ('Пуговка', '2022-10-12', 'кушац', 3),
	   ('Пипка', '2022-11-12', 'не кушац', 3),  
	   ('Шальной', '2022-11-11', 'спи', 3), 
	   ('Соння', '2023-02-10', 'не спи', 3);


CREATE TABLE horses 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO horses (Name, Birthday, Commands, Genus_id)
VALUES ('Мамба', '2018-05-03', 'быстрее, стоп, медленнее', 1),
	   ('Мумба', '2019-06-04', 'ко мне, кушац, можно', 1),  
	   ('Чудо', '2020-07-06', 'бегом, ползком, развернись', 1), 
	   ('Юда', '2021-08-07', 'бегом, шагом, прыжок', 1);


CREATE TABLE donkeys 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO donkeys (Name, Birthday, Commands, Genus_id)
VALUES ('Игорь', '2019-04-08', 'быстрее, стоп, медленнее', 2),
	   ('Славик', '2020-03-09', 'быстрее, стоп, медленнее', 2),  
	   ('Терентий', '2021-02-10', 'быстрее, стоп, медленнее', 2), 
	   ('Марк', '2022-01-11', 'быстрее, стоп, медленнее', 2);


CREATE TABLE camels 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO camels (Name, Birthday, Commands, Genus_id)
VALUES ('Арарат', '2018-04-04', 'быстрее, стоп, медленнее', 3),
	   ('Карлик', '2019-03-05', 'быстрее, стоп, медленнее', 3),  
	   ('Громадина', '2020-02-06', 'быстрее, стоп, медленнее', 3), 
	   ('Нормальдесный', '2021-01-07', 'быстрее, стоп, медленнее', 3);
```

10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.

```sql
SET SQL_SAFE_UPDATES = 0;
DELETE FROM camels;

SELECT Name, Birthday, Commands FROM horses
UNION SELECT  Name, Birthday, Commands FROM donkeys;
```

11. Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице

```sql
CREATE TEMPORARY TABLE animals AS 
SELECT *, 'Лошади' as genus FROM horses
UNION SELECT *, 'Ослы' AS genus FROM donkeys
UNION SELECT *, 'Собаки' AS genus FROM dogs
UNION SELECT *, 'Кошки' AS genus FROM cats
UNION SELECT *, 'Хомяки' AS genus FROM hamsters;

CREATE TABLE yang_animal AS
SELECT Name, Birthday, Commands, genus, TIMESTAMPDIFF(MONTH, Birthday, CURDATE()) AS Age_in_month
FROM animals WHERE Birthday BETWEEN ADDDATE(curdate(), INTERVAL -3 YEAR) AND ADDDATE(CURDATE(), INTERVAL -1 YEAR);
 
SELECT * FROM yang_animal;
```

12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.

```sql
SELECT h.Name, h.Birthday, h.Commands, pa.Genus_name, ya.Age_in_month 
FROM horses h
LEFT JOIN yang_animal ya ON ya.Name = h.Name
LEFT JOIN packed_animals pa ON pa.Id = h.Genus_id
UNION 
SELECT d.Name, d.Birthday, d.Commands, pa.Genus_name, ya.Age_in_month 
FROM donkeys d 
LEFT JOIN yang_animal ya ON ya.Name = d.Name
LEFT JOIN packed_animals pa ON pa.Id = d.Genus_id
UNION
SELECT c.Name, c.Birthday, c.Commands, ha.Genus_name, ya.Age_in_month 
FROM cats c
LEFT JOIN yang_animal ya ON ya.Name = c.Name
LEFT JOIN home_animals ha ON ha.Id = c.Genus_id
UNION
SELECT d.Name, d.Birthday, d.Commands, ha.Genus_name, ya.Age_in_month 
FROM dogs d
LEFT JOIN yang_animal ya ON ya.Name = d.Name
LEFT JOIN home_animals ha ON ha.Id = d.Genus_id
UNION
SELECT hm.Name, hm.Birthday, hm.Commands, ha.Genus_name, ya.Age_in_month 
FROM hamsters hm
LEFT JOIN yang_animal ya ON ya.Name = hm.Name
LEFT JOIN home_animals ha ON ha.Id = hm.Genus_id;
```

13. Создать [класс](https://github.com/kremlik144/final_control_work/tree/main/Kennel_account_system/System/src/Model) с Инкапсуляцией методов и наследованием по диаграмме.

14. Написать [программу](https://github.com/kremlik144/final_control_work/tree/main/Kennel_account_system/System/src), имитирующую работу реестра домашних животных
В программе должен быть реализован следующий функционал:    
	- завести новое животное    
	- определять животное в правильный класс    
	- увидеть список команд, которое выполняет животное    
	- обучить животное новым командам    
	- реализовать навигацию по меню    
	
15. Создайте [класс Счетчик](https://github.com/kremlik144/final_control_work/blob/main/Kennel_account_system/System/src/Controller/Counter.java), у которого есть метод add(), увеличивающий̆
значение внутренней̆ int переменной̆ на 1 при нажатии “Завести новое
животное” Сделайте так, чтобы с объектом такого типа можно было работать в
блоке try-with-resources. Нужно бросить исключение, если работа с объектом
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение
считать в ресурсе try, если при заведении животного заполнены все поля.