## Case study: University Exams

The ifelse() in sql is:
```sql
SELECT Grade,
		CASE
			WHEN Grade>17 THEN 1
			ELSE 0
		END
```

Everything that is available in the operational database should be added, even if not present in the business questions. They will be asked later, so better to add the dimensions at the beginning.



