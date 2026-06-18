# Список выполненных задание и решений к ним в тренажере SQL Academy 
---
<details>
<summary>1. Задание</summary>
Вывести имена всех людей, которые есть в базе данных авиакомпаний
  
```mysql
SELECT Passenger.name FROM Passenger
```
</details>
<details>
<summary>2. Задание</summary>
Вывести названия всеx авиакомпаний

```mysql
SELECT name FROM Company
```
</details>
<details>
<summary>3. Задание</summary>
Вывести все рейсы, совершенные из Москвы
  
```mysql
SELECT * FROM TRIP WHERE town_from = 'Moscow'
```
</details>
<details>
<summary>4. Задание</summary>
Вывести имена людей, которые заканчиваются на "man"

```mysql
SELECT name from Passenger WHERE name LIKE '%man'
```
</details>
<details>
<summary>5. Задание</summary>
Вывести количество рейсов, совершенных на TU-134. Используйте конструкцию "as count" для агрегатной функции подсчета количества рейсов.

```mysql
SELECT COUNT(plane) as count from Trip WHERE plane LIKE 'TU-134'
```
</details>
<details>
<summary>6. Задание</summary>
Какие компании совершали перелеты на Boeing
  
```mysql
SELECT DISTINCT name FROM Company 
	INNER JOIN Trip ON Company.id = Trip.company
	WHERE Trip.plane LIKE 'Boeing'
```
</details>
<details>
<summary>7. Задание</summary>
Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)

```mysql
SELECT DISTINCT plane from TRIP WHERE town_to LIKE 'Moscow'
```
</details>
<details>
<summary>8. Задание</summary>
В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
  
```mysql
SELECT town_to, TIMEDIFF(time_in,time_out) as flight_time  
FROM Trip
WHERE town_from LIKE 'Paris'
```
</details>
<details>
<summary>9. Задание</summary>
Компании с рейсами из Владивостока

```mysql
SELECT DISTINCT name FROM Company
INNER JOIN Trip 
ON Company.id=Trip.company
WHERE Trip.town_from LIKE 'Vladivostok'
```
</details>
<details>
<summary>10. Задание</summary>
Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.

```mysql
SELECT *
FROM Trip
WHERE time_out BETWEEN ('1900-01-01 10:00:00') AND ('1900-01-01 14:00:00')
```
</details>
<details>
<summary>11. Задание</summary>


```mysql
d
```
</details>
