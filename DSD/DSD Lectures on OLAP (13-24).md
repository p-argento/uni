UP TO NOW 
Data Warehouse: Data Models and DW Design and Implementation.
STARTING TODAY 
Data Analysis Using SQL.  How to summarize data using SQL?  What if the query takes a long time to produce the answer?


# dsd13 - Multidimensional Model (Cube)
Multidimensional Cube model: OLAP Operations. 
The extended cube and the lattice of cuboids.
Pivot tables in Excel.

We will see in a couple of lessons how to use advanced sql for reports.

## OLAP Cube Operations

Today we look at multidimensional analysis using an abstraction called OLAP System, also called data cube.

![[Pasted image 20241125155614.png]]

What is the benefit?
A cube is a n-dimensional array where each dimension correspond to a dimension of analysis.
For example, let's consider 3 degenrate dimensions. Every cell in the cube has precomputed values. This can speed up the calculations.

![[Pasted image 20241125155742.png]]

Every night, when the new data is loaded, we run the olap system to also update the cube.

How to navigate the multidimensional cube?
We assume additive and degenerate dimensions for now. The way to present the cube is actually a plot, but it is stored as a matrix.

![[Pasted image 20241125160015.png]]

Let's generalize.
Consider where the number of dimensions is more than 2, say 3.
There can be empty cells. Notice that when we increase the dimensions, most of the cells are empty (sparse). Efficient data structures can be used.

What operations can we do?
Restrict to a subcube, they do not imply calculations
1. slice
	1. selecting a specific subset of data by fixing one dimension to a single value
	2. this operation reduces the cube's dimensionality
	3. for example `Time = 2024`
2. dice
	1. selecting a subset of data by specifying a range or set of values for multiple dimensions
	2. this operation does not necessarily reduce the dimensionality but narrows the data within the cube
	3. for example selecting `Time = [2023, 2024]` and `Region = [North, South]`
More
3. pivot
	1. reorient the cube
	2. we just change the orientation of the axis
Observe that we can compose operators.
To aggregate
4. roll-up
	1. aggregates data by dimension reduction
		1. or by going up in attribute hierarchy
	2. decrease the granularity
5. drill-down
	1. reverse of roll-up
	2. increase the granularity

![[Pasted image 20241125160707.png]]

A 0-dimensional cube is also called an Apex-cube. It is a total and we cannot analyse it further (if not drilling-down).

6. drill through
	1. it produces all the facts that satisfy a cell coordinate

What is the benefit of precomputing the cube?
Different users with different needs but only one cube with all the results already available.

![[Pasted image 20241125161147.png]]

Which tool implement this abstraction?
For the OLAP system, we use
1. SSAS (SQL Server Analysis Server)
2. PowerPivot

For the multidimensional analysis, we use
1. Excel
	1. only for limited size
2. PowerBI
3. Microstrategy

## Playing with Pivot Tables in Excel
> Download excel data for pivot table on didawiki, to play with excel

Showing examples of pivot tables in excel.
So, watching the settings on the right.
1. filters
	1. work as a slice or dice
2. rows and columns
	1. determine if we are rolling-up or drilling-down
3. values
	1. ..
4. right click on cell
	1. we can select drill-through

Data can be also explored by charts.
The chart is dynamic, based on the pivot table.

Excel offer the possibility to explore data in the OLAP.
We now connect the Foodmart DW to Excel (not to the OLAP, you will see that in the lab).
There is a sales_fact table.

![[Pasted image 20241125163801.png]]

The more specific the connection, the faster will be the connection, compared to general connections. We use the OLEDB standard.
Let's build the string.
As a driver, choose `Microsoft OLE DB for SQL Server`.
Follow the steps as usual.

Next step is to *import* the table from the DW.
We can select multiple tables.
We also need to specify the foreign keys for the `Relationships`, look in the section of settings called `Data Tools`.

We now proceed to `Insert` >  `Pivot Table` > `from Data Model` .

The next morning, with `Refresh All` in `Queries and Connections`, we can reimport everything after the night load, without changing the structure of the pivot tables.

Excel is not able to deal with hierarchies.

## Textual Notation for Cube Operators

![[Pasted image 20241125170015.png]]

In roll-up, we use `*` to mean summarize (sum) data by all the dimension values.

![[Pasted image 20241125170111.png]]

For example
1. we have the total quantity by store, only for product P1, independently of the date
	1. `Sales(StoreId, 'P1', *)`

We can read `*` as *any*.
We can add these values to create the *extended cube*.
In this extended cube, we can see all the roll-up values.

![[Pasted image 20241125170438.png]]

Consider now the *DW lattice* (reticolo).
Read by lines.

![[Pasted image 20241125170627.png]]

How many subsets (or cuboids)?
A cuboid is a cube with a subset of dimensions.
The multidimensional cube is the union of these cuboids.
In general, it is the product of the cardinality of the dimensions in the cuboid.
Remember to add +1 in the extended cube.

This number can be enormous, but most of the cells are usually empty, and this allows for efficient implementation of sparse matrices.

![[Pasted image 20241125170942.png]]

How to compute a cuboid given another one?
We will discuss in the future what is precomputed and what is computed on the fly.

Is it always possible to compute functions on the fly when rolling-up or drilling-down?
In the case of distributeive aggregative functions, like sum or count, yes.
For other functions, like the average, called algebraic, this is not possible directly. However, I can compute the average using the aggregate sum and count that are distributive.
There are functions for which this is impossible, called Holistic. It  

![[Pasted image 20241125171414.png]]

# dsd14 - Relational Model
Recalls on: DBMS, from SQL to extended relational algebra.

