# -3
1) Выберите из таблицы orders все заказы

SELECT * FROM orders

![image](https://github.com/user-attachments/assets/2ace5d62-1a47-4b12-8931-7e4ed5719360)



2) Выберите из таблицы orders все заказы кроме новых. У новых заказов status равен "new". Использовать in

SELECT * FROM orders WHERE STATUS IN ('cancelled','in_progress', 'delivery')


![image](https://github.com/user-attachments/assets/12c35a66-e23a-423f-815c-55a1296a2fa0)

3) Выберите из таблицы orders все новые и отмененные заказы. У отмененных заказов status равен "cancelled". У новых заказов status равен "new".

SELECT * FROM orders WHERE STATUS IN ('cancelled','new')


![image](https://github.com/user-attachments/assets/25499796-c063-4967-849e-48346c42298e)

4) Выберите из таблицы orders все заказы содержащие более 3 товаров (products_count).
Вывести нужно только номер (id) и сумму (sum) заказа.

SELECT id,SUM FROM orders WHERE products_count > 3

![image](https://github.com/user-attachments/assets/fe1d14d4-c72a-4480-a670-9ae730392575)

5) Выберите из таблицы orders все отмененные заказы исключая заказы стоимостью от 3000 до 10000 рублей включительно.

select * from orders where status = 'cancelled' and (sum < 3000 or sum > 10000);

6) Выберите из таблицы products все товары

select * from products;

7) Выведите только имена (name) и цены (price).

select name, price from products order by price;

8) Выберите из таблицы products все товары стоимостью 5000 и выше в порядке убывания цены (price).

select * from products where price>=5000 order by price DESC;

9)Выберите из таблицы products все товары стоимостью до 3000 рублей отсортированные в алфавитном порядке. Вывести нужно только имя (name), количество (count) и цену (price).

select name, count, price from products where price<3000 order by name;

10) Выберите из таблицы users фамилии (last_name) и имена (first_name) всех пользователей. 
Данные должны быть отсортированы сначала по фамилии, а затем по имени.

select last_name, first_name from users order by last_name, first_name;

11) Выберите сотрудников из таблицы users с зарплатой (salary) меньше 30 000 рублей и отсортируйте данные по дате рождения (birthday). Сотрудников с нулевой зарплатой выбирать не нужно.

select * from users where salary<30000 and salary>0 order by birthday;

12) Выберите из таблицы orders 5 самых дорогих заказов за всё время. 
Данные нужно отсортировать в порядке убывания цены. 
Отмененные заказы не учитывайте.

select * from orders where status in('new', 'in_progress', 'delivery') 
order by sum desc limit 5;

13) Выберите из таблицы products название и цены трех самых дешевых товаров, которые есть на складе.

select name, price from products where count>0
order by price limit 3;

14) Выберите из таблицы orders три последних заказа (по дате date) стоимостью от 3000 рублей и выше. 
Данные отсортируйте по дате в обратном порядке.

select * from orders where sum>=3000 
order by date DESC limit 3;

15) В таблице products 17 записей. Сайт выводит название (name) и цену (price) товаров в алфавитном порядке, по 6 записей на страницу. Напишите SQL запрос для получения списка товаров для формирования последней страницы каталога. 
Товары, которых нет на складе, выводить не надо (таких товаров 2).

select name, price from products where count>0
order by name limit 6 offset 12;

16) Добавьте в таблицу orders данные о новом заказе стоимостью 3000 рублей. В заказе 3 товара (products).

INSERT INTO orders (id, products, sum) VALUES (6, 3, 3000)

17) Добавьте в таблицу products новый товар — «Xbox», стоимостью 30000 рублей в количестве (count) трех штук.

INSERT INTO products (id, name, count, price) VALUES (7, 'Xbox', 3, 30000)

18) Добавьте в таблицу products новый товар — «iMac 21», стоимостью 100100 рублей. 
Товар пока не завезли на склад.

