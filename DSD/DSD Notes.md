# dsd02

*Table of Contents*
1. What is a Data Warehouse
2. What do we model in a DW
3. Recall of Relational Algebra and SQL

## 1. Definition of Data Warehouse

One *definition* is
"A DW is a decision support database with historical, nonvolatile data, pulled together primarily from operational business systems, structured and tuned  to facilitate analysis of the performance of key business processes, worthy of improvement."

There are two definitions
1. by William Inmon (1990)
2. by Ralph Kimball
It will be discussed in a future lesson.

A DW is a *specialized database*.
But why do we need a specialized database and not a classic database?
It is still a data structure to store and query data, but specialized because it is intended to support a  structured decision making and therefore there are some differences:
1. static (not volatile)
2. with integrated data from different sources
3. organized to analyzed subjects of interest
4. historical data
	1. not transactions, 
	2. we typically scan a large amount of data
5. used to produce summarized data to support decision-making process

These optimization cannot be applied on a transactional database, because we will not be able to exploit the speed for example. Different machines will be used, where we store historical data. There is no need to store data in transactional database.

Data Warehousing (with -ing) is the process of building a data warehouse. It starts from taking the data from operational sources. For example, each night taking the data from the operational database (also called OLTP) to populate the data warehouse (also called OLAP).

Distinguish
1. OLTP -> On Line Transaction Processing
2. OLAP -> On Line Analytical Processing

How can we support DW.
There are *software architecture*.

![[Pasted image 20240919113451.png]]

In the frontend, different type of analysis can be done by the user on the OLAP, for example
1. multidimensional analysis
2. data mining
3. report generation

In small businesses, there is often a single  database instead of the DW, and this is called a "single layer architecture". In medium and bigger companies, the DW allows a multidimensional analysis. This is called a "three layer architecture". 

How to get the data from the data sources like the operational DB and the external data to the DW? There are some tools called ETL that runs every night transforming the transactions to populate the DW. This ETL can be simple, but more likely it is a complex software that process complex data. It often keep data in another temporary database called "data staging" to solve inconsistency with the data.

In the lab, you will work on ETL workflows to create the OLAP  on top of the DW.

## 2. What is modeled in a DW?

The modeling phase is something in which we have to create a representation of the world enough detailed for supporting the decision making.

> The map is not the world

What are the key objects that are modeled in a DW?
Let's look first at the frontend [here](https://community.microstrategy.com/s/gallery) on microstrategy.
We can infere that there is some event of interest, like the sales of a product, over different axes, called dimensions. Once we fix the axes, we get aggregate values.

What can be modeled?
1. facts
	1. observation of the performance of a business process that is the object of the analysis 
	2. (eg sale,...)
2. measures
	1. numerical attributes of a fact 
	2. (eg qty, revenue,...)
3. dimensions
	1. give the context to facts, described by a set of attributes, otherwise called "degenerate"
	2. (eg sales revenue by product category, by month time, by city market,...)
4. hierarchies
	1. the attributes of a dimension may be related via a hierarchy of relationships, meaning that some attributes are connected in hierarchies
	2. (eg a month is related to the quarter and the year attributes)

Managers are interested in aggregated data. 
We call a metric an aggregated value over a group of data, like the mean, the max, the avg,...
Key Performance Indicators (KPI) are vital values for the names, but basically are aggregated values.

## 3. Recall of SQL

Steps
1. Fix the table using "FROM", then use the attributes in the tables;
2. Filter using "WHERE" and "GROUP BY"
3. "SELECT" the output

```sql
SELECT Produc, SUM(Revenue) as Total Revenue
FROM Sales
GROUP BY Product
```

To get the Total, we use `GROUP BY ()`.

Let's consider *hierarchies* now.
The hierarchy is typically represented as a tree.
For example, Mont -> Quarter -> Year
The concept of hierarchy is connected to the one of functional dependency.
In fact, given the Month, we know the Quarter and the Year.

![[Pasted image 20240919123243.png]]