## Functions of a DBMS

DB is a collection of persistent data:
1. schema (or meta-data)
	1. time-invariant
	2. abstract knowledge
2. data
	1. concrete knowledge

A DBMS is a centralized or distributed software system.

The functions are
	1. DDL (Data Description Language)
	2. DML (Data Manipulation Language)
	3. DQL (Data Query Language)
	4. DBA (Database Administrator)

Different levels
	1. logical view
		1. `CREATE VIEW ...`
	2. logical level
		1. `CREATE TABLE ...`
	3. physical level
		1. indexes and other data structures

Let's start from *DBA*.
There is a catalog that is meant to query the DB
![[Pasted image 20241223111506.png]]

Data Control.
1. Access control
	1. we can grant the permissions (or priviledges) to users
	2. ![[Pasted image 20250107105136.png|300]]
2. integrity control
	1. foreign key control for instance
3. concurrency control
	1. to monitor real-time transactions
4. data recovery

## SQL Queries

We explore the SQL standardised in 2003.
1. in 1999 it was extended with ROLLUP CUBE
2. in 2003 it was extended with analytical functions

![[Pasted image 20250107105559.png]]

A catalog consists of one or more schemas

*DDL* -> Data Definition Language
It means "Create / Alter / Drop -> Table / View"

Keywords
1. PRIMARY KEY
2. UNIQUE
3. CHECK
4. ON DELETE ...

![[Pasted image 20250107110536.png]]


*DML* -> Data Manipulation Language
It means "Insert / Update / Delete".

Keywords
1. INSERT INTO

![[Pasted image 20250107110547.png]]

*DQL* -> Data Query Language
It means "Select... From... Where"

If there is no ambiguity, we do not need ALIAS.
UNION keeps duplicates.

![[Pasted image 20250107110601.png]]

## From SQL to Algebra

In SQL, tables may contain duplicates, so we need to extend sets {T} to multisets {{T}}, also called bags, to keep duplicates.
In other words, In SQL the tables of a database may be without keys and so they are not sets ( {T} )  but multisets (bags) ( {{T}} ).

New operators
1. multiset -> represented as $\pi^b$.
2. inverse ->  $\delta(R)$ that is duplicate elimination 
3. sort -> the result is a list $\tau$

Other operators simply add the b to exp to convert to multisets
1. multiset union
2. multiset intersection
3. multiset difference

![[Pasted image 20250107111332.png]]

*How to map sql queries into relational algebra?*

![[Pasted image 20250107111437.png]]

The way to read an SQL is this
![[Pasted image 20250107111642.png]]

*COUNT bug of SQL*: without GROUP BY vs GROUP BY ()
What is the difference if R is empty?
(if R is non-empty, it is the same)
![[Pasted image 20250107112030.png]]

In the query on the right.
If we GROUP BY(), meaning the GROUP BY for an empty set, and then COUNT(\*).
In GROUP BY, we should have one row for each grouping attribute, but since there are no attributes, we will get an empty relation.

In the query on the left.
If we COUNT(\*) an empty relation, we will get zero.

*WITH Clause (subquery factoring)*
To simplify complex queries, use temporary views/tables.

![[Pasted image 20250107112445.png]]

Some calculations, can be only done with views and not with simple queries.
A single query cannot have to groupings (aggregates) one on top of the other. See the mapping above.

## -> exercise with FD on MonthYear
Exercise:
Write a SQL query that returns all constant  customers. Constant means with at least two orders per month for at least three months in the last four months.

![[Pasted image 20250107113030.png]]

Assume there is a functional dependency (FD) `Month -> Year`
We need to transform the Month into contiguous values for all years, so that we do not care about the year.

![[Pasted image 20250107114637.png]]

What if the FD do not hold?
We need to add also the Year in the GROUP BY.

![[Pasted image 20250107114759.png]]

*Nested Queries*

Example:
Student code and name who passed at least one exam with grade 'A'.

![[Pasted image 20250107115027.png]]

*NULLs*
Missing or unknown values of attributes are modelled with the NULL value.

Is NULL > 20? The result is UNKNOWN.
Look at the truth table for 3-value logic.

![[Pasted image 20250107115320.png]]

There is a class of joins that generates NULLs.
It is the LEFT OUTER JOIN.

![[Pasted image 20250107115545.png]]


*CASE*
![[Pasted image 20250107115751.png]]

  **EXAM EXAMPLE**
  ![[Pasted image 20250107120127.png]]

The type of the result is a relation with integers and the value of the result is simply the table with the result.

![[Pasted image 20250107120340.png]]

**EXERCISE AT HOME**

![[Pasted image 20250107120447.png]]

In JRS, Options > Show Logical Plan.

See next lesson for the solution.



# dsd15 - Analytic SQL (1)
OLAP systems. Data Analysis Using SQL. Simple reports. Examples. Moderately Difficult Reports. Solutions in SQL.

> Maybe read https://en.wikipedia.org/wiki/Data_warehouse

OLAP refers to the technique of performing complex business  multidimensional analysis over the data warehouse.
> We will see how report developers use SQL to write queries!

Start of lectures on "Relational DBMS Extensions for DW".
The topics of the lectures from 15 to 23 are

15-17 -> SQL extensions (aka T-SQL)
18 -> Query Plans
19 -> Index and Storage Structures + Star Query Physical Plan
20 -> Materialized Views
21 -> (functional dependencies and their usage in query optimization)
22 -> Optimization techniques for star queries with grouping and aggregations
23 -> Query rewriting to use materialized views

## -> JRS exercise

