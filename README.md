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