insert into products (id, name, count, price) value (8, 'iMac 21', 0, 100100)

19) Добавьте в таблицу users нового пользователя Антона Пепеляева с датой рождения 12 июля 1992 года

insert into users (id, first_name, last_name, birthday) value (9, 'Антон', 'Пепеляев', '1992-07-12')

20) Добавьте в таблицу users нового пользователя Никиту Петрова. Дату рождения не указывайте.

insert into users SET id=10, first_name='Никита', last_name='Петров'

21) Добавьте одним SQL запросом в таблицу products следующие товары: 
* iPhone 7, цена 59990, 1 шт. 
* iPhone 8, цена 64990, 3 шт. 
* iPhone X, цена 79900, 2 шт.

INSERT INTO products (product_name, price, quantity)
VALUES
  ('iPhone 7', 59990, 1),
  ('iPhone 8', 64990, 3),
  ('iPhone X', 79900, 2);

22) Увеличьте в таблице users сотрудникам, у которых зарплата менее 20 000 рублей, зарплату (salary) на 10%.

update users set salary=salary*1.1 where salary<20000

23) В таблицу products внесли данные с ошибкой, вместо iMac в наименовании написали IMAC. Исправьте ошибку.

update products set name='iMac' where name = 'IMAC'

24) Проставьте всем заказам без статуса (status равен NULL) статус "new".

update orders set status='new' where status is NULL

25) В поле amount в таблице orders должно стоять число, которое равно произведению цены (sum) на количество (products_count). Но из-за сбоя в системе некоторые значения суммы получили 0 или NULL. Обновите таблицу, чтобы в поле amount были правильные значения.

update orders set amount=sum*products_count where amount=0 or amount is NULL

26) Измените статус (status) заказа под номером (id) 5 с delivery на success.

update orders set status='success' where id=5

27) Увеличьте цену 5 самых дешевых товаров на 5%.

update products set price=price*1.05 order by price limit 5

28) Увеличьте цену 5 самых дорогих товаров на 5%.

update products set price=price*1.05 order by price desc limit 5

29) Удалите из таблицы visits все данные с помощью конструкции DELETE.

DELETE FROM orders

30) Удалите из таблицы products все товары, которых нет на складе.

delete from products where count<1;

31) Удалите из таблицы cars все автомобили начиная с 2010 года и старше

delete from cars where year<=2010

32) Удалите из таблицы cars все корейские (country = "KR") автомобили, а также все автомобили мощностью (power) меньше 80 лс.

delete from cars where country = 'KR' or power<80

33) Удалите из таблицы cars все японские автомобили мощностью менее 80 и более 130 лс. (включая крайние значения.

delete from cars where country = "JP" and (power <= 80 or power >= 130)

34) 1) Выберите из таблицы orders 3 самых дешевых заказа за всё время.
Данные нужно отсортировать в порядке убывания цены.
Отмененные заказы не учитывайте.

SELECT *
FROM (
    SELECT *
    FROM orders
    WHERE status != 'cancelled'
    ORDER BY sum ASC
    LIMIT 3
) AS cheapest
ORDER BY sum DESC;

![изображение](https://github.com/user-attachments/assets/e26fff39-9523-4df2-80ba-7eda6a96c68f)

35) 2) Выберите из таблицы orders 2 самых дорогих заказов за всё время.
Данные нужно отсортировать в порядке убывания цены.
Отмененные заказы не учитывайте.

SELECT *
FROM orders
WHERE status != 'cancelled'
ORDER BY sum DESC
LIMIT 2;

![изображение](https://github.com/user-attachments/assets/a18ac2c0-7abc-4db2-adce-b7e421f6c4b6)

36) 3) Добавьте в таблицу orders данные о новом заказе стоимостью 8000 рублей. В заказе 4 товара (products)

INSERT INTO orders (id, products, sum)
VALUES (6, 4, 8000);