**EXERCISE AT HOME**

![[Pasted image 20250107120447.png]]

In JRS, Options > Show Logical Plan.

Query 1.
Number of distinct customers by product.
```SQL
SELECT FkProduct, COUNT(DISTINCT(FkCustomer)) AS NCustomers
FROM Invoices, InvoiceLines
WHERE FkInvoiceNo=PkInvoiceNo
GROUP BY FkProduct;
```

Query 2.
Largest invoice revenue by product.
(for every product,  we want to know the total revenue of the invoice containing that product with the highest)

```SQL
WITH TotalByInvoice AS
	(SELECT FkInvoiceNo AS Invoice, SUM(FkProduct * Qty) AS TotalInvoice
	FROM InvoiceLines
	GROUP BY FkInvoiceNo)

SELECT FkProduct, MAX(TotalInvoice)
FROM InvoiceLines, TotalByInvoice
WHERE FkInvoiceNo=Invoice
GROUP BY FkProduct;
```

Query 3.
The percentage of revenue generated by the product over the total revenue of the customer by Customer and Product.

```SQL
WITH
a AS
	(
	SELECT FkCustomer, FkProduct, SUM(Price* Qty) AS Revenue
	FROM InvoiceLines, Invoices
	WHERE FkInvoiceNo=PkInvoiceNo
	GROUP BY FkCustomer, FkProduct
	),
b AS
	(
	SELECT FkCustomer, SUM(Price* Qty) AS Revenue
	FROM InvoiceLines, Invoices
	WHERE FkInvoiceNo=PkInvoiceNo
	GROUP BY FkCustomer
	)

SELECT a.FkCustomer, FkProduct,
	100*a.Revenue / b.Revenue AS pct
FROM a,b
WHERE a.FkCustomer=b.FkCustomer;
```

This is a very complicated version of the query that can be simplified using the extended SQL that we see today.

## Reporting Solutions
UP TO NOW 
Data Warehouse: Data Models and DW Design and Implementation.

STARTING TODAY 
Data Analysis Using SQL.  How to summarize data using SQL?  What if the query takes a long time to produce the answer?


A DW is all about getting answers to business questions, in the form of reports. Reports must communicate pertinent information clearly and concisely.

**First Solution. Visual Reporting Tools** (no sql required)
1. Excel Pivot tables
2. PowerPivot
3. Microstrategy
4. QlinkView
5. ...

**Second solution. OLAP.**
Refers to the technique of performing complex business analysis over the interaction ..

Many types
1.  DOLAP
	1. The OLAP Client may connect to a server with multidimensional
	2. It builds a local representation (Desktop OLAP or DOLAP), which is feasible only for small data, typically single users.
2. RDBMS
	1. The software queries the data using SQL
	2. Cuboids may be already available, if not, there is a sql query to RDBMS
	3. If cuboids exists
		1. MOLAP, using MDX
		2. do not scale with very big because the cube would be too large
	4. if cuboids do not exiists
		1. ROLAP, using SQL
		2. there are ways to speed up calculations, precomputing some cuboids that are stored in the relational db (called materialized views)
	5. hybrid solution
		1. HOLAP

**Third Solution.** 
Like Microstrategy.
We write manually SQL Queries on the relational db.

## ROLLUP and CUBE
Simple Reports with SQL

![[Pasted image 20250107162232.png]]

How to add subtotals and the grand total?

![[Pasted image 20250107163750.png]]

To avoid long UNION ALL, we use an extension of SQL called ROLLUP.
The ROLLUP calculates the subtotal by removing each time the rightmost attribute.
In general, if we have n attributes, it will generate n+1 subtotals.

![[Pasted image 20250107172103.png]]

How to produce the same report using ROLLUP?
![[Pasted image 20250107172152.png]]

*Cross-tabulation*
It cannot be achieved with ROLLUP.
It extends the ROLLUP.
The keyword is CUBE.

![[Pasted image 20250107172336.png]]

![[Pasted image 20250107172400.png]]

Here the order is not important, while it was important for the ROLLUP (?).

*Partial Rollup and Cube*
Rollup and Cube can be mixed to compute only some groupings.

![[Pasted image 20250107172724.png]]
![[Pasted image 20250107172736.png]]

## -> Exercises with Foodmart
> Download "Azure Data Studio"
> Use the VPN
> Add connection
> Use SQL login
> Right-click on foodmart -> new query

Let's build a standard report.

![[Pasted image 20250107173330.png]]

Adding CUBE

![[Pasted image 20250107173541.png]]

Note that, unlike standard SQL, we do not need NULL to compute totals.

Adding CASE, with a trick to obtain the grand total.

![[Pasted image 20250107173931.png]]

Typically the order is done by the tool, do not be too worried.

![[Pasted image 20250107174055.png]]

*What if NULL is present in the data?*
How to distinguish the actual NULLs from those introduced by the ROLLUP?

Remember that with a trick in the DW design, there will not be any nulls.
There will be for instance a fictional customer called UNKNOWN with UNKNOWN values in the attributes. So there will be a foreign key pointing to that row.

We use GROUPING.

![[Pasted image 20250107174638.png]]



# dsd16 - Analytic SQL (2)

## OVER
Moderately Difficult Reports
With comparison across aggregation levels.

![[Pasted image 20250108101431.png]]

In standard sql, it would require different unions.
Complex and inefficient. That's why we introduce:

*OVER* clause.

The granularity do not change, we keep the one of the original data, there's no group by.
We can think of OVER as a group by that do not change the aggregation, but only replicates the result of the group by over the rows.

