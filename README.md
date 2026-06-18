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
Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.

```mysql
SELECT name
FROM Passenger
WHERE LENGTH(name)=(SELECT Max(LENGTH(name))FROM Passenger)
```
</details>
<details>
<summary>12. Задание</summary>
Выведите идентификаторы всех рейсов и количество пассажиров на них. Обратите внимание, что на каких-то рейсах пассажиров может не быть. В этом случае выведите число "0".

```mysql
SELECT trip.id, COUNT(pit.passenger) as count FROM Trip
LEFT JOIN Pass_in_trip as pit 
ON Trip.id = pit.trip
GROUP BY trip.id
```
</details>
<details>
<summary>13. Задание</summary>
Вывести имена людей, у которых есть полный тёзка среди пассажиров

```mysql
SELECT name FROM Passenger 
GROUP BY name 
HAVING COUNT(name)>1
```
</details>
<details>
<summary>14. Задание</summary>
В какие города летал Bruce Willis

```mysql
SELECT DISTINCT town_to FROM Trip
JOIN Pass_in_trip as pit
ON Trip.id=pit.trip
JOIN Passenger
ON Passenger.id=pit.passenger
WHERE Passenger.name LIKE 'Bruce Willis' 
```
</details>
<details>
<summary>15. Задание</summary>
Выведите идентификатор пассажира Стив Мартин (Steve Martin) и дату и время его прилёта в Лондон (London)

```mysql
SELECT Passenger.id, time_in FROM Pass_in_trip as pit
JOIN Passenger 
ON  pit.passenger = Passenger.id 
JOIN Trip 
ON pit.trip = Trip.id
WHERE Passenger.name LIKE  'Steve Martin' AND town_to = 'London'
```
</details>
<details>
<summary>16. Задание</summary>
Вывести идентификатор, имя и количество перелётов каждого пассажира, совершившего хотя бы 1 полёт. Результат отсортировать по количеству перелётов (по убыванию) и имени (по возрастанию).

```mysql
SELECT Passenger.id, Passenger.name, COUNT(pit.trip) as count FROM Pass_in_trip as pit
JOIN Passenger 
ON Passenger.id = pit.passenger
GROUP BY Passenger.id
ORDER BY count DESC, name ASC
```
</details>
<details>
<summary>17. Задание</summary>
Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили.

```mysql
SELECT member_name, status, SUM(unit_price*amount) as costs FROM FamilyMembers
JOIN Payments
ON member_id = family_member
WHERE YEAR(Payments.date) = 2005
GROUP BY family_member
```
</details>
<details>
<summary>18. Задание</summary>
Выведите имя самого старшего человека. Если таких несколько, то выведите их всех.

```mysql
SELECT member_name from FamilyMembers
WHERE birthday = (SELECT MIN(birthday) from FamilyMembers)
```
</details>
<details>
<summary>19. Задание</summary>
Определить, кто из членов семьи покупал картошку (potato)

```mysql
SELECT DISTINCT status FROM FamilyMembers
JOIN Payments
ON member_id = family_member
JOIN Goods 
ON Payments.good = good_id
WHERE good_name LIKE 'potato'
GROUP BY status
```
</details>
<details>
<summary>20. Задание</summary>
Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму
	
```mysql
SELECT DISTINCT status, member_name, SUM(unit_price*amount) as costs FROM FamilyMembers
JOIN Payments 
ON member_id = family_member
JOIN Goods
ON Payments.good=good_id
JOIN GoodTypes
ON Goods.type=good_type_id
WHERE good_type_name LIKE 'entertainment'
GROUP BY family_member
```
</details>
<details>
<summary>21. Задание</summary>
Определить товары, которые покупали более 1 раза

```mysql
SELECT DISTINCT good_name FROM Goods 
JOIN Payments 
ON good_id = Payments.good
GROUP BY good_name HAVING COUNT(good)>1
```
</details>
<details>
<summary>22. Задание</summary>
Найти имена всех матерей (mother)

```mysql
SELECT member_name FROM FamilyMembers
WHERE status LIKE 'mother'
```
</details>
<details>
<summary>23. Задание</summary>
Найдите самый дорогой деликатес (delicacies) и выведите его цену

