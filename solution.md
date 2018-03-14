1.
```
select h1.name as name
from Highschooler h1, Highschooler h2, Friend
where h1.ID=Friend.ID1 and h2.ID=Friend.ID2 and h2.name='Gabriel';

select name
from Highschooler
where ID IN (
select ID2
from Highschooler h, Friend f
where h.name='Gabriel'
and f.ID1 = h.ID);
```
8.
```
SELECT (select count(*) from Friend)/count(*)
FROM Highschooler;

SElECT AVG(c) AS 'avg friends per student'
FROM
  (SELECT ID1, count(*) AS c
   FROM Friend
   GROUP BY ID1) counts;
```