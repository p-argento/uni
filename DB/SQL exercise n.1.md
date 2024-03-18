## Exercise for Tuesday 19.3
Consider the following schema:
 
Students(Sid, Name, Surname)
Exams(Date,Year,Subject,Grade,Sid*,Tid*)
Teachers(Tid,Name,Surname)
 
Write some SQL code for the following queries.
1. Return the Date and Subject of all the exams where the grade is greated than 20 or the name of the student is 'Mario'
2. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is 'Ghelli'
3. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is equal to the surname of the student
4. For each student that passed at least one exam, return the SId, the name, the number of exams passed, the average grade
5. For each student and each year, return the SId, the student name, the year, the number of exams passed in that year, the average grade for that year
6. For each student that passed two different exams with the same Subject but with a different grade return the SId, the subject, the grade of the first exam, the grade of the second exam

## My solutions

1. Return the Date and Subject of all the exams where the grade is greated than 20 or the name of the student is 'Mario'
```SQL
SELECT DISTINCT e.date, e.subject
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE e.grade > 20 OR s.name = 'Mario'
```

2. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is 'Ghelli'

```SQL
SELECT DISTINCT s.name, s.surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
	JOIN Teacher t ON e.Tid=t.Tid
WHERE e.grade >= 18 AND t.surname = 'Ghelli'
```

3. Return the Name and Surname of all students who passed at least one exam where the Surname of the Teacher is equal to the surname of the student

```SQL
SELECT DISTINCT s.Name, s.Surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
	JOIN Teacher t ON e.Tid=t.Tid
WHERE s.Surname=t.Surname
```

4. For each student that passed at least one exam, return the SId, the name, the number of exams passed, the average grade

```SQL
SELECT s.Sid, s.Name, COUNT(e.*), AVG(e.Grade)
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE 
GROUP BY s.Sid
HAVING 
```