```mysql
SELECT good_name, unit_price FROM Goods
JOIN Payments 
ON Payments.good = Goods.good_id 
WHERE type = 3 
ORDER BY unit_price DESC LIMIT 1
```
</details>
<details>
<summary>24. Задание</summary>
Определить, кто и сколько потратил в июне 2005

```mysql
SELECT member_name, SUM(unit_price*amount) as costs FROM FamilyMembers
JOIN Payments ON member_id = family_member 
WHERE YEAR(date)=2005 AND MONTH(date)=06
GROUP BY member_name
```
</details>
<details>
<summary>25. Задание</summary>
Определить, какие товары не покупались в 2005 году

```mysql
SELECT good_name FROM Goods 
LEFT JOIN Payments ON good_id=Payments.good
WHERE good_id NOT IN (SELECT good FROM Payments WHERE YEAR(date)=2005)
```
</details>
<details>
<summary>26. Задание</summary>
Определить группы товаров, которые не приобретались в 2005 году

```mysql
SELECT good_type_name
FROM GoodTypes
WHERE good_type_id NOT IN (
		SELECT TYPE
		FROM Goods
		WHERE good_id IN(
				SELECT good
				FROM Payments
				WHERE YEAR(date) = 2005))
```
</details>
<details>
<summary>27. Задание</summary>
Узнайте, сколько было потрачено на каждую из групп товаров в 2005 году. Выведите название группы и потраченную на неё сумму. Если потраченная сумма равна нулю, т.е. товары из этой группы не покупались в 2005 году, то не выводите её.

```mysql
SELECT good_type_name, SUM(amount*unit_price) as costs  FROM GoodTypes
JOIN Goods on good_type_id = type
JOIN Payments on good_id = good 
WHERE YEAR(date)=2005
GROUP BY good_type_name
```
</details>
<details>
<summary>28. Задание</summary>
Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow) ?

```mysql
SELECT COUNT(company) as count FROM Trip 
WHERE town_from LIKE 'Rostov' AND town_to LIKE 'Moscow'
```
</details>
<details>
<summary>29. Задание</summary>
Выведите имена пассажиров, улетевших в Москву (Moscow) на самолете TU-134. В ответе не должно быть дубликатов.

```mysql
SELECT DISTINCT Passenger.name FROM Passenger
JOIN Pass_in_trip as pit ON Passenger.id = pit.passenger
JOIN Trip ON pit.trip=Trip.id
WHERE town_to = 'Moscow' AND plane = 'TU-134'
```
</details>
<details>
<summary>30. Задание</summary>
Вывести количество занятых мест по каждому рейсу из таблицы Pass_in_trip, отсортировав результат по убыванию количества занятых мест.

```mysql
SELECT trip, COUNT(passenger) as count FROM Pass_in_trip as pit
GROUP BY trip
ORDER BY count DESC
```
</details>
<details>
<summary>31. Задание</summary>
Вывести всех членов семьи с фамилией Quincey.

```mysql
SELECT * FROM FamilyMembers 
WHERE member_name LIKE '%Quincey'
```
</details>
<details>
<summary>32. Задание</summary>
Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону.

```mysql
SELECT FLOOR(AVG((TIMESTAMPDIFF(YEAR,birthday,NOW())))) as age FROM FamilyMembers
```
</details>
<details>
<summary>33. Задание</summary>
Найдите среднюю цену икры на основе данных, хранящихся в таблице Payments. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar). В ответе должна быть одна строка со средней ценой всей купленной когда-либо икры.

```mysql
SELECT AVG(unit_price) as cost FROM  Payments 
WHERE good IN (SELECT good_id FROM Goods WHERE good_name LIKE '%caviar')
```
</details>
<details>
<summary>34. Задание</summary>
Сколько всего 10-ых классов

```mysql
SELECT COUNT(class.id) as count FROM Class
WHERE Class.name LIKE  '10%'
```
</details>
<details>
<summary>35. Задание</summary>
Сколько различных кабинетов школы использовались 2 сентября 2019 года для проведения занятий?

```mysql
SELECT COUNT(DISTINCT Schedule.classroom) as count FROM Schedule
WHERE DATE(Schedule.date) = DATE('2019-09-02')
```
</details>
<details>
<summary>36. Задание</summary>
Выведите информацию об обучающихся, живущих на улице Пушкина (ul. Pushkina)?

