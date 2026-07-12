> [!NOTE]
> **Задание 1:** Магазины с более чем 300 покупателями

```sql
SELECT 
    CONCAT(s.first_name , " ", s.last_name) AS 'Сотрудник магазина', 
    cm.city AS 'Город нахождения магазина', 
    COUNT(c.customer_id) AS 'Количество пользователей'
FROM staff AS s
JOIN address AS a ON a.address_id = s.address_id
JOIN city AS cm ON cm.city_id = a.city_id
JOIN store AS st ON st.store_id = s.store_id
JOIN customer AS c ON c.store_id = s.store_id
GROUP BY staff_id
HAVING COUNT(c.customer_id) > 300;