The PARTITION BY can also be absent. Meaning OVER()

![[Pasted image 20250108103622.png]]

Notice that first we compute the table with the grouping and then we use the OVER. 
This will be important also later. First GROUP BY then aggregate.

![[Pasted image 20250108103745.png]]
![[Pasted image 20250108103827.png]]

What is the position of OVER in the order of a query?
The analytic functions are after HAVING.

![[Pasted image 20250108103913.png]]

And with comparison across aggregation levels?

![[Pasted image 20250108103954.png]]

Now that we are more confident, we can mix GROUP BY and OVER in the same query, instead of using a temp view. Always read GROUP BY first and OVER later.

## RANK
*Very difficult reports*

First without analytic sql.

![[Pasted image 20250108104316.png]]

*RANK*
Without partitions

Without specification, the ORDER BY is ascending.

In the logical plan
1. first we do the group by
2. then OVER, global because no partition
3. then ORDER BY, that is not connected to the analytical part

![[Pasted image 20250108104633.png]]

RANK with partitions.

![[Pasted image 20250108105142.png]]

*rows partitions*
We could require for instance.
- TOP5%
- NEXT15%
- MIDDLE30%
- BOTTOM50%

We need a variant of ranking with the relative position.
These variations are

RANK produce holes because the definition is:
1+ the number of values that strictly precedes it.
This can create ties.
We introduce DENSE_RANK() and others.

![[Pasted image 20250108105719.png]]

We can use ROW_NUMBER() to obtain for instance the first 5 rows.

With the OVER clause, we can use the standard aggregates like COUNT, SUM, AVG, MIN, MAX,..

![[Pasted image 20250108110103.png]]

## -> Exercise at home 16.1

![[Pasted image 20250108110126.png]]

The additional requirement is the subtotal.
Mix the analytic functions to produce the percentage with the ROLLUP to produce subtotals.

> my solution

```sql
SELECT Brand, Product, SUM(Revenue) AS prodRevenue,
	100*RATIO_TO_REPORT(SUM(Revenue))
		OVER(PARTITION BY Brand) AS PctOverBrand,
	100*RATIO_TO_REPORT(SUM(Revenue))
		OVER() AS PctOverTot
FROM sales
GROUP BY Brand, Product, ROLLUP(Brand, Product)
```



## LAG and LEAD
Other analytical functions



![[Pasted image 20250108112405.png]]

Use these functions to create VARIANCE REPORTS.

![[Pasted image 20250108112627.png]]

We need a full outer join!
There are 3 alternatives (same result).
Use the second.

![[Pasted image 20250108112954.png]]

![[Pasted image 20250108113027.png]]

## -> Exercise at home 16.2
Try at home without any join, using LAG and LEAD.

> my solution

```sql
SELECT LEAD(Revenue08, 1, 0) - Revenue08 / Revenue08 AS Delta
FROM sales
ORDER BY Brand, Product

```




## Demo with Foodmart

![[Pasted image 20250108113350.png]]

In the beginning use subqueries, then, when you are confident, use a single query.
In the following, notice that TotalSales is not yet available to be used and we need to use SUM(...)

![[Pasted image 20250108113542.png]]

Using RANK

![[Pasted image 20250108113804.png]]

Using ORDER BY Rk, we would get the order based on RANK

Can we use RkCountry < 5? No, because it is not yet defined, the where is evaluate before. We need to use a subquery where we define it.

![[Pasted image 20250108114150.png]]

Typically you see reports order by country and city, but remember that the calculation of delta with LEAD is ordered by RANK.

# dsd17- Analytic SQL (3)

## -> Solution of exercise at home 16.1

![[Pasted image 20250108121612.png]]

We will do it on FoodMart considering Country and City.

Be careful, if you use ROLLUP, you will sum also the ROLLUP rows for the GrandTotal. Doubling the result.
How to avoid it? Use GROUPING.

## -> Solution 16.2

![[Pasted image 20250108113027.png]]

Try at home without any join, using LAG and LEAD.

With LAG we get the previous year, with 0 if not present (we change it to null).
WITH LEAD we can access the next year.

> START SIMPLE then complicate.
> Start with views then build a unique query.


## ROWS or RANGE
Running Totals (Windowing)

![[Pasted image 20250108180841.png]]


![[Pasted image 20250108180934.png]]

![[Pasted image 20250108181158.png]]

Another example.

![[Pasted image 20250108181223.png]]

Moving averages are good at spotting trends.

![[Pasted image 20250108181255.png]]

## -> Example 17.2
See Azure.


## -> Exercises on SQL Extension

![[Pasted image 20250108183918.png]]
![[Pasted image 20250108183933.png]]

Here's the text.

1. number of customers who spent more than 50% of their total in the store by store

2. number of customers who spent the largest amount of their total in the store by store

3. number of customers with total sales in the store lower or equal than 100 by store

4. number of customers with at least one day with total sales in the store greater or equal than 100 by store

5. number of customers with no day with total sales in the store greater or equal than 100 (but with at least one sale in the store) by store

6. all triples customer_id, the_year, month_of_the_year in which the customer bought something in that month but nothing in the next month.

7. the ratio of total sales to a customer in a year-month over the total sales to the customer in that year, by customer and year-month

8. the top spending day of week, by customer

9. the 10 top spending customers and the ratio of their spending over the total sales of the store, by store_id

10. add to the previous query also the running total of the top k customers, for k=1, …, 10

11. add to the previous query also the delta between customer k and k+1, for k=1,…,9










# dsd18 - Query Plans

## Basics of Query Processing

A DW designer must understand the principles.