The hierarchy is useful both for visualization and optimization.
We can use Views. For example, producing a query for Quarter starting from the result of a group by Months.

Stating the Functional Dependency is better both for the user to navigate and to optimize the report. But can we always optimize? No, for example we cannot take the avg of the avg.

Observe that
1. for distributive aggregate function
	1. like sum(), min(), max(), count()
	2. we can compute the sum
2. for algebraic
	1. like avg(), standard deviation()
	2. we can divide sum() and count() and use them differently
3. for holistic
	1. like median(), mode(), rank()
	2. there is NO hope, we need to go back


# dsd03

## The 3 Models

A data model is a set of abstraction mechanisms to describe abstract knowledge.

In Operational Database
1. conceptual data model
	1. to analyse a problem
	2. use
		1. Entity-Relationship model (ER)
		2. Object Data Model (ODM)
2. logical model
	1. use
		1. Relational Data Model
3. physical model
	1. to realize a project on a specific DBMS

In Data Warehouse
1. conceptual data model
	1. to analyse a problem, given the user requirements
	2. use
		1. Dimensional Fact Model (DFM)
	3. (we see it today)
3. logical model
	1. to design a solution independently of actual DBMS
	2. we aim at simplicity rather than normality
	3. as a logical model, we use
		1. the Relation Data Model 
			1. to describe a solution
		2. the Multidimensional Model (called CUBE)
			1. with the possibility to navigate the data
5. physical model
	1. to realize a project on a specific DBMS

We assume to have business questions like this:
![[Pasted image 20240924092047.png]]

## Data model for  Conceptual Design

Typically arriving at this form requires an effort, because managers speak in natural language.
Be sure that what is available is used and what is useful is available.

In a data model for conceptual design, we have
1. facts
	1. rectangle in the middle
2. measures
	1. quantitative values that are specific of the fact, attached to the fact
3. dimensions
4. dimensional attributes
	1. for example, "date" is a dimension with dimensional attributes like "day","month","quarter","year",...

A dimension without attributes is called degenerate. In the example, it is "OrderNo".

Remind also the concept of hierarchies.
That we represent connecting attributes with arrows.
![[Pasted image 20240924094022.png]]

## Steps for designing a DFM schema

*Step 0. Requirements gathering*
Requirements gathering focuses on the study of business processes and on analysis relevant for decision making.

Business questions can be
1. "why is my business not meeting the targets?"
	1. WRONG, not useful
2. "total revenue, by customer, by product"
	1. useful
	2. observe that
		1. "total" is the metric (aggregated)
		2. "revenue" is the measure
		3. "by customer, by product" are the dimensions
3. report
	1. useful, but more difficult

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line


*Step 1. Identify the granularity of the fact*
The first fundamental decision to be taken is the meaning of the fact. What is the grain?

Identifying the grain means deciding the level of detail you want to be made available in the dimensional model. The more detail, the lower the level of granularity. Consider
1. grain is the precision with which the measurements are taken
2. grain determines measures and dimensions and dimensions determine grain

For example, the fact can be
1. an order line, for example the eggs bought
2. a complete order
More detailed grain, often means more space required.

![[Pasted image 20240924095720.png]]

Fact types can be
1. transaction
	1. one fact per transaction, meaning an event that occurs at a specific point in time
	2. for example, a transaction for an individual account of a customer of a bank
2. periodic
	1. one fact for a group of transactions made over a period of time
	2. for example, the amount is the monthly balance for all transaction against an individual account of a customer of a bank
3. accumulating
	1. one fact for the entire lifetime of an evolving event that has a duration and change over time
	2. for example, the lifetime of a mortgage application


*Step 2. Identifying the fact measures*
The measures of interest are numeric values that make sense to add. Not everything that is numeric is a measure.

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line

Not everything that is numeric is a measure! A measure is an observation of the performance of a business process. They can always be aggregated, for example the order number cannot and hence is not a measure.

Measure types
1. numeric additive
2. factless (or measureless)
	1. if the measure is missing
	2. for example the complaints
	3. there is ONLY one operation that we can do that is COUNT(\*)
