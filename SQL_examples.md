������ SQL (SQL-ex.ru)

�������:�1
������� ����� ������, �������� � ������ �������� ����� ��� ���� �� ���������� ����� 500 ���. �������: model, speed � hd.
SELECT model, speed, hd 
FROM pc 
WHERE price <500

�������:�2
������� �������������� ���������. �������: maker.
SELECT DISTINCT maker 
FROM product
WHERE type='printer'

�������:�3
������� ����� ������, ����� ������ � ������� ������� ��-���������, ���� ������� ��������� 1000 ���.
SELECT model, ram, screen
FROM laptop
WHERE price >1000

�������:�4
������� ��� ������ ������� Printer ��� ������� ���������.
SELECT *
FROM printer
WHERE color='y'

�������:�5
������� ����� ������, �������� � ������ �������� ����� ��, ������� 12x ��� 24x CD � ���� ����� 600 ���.
SELECT model, speed, hd
FROM pc
WHERE cd IN ('12x', '24x') AND
price <600

�������:�6
��� ������� �������������, ������������ ��-�������� c ������� �������� ����� �� ����� 10 �����, ����� �������� ����� ��-���������. �����: �������������, ��������.
SELECT DISTINCT p.maker, l.speed
FROM product p
JOIN laptop l ON p.model = l.model
WHERE l.hd >=10

�������:�7
������� ������ ������� � ���� ���� ��������� � ������� ��������� (������ ����) ������������� B (��������� �����).
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

�������:�8
������� �������������, ������������ ��, �� �� ��-��������.
SELECT DISTINCT maker
FROM product
WHERE type='pc' 
AND maker NOT IN (SELECT maker FROM product WHERE type='laptop')

�������:�9
������� �������������� �� � ����������� �� ����� 450 ���. �������: Maker.
SELECT DISTINCT p.maker 
FROM product p
JOIN pc pc ON p.model=pc.model
WHERE pc.speed>=450

�������:�10
������� ������ ���������, ������� ����� ������� ����. �������: model, price.
SELECT model, price
FROM printer 
WHERE price = (SELECT MAX(price) FROM printer)

�������:�11
������� ������� �������� ��.
SELECT AVG(speed) AS avg_speed
FROM pc

�������:�12
������� ������� �������� ��-���������, ���� ������� ��������� 1000 ���.
SELECT AVG(speed) AS avg_speed
FROM laptop 
WHERE price >1000

�������:�13
������� ������� �������� ��, ���������� �������������� A.
SELECT AVG(pc.speed) AS avg_speed
FROM pc pc
JOIN product p ON pc.model=p.model
WHERE p.maker='A'

�������:�14
������� �����, ��� � ������ ��� �������� �� ������� Ships, ������� �� ����� 10 ������.
SELECT s.class, s.name, c.country
FROM ships s
JOIN classes c ON s.class=c.class
WHERE c.numGuns >= 10

�������:�15
������� ������� ������� ������, ����������� � ���� � ����� PC. �������: HD.
SELECT hd 
FROM pc
GROUP BY hd
HAVING COUNT(hd)>1

�������:�16
������� ���� ������� PC, ������� ���������� �������� � RAM. � ���������� ������ ���� ����������� ������ ���� ���, �.�. (i,j), 
�� �� (j,i), ������� ������: ������ � ������� �������, ������ � ������� �������, �������� � RAM.
SELECT DISTINCT i.model, j.model, i.speed, i.ram
FROM pc i, pc j
WHERE i.model>j.model 
AND i.speed=j.speed
AND i.ram=j.ram

�������:�17
������� ������ ��-���������, �������� ������� ������ �������� ������� �� ��.
�������: type, model, speed.
SELECT DISTINCT p.type, l.model, l.speed
FROM laptop l, product p
WHERE speed < ALL (SELECT speed FROM pc)
AND l.model = p.model

�������:�18
������� �������������� ����� ������� ������� ���������. �������: maker, price.
SELECT DISTINCT p.maker, pr.price
FROM product p, printer pr
WHERE p.model = pr.model
AND pr.color = 'Y'
AND pr.price = (SELECT  MIN (p.price)
FROM printer p
WHERE p.color = 'Y')

�������:�19
��� ������� �������������, �������� ������ � ������� Laptop, ������� ������� ������ ������ ����������� �� ��-���������.
�������: maker, ������� ������ ������.
SELECT p.maker, AVG (l.screen)
FROM product p
JOIN laptop l
ON p.model=l.model
AND p.type = 'Laptop'
GROUP BY p.maker

�������:�20
������� ��������������, ����������� �� ������� ���� ��� ��������� ������ ��. �������: Maker, ����� ������� ��.
SELECT p.maker, COUNT (*)
FROM product p
WHERE p.type = 'PC'
GROUP BY p.maker
HAVING COUNT (*) >= 3