Depending on the actual storage, the implementation on the physical level may be different.

We enter the black box of the DBMS.
![[Pasted image 20250109111827.png]]

Physical query plan contains physical operators, meaning actual forms that allows to speed up queries.
Alternative implementations exists for each relational operator.

Let's introduce the storage structures.

*Heap File*
A table is stored in a Heap File.
This format is typically used in operational db.
A file for each table, with tuples stored in the insertion order.
A record is identified with a Record Identifier (RID), it identifies the disk address of the page containing the record (it is used by the machine, but unknown by the user).

*Indexes*
We can use indexes based on different attributes.

![[Pasted image 20250109112441.png]]

What is the advantage?
Since the index is ordered, we can use a binary search that in logaritmic time can find the desired position.
The index is much smaller than the table, meaning faster access.
Typically they are stored as B-trees.

In sql, there is a CREATE INDEX command.
If the index is on keys, we add the UNIQUE keyword, it means that we cannot add a duplicate values.

![[Pasted image 20250109112730.png]]

*Query execution steps*

![[Pasted image 20250109112947.png]]

The query optimizer choose the implementations to use faster operators in the access plan.

TableScan is materializing, it means computing the full result. But this is not very efficient. We do pipelining, where as soon as a row is executed by an operator, it will be passed to the next one (allow also parallelizing).

![[Pasted image 20250109113550.png]]

*Example of query execution*

![[Pasted image 20250109113611.png]]

## implementations of  relational operations

we will see
1. Projection
2. Selection
3. Group By
4. Join

Operators for R
1. TableScan(R)
2. SortScan
Also
1. Sort

## 1. implementation of projection

Operators for projection
1. Project 
	1. no duplicate elimination
2. Distinct
	1. to eliminate duplicated from sorted records
3. HashDistint
	1. to eliminate duplicated from records
	2. it requires memory to store a hash data structure

## 2. implementation for selection

Operators for restriction
1. Filter
2. IndexFilter
	1. specialized option where is required an index
	2. composed by
		1. RIDIndexFilter, which returns the RID to be read
		2. TableAccess, using the RID obtained in the previous step

Let's see an example of index filter.
Assuming the index already exists.
If the condition is not very selective, it is actually better to use TableScan. The query optimizer will decide.

![[Pasted image 20250109141114.png]]

## 3. impementation of join

More efficient algorithms.

*First. Nested Loop.*
Scan the first table and look in the right looking for all the matching rows.

![[Pasted image 20250109141817.png]]

*Index Nested Loop*
We ask the index to find in logarithmic time the matching rows.
From quadratic complexity to N x logM complexity, where M is the number of rows in S.

It means that for every table scan, you call an IndexFilter.

Exception.
We might also have an additional filter not indexed by the index.

## 4. Implementation of GroupBy
It requires the input already sorted.

![[Pasted image 20250113213814.png]]

![[Pasted image 20250113213847.png]]

There is also a HashGroupBy.


## JRS examples of physical plan

In physical plan panle we can build the physical plan.

In different DBMS,
1. ORACLE
	1. use `explain plan`
2. SQL SERVER
	1. use `estimated execution plan`
	2. or ``
3. Azure
	1. show `Query Plan`

We only need the operators in the book and in JRS.



# dsd19 - Indexes and Partitioning

Remember the lectures on "Relational DBMS Extensions for DW".
The topics of the lectures from 15 to 23 are

15-17 -> SQL extensions (aka T-SQL)
18 -> Query Plans
19 -> Index and Storage Structures + Star Query Physical Plan
20 -> Materialized Views
21 -> (functional dependencies and their usage in query optimization)
22 -> Optimization techniques for star queries with grouping and aggregations
23 -> Query rewriting to use materialized views

Today
![[Pasted image 20250113214139.png|300]]




## Indexes

We assume "Non-volatile data" compared to operational db.
We will see the following index structures for DW:
1. inverted indexes
2. bitmap indexes
3. join 
4. foreign column join (FC join)

## 1. inverted index
for selective attributes (aka high cardinality)

It is the solution in all relational DBMS.
It is useful when the number of distinct values of an indexed attribute is high (called selective attribute).
It the standard solution for primary key in DWMS.

The index allow to map each value to its position.
It is ordered to allow binary search.

![[Pasted image 20250127165905.png]]

During ETL, indexes are dropped and rebuilt from scratch.
The updates are processed in batch.
It is more efficient then updating indexes for each new row as in operational db.

The values in the inverted index are unique. A binary search can be performed.
It is the std solution in dw. Specifically with a high number of different values.
In particular for the primary key.
The rows might have different colums.

## 2. bitmap Index
for non-selective attributes (aka non-selective attributes)

Each value in the indexed attribute is associated to a bit vector (bitmaps).
The length of the bitmap is the number of records in the base table.
The i-th bit is set if the i-th record of the base table has the value for the indexed attribute.
It is used in all DBMS for DW when the number of distinct values of an indexed attribute is small (non-selective attribute).

For non-selective attributes, an inverted-index would be useless.

Efficient bit operations to answer some queries with AND, OR.

In other words.
For each value, we assign a bitmap with 0 and 1, with one position for every read.
The advantage is that every bitmap has the same size.
It is more useful if we need to do comparisons like AND or OR. For example students from Pisa and born in 1972, we compare the two bitmap indexes with AND.
It is created with `CREATE BITMAP INDEX ...`

The utility is complementary to inverted index.
Typically the bitmap is sparse and can be compressed.

![[Pasted image 20250114115106.png]]

