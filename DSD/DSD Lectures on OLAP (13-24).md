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

## Simple Reports with SQL

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

## Exercises with Foodmart
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

## Moderately Difficult Reports
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

## Very difficult reports

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



## Other analytical functions

*LAG* and *LEAD*

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








# dsd18 - Query Plans







# dsd19 - DW Indexes

Start of lectures on "Relational DBMS Extensions for DW".
The topics of the lectures from 19 to 23 are
![[Pasted image 20241224104640.png]]

19 -> Index and Storage Structures + Star Query Physical Plan
20 -> Materialized Views
21 -> (functional dependencies and their usage in query optimization)
22 -> Optimization techniques for star queries with grouping and aggregations
23 -> Query rewriting to use materialized views


# dsd20




# dsd21


# dsd22


# dsd23


# dsd24


