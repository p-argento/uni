Best resource https://www.freecodecamp.org/news/window-functions-in-sql/


Aggregating
1. SUM()
2. COUNT()
3. MAX()



RANK
Distinguish
1. ROW_NUMBER()
	1. all numbers
2. RANK()
	1. ties are counted (meaning that some numbers are skipped)
3. DENSE_RANK()
	1. ties have the same number, but all numbers are showed


Window

You can specify a frame clause using two things – `ROWS` and `RANGE` (Microsoft SQL Server does not support it)

```sql
SELECT
    *,
    SUM(score)OVER(ORDER BY student_id
				    ROWS BETWEEN UNBOUNDED PRECEDING 
						    AND CURRENT ROW) AS cummulative_sum
FROM student_score
```


![[Pasted image 20250128152850.png]]

When using an aggregate window function, you may not include the `ORDER BY` clause. But when you use the `ORDER BY` clause, it's a best practice to specify the frame clause for accurate results. What this means is say you want to use an aggregate window function and you want to also order the observations in that window by a column. It's best practice is to specify a frame clause so that you will get an accurate result. But if you are not ordering the observations in the window when using an aggregate function, you don't need to specify a frame clause.


Another super interesting resource to really understand RANGE.
https://www.bluetickconsultants.com/blogs/advanced-sql-window-functions-part-1.html

However, it is quite weird because it looks like in SQL Server `RANGE is only supported with UNBOUNDED and CURRENT ROW window frame delimiters.`






