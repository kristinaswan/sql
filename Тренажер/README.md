# Решения заданий интерактивного тренажера по SQL
Упражнения по SQL, приближенные к реальным профессиональным задачам

Ссылка на задания SQL тренажёра:  
https://sql-academy.org/ru/trainer

Задание 1. Вывести имена всех людей, которые есть в базе данных авиакомпаний [(сайт)](https://sql-academy.org/ru/trainer/tasks/1)
<details><summary>Решение</summary>

```sql
SELECT name
FROM Passenger;
```

</details>

Задание 2. Вывести названия всеx авиакомпаний [(сайт)](https://sql-academy.org/ru/trainer/tasks/2)
<details><summary>Решение</summary>

```sql
SELECT name  
FROM Company;
```

</details>

Задание 3. Вывести все рейсы, совершенные из Москвы [(сайт)](https://sql-academy.org/ru/trainer/tasks/3)
<details><summary>Решение</summary>

```sql
SELECT *
FROM Trip
WHERE town_from = 'Moscow';
```

</details>

Задание 4. Вывести имена людей, которые заканчиваются на "man" [(сайт)](https://sql-academy.org/ru/trainer/tasks/4)
<details><summary>Решение</summary>

```sql
SELECT name
FROM Passenger
WHERE name LIKE '%man';
```

</details>

Задание 5. Вывести количество рейсов, совершенных на TU-134 [(сайт)](https://sql-academy.org/ru/trainer/tasks/5)
<details><summary>Решение</summary>

```sql
SELECT COUNT(plane) AS count
FROM Trip
WHERE plane = 'TU-134';
```

</details>

Задание 6. Какие компании совершали перелеты на Boeing [(сайт)](https://sql-academy.org/ru/trainer/tasks/6)
<details><summary>Решение</summary>

```sql
SELECT DISTINCT name
FROM Company
INNER JOIN Trip ON Company.id = Trip.company
WHERE plane = 'Boeing';
```

</details>

Задание 7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow) [(сайт)](https://sql-academy.org/ru/trainer/tasks/7)
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
INNER JOIN Trip ON Company.id = Trip.company
WHERE town_from = 'Vladivostok';
```

</details>

Задание 10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г. [(сайт)](https://sql-academy.org/ru/trainer/tasks/10)
<details><summary>Решение</summary>

```sql
SELECT *
FROM Trip
WHERE time_out BETWEEN '1900-01-01T10:00:00.000Z' AND '1900-01-01T14:00:00.000Z';
```

</details>
