1.
```
SELECT h1.name AS name
FROM Highschooler h1, Highschooler h2, Friend
WHERE h1.ID=Friend.ID1 AND h2.ID=Friend.ID2 AND h2.name='Gabriel';

SELECT name
FROM Highschooler
WHERE ID IN (
  SELECT ID2
  FROM Highschooler h, Friend f
  WHERE h.name='Gabriel' and f.ID1 = h.ID);
```

2.
```
SELECT name, grade
FROM Highschooler
WHERE ID NOT IN(
  SELECT ID1 AS ID
  FROM Likes
  UNION
  SELECT ID2 AS ID
  FROM Likes
);

select name, grade
from Highschooler
where ID NOT IN(
  select ID1 as ID
  from Likes)
  AND ID NOT IN(
  select ID2 as ID
  from Likes);

select name, grade
from Highschooler
where NOT EXISTS (
  select *
  from Likes
  where ID = ID1 OR ID = ID2);
```
3.
```
SELECT name, grade
FROM Highschooler h, Likes l
WHERE h.ID = l.ID2
GROUP BY name, grade, ID
HAVING count(*) > 1;

SELECT name, grade
FROM Highschooler
WHERE (
  SElECT count(*)
  FROM Likes
  WHERE ID = ID2) > 1;
```
4.
```
SELECT h1.name, h1.grade, h2.name, h2.grade
FROM Highschooler h1, Likes, Highschooler h2
WHERE h1.ID = ID1 AND ID2 = h2.ID
  AND (h1.grade - h2.grade) >= 2;
```
5.

6.

7.

8.
```
SELECT (SELECT count(*) FROM Friend)/count(*)
FROM Highschooler;

SElECT AVG(c) AS 'avg friends per student'
FROM
  (SELECT ID1, count(*) AS c
   FROM Friend
   GROUP BY ID1) counts;
```