The Bitmap indexe is composed by
1. BMIndexFilter + BMIndexFilter
2. BMAnd
3. BMToRid
4. (TableAccess...)

Example of access plan.
![[Pasted image 20250114115629.png]]


Special case with count.
We might not need to access the table with BMIToRid.
For counting, the index might be enough.

![[Pasted image 20250114115645.png]]

Example of star schema with Inverted Index and BMIndex.
![[Pasted image 20250114115945.png]]
![[Pasted image 20250114115955.png]]
![[Pasted image 20250114120005.png]]





## 3. join index
Also (star) join index.

How to speed up the join?
A join index is a pre-computed join that is stored in a compact form.

![[Pasted image 20250113220246.png]]

The index relates a row in a dimension to a row in the fact table.
Not used in operational DB due to high cost of updates.
It is used to optimizes frequent queries.

Types
1. basic join index
	1. join index we keep the mapping between the RID in the dimension and the RID in the fact.
2. bitmapped join index (BMJ)
	1. ..
3. Foreign Column Join Index (FCJ)
	1. we keep the mapping between the values of an attribute and the RID in the fact.
4. Bitmapped Foreign Column Join Indexes (BMFCJ)
	1. we map the value in the dimension and the bitmap for the fact

An example of JoinIndex and BMJIndex.
![[Pasted image 20250114121007.png]]
![[Pasted image 20250114121548.png]]

An example of FCJ Index.
![[Pasted image 20250114121622.png]]

An example of BMFCJ Index.
In the bottom part, we exploit the indexes without accessing the tables.
Then from bitmap we move to RID (with BMToRid).
![[Pasted image 20250114121646.png]]
![[Pasted image 20250114121658.png]]



## Star query plans

Star queries are the most common kind of queries in data warehousing, OLAP and business intelligence applications.
Optimizers for data warehouse systems generate particular physical plans for star queries, with a structure different from that generated by conventional relational systems.

The major bottleneck in evaluating star queries is the join of the fact table, usually very large, with the dimensional tables.
A star join index (on a star schema) is a multi-attribute join index between the dimension tables and the fact table.

![[Pasted image 20250109160948.png]]
![[Pasted image 20250109161004.png]]


*more*
How do I know if the DBMS allows this indexes?
1. read documentation
2. test a join and  see the query plan

How does the access plan change if we know the dw is a star join?
1. ...

The optimizer will as much as possible to
1. exploit indexes (this lesson)
2. anticipate the grouping before the join (next lesson)

## Storage structure

## 1. Heap File

See HeapFile.

## 2. PARTITION

Until now, we assumed the heap file.
A full scan of the table is always required.
We can use a horizontal partition of tables into multiple files.
For example, we can store different tables one for each country. Meaning many different files.
Use PARTITION.

Partition can be based on 
1. specific values
2. range (for example dates)

![[Pasted image 20250109161128.png]]

How does the access plan change?
We can use `PartitionedTableScan`.

![[Pasted image 20250109161201.png]]
![[Pasted image 20250109161212.png]]



This is very useful if this types of queries are frequent.

![[Pasted image 20250109160110.png|300]]

There are several ways to split into files, depending also on DBMS.




# dsd20 - Materialized Views

![[Pasted image 20250109174709.png]]

It helps with the maintenance.
But there is not an advantage in terms of access plan (?).

Materialized views are stored on disk.
The advantage is that the content of the view is already available, meaning that the access plan will be shorter and faster.

What are the most convenient views to be materialized? We need to choose based on workload and statistics of usage.

Problems.
1. how to select the views to be materialized?
	1. given a query workload Q (type and frequency of queries)
	2. see it now
2. how the system rewrites a query to use materialized view?
	1. see future lesson
3. how to update materialized views if the database is update?
	1. typically drop and rebuild

## Lattice of Views to materialize

![[Pasted image 20250114151658.png]]

This selection algo might run every night, changing the selected views every time.

THe possible views are queries considering a subset.
Mapping the lattice of subset into the lattice of views.

The candidate views v are the possible DW lattice nodes, different from root F.
Let g(v)=X be the grouping attributes in the view for the cuboid v.

![[Pasted image 20250109175832.png]]

We estimate the size of the view.

![[Pasted image 20250109175947.png]]


![[Pasted image 20250109180053.png]]

Sometimes, candidate views are not worth to be materialized. If the size is more or less the same of the full table, it makes no sense and we can store rows in storage.

![[Pasted image 20250114151928.png]]



## Assumptions

The candidate views v are the possible DW lattice notes.

![[Pasted image 20250109180409.png]]

![[Pasted image 20250109180550.png]]


## Benefit of a view

![[Pasted image 20250114152054.png]]
![[Pasted image 20250114152109.png]]
![[Pasted image 20250114152119.png]]

Example.
![[Pasted image 20250114152141.png]]


We would like to choose the materialized view 

The optimizaton problem is NP-complete.
There exisists a greedy algorithm.



Keep in mind the formula of the benefit.
![[Pasted image 20250109183016.png]]
The benefit of a current view v when M is materialized is given by considering the benefit of every subquery q of v in which we compute the maximum between the cost of currently rewriting the subquery q using m and instead the cost of using v.

## HRU algorithm

Now
1. start with all the possible elements in the lattice
2. compute the benefits for each of the queries in the sublattice
3. compare with the best already materialized view
	1. at the beginning is the full table

The first choice is to materialize PD.
Now we compute again the benefits.
Be careful to compare only with ancestors, for example PS cannot be compared with PD but should be compared with PSD.

See the exercise.
Typically $u_q$ is the ancestor with the lowest cost.

