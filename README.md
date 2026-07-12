# SQL-path2
Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.
Решение 
SELECT CONCAT(sf.first_name, ' ', sf.last_name) Сотрудник, c.city Город, COUNT(c2.store_id) Число_пользователей
FROM sakila.staff sf
INNER JOIN sakila.store st ON st.store_id = sf.store_id
INNER JOIN sakila.address a ON a.address_id = sf.address_id
INNER JOIN sakila.city c ON c.city_id  = a.city_id
INNER JOIN sakila.customer c2 ON c2.store_id = sf.store_id
GROUP BY sf.staff_id
HAVING COUNT(c2.store_id) > 300;
<img width="918" height="598" alt="1" src="https://github.com/user-attachments/assets/3905d909-aa42-4345-b59a-bf50593fe6e6" />

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

