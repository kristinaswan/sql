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

Задание 3. Вывести все рейсы, совершенные из Москвы [(сайт)]([https://sql-academy.org/ru/trainer/tasks/2](https://sql-academy.org/ru/trainer/tasks/3))
<details><summary>Решение</summary>

```sql
SELECT *
FROM Trip
WHERE town_from='Moscow';
```

</details>
