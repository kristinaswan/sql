# Решения заданий интерактивного тренажера по SQL
Упражнения по SQL, приближенные к реальным профессиональным задачам

Ссылка на задания SQL тренажёра:  
https://sql-academy.org/ru/trainer

Задание 1. Вывести имена всех людей, которые есть в базе данных авиакомпаний. [(сайт)](https://sql-academy.org/ru/trainer/tasks/1)

<details><summary>Решение</summary>

```sql
SELECT 
  name 
FROM 
  Passenger;
```

</details>

Задание 2. Вывести названия всеx авиакомпаний. [(сайт)](https://sql-academy.org/ru/trainer/tasks/2)

<details><summary>Решение</summary>

```sql
SELECT
  name  
FROM
  Company;
```

</details>

Задание 3. Вывести все рейсы, совершенные из Москвы. [(сайт)](https://sql-academy.org/ru/trainer/tasks/3)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  Trip 
WHERE 
  town_from = 'Moscow';
```

</details>

Задание 4. Вывести имена людей, которые заканчиваются на "man". [(сайт)](https://sql-academy.org/ru/trainer/tasks/4)

<details><summary>Решение</summary>

```sql
SELECT 
  name 
FROM 
  Passenger 
WHERE 
  name LIKE '%man';
```

</details>

Задание 5. Вывести количество рейсов, совершенных на TU-134. [(сайт)](https://sql-academy.org/ru/trainer/tasks/5)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(plane) AS count 
FROM 
  Trip 
WHERE 
  plane = 'TU-134';
```

</details>

Задание 6. Какие компании совершали перелеты на Boeing. [(сайт)](https://sql-academy.org/ru/trainer/tasks/6)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT name 
FROM 
  Company 
  INNER JOIN Trip ON Company.id = Trip.company 
WHERE 
  plane = 'Boeing';
```

</details>

Задание 7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow). [(сайт)](https://sql-academy.org/ru/trainer/tasks/7)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT plane 
FROM 
  Trip 
WHERE 
  town_from = 'Moscow';
```

</details>

Задание 8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт? [(сайт)](https://sql-academy.org/ru/trainer/tasks/8)

<details><summary>Решение</summary>

```sql
SELECT 
  town_to, 
  TIME(time_in - time_out) AS flight_time 
FROM 
  Trip 
WHERE 
  town_from = 'Paris';
```

</details>

Задание 9. Какие компании организуют перелеты из Владивостока (Vladivostok)? [(сайт)](https://sql-academy.org/ru/trainer/tasks/9)

<details><summary>Решение</summary>

```sql
SELECT 
  name 
FROM 
  Company 
  INNER JOIN Trip ON Company.id = Trip.company 
WHERE 
  town_from = 'Vladivostok';
```

</details>

Задание 10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.. [(сайт)](https://sql-academy.org/ru/trainer/tasks/10)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  Trip 
WHERE 
  time_out BETWEEN '1900-01-01T10:00:00.000Z' 
  AND '1900-01-01T14:00:00.000Z';
```

</details>

Задание 11. Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени. [(сайт)](https://sql-academy.org/ru/trainer/tasks/11)

<details><summary>Решение</summary>

```sql
SELECT 
  name 
FROM 
  Passenger 
WHERE 
  LENGTH(name) = (
    SELECT 
      MAX(
        LENGTH(name)
      ) 
    FROM 
      Passenger
  );
```

</details>

Задание 12. Вывести id и количество пассажиров для всех прошедших полётов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/12)

<details><summary>Решение</summary>

```sql
SELECT 
  trip, 
  COUNT(passenger) AS count 
FROM 
  Pass_in_trip 
GROUP BY 
  trip;
```

</details>

Задание 13. Вывести имена людей, у которых есть полный тёзка среди пассажиров. [(сайт)](https://sql-academy.org/ru/trainer/tasks/13)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT name.name 
FROM 
  Passenger AS name, 
  Passenger AS same 
WHERE 
  name.id != same.id 
  AND name.name = same.name;
```

</details>

Задание 14. В какие города летал Bruce Willis. [(сайт)](https://sql-academy.org/ru/trainer/tasks/14)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT town_to 
FROM 
  Trip 
  INNER JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip 
  INNER JOIN Passenger ON Pass_in_trip.passenger = Passenger.id 
WHERE 
  name = 'Bruce Willis';
```

</details>

Задание 15. Выведите дату и время прилёта пассажира Стив Мартин (Steve Martin) в Лондон (London). [(сайт)](https://sql-academy.org/ru/trainer/tasks/15)

<details><summary>Решение</summary>

```sql
SELECT 
  Trip.time_in 
FROM 
  Passenger 
  INNER JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger 
  INNER JOIN TRIP ON Pass_in_trip.trip = Trip.id 
WHERE 
  (name = 'Steve Martin') 
  AND (town_to = 'London');
```

</details>

Задание 16. Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет. [(сайт)](https://sql-academy.org/ru/trainer/tasks/16)

<details><summary>Решение</summary>

```sql
SELECT 
  name, 
  COUNT(trip) AS count 
FROM 
  Pass_in_trip 
  INNER JOIN Passenger ON Pass_in_trip.passenger = Passenger.id 
GROUP BY 
  name 
HAVING 
  count > 0 
ORDER BY 
  count DESC, 
  name ASC;
```

</details>

Задание 17. Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили. [(сайт)](https://sql-academy.org/ru/trainer/tasks/17)

<details><summary>Решение</summary>

```sql
SELECT 
  member_name, 
  status, 
  SUM(unit_price * amount) AS costs 
FROM 
  FamilyMembers 
  INNER JOIN Payments ON FamilyMembers.member_id = Payments.family_member 
WHERE 
  date LIKE '2005%' 
GROUP BY 
  member_name, 
  status;
```

</details>

Задание 18. Выведите имя самого старшего человека. Если таких несколько, то выведите их всех. [(сайт)](https://sql-academy.org/ru/trainer/tasks/18)

<details><summary>Решение</summary>

```sql
SELECT 
  member_name 
FROM 
  FamilyMembers 
WHERE 
  birthday = (
    SELECT 
      MIN(birthday) 
    FROM 
      FamilyMembers
  );
```

</details>

Задание 19. Определить, кто из членов семьи покупал картошку (potato). [(сайт)](https://sql-academy.org/ru/trainer/tasks/19)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT status 
FROM 
  FamilyMembers 
  INNER JOIN Payments ON FamilyMembers.member_id = Payments.family_member 
  INNER JOIN Goods ON Payments.good = Goods.good_id 
WHERE 
  good_name = 'potato';
```

</details>

Задание 20. Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму. [(сайт)](https://sql-academy.org/ru/trainer/tasks/20)

<details><summary>Решение</summary>

```sql
SELECT 
  status, 
  member_name, 
  SUM(unit_price * amount) AS costs 
FROM 
  FamilyMembers 
  INNER JOIN Payments ON FamilyMembers.member_id = Payments.family_member 
  INNER JOIN Goods ON Payments.good = Goods.good_id 
  INNER JOIN GoodTypes ON Goods.type = GoodTypes.good_type_id 
WHERE 
  good_type_name = 'entertainment' 
GROUP BY 
  status, 
  member_name;
```

</details>

Задание 21. Определить товары, которые покупали более 1 раза. [(сайт)](https://sql-academy.org/ru/trainer/tasks/21)

<details><summary>Решение</summary>

```sql
SELECT 
  good_name 
FROM 
  Goods 
  INNER JOIN Payments ON Goods.good_id = Payments.good 
GROUP BY 
  good 
HAVING 
  COUNT(amount) > 1;
```

</details>

Задание 22. Найти имена всех матерей (mother). [(сайт)](https://sql-academy.org/ru/trainer/tasks/22)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT member_name 
FROM 
  FamilyMembers 
WHERE 
  status = 'mother';
```

</details>

Задание 23. Найдите самый дорогой деликатес (delicacies) и выведите его цену. [(сайт)](https://sql-academy.org/ru/trainer/tasks/23)

<details><summary>Решение</summary>

```sql
SELECT 
  good_name, 
  unit_price 
FROM 
  GoodTypes 
  INNER JOIN Goods ON GoodTypes.good_type_id = Goods.type 
  INNER JOIN Payments ON Goods.good_id = Payments.good 
WHERE 
  good_type_name = 'delicacies' 
LIMIT 
  1;
```

</details>

Задание 24. Определить кто и сколько потратил в июне 2005. [(сайт)](https://sql-academy.org/ru/trainer/tasks/24)

<details><summary>Решение</summary>

```sql
SELECT 
  member_name, 
  SUM(unit_price * amount) AS costs 
FROM 
  FamilyMembers 
  INNER JOIN Payments ON FamilyMembers.member_id = Payments.family_member 
WHERE 
  date LIKE '2005-06-%' 
GROUP BY 
  member_name;
```

</details>

Задание 25. Определить, какие товары не покупались в 2005 году. [(сайт)](https://sql-academy.org/ru/trainer/tasks/25)

<details><summary>Решение</summary>

```sql
SELECT 
  good_name 
FROM 
  Goods 
WHERE 
  good_id NOT IN (
    SELECT 
      good 
    FROM 
      Payments 
    WHERE 
      YEAR(date) = 2005
  );
```

</details>

Задание 26. Определить группы товаров, которые не приобретались в 2005 году. [(сайт)](https://sql-academy.org/ru/trainer/tasks/26)

<details><summary>Решение</summary>

```sql
SELECT 
  good_type_name 
FROM 
  GoodTypes 
WHERE 
  good_type_id NOT IN (
    SELECT 
      type 
    FROM 
      Goods 
      LEFT JOIN Payments ON Goods.good_id = Payments.good 
    WHERE 
      YEAR(date) = 2005
  );
```

</details>

Задание 27. Узнайте, сколько было потрачено на каждую из групп товаров в 2005 году. Выведите название группы и потраченную на неё сумму. Если потраченная сумма равна нулю, т.е. товары из этой группы не покупались в 2005 году, то не выводите её. [(сайт)](https://sql-academy.org/ru/trainer/tasks/27)

<details><summary>Решение</summary>

```sql
SELECT 
  good_type_name, 
  SUM(amount * unit_price) AS costs 
FROM 
  Payments 
  RIGHT JOIN Goods ON Payments.good = Goods.good_id 
  RIGHT JOIN GoodTypes ON Goods.type = GoodTypes.good_type_id 
WHERE 
  YEAR(date) = 2005 
GROUP BY 
  good_type_name 
ORDER BY 
  costs;
```

</details>

Задание 28. Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow)? [(сайт)](https://sql-academy.org/ru/trainer/tasks/28)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(id) AS count 
FROM 
  Trip 
WHERE 
  (town_from = 'Rostov') 
  AND (town_to = 'Moscow');
```

</details>

Задание 29. Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134. [(сайт)](https://sql-academy.org/ru/trainer/tasks/29)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT name 
FROM 
  Passenger 
  INNER JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger 
  INNER JOIN Trip ON Pass_in_trip.trip = Trip.id 
WHERE 
  town_to = 'Moscow' 
  AND plane = 'TU-134';
```

</details>

Задание 30. Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности. [(сайт)](https://sql-academy.org/ru/trainer/tasks/30)

<details><summary>Решение</summary>

```sql
SELECT 
  trip, 
  COUNT(passenger) AS count 
FROM 
  Pass_in_trip 
GROUP BY 
  trip 
ORDER BY 
  COUNT(passenger) DESC;
```

</details>

Задание 31. Вывести всех членов семьи с фамилией Quincey. [(сайт)](https://sql-academy.org/ru/trainer/tasks/31)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  FamilyMembers 
WHERE 
  member_name LIKE '% Quincey';
```

</details>

Задание 32. Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону. [(сайт)](https://sql-academy.org/ru/trainer/tasks/32)

<details><summary>Решение</summary>

```sql
SELECT 
  FLOOR(
    AVG(
      TIMESTAMPDIFF(YEAR, birthday, CURRENT_DATE)
    )
  ) AS age 
FROM 
  FamilyMembers;
```

</details>

Задание 33. Найдите среднюю цену икры на основе данных, хранящихся в таблице Payments. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar). В ответе должна быть одна строка со средней ценой всей купленной когда-либо икры. [(сайт)](https://sql-academy.org/ru/trainer/tasks/33)

<details><summary>Решение</summary>

```sql
SELECT 
  AVG(unit_price) AS cost 
FROM 
  Payments 
  INNER JOIN Goods ON Payments.good = Goods.good_id 
WHERE 
  good_name LIKE '%caviar';
```

</details>

Задание 34. Сколько всего 10-ых классов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/34)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(name) AS count 
FROM 
  Class 
WHERE 
  name LIKE '10%';
```

</details>

Задание 35. Сколько различных кабинетов школы использовались 2 сентября 2019 года для проведения занятий? [(сайт)](https://sql-academy.org/ru/trainer/tasks/35)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(DISTINCT classroom) AS count 
FROM 
  Schedule 
WHERE 
  date LIKE '2019-09-02%';
```

</details>

Задание 36. Выведите информацию об обучающихся живущих на улице Пушкина (ul. Pushkina)? [(сайт)](https://sql-academy.org/ru/trainer/tasks/36)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  Student 
WHERE 
  address LIKE 'ul. Pushkina%';
```

</details>

Задание 37. Сколько лет самому молодому обучающемуся? [(сайт)](https://sql-academy.org/ru/trainer/tasks/37)

<details><summary>Решение</summary>

```sql
SELECT 
  MIN(
    TIMESTAMPDIFF(YEAR, birthday, CURRENT_DATE)
  ) AS year 
FROM 
  Student;
```

</details>

Задание 38. Сколько Анн (Anna) учится в школе? [(сайт)](https://sql-academy.org/ru/trainer/tasks/38)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(first_name) AS count 
FROM 
  Student 
WHERE 
  first_name = 'Anna';
```

</details>

Задание 39. Сколько обучающихся в 10 B классе? [(сайт)](https://sql-academy.org/ru/trainer/tasks/39)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(student) AS count 
FROM 
  Student_in_class 
  INNER JOIN Class ON Student_in_class.class = Class.id 
WHERE 
  name = '10 B';
```

</details>

Задание 40. Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.). Обратите внимание, что в базе данных есть несколько учителей с такими фамилией и инициалами. [(сайт)](https://sql-academy.org/ru/trainer/tasks/40)

<details><summary>Решение</summary>

```sql
SELECT 
  Subject.name AS subjects 
FROM 
  Teacher 
  RIGHT JOIN Schedule ON Teacher.id = Schedule.teacher 
  LEFT JOIN Subject ON Schedule.subject = Subject.id 
WHERE 
  first_name LIKE 'P%' 
  AND middle_name LIKE 'P%' 
  AND last_name = 'Romashkin';
```

</details>

Задание 41. Выясните, во сколько по расписанию начинается четвёртое занятие. [(сайт)](https://sql-academy.org/ru/trainer/tasks/41)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT start_pair 
FROM 
  Timepair 
  INNER JOIN Schedule ON Timepair.id = Schedule.number_pair 
WHERE 
  number_pair = '4';
```

</details>

Задание 42. Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет? [(сайт)](https://sql-academy.org/ru/trainer/tasks/42)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT (
    TIMEDIFF(
      (
        SELECT 
          end_pair 
        FROM 
          Timepair 
        WHERE 
          id = 4
      ), 
      (
        SELECT 
          start_pair 
        FROM 
          Timepair 
        WHERE 
          id = 2
      )
    )
  ) AS time 
FROM 
  Timepair;
```

</details>

Задание 43. Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отсортируйте преподавателей по фамилии в алфавитном порядке. [(сайт)](https://sql-academy.org/ru/trainer/tasks/43)

<details><summary>Решение</summary>

```sql
SELECT 
  last_name 
FROM 
  Teacher 
  INNER JOIN Schedule ON Teacher.id = Schedule.teacher 
  INNER JOIN Subject ON Schedule.subject = Subject.id 
WHERE 
  Subject.name = 'Physical Culture' 
ORDER BY 
  last_name;
```

</details>

Задание 44. Найдите максимальный возраст (количество лет) среди обучающихся 10 классов на сегодняшний день. Для получения текущих даты и времени используйте функцию NOW(). [(сайт)](https://sql-academy.org/ru/trainer/tasks/44)

<details><summary>Решение</summary>

```sql
SELECT 
  MAX(
    TIMESTAMPDIFF(YEAR, birthday, NOW())
  ) AS max_year 
FROM 
  Student 
  JOIN Student_in_class ON Student.id = Student_in_class.student 
  JOIN Class ON Student_in_class.class = Class.id 
WHERE 
  Class.name LIKE '10%';
```

</details>

Задание 45. Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз. [(сайт)](https://sql-academy.org/ru/trainer/tasks/45)

<details><summary>Решение</summary>

```sql
SELECT 
  classroom 
FROM 
  Schedule 
GROUP BY 
  classroom 
HAVING 
  COUNT(classroom) = (
    SELECT 
      COUNT(classroom) 
    FROM 
      Schedule 
    GROUP BY 
      classroom 
    ORDER BY 
      COUNT(classroom) DESC 
    LIMIT 
      1
  );
```

</details>

Задание 46. В каких классах введет занятия преподаватель "Krauze"? [(сайт)](https://sql-academy.org/ru/trainer/tasks/46)

<details><summary>Решение</summary>

```sql
SELECT 
  DISTINCT name 
FROM 
  Class 
  INNER JOIN Schedule ON Class.id = Schedule.class 
  INNER JOIN Teacher ON Schedule.teacher = Teacher.id 
WHERE 
  last_name = 'Krauze';
```

</details>

Задание 47. Сколько занятий провел Krauze 30 августа 2019 г.? [(сайт)](https://sql-academy.org/ru/trainer/tasks/47)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(class) AS count 
FROM 
  Schedule 
  INNER JOIN Teacher ON Schedule.teacher = Teacher.id 
WHERE 
  (last_name = 'Krauze') 
  AND (date LIKE '2019-08-30%');
```

</details>

Задание 48. Выведите заполненность классов в порядке убывания. [(сайт)](https://sql-academy.org/ru/trainer/tasks/48)

<details><summary>Решение</summary>

```sql
SELECT 
  name, 
  COUNT(Student_in_class.id) AS count 
FROM 
  Class 
  INNER JOIN Student_in_class ON Class.id = Student_in_class.class 
GROUP BY 
  name 
ORDER BY 
  count DESC;
```

</details>

Задание 49. Какой процент обучающихся учится в "10 A" классе? Выведите ответ в диапазоне от 0 до 100 с округлением до четырёх знаков после запятой, например, 96.0201. [(сайт)](https://sql-academy.org/ru/trainer/tasks/49)

<details><summary>Решение</summary>

```sql
SELECT 
  COUNT(student) / (
    SELECT 
      COUNT(student) 
    FROM 
      Student_in_class
  ) * 100 AS percent 
FROM 
  Student_in_class 
  JOIN Class ON Student_in_class.class = Class.id 
WHERE 
  name = '10 A';
```

</details>

Задание 50. Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону. [(сайт)](https://sql-academy.org/ru/trainer/tasks/50)

<details><summary>Решение</summary>

```sql
SELECT 
  FLOOR(
    COUNT(id) / (
      SELECT 
        COUNT(id) 
      FROM 
        Student
    ) * 100
  ) AS percent 
FROM 
  Student 
WHERE 
  birthday LIKE '2000%';
```

</details>

Задание 51. Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods). [(сайт)](https://sql-academy.org/ru/trainer/tasks/51)

<details><summary>Решение</summary>

```sql
INSERT INTO Goods 
SET 
  good_id = (
    SELECT 
      COUNT(*)+ 1 
    FROM 
      Goods a
  ), 
  good_name = 'Cheese', 
  type = (
    SELECT 
      good_type_id 
    FROM 
      GoodTypes 
    WHERE 
      good_type_name = 'food'
  );
```

</details>

Задание 52. Добавьте в список типов товаров (GoodTypes) новый тип "auto". [(сайт)](https://sql-academy.org/ru/trainer/tasks/52)

<details><summary>Решение</summary>

```sql
INSERT INTO GoodTypes 
SET 
  good_type_id = (
    SELECT 
      COUNT(*)+ 1 
    FROM 
      GoodTypes AS a
  ), 
  good_type_name = 'auto';
```

</details>

Задание 53. Измените имя "Andie Quincey" на новое "Andie Anthony". [(сайт)](https://sql-academy.org/ru/trainer/tasks/53)

<details><summary>Решение</summary>

```sql
UPDATE 
  FamilyMembers 
SET 
  member_name = 'Andie Anthony' 
WHERE 
  member_name = 'Andie Quincey';
```

</details>

Задание 54. Удалить всех членов семьи с фамилией "Quincey". [(сайт)](https://sql-academy.org/ru/trainer/tasks/54)

<details><summary>Решение</summary>

```sql
DELETE FROM 
  FamilyMembers 
WHERE 
  member_name LIKE '%Quincey';
```

</details>

Задание 55. Удалить компании, совершившие наименьшее количество рейсов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/55)

<details><summary>Решение</summary>

```sql
DELETE FROM 
  Company 
WHERE 
  Company.id IN (
    SELECT 
      company 
    FROM 
      Trip 
    GROUP BY 
      company 
    HAVING 
      COUNT(id) = (
        SELECT 
          MIN(count) 
        FROM 
          (
            SELECT 
              COUNT(id) AS count 
            FROM 
              Trip 
            GROUP BY 
              company
          ) AS min_count
      )
  )
;
```

</details>

Задание 56. Удалить все перелеты, совершенные из Москвы (Moscow). [(сайт)](https://sql-academy.org/ru/trainer/tasks/56)

<details><summary>Решение</summary>

```sql
DELETE FROM 
  Trip 
WHERE 
  town_from = 'Moscow';
```

</details>

Задание 57. Перенести расписание всех занятий на 30 мин. вперед. [(сайт)](https://sql-academy.org/ru/trainer/tasks/57)

<details><summary>Решение</summary>

```sql
UPDATE 
  Timepair 
SET 
  start_pair = start_pair + INTERVAL 30 MINUTE, 
  end_pair = end_pair + INTERVAL 30 MINUTE;
```

</details>

Задание 58. Добавить отзыв с рейтингом 5 на жилье, находящиеся по адресу "11218, Friel Place, New York", от имени "George Clooney". [(сайт)](https://sql-academy.org/ru/trainer/tasks/58)

<details><summary>Решение</summary>

```sql
INSERT INTO Reviews 
SET 
  id = (
    SELECT 
      COUNT(*)+ 1 
    FROM 
      Reviews AS a
  ), 
  rating = 5, 
  reservation_id = (
    SELECT 
      Reservations.id 
    FROM 
      Reservations 
      JOIN Rooms ON Reservations.room_id = Rooms.id 
      JOIN Users ON Reservations.user_id = Users.id 
    WHERE 
      address = '11218, Friel Place, New York' 
      AND name = 'George Clooney'
  );
```

</details>

Задание 59. Вывести пользователей,указавших Белорусский номер телефона? Телефонный код Белоруссии +375. [(сайт)](https://sql-academy.org/ru/trainer/tasks/59)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  Users 
WHERE 
  phone_number LIKE '+375%';
```

</details>

Задание 60. Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/60)

<details><summary>Решение</summary>

```sql
SELECT 
  teacher 
FROM 
  Schedule 
  INNER JOIN Class ON Schedule.class = Class.id 
WHERE 
  name LIKE '11%' 
GROUP BY 
  teacher 
HAVING 
  COUNT(DISTINCT name) = 2;
```

</details>

Задание 61. Выведите список комнат, которые были зарезервированы хотя бы на одни сутки в 12-ую неделю 2020 года. В данной задаче в качестве одной недели примите период из семи дней, первый из которых начинается 1 января 2020 года. Например, первая неделя года — 1–7 января, а третья — 15–21 января. [(сайт)](https://sql-academy.org/ru/trainer/tasks/61)

<details><summary>Решение</summary>

```sql
SELECT 
  Rooms.* 
FROM 
  Rooms 
  JOIN Reservations ON Rooms.id = Reservations.room_id 
WHERE 
  WEEK(start_date, 1) = 12 
  AND YEAR(start_date) = 2020;
```

</details>

Задание 62. Вывести в порядке убывания популярности доменные имена 2-го уровня, используемые пользователями для электронной почты. Полученный результат необходимо дополнительно отсортировать по возрастанию названий доменных имён. [(сайт)](https://sql-academy.org/ru/trainer/tasks/62)

<details><summary>Решение</summary>

```sql
SELECT 
  SUBSTRING_INDEX(email, '@', -1) AS domain, 
  COUNT(
    SUBSTRING_INDEX(email, '@', -1)
  ) AS count 
FROM 
  Users 
GROUP BY 
  domain 
ORDER BY 
  count DESC, 
  domain ASC;
```

</details>

Задание 63. Выведите отсортированный список (по возрастанию) фамилий и имен студентов в виде Фамилия.И.. [(сайт)](https://sql-academy.org/ru/trainer/tasks/63)

<details><summary>Решение</summary>

```sql
SELECT 
  CONCAT(
    last_name, 
    '.', 
    SUBSTRING(first_name, 1, 1), 
    '.'
  ) AS name 
FROM 
  Student 
ORDER BY 
  name ASC;
```

</details>

Задание 64. Вывести количество бронирований по каждому месяцу каждого года, в которых было хотя бы 1 бронирование. Результат отсортируйте в порядке возрастания даты бронирования. [(сайт)](https://sql-academy.org/ru/trainer/tasks/64)

<details><summary>Решение</summary>

```sql
SELECT 
  Year(start_date) AS year, 
  MONTH(start_date) AS month, 
  COUNT(id) AS amount 
FROM 
  Reservations 
GROUP BY 
  year, 
  month 
HAVING 
  amount > 0 
ORDER BY 
  year, 
  month;
```

</details>

Задание 65. Необходимо вывести рейтинг для комнат, которые хоть раз арендовали, как среднее значение рейтинга отзывов округленное до целого вниз. [(сайт)](https://sql-academy.org/ru/trainer/tasks/65)

<details><summary>Решение</summary>

```sql
SELECT 
  room_id, 
  FLOOR(
    AVG(rating)
  ) AS rating 
FROM 
  Reservations 
  JOIN Reviews ON Reservations.id = Reviews.reservation_id 
GROUP BY 
  room_id;
```

</details>

Задание 66. Вывести список комнат со всеми удобствами (наличие ТВ, интернета, кухни и кондиционера), а также общее количество дней и сумму за все дни аренды каждой из таких комнат. [(сайт)](https://sql-academy.org/ru/trainer/tasks/66)

<details><summary>Решение</summary>

```sql
SELECT 
  home_type, 
  address, 
  IF(
    SUM(
      TIMESTAMPDIFF(DAY, start_date, end_date)
    ) > 0, 
    SUM(
      TIMESTAMPDIFF(DAY, start_date, end_date)
    ), 
    0
  ) AS days, 
  IF(
    SUM(total) > 0, 
    SUM(total), 
    0
  ) AS total_fee 
FROM 
  Rooms 
  LEFT JOIN Reservations ON Rooms.id = Reservations.room_id 
WHERE 
  Rooms.has_tv = 1 
  AND Rooms.has_internet = 1 
  AND Rooms.has_air_con = 1 
  AND Rooms.has_kitchen = 1 
GROUP BY 
  home_type, 
  address;
```

</details>

Задание 67. Вывести время отлета и время прилета для каждого перелета в формате "ЧЧ:ММ, ДД.ММ - ЧЧ:ММ, ДД.ММ", где часы и минуты с ведущим нулем, а день и месяц без. [(сайт)](https://sql-academy.org/ru/trainer/tasks/67)

<details><summary>Решение</summary>

```sql
SELECT 
  CONCAT (
    TIME_FORMAT(time_out, '%H:%i'), 
    ', ', 
    DAY(time_out), 
    '.', 
    MONTH(time_out), 
    ' - ', 
    TIME_FORMAT(time_in, '%H:%i'), 
    ', ', 
    DAY(time_in), 
    '.', 
    MONTH(time_in)
  ) AS flight_time 
FROM 
  Trip;
```

</details>

Задание 68. Для каждой комнаты, которую снимали как минимум 1 раз, найдите имя человека, снимавшего ее последний раз, и дату, когда он выехал. [(сайт)](https://sql-academy.org/ru/trainer/tasks/68)

<details><summary>Решение</summary>

```sql
SELECT 
  room_id, 
  name, 
  end_date 
FROM 
  Reservations 
  JOIN Users ON Reservations.user_id = Users.id 
WHERE 
  end_date IN (
    SELECT 
      MAX(end_date) 
    FROM 
      Reservations 
    GROUP BY 
      room_id
  );
```

</details>

Задание 69. Вывести идентификаторы всех владельцев комнат, что размещены на сервисе бронирования жилья и сумму, которую они заработали. [(сайт)](https://sql-academy.org/ru/trainer/tasks/69)

<details><summary>Решение</summary>

```sql
SELECT 
  owner_id, 
  IFNULL(
    SUM(total), 
    0
  ) AS total_earn 
FROM 
  Rooms 
  LEFT JOIN Reservations ON Rooms.id = Reservations.room_id 
GROUP BY 
  owner_id;
```

</details>

Задание 70. Необходимо категоризовать жилье на economy, comfort, premium по цене соответственно <= 100, 100 < цена < 200, >= 200. В качестве результата вывести таблицу с названием категории и количеством жилья, попадающего в данную категорию. [(сайт)](https://sql-academy.org/ru/trainer/tasks/70)

<details><summary>Решение</summary>

```sql
SELECT 
  CASE WHEN price <= 100 THEN 'economy' WHEN price >= 200 THEN 'premium' WHEN 100 < price < 200 THEN 'comfort' END AS category, 
  COUNT(*) AS count 
FROM 
  Rooms 
GROUP BY 
  category;
```

</details>

Задание 71. Найдите какой процент пользователей, зарегистрированных на сервисе бронирования, хоть раз арендовали или сдавали в аренду жилье. Результат округлите до сотых. [(сайт)](https://sql-academy.org/ru/trainer/tasks/71)

<details><summary>Решение</summary>

```sql
SELECT 
  ROUND(
    (
      SELECT 
        COUNT(*) 
      FROM 
        (
          SELECT 
            DISTINCT owner_id 
          FROM 
            Rooms 
            JOIN Reservations ON Rooms.id = Reservations.room_id 
          UNION 
          SELECT 
            DISTINCT user_id 
          FROM 
            Reservations
        ) AS active_users
    )* 100 / (
      SELECT 
        COUNT(id) 
      FROM 
        Users
    ), 
    2
  ) AS percent;
```

</details>

Задание 72. Выведите среднюю цену бронирования за сутки для каждой из комнат, которую бронировали хотя бы один раз. Среднюю цену необходимо округлить до целого значения вверх. [(сайт)](https://sql-academy.org/ru/trainer/tasks/72)

<details><summary>Решение</summary>

```sql
SELECT 
  room_id, 
  CEIL(
    AVG(price)
  ) AS avg_price 
FROM 
  Reservations 
GROUP BY 
  room_id 
HAVING 
  count(room_id)> 0;
```

</details>

Задание 73. Выведите id тех комнат, которые арендовали нечетное количество раз. [(сайт)](https://sql-academy.org/ru/trainer/tasks/73)

<details><summary>Решение</summary>

```sql
SELECT 
  room_id, 
  COUNT(room_id) AS count 
FROM 
  Reservations 
GROUP BY 
  room_id 
HAVING 
  count % 2 = 1;
```

</details>

Задание 74. Выведите идентификатор и признак наличия интернета в помещении. Если интернет в сдаваемом жилье присутствует, то выведите «YES», иначе «NO». [(сайт)](https://sql-academy.org/ru/trainer/tasks/74)

<details><summary>Решение</summary>

```sql
SELECT 
  id, 
  CASE WHEN has_internet = '1' THEN 'YES' ELSE 'NO' END AS has_internet 
FROM 
  Rooms;
```

</details>

Задание 75. Выведите фамилию, имя и дату рождения студентов, кто был рожден в мае. [(сайт)](https://sql-academy.org/ru/trainer/tasks/75)

<details><summary>Решение</summary>

```sql
SELECT 
  last_name, 
  first_name, 
  birthday 
FROM 
  Student 
WHERE 
  birthday LIKE '%-05-%';
```

</details>

Задание 76. Вывести имена всех пользователей сервиса бронирования жилья, а также два признака: является ли пользователь собственником какого-либо жилья (is_owner) и является ли пользователь арендатором (is_tenant). В случае наличия у пользователя признака необходимо вывести в соответствующее поле 1, иначе 0. [(сайт)](https://sql-academy.org/ru/trainer/tasks/76)

<details><summary>Решение</summary>

```sql
SELECT 
  name, 
  IF(
    id IN (
      SELECT 
        DISTINCT owner_id 
      FROM 
        Rooms
    ), 
    1, 
    0
  ) AS is_owner, 
  IF(
    id IN (
      SELECT 
        DISTINCT user_id 
      FROM 
        Reservations
    ), 
    1, 
    0
  ) AS is_tenant 
FROM 
  Users;
```

</details>

Задание 77. Создайте представление с именем "People", которое будет содержать список имен (first_name) и фамилий (last_name) всех студентов (Student) и преподавателей(Teacher). [(сайт)](https://sql-academy.org/ru/trainer/tasks/77)

<details><summary>Решение</summary>

```sql
CREATE VIEW People AS 
    SELECT Student.first_name, Student.last_name
    FROM Student
    UNION 
    SELECT Teacher.first_name, Teacher.last_name
    FROM Teacher;
```

</details>

Задание 78. Выведите всех пользователей с электронной почтой в «hotmail.com». [(сайт)](https://sql-academy.org/ru/trainer/tasks/78)

<details><summary>Решение</summary>

```sql
SELECT 
  * 
FROM 
  Users 
WHERE 
  email LIKE '%@hotmail.com';
```

</details>

Задание 79. Выведите поля id, home_type, price у всего жилья из таблицы Rooms. Если комната имеет телевизор и интернет одновременно, то в качестве цены в поле price выведите цену, применив скидку 10%. [(сайт)](https://sql-academy.org/ru/trainer/tasks/79)

<details><summary>Решение</summary>

```sql
SELECT 
  id, 
  home_type, 
  IF(
    has_tv 
    AND has_internet, 
    price * 0.9, 
    price
  ) AS price 
FROM 
  Rooms;
```

</details>

Задание 80. Создайте представление «Verified_Users» с полями id, name и email, которое будет показывает только тех пользователей, у которых подтвержден адрес электронной почты. [(сайт)](https://sql-academy.org/ru/trainer/tasks/80)

<details><summary>Решение</summary>

```sql
CREATE VIEW Verified_Users AS 
SELECT 
  id, 
  name, 
  email 
FROM 
  Users 
WHERE 
  email_verified_at IS NOT NULL;
```

</details>

Задание 93. Какой средний возраст клиентов, купивших Smartwatch (использовать наименование товара product.name) в 2024 году? [(сайт)](https://sql-academy.org/ru/trainer/tasks/93)

<details><summary>Решение</summary>

```sql
SELECT 
  AVG(uniqueCustomers.age) AS average_age 
FROM 
  (
    SELECT 
      DISTINCT Customer.customer_key, 
      Customer.age 
    FROM 
      Purchase 
      JOIN Customer ON Purchase.customer_key = Customer.customer_key 
      JOIN Product ON Purchase.product_key = Product.product_key 
    WHERE 
      Product.name = 'Smartwatch' 
      AND YEAR(Purchase.date)= 2024
  ) AS uniqueCustomers;
```

</details>

Задание 94. Вывести имена покупателей, каждый из которых приобрёл Laptop и Monitor (использовать наименование товара product.name) в марте 2024 года? [(сайт)](https://sql-academy.org/ru/trainer/tasks/94)

<details><summary>Решение</summary>

```sql
SELECT 
  Customer.name AS name 
FROM 
  Customer 
  JOIN Purchase ON Customer.customer_key = Purchase.customer_key 
  JOIN Product ON Purchase.product_key = Product.product_key 
WHERE 
  YEAR(date)= 2024 
  AND MONTH(date)= 3 
  AND Product.name IN ('Laptop', 'Monitor') 
GROUP BY 
  Customer.customer_key 
HAVING 
  COUNT(
    DISTINCT(Product.name)
  )= 2;
```

</details>

Задание 97. Посчитать количество работающих складов на текущую дату по каждому городу. Вывести только те города, у которых количество складов более 80. Данные на выходе - город, количество складов. [(сайт)](https://sql-academy.org/ru/trainer/tasks/97)

<details><summary>Решение</summary>

```sql
SELECT 
  city, 
  COUNT(warehouse_id) AS warehouse_count 
FROM 
  Warehouses 
WHERE 
  date_close IS NULL 
GROUP BY 
  city 
HAVING 
  warehouse_count > 80;
```

</details>

Задание 99. Посчитай доход с женской аудитории (доход = сумма(price * items)). Обратите внимание, что в таблице женская аудитория имеет поле user_gender «female» или «f». [(сайт)](https://sql-academy.org/ru/trainer/tasks/99)

<details><summary>Решение</summary>

```sql
SELECT 
  SUM(price * items) AS income_from_female 
FROM 
  Purchases 
WHERE 
  user_gender IN ('female', 'f');
```

</details>

Задание 101. Выведи для каждого пользователя первое наименование, которое он заказал (первое по времени транзакции). [(сайт)](https://sql-academy.org/ru/trainer/tasks/101)

<details><summary>Решение</summary>

```sql
WITH tmp AS (
  SELECT 
    *, 
    ROW_NUMBER() OVER (
      PARTITION BY user_id 
      ORDER BY 
        transaction_ts ASC
    ) AS rn 
  FROM 
    Transactions
) 
SELECT 
  user_id, 
  item 
FROM 
  tmp 
WHERE 
  rn = 1;
```

</details>

Задание 103. Вывести список имён сотрудников, получающих большую заработную плату, чем у непосредственного руководителя. [(сайт)](https://sql-academy.org/ru/trainer/tasks/103)

<details><summary>Решение</summary>

```sql
SELECT 
  employees.name 
FROM 
  Employee AS employees, 
  Employee AS chieves 
WHERE 
  chieves.id = employees.chief_id 
  AND employees.salary > chieves.salary;
```

</details>

Задание 109. Выведите название страны, где находится город «Salzburg». [(сайт)](https://sql-academy.org/ru/trainer/tasks/109)

<details><summary>Решение</summary>

```sql
SELECT 
  Countries.name AS country_name 
FROM 
  Countries 
  INNER JOIN Regions ON Countries.id = Regions.countryid 
  INNER JOIN Cities ON Regions.id = Cities.regionid 
WHERE 
  Cities.name = 'Salzburg';
```

</details>

Задание 111. Посчитайте население каждого региона. В качестве результата выведите название региона и его численность населения. [(сайт)](https://sql-academy.org/ru/trainer/tasks/111)

<details><summary>Решение</summary>

```sql
SELECT 
  SUM(population) AS total_population, 
  Regions.name AS region_name 
FROM 
  Cities 
  INNER JOIN Regions ON Cities.regionid = Regions.id 
GROUP BY 
  Regions.name;
```

</details>
