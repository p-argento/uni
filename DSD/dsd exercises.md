These are the exercises in the folder dsd-ruggieri-assignments. I think I will focus on SQL here.

## dsd-ruggieri-exercises
[[dsd-ruggieri-exercises.pdf]]

example1.
a) total sales revenue by product
```sql
SELECT PkP, UnitPrice*Qty AS Revenue
FROM Sales, Product
WHERE FkP=PkP
GROUP BY PkP
```

b) logical query plan, the type and the value of the result.






## assignment07




