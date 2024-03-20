Exercise for Wednesday 20Consider the following schema: 

Students(Sid, Name, Surname)
Exams(Date,Year,Subject,Grade,Sid*,Tid*)
Teachers(Tid,Name,Surname)

Write some SQL code for the following queries.

1. Return the Name and Surname of all students who only passed exams where the Surname of the Teacher is 'Ghelli'

2. Return the Name and Surname of all teachers who are only related to exams with a grade greater than 25


## My solutions
1. Return the Name and Surname of all students who only passed exams where the Surname of the Teacher is 'Ghelli'

Universal quantifier.
```sql
SELECT s.Name, s.Surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE t.Surname =ALL (SELECT t.Surname
					 FROM Teachers t
					 WHERE t.Name='Ghelli')

```

Or maybe
```sql
SELECT s.Name, s.Surname
FROM Students s JOIN Exams e ON s.Sid=e.Sid
WHERE NOT EXISTS (SELECT t.Surname
					 FROM Teachers t
					 WHERE t.Name <> 'Ghelli')

```


2. Return the Name and Surname of all teachers who are only related to exams with a grade greater than 25

```sql
SELECT t.Name, t.Surname
FROM Teachers t JOIN Exams e ON t.Tid=e.Tid
WHERE NOT EXIST (SELECT e.grade
				FROM Exams e
				WHERE e.Grade > 25)

```