In the second choice, we add S to the set M,
that now is {M=PSD,PD,S}.
And repeat for the third choice. 

Let's summarize the algo.

![[Pasted image 20250114152318.png]]

M is the set of materialized views.
N is the set of candidate views.


HRU is an heuristic.
In general it does not find the best subset.

In general, the greedy algorithm not perform 0.63 times worst than the best algorithm.

HRU has a time complexity O(km^2)
where k is the number of views selected
and m is the number of lattice views.

We can also use a polynomial greedy algorithm with a more limited number of views.

![[Pasted image 20250114152339.png]]
![[Pasted image 20250114152436.png]]

## Other algorithms

![[Pasted image 20250114152449.png]]
![[Pasted image 20250114152502.png]]





## algo with dimensional attributes
Until now, we considered flat dimensions.
By exploiting functional dependencies, we can run the HRU on a simpler lattice, without compromising the result.

![[Pasted image 20250109190251.png]]

*more complex queries*
![[Pasted image 20250114152538.png]]

*techniques*
They can be statics or dynamics.

![[Pasted image 20250109190548.png]]

## -> exercise at home on HRU

![[Pasted image 20250109190627.png]]

apply the algo with the variable x, which we do not know.







# dsd21 - Functional Dependencies

## -> exercise on materialized views

> from 0:00 to 17:00


## Functional Dependencies

We consider now optimization techniques for star queries with grouping and aggregations.
But today we recall notions of functional dependencies.

Assumptions
1. no null values
2. primary keys (no duplicates)
	1. no multisets problems
3. simple queries with no analytical functions

![[Pasted image 20250110111839.png]]

![[Pasted image 20250110111939.png]]

![[Pasted image 20250110112339.png]]

We can extend now the definition of schema.

![[Pasted image 20250110112422.png]]

We could add the notion of hierarchies in the logical design, but actually only the FD of keys is used.

*Inference Rules*

![[Pasted image 20250110113729.png]]
The UNION can be derived using the axioms.
![[Pasted image 20250110113903.png]]

Instead of Armstrong axioms, we will actually use something else.

![[Pasted image 20250110114319.png]]

The closure of X is the set of attributes that is implied by X.

![[Pasted image 20250110121305.png]]

*slow closure*

..


## -> exercise at home

![[Pasted image 20250110121803.png]]

You can think of functional dependencies as generalizations of hierarchies.

...







![[Pasted image 20250110122737.png]]

The FD hols in the output.
This algorithm works directly in sql.





# dsd22 - Optimization with Grouping and Aggregation

Today we consider how to anticipate the groupby before the join.
Since the join is very expensive, reducing the number of rows with grouping can be very efficient.

Basically we want to do *query rewriting optimization* exploiting grouping.
In the next lesson, we will exploit the materialized views.

## FDs and Groupings

![[Pasted image 20250114180733.png]]

If you consider the FD, the granularity do not change.
Under which cases can we do the grouping before the join?

## Query Rewriting Optimization
 ![[Pasted image 20250114180348.png]]



## Anticipating HAVING
Simple query rewriting.

![[Pasted image 20250110165131.png]]

First option is to use the where.
Not very general, because typically the condition of the having depends on the aggregation function.
In this second option, we have two cases.

![[Pasted image 20250110165309.png]]

If there is an order with at least 10 qty...
It's very specific.

## The pre-grouping problem
Consider the star schema.
Under which condition can we rewrite the query so that the join is after the condition.

![[Pasted image 20250114180827.png]]


## 1. invariant grouping

![[Pasted image 20250114181038.png]]
![[Pasted image 20250114181021.png]]

When does it work?
When R has the invariant grouping property.

![[Pasted image 20250110170015.png]]

Grouping by X or by f produce the same granularity.

If the forign key is not in the grouping it would not be possible (?).

![[Pasted image 20250110171124.png]]

ask two questions
...

Remember that we assume that all the aggregation functions are from the left.
Then we will add the columns we need from the join coming from right.



![[Pasted image 20250110171613.png]]

We can demonstrate the invariant grouping using the closures because AName is a key (it is underlined).

![[Pasted image 20250114181115.png]]

## 2. double grouping
aka early partial aggregation

If the invariant grouping is possible, it is the best option. However, if it is not possible because the granularity changes, we can still apply the double grouping rule if the aggregation function is decomposable.
If the function is decomposable, we can anticipate one part of the grouping before the join.

![[Pasted image 20250114181141.png]]

![[Pasted image 20250114181202.png]]

We have to check that
1. the function is decomposable
	1. because we need to aggregate differently in the fact table and after the join
2. the attributes for the aggregation function must be from the fact table R

![[Pasted image 20250114181238.png]]

![[Pasted image 20250114181250.png]]

![[Pasted image 20250114181302.png]]

![[Pasted image 20250114181314.png]]

## 3. grouping and counting

There is a third case.
If the two conditions of invariant and the two conditions of decomposition are not true.
Not general, but requires some condition.

It is called "the grouping and counting rule".


![[Pasted image 20250114181325.png]]

![[Pasted image 20250114181339.png]]




![[Pasted image 20250114181353.png]]


## exercise

![[Pasted image 20250114181415.png]]

See kindle.









# dsd23 - Query Rewriting to use materialized views

How to rewrite the query using materialized views if possible.

This is known as the "query rewriting problem".
It is not a problem of the user who writes queries, but rather for the query optimizer.

Who write a query is NOT aware that exist materialized views.

Star Schema Assumptions.
![[Pasted image 20250116171003.png]]

Lossless means that being a fk every fact join one row in the dimension table.
Non-duplicating means that every fact match exactly one row and no more.