![изображение](https://github.com/user-attachments/assets/1e81714e-24b1-4522-bef2-8513851a7667)

37) 4) Добавьте в таблицу products новый товар — «VR-очки», стоимостью 70000 рублей в количестве (count) 2 штук.

INSERT INTO products (id, name, count, price)
VALUES (7, 'VR-очки', 2, 70000);

![изображение](https://github.com/user-attachments/assets/b2abfb56-9ef3-4bee-883a-5a708c5ae8f0)

38) 5) В таблицу products внесли данные с ошибкой, вместо "PS5" в наименовании написали IMAC. Исправьте ошибку.

UPDATE products
SET name = 'PS5'
WHERE name = 'IMAC';

![изображение](https://github.com/user-attachments/assets/bea7f10a-6c51-4d71-94c5-1ddcc39a971b)

39) Создайте таблицу users с полем id типа INT и двумя текстовыми полями, которые будут хранить имя (first_name) и фамилию (last_name). Длина имени и фамилии не превышает 50 символов.
Добавьте в таблицу трех пользователей: Дмитрия Иванова, Анатолия Белого и Дениса Давыдова.

CREATE TABLE users (
    id INT UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);

INSERT INTO users (first_name, last_name)
VALUES 
    ('Дмитрий', 'Иванов'),
    ('Анатолий', 'Белый'),
    ('Денис', 'Давыдов');

40) Создайте таблицу orders с полем id типа INT, полем state для хранения статуса заказа и полем amount для хранения суммы заказа. Статус заказа умещается в строку в 10 символов, а сумма заказа имеет целочисленный тип данных.
Заполните таблицу тремя заказами:
со статусом new на сумму 10000 рублей;
со статусом new на сумму 3400 рублей;
со статусом delivery на сумму 7300 рублей.

CREATE TABLE orders1 (
    id int, state VARCHAR (10), amount int
);
INSERT into orders1 (id, state, amount)
VALUES 
(1, 'new', 10000),
(2, 'new', 3400),
(3, 'delivery', 7300);

41) Создайте таблицу users с полем id типа INT и двумя строковыми полями, которые будут хранить имя и фамилию. Длина имени не превышает 20 символов, а фамилии 50 символов. Также добавьте в таблицу поле birthday типа DATE.
Заполните таблицу тремя пользователями:
Дмитрий Иванов, 12 августа 1995
Светлана Демчук, 8 июля 1993
Денис Антонов, 23 декабря 1996

CREATE TABLE users5 (
 id INT,
 first_name VARCHAR (20),
 last_name VARCHAR (50),
 birthday DATE
 );
INSERT INTO users5 (id, first_name, last_name, birthday)
VALUES 
(1, "Дмитрий","Иванов", '1995-08-12'),
(2, "Светлана","Демчук", '1995-08-12'),
(3, "Денис","Антонов", '1995-08-12');

42) Создайте таблицу messages с со следующими полями:
id типа INT;
subject типа VARCHAR длиной 100 символов
message тип TEXT;
add_date типа DATETIME;
is_public логического типа.
Добавьте в таблицу сообщение с темой «Первое сообщение» и текстом «Это мое первое сообщение!». Дату установите 12 декабря 2016 года 14 часов, 16 минут. Сообщение должно быть публичным.

CREATE TABLE messages (
id int, subject VARCHAR (100), message TEXT, add_date DATETIME, is_public BOOL);
INSERT INTO messages (id, subject, message, add_date, is_public)
VALUES
(1, 'Первое сообщение', 'Это мое первое сообщение!', '2016-12-12 14:16:00', TRUE);

43) Создайте таблицу rating
id типа INT;
car_id типа INT;
user_id типа INT;
rating типа FLOAT.
Добавьте в неё 4 записи 
(1,1,1,4.54),
(2,1,2,3.34),
(3,2,3,4.19),
(4,2,11,1.12)

