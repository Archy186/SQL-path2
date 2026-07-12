# SQL-path2
> **Задание 1:** Получить информацию о магазине, в котором обслуживается более 300 покупателей.
> 
> **Что делает запрос:**
> - Объединяет таблицы staff, address, city, store и customer
> - Группирует данные по сотрудникам магазинов
> - Оставляет только те магазины, где количество покупателей > 300
> - Выводит полное имя сотрудника, город и количество покупателей

```sql
SELECT 
    CONCAT(s.first_name, ' ', s.last_name) AS 'Сотрудник магазина',
    cm.city AS 'Город нахождения магазина',
    COUNT(c.customer_id) AS 'Количество пользователей'
FROM staff AS s
JOIN address AS a ON a.address_id = s.address_id
JOIN city AS cm ON cm.city_id = a.city_id
JOIN store AS st ON st.store_id = s.store_id
JOIN customer AS c ON c.store_id = s.store_id
GROUP BY s.staff_id, s.first_name, s.last_name, cm.city
HAVING COUNT(c.customer_id) > 300;




Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
Решение 

SELECT COUNT(film_id) Число_фильмов, (SELECT AVG(length) FROM sakila.film) Средняя_длительность
FROM sakila.film 
WHERE length > (SELECT AVG(length) FROM sakila.film);

<img width="918" height="598" alt="2" src="https://github.com/user-attachments/assets/749d1a2c-1b5d-43f9-bb0e-4b1f92418b52" />
Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
Решение

SELECT SUM(amount) Платеж, DATE_FORMAT(payment_date, '%Y-%m') Месяц, COUNT(rental_id) Количество_аренд 
FROM sakila.payment
GROUP BY DATE_FORMAT(payment_date, '%Y-%m')
ORDER BY SUM(amount) DESC 
LIMIT 1;

<img width="918" height="598" alt="3" src="https://github.com/user-attachments/assets/04df3b9b-0323-4208-ae40-0b89a00837a0" />

