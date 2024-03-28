## Exercise for Tuesday 19.03
Consider the following schema:
 
Students(Sid, Name, Surname)
Exams(Date,Year,Subject,Grade,Sid\*,Tid\*)
Teachers(Tid,Name,Surname)
 
Write some SQL code for the following queries.
1. Return the Date and Subject of all the exams where the grade is greated than 20 or the name of the student is 'Mario'
2. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is 'Ghelli'
3. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is equal to the surname of the student
4. For each student that passed at least one exam, return the SId, the name, the number of exams passed, the average grade
5. For each student and each year, return the SId, the student name, the year, the number of exams passed in that year, the average grade for that year
6. For each student that passed two different exams with the same Subject but with a different grade return the SId, the subject, the grade of the first exam, the grade of the second exam

## Correct Solutions

1. Return the Date and Subject of all the exams where the grade is greated than 20 or the name of the student is 'Mario'
```SQL
SELECT DISTINCT e.Date, e.Subject
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE e.Grade > 20 OR s.Name = 'Mario'
```
Also possible to use `NATURAL JOIN`. But Ghelli does not like Natural Join because it is not robust. If you modify the schema, it may break.
Also possible `JOIN...USING (TId)`, it intermediate between natural and on, where you specify the condition. It is like saying "do a natural join using (attribute)".
Also possible to use Cross Join with the comma and add the condition in WHERE.

2. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is 'Ghelli'

```SQL
SELECT DISTINCT s.Sid, s.Name, s.Surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
	JOIN Teacher t ON e.Tid=t.Tid
WHERE t.surname = 'Ghelli'
```

If the question was to find students with at least two exams, a COUNT was needed.
```sql
SELECT s.Sid, s.Name, s.Surname, COUNT(*), AVG(e.Grade)
FROM Students s JOIN Exams e ON s.Sid=e.Sid
	JOIN Teacher t ON e.Tid=t.Tid
WHERE t.surname = 'Ghelli'
GROUP BY s.Sid, s.Name, s.Surname
HAVING COUNT(*)>=2
```
*We need to add s.Name and s.Surname in the GROUP BY otherwise they are deleted.* But we want them as outputs in SELECT. Otherwise the number of record would not match if they are not grouped.
GROUP BY already does DISTINCT elimination.


3. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is equal to the surname of the student

```SQL
SELECT DISTINCT s.Sid, s.Name, s.Surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
	JOIN Teacher t ON e.Tid=t.Tid
WHERE s.Surname=t.Surname
```

4. For each student that passed at least one exam, return the SId, the name, the number of exams passed, the average grade

```SQL
SELECT DISTINCT s.Sid, s.Name, s.Surname, COUNT(e.*), COUNT(e.Grade), AVG(e.Grade)
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE 
GROUP BY s.Sid, s.Name, s.Surname
HAVING 
```
Whenever you mix records and functions is a GROUP BY.
Note that some exams may not have grade, so we can use `COUNT(e.Grade)` which counts only where grade is not NULL.

5. For each student and each year, return the SId, the student name, the year, the number of exams passed in that year, the average grade for that year

```SQL
SELECT DISTINCT s.Sid, s.Name, s.Surname, e.Year, COUNT(e.*), COUNT(e.Grade), AVG(e.Grade)
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE 
GROUP BY s.Sid, s.Name, s.Surname, e.Year
HAVING 
```

6. For each student that passed two different exams with the same Subject but with a different grade return the SId, the subject, the grade of the first exam, the grade of the second exam

```SQL
SELECT s.Sid, e1.Subject, e1.Grade, e2.Grade
FROM Students s JOIN Exams e1 ON s.Sid=e1.Sid
	JOIN Exams e2 ON s.Sid=e2.Sid
WHERE e1.Subject = e2.Subject AND e1.Grade <> e2.Grade
```
Note the JOIN, one is not enough to compare two records of exams.
We assume different grade means different different exam.
Note that the students table is not necessary, because we are asked only the Sid.

