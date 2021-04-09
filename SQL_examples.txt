Задачи SQL (SQL-ex.ru)

Задание: 1
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd.
SELECT model, speed, hd 
FROM pc 
WHERE price <500

Задание: 2
Найдите производителей принтеров. Вывести: maker.
SELECT DISTINCT maker 
FROM product
WHERE type='printer'

Задание: 3
Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.
SELECT model, ram, screen
FROM laptop
WHERE price >1000

Задание: 4
Найдите все записи таблицы Printer для цветных принтеров.
SELECT *
FROM printer
WHERE color='y'

Задание: 5
Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.
SELECT model, speed, hd
FROM pc
WHERE cd IN ('12x', '24x') AND
price <600

Задание: 6
Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.
SELECT DISTINCT p.maker, l.speed
FROM product p
JOIN laptop l ON p.model = l.model
WHERE l.hd >=10

Задание: 7
Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).
SELECT l.model, l.price
FROM laptop l
JOIN product p ON l.model=p.model
WHERE p.maker='B'
UNION
SELECT pc.model, pc.price
FROM pc pc
JOIN product p ON pc.model=p.model
WHERE p.maker='B'
UNION
SELECT pr.model, pr.price
FROM printer pr
JOIN product p ON pr.model=p.model
WHERE p.maker='B'

Задание: 8
Найдите производителя, выпускающего ПК, но не ПК-блокноты.
SELECT DISTINCT maker
FROM product
WHERE type='pc' 
AND maker NOT IN (SELECT maker FROM product WHERE type='laptop')

Задание: 9
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker.
SELECT DISTINCT p.maker 
FROM product p
JOIN pc pc ON p.model=pc.model
WHERE pc.speed>=450

Задание: 10
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price.
SELECT model, price
FROM printer 
WHERE price = (SELECT MAX(price) FROM printer)

Задание: 11
Найдите среднюю скорость ПК.
SELECT AVG(speed) AS avg_speed
FROM pc

Задание: 12
Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
SELECT AVG(speed) AS avg_speed
FROM laptop 
WHERE price >1000

Задание: 13
Найдите среднюю скорость ПК, выпущенных производителем A.
SELECT AVG(pc.speed) AS avg_speed
FROM pc pc
JOIN product p ON pc.model=p.model
WHERE p.maker='A'

Задание: 14
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.
SELECT s.class, s.name, c.country
FROM ships s
JOIN classes c ON s.class=c.class
WHERE c.numGuns >= 10

Задание: 15
Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD.
SELECT hd 
FROM pc
GROUP BY hd
HAVING COUNT(hd)>1

Задание: 16
Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), 
но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.
SELECT DISTINCT i.model, j.model, i.speed, i.ram
FROM pc i, pc j
WHERE i.model>j.model 
AND i.speed=j.speed
AND i.ram=j.ram

Задание: 17
Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed.
SELECT DISTINCT p.type, l.model, l.speed
FROM laptop l, product p
WHERE speed < ALL (SELECT speed FROM pc)
AND l.model = p.model

Задание: 18
Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price.
SELECT DISTINCT p.maker, pr.price
FROM product p, printer pr
WHERE p.model = pr.model
AND pr.color = 'Y'
AND pr.price = (SELECT  MIN (p.price)
FROM printer p
WHERE p.color = 'Y')

Задание: 19
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.
SELECT p.maker, AVG (l.screen)
FROM product p
JOIN laptop l
ON p.model=l.model
AND p.type = 'Laptop'
GROUP BY p.maker

Задание: 20
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.
SELECT p.maker, COUNT (*)
FROM product p
WHERE p.type = 'PC'
GROUP BY p.maker
HAVING COUNT (*) >= 3