3. numeric non-additive
	1. for example "unit price" or "gross margin"
4. numeric semi-additive
	1. with respect to a dimension, meaning that sometimes the sum makes sense, sometimes it doesn't
	2. "a measure M is semi-additive with respect to a dimension D1 when it cannot be aggregated with the function SUM for groups of data with different values of D1"
	3. for example "monthly balance" cannot be summed by time, but we can sum the "monthly balance" of two people for a fixed month


*Step 3. Identify the fact dimensions*
Identify the dimensions to give fact measures their context.



*Step 4. Identify Dimensional Attributes*
The dimensional attributes are important for analysis and for reports.



*Step 5. Identify the Dimensional Attribute Hierarchies*
Attribute hierarchies is a natural way to support interactive exploration of facts.

Users understand them intuitively, because they are used to look at a summarized report and then to decide to look at a more detailed one.


*ASSIGNMENT AT HOME*: university exams





# dsd04

...


# dsd05
The example of a data model for Master program exams. Presentation and discussion of the Hospital case study. [Exercises at home (Assignment III) for the lesson 07](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd05.assignments.pdf "mds:dsd:dsd05.assignments.pdf (440.6 KB)").

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




# dsd06
Recalls: the relational model and relational algebra. Exercises. [Exercises at home (Assignment IV) for the lesson 08](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd06.assignments.pdf "mds:dsd:dsd06.assignments.pdf (55 KB)").

## The relational data model

Definition.
1. int, floats, bool and strings are primitive types
2. (A1: T1, ..., An: Tn) is a tuple type of degree n
	1. where T1,...,Tn are primitive types and A1,...,An are distinct attributes names;
	2. attribute order is NOT important
3. (A1 := V1, ..., An := Vn) of type T = (A1: T1, ..., An:Tn) is a set of pairs (Ai, Vi) with Vi of primitive type Ti


Definition.
A relational database is described by a set of relation schemes R:{T} defined as
1. T =


Definition.
Consider a relation scheme R:{T}
1. a schema instance (or relation) is a finite set of tuples with type T


> Since the relations are sets of tuples, they do not have duplicates


# dsd07
More about data mart conceptual design, changing dimensions and advanced data model features. From Conceptual design to relational logical design. Star model, snowflake, and constellation. Logical schema of the Hospital case study. [Exercises at home (Travel agency) for the lesson 09](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd07.assignments.pdf "mds:dsd:dsd07.assignments.pdf (390 KB)").

...

## Types of Relational Model

A DW is represented with a special kind of relational schema 
1. star schema,
2. snowflake schema or
3. constellation schema

# dsd08
Recalls: the relational model and relational algebra. Logical trees.






# dsd09
Discussion of students' solutions of conceptual and logical design case studies.

## Queries on JRS

![[Pasted image 20241122161231.png]]

> I installed JRS on the VM and it works.
> I tried only the first two queries, I should do all of them.
> Skipped this part of the lecture and went directly to the shema



## Exercise: design of Logical Star Schema from DFM Schema

See also the notes on the kindle.

