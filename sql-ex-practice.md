+ [1](#1)
+ [2](#2)
+ [3](#3)
+ [4](#4)
+ [5](#5)
+ [6](#6)
+ [7](#7)
+ [8](#8)
+ [9](#9)
+ [10](#10)
+ [11](#11)
+ [12](#12)
+ [13](#13)
+ [14](#14)
+ [15](#15)
+ [16](#16)
+ [17](#17)
+ [18](#18)
+ [19](#19)
+ [20](#20)
+ [21](#21)
+ [22](#22)
+ [23](#23)
+ [24](#24)
+ [25](#25)
+ [26](#26)
+ [27](#27)
+ [28](#28)
+ [29](#29)
+ [30](#30)
+ [31](#31)
+ [32](#32)
+ [33](#33)
+ [34](#34)
+ [35](#35)
+ [36](#36)
+ [37](#37)
+ [38](#38)
+ [39](#39)
+ [40](#40)
+ [41](#41)
+ [42](#42)
+ [43](#43)
+ [44](#44)
+ [45](#45)
+ [46](#46)
+ [47](#47)
+ [48](#48)
+ [49](#49)
+ [50](#50)
+ [51](#51)
+ [52](#52)
+ [53](#53)
+ [54](#54)
+ [55](#55)
+ [56](#56)


## 1

https://sql-ex.ru/learn_exercises.php?LN=1

```sql
SELECT model, speed, hd
FROM PC
WHERE price < 500
```
## 2

https://sql-ex.ru/learn_exercises.php?LN=2

```sql
SELECT DISTINCT maker
FROM Product
WHERE type = 'printer'
```
## 3

https://sql-ex.ru/learn_exercises.php?LN=3

```sql
SELECT model, ram, screen
FROM Laptop
WHERE Price > 1000
```
## 4

https://sql-ex.ru/learn_exercises.php?LN=4
```sql
SELECT *
FROM Printer
WHERE color = 'y'
```
## 5

https://sql-ex.ru/learn_exercises.php?LN=5
```sql
SELECT model, speed, hd
FROM PC
WHERE (cd = '12x' OR cd = '24x') AND price < 600
```
## 6

https://sql-ex.ru/learn_exercises.php?LN=6
```sql
SELECT DISTINCT Product.maker, Laptop.speed
FROM Product, Laptop 
WHERE Laptop.model = Product.model AND Laptop.hd >= 10 AND Product.TYPE = 'laptop'
```
## 7

https://sql-ex.ru/learn_exercises.php?LN=7
```sql
SELECT DISTINCT product.model, pc.price
FROM Product JOIN pc ON product.model = pc.model WHERE maker = 'B'
UNION
SELECT DISTINCT product.model, laptop.price
FROM product JOIN laptop ON product.model=laptop.model WHERE maker='B'
UNION
SELECT DISTINCT product.model, printer.price
FROM product JOIN printer ON product.model=printer.model WHERE maker='B';
```
## 8

https://sql-ex.ru/learn_exercises.php?LN=8
```sql
SELECT DISTINCT maker
FROM Product
WHERE type='PC' AND maker NOT IN (SELECT maker
FROM product
WHERE type = 'Laptop')
```
## 9

https://sql-ex.ru/learn_exercises.php?LN=9
```sql
SELECT DISTINCT maker
FROM PC INNER JOIN
Product ON PC.model = Product.model
WHERE speed >= 450
```
## 10

https://sql-ex.ru/learn_exercises.php?LN=10
```sql
SELECT Printer.model, price
FROM Printer INNER JOIN
Product ON Printer.model = Product.model
WHERE price = (SELECT MAX(price) FROM Printer)
```
## 11

https://sql-ex.ru/learn_exercises.php?LN=11
```sql
SELECT AVG(speed)
FROM PC
```
## 12

https://sql-ex.ru/learn_exercises.php?LN=12
```sql
SELECT AVG(speed)
FROM Laptop
WHERE price > 1000
```
## 13

https://sql-ex.ru/learn_exercises.php?LN=13
```sql
SELECT AVG(speed)
FROM PC INNER JOIN
Product ON PC.model = Product.model
WHERE maker = 'A'
```
## 14

https://sql-ex.ru/learn_exercises.php?LN=14
```sql
SELECT s.class, s.name, c.country
FROM ships s
LEFT JOIN classes c ON s.class = c.class
WHERE c.numGuns >= 10
```
## 15

https://sql-ex.ru/learn_exercises.php?LN=15
```sql
SELECT hd
FROM PC
GROUP BY hd HAVING COUNT (model) > 1
```
## 16

https://sql-ex.ru/learn_exercises.php?LN=16
```sql
SELECT DISTINCT p1.model, p2.model, p1.speed, p1.ram
FROM pc p1, pc p2
WHERE p1.speed = p2.speed AND p1.ram = p2.ram AND p1.model > p2.model
```
## 17

https://sql-ex.ru/learn_exercises.php?LN=17
```sql
SELECT distinct p.type,p.model,l.speed
FROM laptop l
JOIN product p on l.model=p.model
WHERE l.speed<(select min(speed)
                      from pc)
```
## 18


https://sql-ex.ru/learn_exercises.php?LN=18
```sql
SELECT DISTINCT product.maker, printer.price
FROM product, printer
WHERE product.model = printer.model
AND printer.color = 'y'
AND printer.price = (
SELECT MIN(price) FROM printer
WHERE printer.color = 'y'
)
```
## 19 

https://sql-ex.ru/learn_exercises.php?LN=19
```sql
SELECT maker, AVG(screen)
FROM Laptop INNER JOIN
Product ON Laptop.model = Product.model
GROUP BY maker
```
## 20

https://sql-ex.ru/learn_exercises.php?LN=20
```sql
SELECT maker, COUNT(model)
FROM product
WHERE type = 'pc'
GROUP BY product.maker
HAVING COUNT (DISTINCT model) >= 3
```
## 21

https://sql-ex.ru/learn_exercises.php?LN=21
```sql
SELECT maker, MAX(price)
FROM PC INNER JOIN
Product ON PC.model = Product.model
GROUP BY maker
```
## 22

https://sql-ex.ru/learn_exercises.php?LN=22
```sql
SELECT pc.speed, AVG(pc.price)
FROM pc
WHERE pc.speed > 600
GROUP BY pc.speed
```
## 23

https://sql-ex.ru/learn_exercises.php?LN=23
```sql
SELECT DISTINCT maker
FROM product t1 JOIN pc t2 ON t1.model=t2.model
WHERE speed>=750 AND maker IN
( SELECT maker
FROM product t1 JOIN laptop t2 ON t1.model=t2.model
WHERE speed>=750 )
```
## 24

https://sql-ex.ru/learn_exercises.php?LN=24
```sql
SELECT model
FROM (
 SELECT model, price
 FROM pc
 UNION
 SELECT model, price
 FROM Laptop
 UNION
 SELECT model, price
 FROM Printer
) t1
WHERE price = (
 SELECT MAX(price)
 FROM (
  SELECT price
  FROM pc
  UNION
  SELECT price
  FROM Laptop
  UNION
  SELECT price
  FROM Printer
  ) t2
 )
```
## 25

https://sql-ex.ru/learn_exercises.php?LN=25
```sql
SELECT DISTINCT maker
FROM product
WHERE model IN (
SELECT model
FROM pc
WHERE ram = (
  SELECT MIN(ram)
  FROM pc
  )
AND speed = (
  SELECT MAX(speed)
  FROM pc
  WHERE ram = (
   SELECT MIN(ram)
   FROM pc
   )
  )
)
AND
maker IN (
SELECT maker
FROM product
WHERE type='printer'
)
```
## 26

https://sql-ex.ru/learn_exercises.php?LN=26
```sql
SELECT sum(s.price)/sum(s.kol) as sredn FROM
(SELECT price,1 as kol FROM pc,product
 WHERE pc.model=product.model AND product.maker='A'
UNION all
 SELECT price,1 as kol FROM laptop,product
 WHERE laptop.model=product.model AND product.maker='A') as s
```
## 27

https://sql-ex.ru/learn_exercises.php?LN=27
```sql
SELECT product.maker, AVG(pc.hd)
FROM pc, product WHERE product.model = pc.model
AND product.maker IN ( SELECT DISTINCT maker
FROM product
WHERE product.type = 'printer')
GROUP BY maker
```
## 28

https://sql-ex.ru/learn_exercises.php?LN=28
```sql
SELECT count(*)
FROM (SELECT maker
FROM product
GROUP BY maker HAVING COUNT(model)=1) as count
```
## 29

https://sql-ex.ru/learn_exercises.php?LN=29
```sql
SELECT t1.point, t1.date, inc, out
FROM income_o t1 LEFT JOIN outcome_o t2 ON t1.point = t2.point
AND t1.date = t2.date
UNION
SELECT t2.point, t2.date, inc, out
FROM income_o t1 RIGHT JOIN outcome_o t2 ON t1.point = t2.point
AND t1.date = t2.date
```
## 30

https://sql-ex.ru/learn_exercises.php?LN=30
```sql
SELECT point, date, SUM(sum_out), SUM(sum_inc)
FROM( SELECT point, date, SUM(inc) as sum_inc, null as sum_out FROM Income Group BY point, date
UNION
SELECT point, date, null as sum_inc, SUM(out) as sum_out from Outcome Group BY point, date ) as t
group BY point, date order BY point
```
## 31

https://sql-ex.ru/learn_exercises.php?LN=31
```sql
SELECT DISTINCT class, country
FROM classes
WHERE bore >= 16
```

## 32

https://sql-ex.ru/learn_exercises.php?LN=32
```sql
SELECT country, cast(AVG((power(bore,3)/2)) as numeric(6,2)) as weight
FROM (select country, classes.class, bore, name FROM classes left JOIN ships on classes.class=ships.class
UNION all
SELECT distinct country, class, bore, ship FROM classes t1 left JOIN outcomes t2 on t1.class=t2.ship
WHERE ship=class and ship not in (SELECT name FROM ships) ) a
WHERE name IS NOT NULL group BY country
```

## 33

https://sql-ex.ru/learn_exercises.php?LN=33
```sql
SELECT o.ship FROM
BATTLES b
LEFT join outcomes o ON o.battle = b.name
WHERE b.name = 'North Atlantic' AND o.result = 'sunk'
```
## 34

https://sql-ex.ru/learn_exercises.php?LN=34
```sql
SELECT name FROM classes, ships 
WHERE launched >= 1922 
AND displacement > 35000 
AND type = 'bb' 
AND ships.class = classes.class
```
## 35

https://sql-ex.ru/learn_exercises.php?LN=35
```sql
SELECT model, type
FROM product
WHERE upper(model) NOT LIKE '%[^A-Z]%'
OR model NOT LIKE '%[^0-9]%'
```
## 36

https://sql-ex.ru/learn_exercises.php?LN=36
```sql
SELECT name FROM ships WHERE class = name
UNION
SELECT ship AS name FROM classes,Outcomes WHERE classes.class = outcomes.ship
```
## 37

https://sql-ex.ru/learn_exercises.php?LN=37
```sql
```
## 38

https://sql-ex.ru/learn_exercises.php?LN=38
```sql
SELECT country
FROM classes
GROUP BY country
HAVING COUNT(DISTINCT type) = 2
```
## 39

https://sql-ex.ru/learn_exercises.php?LN=39
```sql
WITH b_s AS
(SELECT o.ship, b.name, b.date, o.result
FROM Outcomes o
LEFT JOIN battles b ON o.battle = b.name )
SELECT DISTINCT a.ship FROM b_s a
WHERE UPPER(a.ship) IN
(SELECT UPPER(ship) FROM b_s b
WHERE b.date < a.date AND b.result = 'damaged')
```
## 40

https://sql-ex.ru/learn_exercises.php?LN=40
```sql
SELECT maker, MAX(type)
FROM product
GROUP BY maker
HAVING COUNT(DISTINCT type) = 1 AND COUNT(model) > 1
```
## 41

https://sql-ex.ru/learn_exercises.php?LN=41
```sql
WITH new AS (SELECT model,price FROM PC
UNION
SELECT model,price FROM Laptop
UNION
SELECT model,price FROM Printer
) 
SELECT t.maker, case WHEN count(price) = count(*) THEN MAX(price) END
FROM Product AS t, new
WHERE t.model=new.model
GROUP BY t.maker
```
## 42

https://sql-ex.ru/learn_exercises.php?LN=42
```sql
SELECT ship, battle FROM Outcomes WHERE result = 'sunk'
```
## 43

https://sql-ex.ru/learn_exercises.php?LN=43
```sql
SELECT name
FROM battles
WHERE year(date) NOY IN
     (SELECT launched
      FROM ships
      WHERE launched IS NOT NULL)
```
## 44

https://sql-ex.ru/learn_exercises.php?LN=44
```sql
SELECT name FROM Ships
WHERE name LIKE 'R%'
UNION
SELECT Ship FROM Outcomes
WHERE Ship LIKE 'R%'
```
## 45

https://sql-ex.ru/learn_exercises.php?LN=45
```sql
SELECT name FROM ships
WHERE name LIKE '% % %'
UNION
SELECT ship FROM Outcomes
WHERE ship LIKE '% % %'
```
## 46

https://sql-ex.ru/learn_exercises.php?LN=46
```sql
SELECT o.ship, displacement, numGuns FROM
(SELECT name AS ship, displacement, numGuns
FROM Ships s JOIN Classes c ON c.class=s.class
UNION
SELECT class AS ship, displacement, numGuns
FROM Classes c) AS a
RIGHT JOIN Outcomes o
ON o.ship=a.ship
WHERE battle = 'Guadalcanal'
```
## 47

https://sql-ex.ru/learn_exercises.php?LN=47
```sql
```
## 48

https://sql-ex.ru/learn_exercises.php?LN=48
```sql
SELECT cl.class
FROM Classes cl
LEFT JOIN Ships s ON s.class = cl.class
WHERE cl.class IN (SELECT ship FROM Outcomes WHERE result = 'sunk') OR
s.name IN (SELECT ship FROM Outcomes WHERE result = 'sunk')
GROUP BY cl.class
```
## 49

https://sql-ex.ru/learn_exercises.php?LN=49
```sql
SELECT Ships.name
FROM Classes JOIN
Ships ON Classes.class = ships.class
WHERE bore = 16
UNION
SELECT Outcomes.ship
FROM Outcomes JOIN
Classes ON Classes.class = Outcomes.ship
WHERE bore = 16
```
## 50

https://sql-ex.ru/learn_exercises.php?LN=50
```sql
SELECT distinct battle FROM Outcomes
WHERE ship IN (SELECT name
               FROM ships
               WHERE class = 'kongo')
```
## 51

https://sql-ex.ru/learn_exercises.php?LN=51
```sql
```
## 52

https://sql-ex.ru/learn_exercises.php?LN=52
```sql
SELECT DISTINCT s.name
FROM ships s
JOIN classes c ON c.class = s.class
WHERE UPPER(c.country) = 'JAPAN'
and (numguns>=9 or numguns IS NULL)
AND (c.bore < 19 OR c.bore IS NULL)
AND (displacement <= 65000 OR c.displacement IS NULL)
AND c.type = 'bb'
```
## 53

https://sql-ex.ru/learn_exercises.php?LN=53
```sql
```
## 54

https://sql-ex.ru/learn_exercises.php?LN=54
```sql
```
## 55

https://sql-ex.ru/learn_exercises.php?LN=55
```sql
SELECT c.class, t.y
FROM classes c
LEFT JOIN
(SELECT class, MIN(launched) AS y
FROM ships
GROUP BY class
) AS t ON c.class = t.class
```
## 56

https://sql-ex.ru/learn_exercises.php?LN=56
```sql
SELECT
  class
  , SUM(CASE WHEN result='sunk' THEN 1 ELSE 0 END) as sunks
  from (
    SELECT c.class, name FROM classes c
      left JOIN ships s on c.class=s.class
    UNION
    SELECT class, ship FROM classes
      JOIN Outcomes ON class=ship
  ) as sh
  left JOIN Outcomes o ON sh.name=o.ship
  GROUP BY class
```
