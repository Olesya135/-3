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

16) 11.02