```mysql
SELECT * FROM STUDENT 
WHERE address LIKE 'ul. Pushkina%'
```
</details>
<details>
<summary>37. Задание</summary>
Сколько лет самому молодому обучающемуся ?

```mysql
SELECT TIMESTAMPDIFF(YEAR,MAX(birthday),NOW()) as year FROM Student
```
</details>
<details>
<summary>38. Задание</summary>
Сколько учениц с именем Анна (Anna) учится в школе?

```mysql
SELECT COUNT(student.first_name) as count FROM Student 
WHERE Student.first_name LIKE  'Anna%'
```
</details>
<details>
<summary>39. Задание</summary>
Сколько обучающихся в 10 B классе ?

```mysql
SELECT COUNT(student) as count FROM Student_in_class
JOIN Class ON Class.id = Student_in_class.class
WHERE Class.name = '10 B'
```
</details>
<details>
<summary>40. Задание</summary>
Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.). Обратите внимание, что в базе данных есть несколько учителей с такой фамилией.

```mysql
SELECT Subject.name as subjects FROM Subject 
JOIN Schedule on Subject.id = Schedule.subject
JOIN TEACHER ON Teacher.id = Schedule.teacher
WHERE Teacher.first_name LIKE 'P%' AND Teacher.middle_name LIKe 'P%' AND Teacher.last_name = 'Romashkin'
```
</details>
<details>
<summary>41. Задание</summary>
Выясните, во сколько по расписанию начинается четвёртое занятие.

```mysql
SELECT start_pair FROM Timepair 
WHERE Timepair.id = 4
```
</details>
<details>
<summary>42. Задание</summary>
Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет?

```mysql
SELECT TIMEDIFF(MAX(end_pair),MIN(start_pair)) as time FROM  Timepair
WHERE id BETWEEN 2 AND 4
```
</details>
<details>
<summary>43. Задание</summary>
Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отсортируйте преподавателей по фамилии в алфавитном порядке.

```mysql
SELECT DISTINCT Teacher.last_name FROM Teacher 
JOIN Schedule on Teacher.id = Schedule.teacher
Join Subject On Subject.id=Schedule.subject
WHERE Subject.name = 'Physical Culture'
ORDER BY Teacher.last_name ASC
```
</details>
<details>
<summary>44. Задание</summary>
Найдите максимальный возраст (количество лет) среди обучающихся 10 классов на сегодняшний день.

```mysql
SELECT MAX(TIMESTAMPDIFF(YEAR,Student.birthday,NOW())) as max_year FROM Student
WHERE Student.id IN (SELECT student FROM Student_in_class WHERE class IN (SELECT Class.id FROM  Class WHERE name LIKE '10%'))
```
</details>
<details>
<summary>45. Задание</summary>
Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз.

```mysql
SELECT classroom FROM  Schedule
GROUP BY classroom
HAVING count(classroom) = (SELECT count(classroom) as cnt
FROM Schedule
GROUP BY classroom
ORDER BY cnt DESC
LIMIT 1)
```
</details>
<details>
<summary>46. Задание</summary>
В каких классах ведёт занятия преподаватель "Krauze"?

```mysql
SELECT Class.name
FROM Class
WHERE class.id IN (
		SELECT Schedule.class
		FROM Schedule
		WHERE Schedule.teacher IN (
				SELECT Teacher.id
				FROM Teacher
				WHERE Teacher.last_name = 'Krauze'))
```
</details>
<details>
<summary>47. Задание</summary>
Сколько занятий провел Krauze 30 августа 2019 г.?

```mysql
SELECT COUNT(Schedule.teacher) as count FROM Schedule 
WHERE Schedule.teacher IN (SELECT id FROM Teacher where Teacher.last_name ='Krauze') AND DATE(Schedule.date) = ('2019-08-30')
GROUP BY Schedule.teacher
```
</details>
<details>
<summary>48. Задание</summary>
Выведите заполненность классов в порядке убывания. Не выводите классы, в которых нет ни одного учащегося.

