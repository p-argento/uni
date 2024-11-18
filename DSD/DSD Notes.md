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

3 Steps
1. Dimensional Fact Model (DFM)
	1. we see today
2. Relation Data Model (RDM)
	1. to describe a solution
	2. we aim at simplicity rather than normality
3. Multidimensional Model (called CUBE)
	1. with the possibility to navigate the data

We assume to have business questions like this:
![[Pasted image 20240924092047.png]]

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












