
## Solutions

Exercise for Wednesday 20Consider the following schema: 

Students(Sid, Name, Surname)
Exams(Date,Year,Subject,Grade,Sid*,Tid*)
Teachers(Tid,Name,Surname)

Write some SQL code for the following queries.

1. Return the Name and Surname of all students who only passed exams where the Surname of the Teacher is 'Ghelli'
$$\begin{align}
&(Name,Surname)|s\in Students\ \forall e \in exams, t\in Teachers \\ &e.Sid=t.Sid\ \wedge\ e.Tid=t.Tid,\ t.Name='Ghelli'
\end{align}$$
Unfortunately, in sql, we do not have forall, so we use NOT EXISTS and NOT the condition.

```sql
SELECT s.Name, s.Surname
FROM Students s
WHERE NOT EXISTS (SELECT *
					 FROM Exams e JOIN Teachers t ON e.Tid=t.Tid
					 WHERE e.Sid=s.Sid AND NOT t.Name='Ghelli')
```
This is a universal query, returning also students with no exams.
If we wanted only students with at least one exam is
```sql
SELECT s.Name, s.Surname
FROM Students s JOIN Exams e1 ON s.Sid=e1.Sid
WHERE NOT EXISTS (SELECT *
					 FROM Exams e2 JOIN Teachers t ON e2.Tid=t.Tid
					 WHERE e2.Sid=s.Sid AND NOT t.Name='Ghelli')
```
NEVER reuse the same alias in different nested parts. It means distinguish e1 and e2.

If you want to quantify the exams, the condition must be INSIDE the NOT EXISTS, and not only outside. This is the MAIN error you make during mid-term.



2. Return the Name and Surname of all teachers who are only related to exams with a grade greater than 25

```sql
SELECT t.Name, t.Surname
FROM Teachers t 
WHERE NOT EXISTS (SELECT *
				FROM Exams e
				WHERE NOT (e.Grade > 25)
```

To add subject=db.
```sql
SELECT t.Name, t.Surname
FROM Teachers t 
WHERE NOT EXISTS (SELECT *
				FROM Exams e
				WHERE e.Tid=t.Tid AND 
					NOT (e.Grade > 25 AND 
						e.Subject='Database')
```

Let's see some alternatives.
But remember that for more complicated queries it is better to use NOT EXISTS
```sql
SELECT t.Name, t.Surname
FROM Teachers t 
WHERE 25 <ALL (SELECT e.grade
				FROM Exams e
				WHERE e.Tid=t.Tid
```
Also (maybe compact but not readable). I suggest you not to use it.
```sql
SELECT t.Name, t.Surname
FROM Teachers t 
WHERE t.Tid NOT IN (SELECT e.Tid
				FROM Exams e
				WHERE NOT (e.Grade>25)
```
Another way is EXCEPT, like in the algebric way. But it is horrible.




