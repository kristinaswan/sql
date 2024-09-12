# Решения заданий интерактивного тренажера по SQL
Упражнения по SQL, приближенные к реальным профессиональным задачам

Ссылка на задания SQL тренажёра:  
https://sql-academy.org/ru/trainer

Задание 1. Вывести имена всех людей, которые есть в базе данных авиакомпаний. [(сайт)](https://sql-academy.org/ru/trainer/tasks/1)

<details><summary>Решение</summary>

```sql
SELECT name
FROM Passenger;
```

</details>

Задание 2. Вывести названия всеx авиакомпаний. [(сайт)](https://sql-academy.org/ru/trainer/tasks/2)

<details><summary>Решение</summary>

```sql
SELECT name  
FROM Company;
```

</details>

Задание 3. Вывести все рейсы, совершенные из Москвы. [(сайт)](https://sql-academy.org/ru/trainer/tasks/3)

<details><summary>Решение</summary>

```sql
SELECT *
FROM Trip
WHERE town_from = 'Moscow';
```

</details>

Задание 4. Вывести имена людей, которые заканчиваются на "man". [(сайт)](https://sql-academy.org/ru/trainer/tasks/4)

<details><summary>Решение</summary>

```sql
SELECT name
FROM Passenger
WHERE name LIKE '%man';
```

</details>

Задание 5. Вывести количество рейсов, совершенных на TU-134. [(сайт)](https://sql-academy.org/ru/trainer/tasks/5)

<details><summary>Решение</summary>

```sql
SELECT COUNT(plane) AS count
FROM Trip
WHERE plane = 'TU-134';
```

</details>

Задание 6. Какие компании совершали перелеты на Boeing. [(сайт)](https://sql-academy.org/ru/trainer/tasks/6)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT name
FROM Company
INNER JOIN Trip
  ON Company.id = Trip.company
WHERE plane = 'Boeing';
```

</details>

Задание 7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow). [(сайт)](https://sql-academy.org/ru/trainer/tasks/7)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT plane
FROM Trip
WHERE town_from = 'Moscow';
```

</details>

Задание 8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт? [(сайт)](https://sql-academy.org/ru/trainer/tasks/8)

<details><summary>Решение</summary>

```sql
SELECT town_to, TIME(time_in-time_out) AS flight_time
FROM Trip
WHERE town_from = 'Paris';
```

</details>

Задание 9. Какие компании организуют перелеты из Владивостока (Vladivostok)? [(сайт)](https://sql-academy.org/ru/trainer/tasks/9)

<details><summary>Решение</summary>

```sql
SELECT name
FROM Company
INNER JOIN Trip
  ON Company.id = Trip.company
WHERE town_from = 'Vladivostok';
```

</details>

Задание 10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.. [(сайт)](https://sql-academy.org/ru/trainer/tasks/10)

<details><summary>Решение</summary>

```sql
SELECT *
FROM Trip
WHERE time_out BETWEEN '1900-01-01T10:00:00.000Z' AND '1900-01-01T14:00:00.000Z';
```

</details>

Задание 11. Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени. [(сайт)](https://sql-academy.org/ru/trainer/tasks/11)

<details><summary>Решение</summary>

```sql
SELECT name
FROM Passenger
WHERE LENGTH(name) = (SELECT MAX(LENGTH(name)) FROM Passenger);
```

</details>

Задание 12. Вывести id и количество пассажиров для всех прошедших полётов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/12)

<details><summary>Решение</summary>

```sql
SELECT trip, COUNT(passenger) AS count
FROM Pass_in_trip
GROUP BY trip;
```

</details>

Задание 13. Вывести имена людей, у которых есть полный тёзка среди пассажиров. [(сайт)](https://sql-academy.org/ru/trainer/tasks/13)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT name.name
FROM Passenger AS name, Passenger AS same
WHERE name.id != same.id AND name.name=same.name;
```

</details>

Задание 14. В какие города летал Bruce Willis. [(сайт)](https://sql-academy.org/ru/trainer/tasks/14)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT town_to
FROM Trip
INNER JOIN Pass_in_trip
  ON Trip.id = Pass_in_trip.trip
INNER JOIN Passenger
  ON Pass_in_trip.passenger = Passenger.id
WHERE name = 'Bruce Willis';
```

</details>

Задание 15. Выведите дату и время прилёта пассажира Стив Мартин (Steve Martin) в Лондон (London). [(сайт)](https://sql-academy.org/ru/trainer/tasks/15)

<details><summary>Решение</summary>

```sql
SELECT Trip.time_in
FROM Passenger
INNER JOIN Pass_in_trip
  ON Passenger.id = Pass_in_trip.passenger
INNER JOIN TRIP
  ON Pass_in_trip.trip = Trip.id
WHERE (name = 'Steve Martin') AND (town_to = 'London');
```

</details>

Задание 16. Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет. [(сайт)](https://sql-academy.org/ru/trainer/tasks/16)

<details><summary>Решение</summary>

```sql
SELECT name, COUNT(trip) AS count
FROM Pass_in_trip
INNER JOIN Passenger
  ON Pass_in_trip.passenger = Passenger.id
GROUP BY name
HAVING count > 0
ORDER BY count DESC, name ASC;
```

</details>

Задание 17. Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили. [(сайт)](https://sql-academy.org/ru/trainer/tasks/17)

<details><summary>Решение</summary>

```sql
SELECT member_name, status, SUM(unit_price * amount) AS costs
FROM FamilyMembers
INNER JOIN Payments
  ON FamilyMembers.member_id = Payments.family_member
WHERE date LIKE '2005%'
GROUP BY member_name, status;
```

</details>

Задание 18. Выведите имя самого старшего человека. Если таких несколько, то выведите их всех. [(сайт)](https://sql-academy.org/ru/trainer/tasks/18)

<details><summary>Решение</summary>

```sql
SELECT member_name
FROM FamilyMembers
WHERE birthday = (SELECT MIN(birthday) FROM FamilyMembers);
```

</details>

Задание 19. Определить, кто из членов семьи покупал картошку (potato). [(сайт)](https://sql-academy.org/ru/trainer/tasks/19)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT status
FROM FamilyMembers
INNER JOIN Payments
  ON FamilyMembers.member_id = Payments.family_member
INNER JOIN Goods
  ON Payments.good = Goods.good_id
WHERE good_name = 'potato';
```

</details>

Задание 20. Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму. [(сайт)](https://sql-academy.org/ru/trainer/tasks/20)

<details><summary>Решение</summary>

```sql
SELECT status, member_name, SUM(unit_price * amount) AS costs
FROM FamilyMembers
INNER JOIN Payments
  ON FamilyMembers.member_id = Payments.family_member
INNER JOIN Goods
  ON Payments.good = Goods.good_id
INNER JOIN GoodTypes
  ON Goods.type = GoodTypes.good_type_id
WHERE good_type_name = 'entertainment'
GROUP BY status, member_name;
```

</details>

Задание 21. Определить товары, которые покупали более 1 раза. [(сайт)](https://sql-academy.org/ru/trainer/tasks/21)

<details><summary>Решение</summary>

```sql
SELECT good_name
FROM Goods
INNER JOIN Payments
  ON Goods.good_id = Payments.good
GROUP BY good
HAVING COUNT(amount) > 1;
```

</details>

Задание 22. Найти имена всех матерей (mother). [(сайт)](https://sql-academy.org/ru/trainer/tasks/22)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT member_name
FROM FamilyMembers
WHERE status = 'mother';
```

</details>

Задание 23. Найдите самый дорогой деликатес (delicacies) и выведите его цену. [(сайт)](https://sql-academy.org/ru/trainer/tasks/23)

<details><summary>Решение</summary>

```sql
SELECT good_name, unit_price
FROM GoodTypes
INNER JOIN Goods
  ON GoodTypes.good_type_id = Goods.type
INNER JOIN Payments
  ON Goods.good_id = Payments.good
WHERE good_type_name = 'delicacies'
LIMIT 1;
```

</details>

Задание 24. Определить кто и сколько потратил в июне 2005. [(сайт)](https://sql-academy.org/ru/trainer/tasks/24)

<details><summary>Решение</summary>

```sql
SELECT member_name, SUM(unit_price * amount) AS costs
FROM FamilyMembers
INNER JOIN Payments
  ON FamilyMembers.member_id = Payments.family_member
WHERE date LIKE '2005-06-%'
GROUP BY member_name;
```

</details>

Задание 25. Определить, какие товары не покупались в 2005 году. [(сайт)](https://sql-academy.org/ru/trainer/tasks/25)

<details><summary>Решение</summary>

```sql
SELECT good_name
FROM Goods
WHERE good_id NOT IN (
  SELECT good
  FROM Payments
  WHERE YEAR(date) = 2005
);
```

</details>

Задание 26. Определить группы товаров, которые не приобретались в 2005 году. [(сайт)](https://sql-academy.org/ru/trainer/tasks/26)

<details><summary>Решение</summary>

```sql
SELECT good_type_name
FROM GoodTypes
WHERE good_type_id NOT IN (
    SELECT type 
    FROM Goods
    LEFT JOIN Payments
      ON Goods.good_id = Payments.good
    WHERE YEAR(date) = 2005
);
```

</details>

Задание 27. Узнайте, сколько было потрачено на каждую из групп товаров в 2005 году. Выведите название группы и потраченную на неё сумму. Если потраченная сумма равна нулю, т.е. товары из этой группы не покупались в 2005 году, то не выводите её. [(сайт)](https://sql-academy.org/ru/trainer/tasks/27)

<details><summary>Решение</summary>

```sql
SELECT good_type_name, SUM(amount * unit_price) AS costs
FROM Payments
RIGHT JOIN Goods
  ON Payments.good = Goods.good_id
RIGHT JOIN GoodTypes
  ON Goods.type = GoodTypes.good_type_id
WHERE YEAR(date) = 2005
GROUP BY good_type_name
ORDER BY costs;
```

</details>

Задание 28. Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow)? [(сайт)](https://sql-academy.org/ru/trainer/tasks/28)

<details><summary>Решение</summary>

```sql
SELECT COUNT(id) AS count
FROM Trip
WHERE (town_from = 'Rostov') AND (town_to = 'Moscow');
```

</details>

Задание 29. Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134. [(сайт)](https://sql-academy.org/ru/trainer/tasks/29)

<details><summary>Решение</summary>

```sql
SELECT DISTINCT name
FROM Passenger
INNER JOIN Pass_in_trip
  ON Passenger.id = Pass_in_trip.passenger
INNER JOIN Trip
  ON Pass_in_trip.trip=Trip.id
WHERE town_to = 'Moscow' AND plane = 'TU-134';
```

</details>

Задание 30. Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности. [(сайт)](https://sql-academy.org/ru/trainer/tasks/30)

<details><summary>Решение</summary>

```sql
SELECT trip, COUNT(passenger) as count
FROM Pass_in_trip
GROUP BY trip
ORDER BY COUNT(passenger) DESC ;
```

</details>

Задание .  [(сайт)]()
<details><summary>Решение</summary>

```sql
;
```

</details>
