Задание 1
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
