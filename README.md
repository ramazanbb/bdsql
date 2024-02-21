# Домашнее задание к занятию "`SQL. Часть 2`" - `Рамазанов Бакит`

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.
```
SELECT s.store_id, count(c.customer_id) AS "number of buyers", ci.city, concat(st.last_name, ' ', st.first_name) AS "salesman"
FROM store s
JOIN customer c ON c.store_id = s.store_id
JOIN address a ON a.address_id = s.address_id
JOIN city ci ON ci.city_id = a.city_id
JOIN staff st ON st.store_id = s.store_id
GROUP BY s.store_id, ci.city_id, st.staff_id
HAVING count(c.customer_id) > 300;
```
### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
```
SELECT COUNT(film_id) AS 'number of films'
FROM (SELECT *, AVG(LENGTH) OVER () AS TIME FROM film) t
WHERE TIME < LENGTH;
```

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```
SELECT MONTH(p.payment_date) AS month, SUM(p.amount) AS 'total amount', count(p.rental_id) AS 'rentals by month'
FROM payment p
GROUP BY MONTH(p.payment_date)
ORDER BY SUM(p.amount) DESC
LIMIT 1;
```