[dsd07.assignments.pdf](file:///Users/pietro/_DS/DSD/exercises/dsd07.assignments.pdf)

![[Pasted image 20241122224343.png]]

Quite mechanically, it becomes

![[Pasted image 20241122224550.png]]

There is a surrogate key for each dimensional table.
Observe that in the dimensional tables the hierarchical information is lost.

How can we verify that the logical schema we designed can answer the business questions?
For each of the business question, write an sql query on the logical schema.

I noticed that he uses the condition of the join in the WHERE. It looks quite clean.

There is actually an advantage in putting the IntitialTouristsFK in the fact table. It can be useful for some queries that would not need the join with Tourists.

## Airlane Company Data Mart Design

[dsd08.assignments.pdf](file:///Users/pietro/_DS/DSD/exercises/dsd08.assignments.pdf)

Starting from business questions, we should do a preliminary analysis on the dimensions, measures, metrics. The goal is to design a DFM Schema.

![[Pasted image 20241122225940.png]]

![[Pasted image 20241123001147.png]]

![[Pasted image 20241123001720.png]]


# dsd10
Data Warehouse design approaches. Data mart logical design.

## Comparison of Design Approaches

We have followed a mixed approach. Let's formalized.

1. Analysis Driven (Kimball)
	1. also bottom-up
The idea is to start from separate data marts for each business process


One problem is that interviewing the managers, they might not be able to describe the bq because they do not know OLAP analysis.

2. Data Drive (Inmon)
	1. also top-down or data-push
It starts from available data.
No need to get business questions.

Risky to do a complex analysis and then maybe get a bad feedback from manager.

3. Combination of both methods
Mainly analysis driven.



![[Pasted image 20241123152923.png]]

We design a data mart at a time, like in the analysis driven approach.
For each data mart:
1. requirement analysis
2. design of two conceptual designs
	1. initial conceptual schema
		1. (what will be useful for the manager)
	2. candidate conceptual schema
		1. (what can be delivered with data)
	3. final conceptual design
3. derive the logical design
4. get the physical design 
	1. given a specific DBMS
	2. indexes, materialized views, etc
6. population through ETL scripts
	1. covered in LDS
	2. largest effort

## 1. Formalizing the Requirements Analysis

The choice of the first data mart to be implemented is of fundamental importance.
It should be the one that is most likely to be delivered on time, within budget, and to answer the most commercially important business questions.

The easiast choice for the first data mart is usually the sales.

The purpose of a data warehouse is not just to store data but rather to facilitate decision making. 

Remember that to close the loop we validate the star schema designing sql queries of business questions on the final schema.

Recall
1. Requirements gathering
	1. is a matter of understanding, interviewing the managers
	2. to obtain business question, we interview 
		1. business users
			1. about inventory process and sales process
		2. data source system experts
			1. to understand source schema
2. Requirements specification
	1. means being able to write down the business questions in the correct form we use

In Requirements Specification, we have
1. Business process requirements
2. Fact Description
3. Dimensions
4. Dimensional attributes

First step. Business Process Requirements
How to document the requirements in a large project?
We need to formalize the various steps.
We assign numbers to business questions and summarize in a table where we have the columns:
`id, business question, dimensions, measures, metrics`

![[Pasted image 20241123155108.png]]

Second step. Fact Table.
The event of interest, that is the fact description.
Fill the table with
`Grain description of fact type, preliminary dimensions, preliminary measures`

Third. Dimensions.
For each dimension, the table is 
`Name, Description, Granularity`
Granularity is the granularity of a tuple in the table.

Fourth. Dimensional attributes.
For each dimensional attributes, it might be worth a description in detail.
> maybe also the way it was cleaned


![[Pasted image 20241123155045.png]]

Fifth. Dimensional Hierarchies.
What is the structure of the hierarchy?


Sixth. How to deal with changes with attributes.
We will see it later.
We need a table to understand how the changes are treated.

![[Pasted image 20241123155633.png]]


Now the MEASURES..



Some measures can be calculated from other.
We do not need to store them in the fact table.
In the fact table we do not store the revenue, we will use a view for the that, computing the revenue on qty and price in the fact table.
> The storage space is used only for features that are not easily calculated.

Then, the Descriptive attributes of the fact.


![[Pasted image 20241123155955.png]]

This happens for every data mart.
But when we have multiply data marts, we can add the following table to summarize which dimensions are shared.
The goal is to know where to look for possible inconsistencies.

![[Pasted image 20241123160200.png]]

## 2b. Initial Analysis-Driven Data Mart Conceptual Design

Using the requirement analysis.
We arrive at designing a possible data mart.

![[Pasted image 20241123160354.png]]

The granularity comes from the Sales data mart requirements, if it was only the inventory, we could have used only month. Be aware of shared dimensions like this.


## 2b. Candidate Data-Driven Conceptual Design

Ignoring the business question, we can build a conceptual design starting completely from the data available.

Start from the logical schema of the relational operational database. 
What are the dimensions?

1. we remove the tables that are not related to the project
	1. (starting a project, we always know what is the process under analysis)
2. (key step) look for
	1. Transactional entities
		1. they describe events that occur at a point in time and contain measurements (quantitative values)
		2. for instance: orderLine in sales, 
	2. Component entities
		1. related to transaction entities via a one-to-many relationship
		2. for instance: for each model there are many entries in the inventory
		3. we usually look for arrows from the transaction to the component
	3. Classification entities
		1. related to component entities via a one-to-many relationship chain.
		2. for instance: region is connected to manifactury via city
		3. it means that we should follow the chain of arrows for external entities
The idea is that starting from the transaction entity we can recognize the snowflake schema (see bottom left in the image below).

![[Pasted image 20241123161851.png]]

3. we get the candidate data mart conceptual design (obtained from the data)

![[Pasted image 20241123162011.png]]

## 2c. Final data mart, obtained from combination

The design of
1. what will be useful
2. what can be delivered

![[Pasted image 20241123162125.png]]

How to merge?
The more structure, the better.
If there is data, we can decide to offer the city even if the bq was the region.

What if we want to add "raining day" in the data?
If external data source allows it or it not to costly. It depends.

## 3. Move from conceptual data model to logical design

It is different from the Database course.
![[Pasted image 20241123173406.png]]

In DB, the priority is not to replicate information. using normalization.
In DW, normalization is a wrong idea, most of the space is stored in the fact table, there is no need to create a complex snowflake. Also, a very simple schema is better to support queries by joining less.

The main idea in the DW is to have the fact table with the foreign surrogate keys created for each dimension table.
(In this and the following lecture we will explore more complex cases)

![[Pasted image 20241123173654.png]]

Once we get the star schema of each data mart, we put them together to obtain the constellation schema. So that for shared tables, we do not replicate them.

![[Pasted image 20241123173846.png]]

Observe that we loose the hierarchical information. In the theory of relational model, we specify the functional dependecies. In most DWMS, functional dependecies are not checked, because it would be too costly. 

How to verify the presence of hierarchy `Month -> Year`?
Write a query that returns an empty result set, iff the functional dependency is valid.
![[Pasted image 20241123174645.png]]
```sql
SELECT Month
FROM Date
WHERE  SUM()
GROUP BY Month
HAVING COUNT(DISTINCT Year > 1)
```

This query can be also be written as follows, without using `COUNT(DISTINCT)`, but using the `WITH...AS` clause, that allows to give a name to a subquery.

```sql
WITH MonthYearSubquery AS
	(SELECT DISTINCT Month, Year
	 FROM Date)
SELECT Month
FROM MonthYearSubquery
GROUP BY Month
HAVING COUNT(*) > 1
```

It is like having a View, but the View is persistent, this subquery is not. The advantage is that the DISTINCT is moved to the subquery. This will be useful later on in the course.

*About Degenerate Dimensions.* They are usually stored in the fact table, but not always. To save space, we could use a junk table (or junk dimension) that contains all possible combinations of values. It depends. We need to do the calculation each time. Or we can also use a mixed approach. But remember that we would need an additional join.

![[Pasted image 20241123175620.png]]


# dsd11
Slowly changing dimensions, fast changing dimensions, shared dimensions. Recursive hierarchies. Multivalued dimensions. [Exercises at home (Travel agency extended) for the lesson 12](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd11.assignments.pdf "mds:dsd:dsd11.assignments.pdf (142.7 KB)").

Let's start with the changes in the dimensions.



# dsd12
A DW to support Analytical CRM Analysis. Wrap up on DW design. [Exercises at home for the lesson 14](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd12.assignments.pdf "mds:dsd:dsd12.assignments.pdf (157.6 KB)").


...



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


# dsd15
OLAP systems. Data Analysis Using SQL. Simple reports. Examples. Moderately Difficult Reports. Solutions in SQL.

> Maybe read https://en.wikipedia.org/wiki/Slowly_changing_dimension and https://en.wikipedia.org/wiki/Data_warehouse