Query rewriting is complex.
In the docs of DBMS you will find recommendations to use materialized views. They should be simple in structure to be used by systems to rewrite queries.


We will see 2 approaches.
1. try and built on top of an existing view some compensations to produce the query logical plan
	1. we can call directly the materialized view
2. we start from the query trying to move the operators in a way 
	1. the logical plan of the query will have a bottom part equivalent to the view logical plan

Approach 1.
More algoriothmically, with well-established steps.
![[Pasted image 20250110184122.png]]

Approach 2.
More about intuition.
![[Pasted image 20250110184200.png]]

## Simple cases
What?
1. g(Q) -> g(V)
	1. the query has a finer granularity than the view
	2. ?
2. g(Q) -> g(V) and g(V) -> g(Q)
	1. the query has the same granularity of the view
	2. the 
3. g(V) -> g(Q)
	1. A,B->A
	2. the view has more groups than the query
	3. still rewritable


Recall that "determines" means that the attribute on the left produce finer granularity.

The grouping by A,B and by B only are exactly the same.
g(Q) means the grouping attribute in the query and
g(V) means the grouping attribute in the View.

The groups in the view produce finer granularity.

## approach 1

Compare the query and the view.
Start bottom-up and do an operator match.
If there's a partial match, we need to do a compensation.

1. matching
	1. exact or partial
2. compensation
	1. float or not

A compensation is a tree floating on top of the view to match.
Can the compensation float on top of the view?
If the compensation cannot float, then the query is not rewritable.


![[Pasted image 20250114233551.png]]
![[Pasted image 20250114233604.png]]

The optimizer should do this analysis for each materialized view and decide which to optimize.

Example.
1. start from the logical plan

Let' check the join, there is a partial match. We need a partial compensation. Does this compensation float? If we move it on top of the view, will it work? Yes.

Now the restriction, the partial match is simply adding the restriction on top of the compensation.
If there is no possibility to restrict the view to get the query condition, we simply stop the rewriting. For this reason, we should not use restrictions because they limit the usability of the view.

Now cosider the matching between the groupings.
Even if there is an exact match, we need to project over different projects because after the join we get attributes that are not required in the query.

The optimizer would rewrite the query using the materialized view.

![[Pasted image 20250114233622.png]]

We assume obviously that the relations in the view are included in the relations of the query.

*Rewriting algorithm.*
1. JOIN
	1. If the joins do not match, a compensation is added to the view
	2. on top of the join of the view we also add the join at the root of the compensation tree
	3. the compensation can float if g(V) contains the foreign keys for the tables  W, otherwise Q is not rewritable 
2. RESTRICTION
	1. if the selection do not match, but it is possible
	2. we add it on top of the compensation tree
	3. CONDITION: in order to float, the restriction attribute must be available in the grouping or after the join (using the fk in the groupings?)
		1. otherwise, Q is not rewritable
3. GROUPING
	1. comparing the grouping of the view and the one of the query
	2. in the lecture notes there are other example
	3. we distinguish
		1. case WITHOUT grouping
			1. the rewriting is without groping when the groupings in Q and V partition data into the same number of groups
			2. meaning that the granularity is the same  g(Q)->g(V) and g(V)->g(Q)
			3. what we need is just a projection and the aggregation function if any, because the grouping is already computed
		2. case WITH grouping
			1. if query and view have different granularity
			2. but the granularity of the view must still be larger, meaning g(V)->g(Q)
			3. otherwise the query is not rewritable
			4. we add another grouping and aggregate functions appropriatly


![[Pasted image 20250114233644.png]]

![[Pasted image 20250114233658.png]]


![[Pasted image 20250114233718.png]]

![[Pasted image 20250114233737.png]]
![[Pasted image 20250114233751.png]]

![[Pasted image 20250114233816.png]]
![[Pasted image 20250114233829.png]]



In general, if the view is more restrictive than the query we cannot generate the missing data. And this is also a reason why in materialized views we should not have restrictions.
The would limit the usability.

On top of the materialized view, we add the compesation. The optimizer will rewrite the query into a new one using the materialized query.


$A_v$ is the root of the compensation tree.

![[Pasted image 20250111174413.png]]

Formally, we should show that FDs are satisfied.
In the example above, we need to show that Market,Year->MCity, because we need to group (case WITH grouping). Since Market->MCity, the grouping is fine and the query can be rewritten.
However, we still need to add the attribute MCity joining the table and obtaining the MCity. 
Observe that here the join is needed for retrieving the attribute and not at a lower level as usual in the algorithm.

*examples*

![[Pasted image 20250116191020.png]]

1. the rewriting will not be possible because the restriction in the view is too restrictive
2. in the view, the group by empty set means that we should check if Market->0 that is trivial and 0->Market that is true only if Market is constant. We cannot rewrite because the granularity in the query is larger than the one in the view.
3. same (no rewriting)

Let's try to rewrite this query with the first approch and then with the second.
![[Pasted image 20250116191549.png]]

Observe that we need the case WITH grouping because it is not true that Product->Product,Market but it is true that Product,Market->Product.


## approach 2

How can we start from the plan of the query and pushing down operators find the plan for the view.
The idea is to transform the plan of the query to recognize at some point the plan of the view.

Transform the plan of the query finding an equivalent to the view logical plan.



![[Pasted image 20250114233854.png]]
![[Pasted image 20250111175843.png]]

The idea is to push down operators and try to find the plan for the view.
The other approch is more algorithmically, trying to find steps for compensation and floating. It can be implemented more clearly.



# dsd24 - 

....





