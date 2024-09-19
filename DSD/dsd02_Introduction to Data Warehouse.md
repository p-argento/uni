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