CREATE TABLE rating (
id int, car_id int, user_id int, rating FLOAT);
INSERT INTO rating (id, car_id, user_id, rating)
VALUES
(1,1,1,4.54),
(2,1,2,3.34),
(3,2,3,4.19),
(4,2,11,1.12);

44)Создайте таблицу products для хранения информации о товарах в магазине. Выберите оптимальные поля для хранения данных в соответствии с условиями:
id типа INT – только положительные числа;
name – символьный тип до 100 символов;
count – количество товара на складе (до 200 штук);
price – цена в рублях без копеек (не более 1 млн рублей).
Заполните таблицу тремя товарами:
Холодильник, 10 штук, 50 000 рублей.
Стиральная машина, 0 штук, 23 570 рублей.
Утюг, 3 штуки, 7300 рублей

CREATE TABLE products
(id INT UNSIGNED, name VARCHAR(100), count TINYINT UNSIGNED, price MEDIUMINT UNSIGNED);
INSERT INTO products 
(id, name, count, price)
VALUES
(1, "Холодильник", 10, 50000),
(2, "Стиральная машина", 0, 23570),
(3, "Утюг", 3, 7300);

45) Создайте таблицу orders для хранения заказов в магазине. Выберите оптимальные поля для хранения данных в соответствии с условиями:
id – тип INT. Только положительные числа.
product_id – для хранения номера товара. Только положительные числа от 0 до 4294967295.
sale – скидка. Целое положительное число от 0 до 100.
amount – сумма заказа. Денежный тип. Максимальная сумма заказа 999999.99 рублей.
Добавьте три записи так, чтобы получалась таблица

CREATE TABLE orders
(id INT UNSIGNED, products_id INT UNSIGNED, sale TINYINT UNSIGNED, amount decimal(8,2));
INSERT INTO orders 
(id,products_id,sale,amount)
VALUES
(1, 245, 0, 230.5),
(2, 17, 15, 999999.99),
(3, 145677, 21, 1240.00)

46) Создайте таблицу films с информацией о фильмах. Выберете оптимальные поля для хранения данных в соответствии с условиями:
id типа INT, только положительные числа.
name – символьное поле длиной 100.
rating – рейтинг, вещественное число. Принимает положительные значения от 0 до 10.
country – страна фильма. Символьное поле, содержащее ровно 2 символа.
Добавьте в неё 3 записи так, чтобы получалась таблица ниже

CREATE TABLE films (
id INT UNSIGNED,
name VARCHAR (100),
rating FLOAT UNSIGNED,
country VARCHAR (2)
);
INSERT INTO films (id, name, rating, country)
VALUES (1, 'Большая буря', '3.45', 'RU'),
(2, 'Игра', '7.5714', 'US'),
(3, 'Война', '10', 'RU');

47) Создайте таблицу files для хранения информации о файлах. Выберете оптимальные поля исходя из условий ниже:
id — типа INT, только положительные числа.
filename — текстовое поле длиной 255 символов для хранения имени файла.
size — целочисленное поле для хранения размера файла в байтах. Только положительные числа. Могут храниться данные до 100 Гб.
filetype — поле для хранения типа файла, строка до 3 символов.
Добавьте 3 записи так, чтобы получалась таблица ниже:
('big_archive.zip', 81604378624, 'zip'),
('movie_37.mp4', 7838315315, 'mp4'),
('music007.mp3', 5242880, 'mp3');

CREATE TABLE files (
    id INT UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
    filename VARCHAR(255) NOT NULL,
    size BIGINT UNSIGNED NOT NULL,
    filetype CHAR(3) NOT NULL
);

INSERT INTO files (filename, size, filetype)
VALUES
    ('big_archive.zip', 81604378624, 'zip'),
    ('movie_37.mp4', 7838315315, 'mp4'),
    ('music007.mp3', 5242880, 'mp3');

DESCRIBE files;

