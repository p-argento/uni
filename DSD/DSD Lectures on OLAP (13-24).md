
# dsd13
Multidimensional Cube model: OLAP Operations. The extended cube and the lattice of cuboids. Pivot tables in Excel.

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

# dsd14
Recalls on: DBMS, from SQL to extended relational algebra.

DB is a collection of persistent data:
1. schema (or meta-data)
	1. time-invariant
	2. abstract knowledge
2. data
	1. concrete knowledge
DBMS
1. is a centralized or distributed software system
2. functions
	1. DDL (Data Description Language)
	2. DML (Data Manipulation Language)
	3. DQL (Data Query Language)
	4. DBA (Database Administrator)
3. different levels
	1. logical view
		1. `CREATE VIEW ...`
	2. logical level
		1. `CREATE TABLE ...`
	3. physical level
		1. indexes and other data structures

Let's start from DBA.
There is a catalog
![[Pasted image 20241223111506.png]]













# dsd15
OLAP systems. Data Analysis Using SQL. Simple reports. Examples. Moderately Difficult Reports. Solutions in SQL.

> Maybe read https://en.wikipedia.org/wiki/Slowly_changing_dimension and https://en.wikipedia.org/wiki/Data_warehouse





# dsd 19

Start of lectures on "Relational DBMS Extensions for DW".
The topics of the lectures from 19 to 23 are
![[Pasted image 20241224104640.png]]

19 -> 




