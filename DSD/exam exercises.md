Types
## 1. DW schema

 1. analysis requirements
	 1. fact granularity
	 2. additive measures
 2. conceptual schema
 3. logical schema
 4. update of dimensional attributes


## 2. SQL Queries with indexes and trees

1. analytical sql query
2. query logical tree
3. type and value of the result
4. use of indexes (and definition)
	1. bitmap
5. physical query plan

Basic functions
1. SELECT, FROM, WHERE
2. GROUP BY, HAVING, ORDER BY... DESC
3. WITH view AS ...
4. IN (nested query)
5. JOIN, LEFT OUTER JOIN, ...
6. CASE WHEN... THEN... ELSE... END

## 3. Analytic SQL for reporting

on foodmart, with many join I guess.
Using ROLLUP and CUBE.

Analytical Functions for reporting
1. ROLLUP, CUBE, GROUPING
2. OVER, PARTITION BY
3. RANK, DENSE_RANK(), PERCENT_RANK()
4. ROW_NUMBER(), CUME_DIST(), NTILE(3)
5. COUNT(), SUM(), AVG(), MIN(), MAX()
6. LAG(attribute, offset=1, default=NULL) and LEAD(attribute, offset=1, default =NULL)
7. ROWS, RANGE

Rollup eliminate the rightmost attribute each time.
Over creates a column as it was a groupby but keeping all the rows, meaning that the rows that should have been grouped have the same value. Partition by is for the attribute to group by, if there isn't any, it means no groupby, and can be used for the total. 
Rank can be used together with groupby within the over to display the rank order, also within the partition if specified.
Lag and lead get the value of attribute in offset rows before or after.


## 4. Materialized Views

1. Given a lattice, select 2 views to materialize with the greedy algorithm HRU.


## 5. Query optimization

1. Show how to perform before the join the GROUP BY.
2. Show how to rewrite the query Q using the view V



???
![[Pasted image 20250113123821.png]]