48) Создайте таблицу users для хранения информации о пользователях сайта.
В таблице должны быть следующие поля:
id – идентификатор, целое положительное;
email – адрес электронной почты, строка не более 100 символов;
date_joined – дата регистрации (достаточно хранить дату, без времени)
last_activity – дата и время последней активности (с точностью до секунд).

create table users (
id int(10) unsigned,
email varchar (100),
date_joined date,
last_activity datetime
);
insert into users (id, email, date_joined,last_activity)
values
(1,'user1@domain.com', '2014-12-12','2016-04-08 12:34:54'),
(2,'user2@domain.com', '2014-12-12','2017-02-13 11:46:53'),
(3,'user3@domain.com', '2014-12-13','2017-04-04 05:12:07');

49) Создайте таблицу calendar для хранения календаря посетителей.
В таблице должны быть следующие поля:
id – идентификатор записи в календаре, целое положительное;
user_id – идентификатор пользователя, целое положительное;
doctor_id – идентификатор доктора, целое положительное;
visit_date – дата и время визита (точность до секунд).

Create table calendar (
id int unsigned,
user_id int unsigned,
doctor_id int unsigned,
visit_date datetime);
Insert into calendar (id, user_id, doctor_id, visit_date)
Values 
(1, 1914 , 1, '2017-04-08 12:00:00'),
(2, 12, 1, '2017-04-08 12:30:00'),
(3, 4641, 2, '2017-04-09 09:00:00'),
(4, 784, 1,'2017-04-08 13:00:00'),
(5, 15, 2,'2017-04-09 10:00:00');

50) Создайте таблицу users , в которой будут следующие поля:
id — идентификатор, целые положительные числа.
first_name— имя, строки до 50 символов.
last_name — фамилия, строки до 60 символов.
bio — биография, текст до 65000 символов.

create table users (
id int (10) unsigned,
first_name varchar (50),
last_name varchar (60),
bio text
);
INSERT INTO users (id, first_name, last_name, bio)
VALUES
(1,'Антон','Кулик','С отличием окончил 39 лицей.'),
(2,'Сергей','Давыдов',''),
(3,'Дмитрий','Соколов','Профессиональный программист.');

51) 1) Выберите из таблицы orders 4 самых дорогих заказов за всё время.
Данные нужно отсортировать в порядке убывания цены.
Отмененные заказы не учитывайте.

select * from orders where status != "cancelled" order by sum desc limit 4

52) 2) Выберите из таблицы products название и цены четырех самых дешевых товаров, которые есть на складе.

select name, price from products where count != 0 order by price limit 4

53) 3) Выберите из таблицы orders три последних заказа (по дате date) стоимостью от 3200 рублей и выше.
Данные отсортируйте по дате в обратном порядке.

select * from orders where sum >= 3200 order by date desc limit 3

54) 4) Создайте данную таблицу:

DROP TABLE IF EXISTS products;
CREATE TABLE products (
    id INT UNSIGNED NOT NULL,
    name VARCHAR(255) NULL,
    count INTEGER NULL,
    price INTEGER NULL
);
INSERT INTO products (id, name, count, price)
VALUES
    (1, 'Стиральная машина', 5, 10000),
    (2, 'Холодильник', 0, 10000),
    (3, 'Микроволновка', 3, 4000),
    (4, 'Пылесос', 2, 4500),
    (5, 'Вентилятор', 0, 700),
    (6, 'Телевизор', 7, 31740),
    (7, 'Тостер', 2, 2500),
    (8, 'Принтер', 4, 3000),
    (9, 'Активные колонки', 1, 2900),
    (10, 'Ноутбук', 4, 36990),
    (11, 'Посудомоечная машина', 0, 17800),
    (12, 'Видеорегистратор', 23, 4000),
    (13, 'Смартфон', 8, 12300),
    (14, 'Флешка', 4, 1400),
    (15, 'Блендер', 0, 5500),
    (16, 'Газовая плита', 5, 11900),
    (17, 'Клавиатура', 3, 1800);