```mysql
SELECT Class.name,COUNT(Student) as count FROM Student_in_class sic
JOIN Class ON Class.id=sic.class
GROUP BY Class
ORDER BY count DESC
```
</details>
<details>
<summary>49. Задание</summary>
Какой процент обучающихся учится в "10 A" классе? Выведите ответ в диапазоне от 0 до 100 с округлением до четырёх знаков после запятой

```mysql
SELECT (
		SELECT COUNT(student)
		FROM Student_in_class
		WHERE class IN (
				SELECT id
				FROM CLASS
				WHERE Class.name = '10 A'
			)
	) / COUNT(*) * 100 AS percent
	FROM Student_in_class
```
</details>
<details>
<summary>50. Задание</summary>
Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону.

```mysql
SELECT FLOOR(
		(
			SELECT COUNT(birthday)
			FROM Student
			WHERE YEAR(birthday) = 2000
		) / COUNT(*) * 100
	) as percent
FROM Student
```
</details>
<details>
<summary>51. Задание</summary>
Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods).

```mysql
INSERT Goods SELECT MAX(good_id)+1, 'Cheese', 2 FROM Goods
```
</details>
<details>
<summary>52. Задание</summary>
Добавьте в список типов товаров (GoodTypes) новый тип "auto".

```mysql
INSERT GoodTypes SELECT MAX(good_type_id)+1, 'auto' FROM GoodTypes
```
</details>
<details>
<summary>53. Задание</summary>
Измените имя "Andie Quincey" на новое "Andie Anthony".

```mysql
UPDATE FamilyMembers 
SET member_name = 'Andie Anthony'
WHERE member_name = 'Andie Quincey'
```
</details>
<details>
<summary>54. Задание</summary>
Удалить всех членов семьи с фамилией "Quincey".

```mysql
DELETE FROM FamilyMembers
WHERE member_name LIKE  '%Quincey'
```
</details>
<details>
<summary>55. Задание</summary>
Удалить компании, совершившие наименьшее количество рейсов.

```mysql
DELETE FROM Company
WHERE Company.id IN (
    SELECT company FROM Trip
    GROUP BY company
    HAVING COUNT(*)= 
    (
        SELECT COUNT(*) count FROM  Trip
        GROUP BY company
        ORDER BY count ASC
        LIMIT 1
    )
)
```
</details>
<details>
<summary>56. Задание</summary>
Удалить все перелеты, совершенные из Москвы (Moscow).

```mysql
DELETE Trip FROM Trip
WHERE town_from = 'Moscow'
```
</details>
<details>
<summary>57. Задание</summary>
Перенести расписание всех занятий на 30 мин. вперед.

```mysql
UPDATE Timepair
SET start_pair = ADDDATE(start_pair, INTERVAL 30 MINUTE),
    end_pair = ADDDATE(end_pair, INTERVAL 30 minute)
```
</details>
<details>
<summary>58. Задание</summary>
Добавить отзыв с рейтингом 5 на жилье, находящиеся по адресу "11218, Friel Place, New York", от имени "George Clooney"

```mysql
INSERT INTO Reviews(id, reservation_id, rating)
SELECT MAX(Reviews.id) + 1,
	(
		SELECT Reservations.id
		FROM Reservations
		WHERE Reservations.user_id =(
				SELECT Users.id
				FROM Users
				WHERE name = "George Clooney"
			)
			AND room_id =(
				SELECT Rooms.id
				FROM Rooms
				WHERE address = "11218, Friel Place, New York"
			)
	),
	5
FROM Reviews
```
</details>
<details>
<summary>59. Задание</summary>
Вывести пользователей,указавших Белорусский номер телефона ? Телефонный код Белоруссии +375.

```mysql
SELECT * FROM  Users 
WHERE phone_number  LIKE '+375%'
```
</details>
<details>
<summary>60. Задание</summary>
Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов.

```mysql
SELECT teacher FROM  Schedule
Join Class ON Schedule.class = Class.id
WHERE Class.name RLIKE "11"
GROUP BY teacher
HAVING COUNT(DISTINCT class) = 2;
```
</details>
<details>
<summary>61. Задание</summary>
Выведите список комнат, которые были зарезервированы хотя бы на одни сутки в 12-ую неделю 2020 года.

