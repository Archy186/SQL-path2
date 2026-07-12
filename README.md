**Задание 1**
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.
markdown
> ```sql
> SELECT 
>     CONCAT(s.first_name , " ", s.last_name) AS 'Сотрудник магазина', 
>     cm.city AS 'Город нахождения магазина', 
>     COUNT(c.customer_id) AS 'Количество пользователей'
> FROM staff AS s
> JOIN address AS a ON a.address_id = s.address_id
> JOIN city AS cm ON cm.city_id = a.city_id
> JOIN store AS st ON st.store_id = s.store_id
> JOIN customer AS c ON c.store_id = s.store_id
> GROUP BY staff_id
> HAVING COUNT(c.customer_id) > 300;
> ```
<img width="918" height="598" alt="1" src="https://github.com/user-attachments/assets/d4fe9286-f852-4958-b3a0-ed42dffe8103" />

**Задание 2**
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


> ```sql
> SELECT  
>     COUNT(*) AS 'Количество фильмов длиннее среднего',
>     (SELECT AVG(length) FROM film) AS 'Средняя длительность всех фильмов'
> FROM film
> WHERE length > (SELECT AVG(length) FROM film);
> ```
> <img width="915" height="557" alt="2" src="https://github.com/user-attachments/assets/624b759e-4460-43c8-a969-fc8664effc15" />

**Задание 3**
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
> ```sql
> SELECT 
>     SUM(amount) AS 'Платеж',
>     DATE_FORMAT(payment_date, '%Y-%m') AS 'Месяц',
>     COUNT(rental_id) AS 'Количество_аренд'
> FROM sakila.payment
> GROUP BY DATE_FORMAT(payment_date, '%Y-%m')
> ORDER BY SUM(amount) DESC 
> LIMIT 1;
> ```
> <img width="916" height="557" alt="3" src="https://github.com/user-attachments/assets/1816b75f-1233-4b15-8747-f3a1221b3802" />