55) 5) Из этой таблицы сделать выборку на основе задания: Сайт выводит товары по 5 штук. Выберите из таблицы products товары, которые пользователи увидят на 3 странице каталога при сортировке в порядке возрастания цены (price).

select * from products order by price limit 10,5

56) Создайте таблицу articles для хранения данных о статьях. В таблице должны быть следующие поля:
id — идентификатор, целое положительное, NULL запрещен
name — название статьи, строка до 80 символов.text — текст статьи.
state — статус статьи. Поле из 3 вариантов: draft (черновик), correction (корректура), public (опубликована).Добавьте 3 записи

Create table articles (
id int unsigned not null,
name varchar (80),
text text,
state enum('draft', 'correction', 'public')
);
insert into articles (id, name, text, state)
VALUES
(1, 'Новое в Python 3.6', '', 'draft'),
(2, 'Оптимизация SQL запросов', 'При больших объемах данных ...', 'correction'),
(3, 'Транзакции в MySQL', 'По долгу службы мне приходится ...', 'public');

57) Создайте таблицу rooms для хранения номеров в отеле:
id — идентификатор, целое положительное.
number — номер комнаты, целое положительное. Всего в отеле 107 комнат. NULL запрещен.
beds — количество спальных мест. Выбор из 1+1, 2+1, 2+2. Можно выбрать только один вариант. NULL запрещен.
additional — дополнительные удобства в номере. Можно выбрать несколько вариантов из списка: conditioner, bar, fridge и wifi.
Добавьте 3 записи

create table rooms (
id int unsigned not null,
number tinyint unsigned not null,
beds enum('1+1','2+1','2+2') not null,
additional set('conditioner','bar','fridge','wifi')
);
insert into rooms (id,number,beds,additional)
values
(1,10,'1+1','conditioner,bar,wifi'),
(2,12,'2+1',''),
(3,24,'2+2','fridge,bar,wifi');

58)Выберите из таблицы products название, цену и страны всех товаров из России и Белоруссии (в поле country обязательно должна присутствовать или Россия, или Белоруссия).
Выбирайте только товары, у которых задана категория.
Данные отсортируйте по цене в обратном порядке.
Поле country относится к типу SET('RU', 'UA', 'BY', 'KZ') NOT NULL.

SELECT name,price,country FROM products 
WHERE (find_in_set ('RU',country) OR find_in_set ('BY',country)) AND category_id IS NOT NULL ORDER BY price DESC

59) 1) Создайте таблицу orders для хранения списка заказов:
id — идентификатор, целое положительное.
user_id — идентификатор пользователя, который оформил заказ. Целое положительное, NULL запрещен.
amount — стоимость заказа. Целое положительное число не более 1 млн. NULL запрещен, по умолчанию 0.
created — дата и время создания заказа. NULL запрещен.
state — статус заказа. Выбор из new, cancelled, in_progress, delivered, completed. Можно выбрать только один вариант. NULL запрещен. По умолчанию должен стоять new.
Добавьте 3 записи так, чтобы получалась таблица ниже:

CREATE TABLE orders (
    id INT UNSIGNED NOT NULL PRIMARY KEY,
    user_id INT UNSIGNED NOT NULL,
    amount INT UNSIGNED NOT NULL DEFAULT 0 CHECK (amount <= 1000000),
    created DATETIME NOT NULL,
    state ENUM('new', 'cancelled', 'in_progress', 'delivered', 'completed') NOT NULL DEFAULT 'new'
);

INSERT INTO orders (id, user_id, amount, created)
VALUES
    (1, 56, 5400, '2018-02-01 17:46:59'),
    (2, 90, 249, '2018-02-01 19:13:04'),
    (3, 78, 2200, '2018-02-01 22:43:09');

