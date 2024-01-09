# Домашнее задание к занятию «SQL. Часть 2»

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.


---

### Решение 1

#### Листинг запроса:

```
	SELECT COUNT(customer_id) AS 'Customer summary', CONCAT(s.first_name,'  ',s.last_name) AS 'Saler Name' ,city
	from customer c
	INNER JOIN store st ON st.store_id = c.store_id
	INNER JOIN staff s  ON s.staff_id  = st.manager_staff_id
	INNER JOIN address a ON a.address_id = s.address_id
	INNER JOIN city ct ON ct.city_id = a.city_id
	GROUP BY s.first_name,s.last_name,city
	HAVING COUNT(c.customer_id)  > 300;
```

#### Скриншот запроса:

![Commit Task1](https://github.com/AndrewZnamenskiy/SQL2/blob/main/img/task1p1.png)


### Решение 2


#### Листинг запроса:

```
	SELECT f.title, f.length
	from film f
	WHERE  f.length > (SELECT AVG(f.length) from film f)
	ORDER BY f.length

```

#### Скриншот запроса:

![Commit Task2](https://github.com/AndrewZnamenskiy/SQL2/blob/main/img/task2p1.png)


### Решение 3


#### Листинг запроса:

```
	SELECT SUM(amount),MONTH(payment_date),COUNT(p.rental_id) 
	from payment p 
	GROUP by MONTH(payment_date)
	ORDER BY SUM(amount) DESC
	LIMIT 1;
```

#### Скриншот запроса:

![Commit Task3](https://github.com/AndrewZnamenskiy/SQL2/blob/main/img/task3p1.png)