```mysql
SELECT Rooms.* FROM Reservations
JOIN Rooms ON Rooms.id=Reservations.room_id
WHERE YEAR(start_date) = 2020 AND WEEK(start_date,1)=12
```
</details>
<details>
<summary>62. Задание</summary>
Вывести в порядке убывания популярности доменные имена 2-го уровня, используемые пользователями для электронной почты.

```mysql
SELECT SUBSTRING_INDEX(email, '@', -1) as domain, COUNT(email) as count
FROM Users
GROUP BY domain
ORDER BY count DESC, domain 
```
</details>
<details>
<summary>63. Задание</summary>
Выведите отсортированный список (по возрастанию) фамилий и имен студентов в виде Фамилия.И.

```mysql
SELECT CONCAT(last_name,'.', LEFT(first_name,1),'.') AS NAME FROM Student
ORDER BY name ASC
```
</details>
<details>
<summary>64. Задание</summary>
Вывести количество бронирований по каждому месяцу каждого года, в которых было хотя бы 1 бронирование. Результат отсортируйте в порядке возрастания даты бронирования.

```mysql
SELECT YEAR(start_date) as year, MONTH(start_date) as month, COUNT(id) as amount
FROM Reservations
GROUP BY year, month
ORDER BY year, month ASC
```
</details>
<details>
<summary>65. Задание</summary>
Необходимо вывести рейтинг для комнат, которые хоть раз арендовали, как среднее значение рейтинга отзывов округленное до целого вниз

```mysql
SELECT room_id, TRUNCATE(AVG(rating),0) AS rating
FROM Reservations
JOIN Reviews ON Reservations.id = Reviews.reservation_id
GROUP BY room_id
```
</details>
<details>
<summary>66. Задание</summary>
Вывести список комнат со всеми удобствами (наличие ТВ, интернета, кухни и кондиционера), а также общее количество дней и сумму за все дни аренды каждой из таких комнат.

```mysql
SELECT home_type, address, IFNULL(SUM(TIMESTAMPDIFF(DAY, start_date, end_date)),0) AS days, IFNULL(SUM(total),0) AS total_fee
FROM Rooms
LEFT JOIN Reservations ON Reservations.room_id=Rooms.id
WHERE has_tv = 1 AND has_air_con = 1 AND has_internet = 1 AND has_kitchen = 1
GROUP BY home_type, address
```
</details>
<details>
<summary>67. Задание</summary>
Вывести время отлета и время прилета для каждого перелета в формате "ЧЧ:ММ, ДД.ММ - ЧЧ:ММ, ДД.ММ", где часы и минуты с ведущим нулем, а день и месяц без.

```mysql
SELECT CONCAT(DATE_FORMAT(time_out,'%H:%i, %e.%c'),' - ',DATE_FORMAT(time_in,'%H:%i, %e.%c')) AS flight_time FROM Trip
```
</details>
<details>
<summary>68. Задание</summary>
Для каждой комнаты, которую снимали как минимум 1 раз, найдите имя человека, снимавшего ее последний раз, и дату, когда он выехал

```mysql
SELECT room_id, name, end_date FROM Reservations
JOIN Users ON Reservations.user_id=Users.id
WHERE end_date IN (SELECT MAX(end_date) FROM Reservations GROUP BY room_id)
```
</details>
<details>
<summary>69. Задание</summary>
Вывести идентификаторы всех владельцев комнат, что размещены на сервисе бронирования жилья и сумму, которую они заработали

```mysql
SELECT owner_id, IFNULL(SUM(total),0) AS total_earn FROM Rooms
LEFT JOIN Reservations on Rooms.id = Reservations.room_id
GROUP by owner_id
```
</details>
<details>
<summary>70. Задание</summary>
Необходимо категоризовать жилье на economy, comfort, premium по цене соответственно <= 100, 100 < цена < 200, >= 200. В качестве результата вывести таблицу с названием категории и количеством жилья, попадающего в данную категорию

```mysql
SELECT CASE 
WHEN price<= 100 THEN 'economy'
WHEN price < 200 THEN 'comfort'
WHEN price >=200 THEN 'premium'
END AS category,
COUNT(*) as count 
FROM Rooms
GROUP BY category
```
</details>