60) 2) Создайте таблицу users для хранения списка пользователей сайта:
id — идентификатор, целое положительное.
first_name — имя, строка до 20 символов. NULL запрещен.
last_name — фамилия, строка до 20 символов. NULL запрещен.
patronymic — отчество, строка до 20 символов. NULL запрещен, по умолчанию пустая строка.
is_active — отметка об активности пользователя. Логическое поле, по умолчанию TRUE.
is_superuser — отметка администратора. Логическое поле, по умолчанию FALSE.
Добавьте 3 записи так, чтобы получалась таблица ниже:

CREATE TABLE users (
    id INT UNSIGNED NOT NULL PRIMARY KEY,
    first_name VARCHAR(20) NOT NULL,
    last_name VARCHAR(20) NOT NULL,
    patronymic VARCHAR(20) NOT NULL DEFAULT '',
    is_active BOOLEAN NOT NULL DEFAULT TRUE,
    is_superuser BOOLEAN NOT NULL DEFAULT FALSE
);

INSERT INTO users (id, first_name, last_name, patronymic, is_active, is_superuser)
VALUES
    (1, 'Дмитрий', 'Иванов', '', TRUE, FALSE),
    (2, 'Анатолий', 'Белый', 'Сергеевич', TRUE, TRUE),
    (3, 'Андрей', 'Крючков', '', FALSE, FALSE);

61) 3) Создайте таблицу products для хранения товаров в интернет магазине:
id — идентификатор, целое положительное.
category_id — категория, целое положительное. Может принимать NULL. По умолчанию NULL.
name — название, строка до 100 символов. NULL запрещен.
count — количество, целое положительное до 255. NULL запрещен, по умолчанию 0.
price — цена типа DECIMAL с 10 знаками, 2 из которых выделены для копеек. NULL запрещен, по умолчанию 0.00.
Добавьте 3 записи так, чтобы получалась таблица ниже:

CREATE TABLE products (
    id INT UNSIGNED NOT NULL PRIMARY KEY,
    category_id INT UNSIGNED DEFAULT NULL,
    name VARCHAR(100) NOT NULL,
    count TINYINT UNSIGNED NOT NULL DEFAULT 0 CHECK (count <= 255),
    price DECIMAL(10,2) NOT NULL DEFAULT 0.00
);

INSERT INTO products (id, category_id, name, count, price)
VALUES
    (1, 1, 'Кружка', 5, 45.90),
    (2, 17, 'Фломастеры', 0, 78.00),
    (3, NULL, 'Сникерс', 12, 50.80);

62) cоздайте таблицу users с со следующими полями:
id — идентификатор, целое положительное, первичный ключ без автоинкремента, NULL запрещен.
first_name — имя пользователя, строка до 50 символов.
last_name — фамилия пользователя, строка до 50 символов.
birthday — дата рождения. Пользователь может не указать день рождения и тогда в поле нужно хранить NULL.
Добавьте 3 записи

CREATE TABLE users (
id INT(10)UNSIGNED NOT NULL PRIMARY KEY,
first_name VARCHAR (50) NULL,
last_name VARCHAR (50) NULL,
birthday DATE NULL );
INSERT INTO users (id, first_name, last_name, birthday)
VALUES (1,'Дмитрий','Иванов',NULL),
(2,'Анатолий','Белый',NULL),
(3,'Денис','Давыдов','1995-09-08');

63) Создайте таблицу orders с автоинкрементальным первичным ключом id, полем state для хранения статуса заказа и полем amount для хранения суммы заказа. Статус заказа умещается в строку длиной 8 символов, а сумма заказа является денежным типом до 1 млн. с двумя знаками после десятичной точки.
Добавьте 3 записи 

create table orders (
id int unsigned not null primary key auto_increment,
state varchar (8),
amount decimal (8,2)
);
insert into orders (state, amount)
VALUES 
('new', 1000.50),
('new', 3400.10),
('delivery', 7300.00);



