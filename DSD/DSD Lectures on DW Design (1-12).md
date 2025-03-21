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

## ...
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

## Changing dimensions
Let's start with the changes in the dimensions.

![[Pasted image 20250205161544.png]]
An example of fast change is the year of the customer. 

## Type 1. Overwriting history
Overwrite the value.

Type 1 is obvious, because we just overwrite the value.

## Type 2. Preserving history
Add a dimension row.

Let's analyse the type. 2.
When we want to preserve the full history of cases.
We have 3 cases.
1. there is a natural key identifier
2. using InitialSurrogateKey in the dimension table
3. using InitialSurrogateKey in the fact table

*Case 1. Both the surrogate key and a natural key identifier.*
4. for instance for people we may have the SSN (Social Security Number), 
5. we may track the same person with different addresses, because these rows will have the same SSN
6. if one customer change the zip code, we just create a new row with the same SSN and a different zip
7. This means that we need to COUNT(DISTINCT SSN), not count(\*)
8. we can also add two more columns with DateStart and DateEnd
	1. where all date start with the beginning of the dw and NULL as end, then if needed we add a DateEnd in the older and set the next day for the new start.

![[Pasted image 20250205183444.png]]

*Case 2. Surrogate Key only.*

We create a new surrogate kay, but the InitialCustomerPK is the same.

![[Pasted image 20250205183923.png]]

*Case 3. Surrogate key only, with FIRST surrogate key in the fact table*
There is a variant.
We keep the InitalCustomerPK as a degenerate dimension in the fact table.

![[Pasted image 20250205184221.png]]

Having an attribute in the fact table is space consuming, if we consider the large number of rows in the fact table.

Note that we will need the inital surrogate key in the staging area to assign it to the customer


## Type 3. Preserving more versions
Add new attributes.

Type 3. Do not use it.
Add a column with old_zip.
This complicates a lot the queries.
And we can keep only a smaller portion of older values.

![[Pasted image 20250205211137.png]]


## Type 4. Fast changing
Add a new dimension (called mini or profile).

Think about the years of service for each guide.
We may decide to use type 2, but it is not a good idea because we will have too many and frequent changes.

It is better to use a separate table, very similar to the junk table used for degenerate dimensions.

We add a row for every possible combination of attributes that change fast.
By constructing this "mini-table".
Changing means changing the foreign key in the fact table to link it to the new row in the mini-table with the new attributes updated.
Meaning that we move the changes from the dimension to a different table.
The number of rows in the mini-table is given by the product of cardinality of the attributes to be changed.

![[Pasted image 20250205212638.png]]

For small dimensions, type 2 is still recommended.

In type 4, the advantage is that we do not need to add new rows in the dimension as for type 2. Only a change in the foreign key is needed.
However, the disadvantage of type 4 is an additional column in the (large) fact table.

Now there are 3 more advanced topics.
1. shared dimensions
2. recursive hierarchies
3. multivalued dimensions

## Shared dimensions.

![[Pasted image 20250205213211.png]]

## Recursive hierarchies

Each agent has a boss, which is an agent, except the boss.

*Solution 1. Without a bridge table*

The supervisor of the agent will be a foreign key SupervisorFK to an agentPK. This fk will be absent for the boss, ie NULL.

![[Pasted image 20250205213442.png]]

![[Pasted image 20250205213530.png]]

There are some problems with this solution.
How can we find the total revenue for the subordinates?
We want all the subordinates.
It will require many joins, but how many? There is an extension of SQL called Recursive SQL, but these queries are slow.
Not a good solution.

![[Pasted image 20250205213820.png]]

*Solution 2. With ForTheHierarchies table*

Build a table "ForTheHierarchy", where we have one row for each ascendent and discendent.
Not only for father-child, but for all possible descendants of father1.
We precompute all possible pairs, also with some informations like the NoLevels, also whether the agent is a leaf in the hierarchy.
The key point is that we precompute this table.

![[Pasted image 20250205214125.png]]

How to use this table?
Starting from order, we will join with the rows where the supervisor is agent 2, and they will match with all the subordinates.
With a single query.

![[Pasted image 20250205214318.png]]

## Multivalued dimensions
One last complicated transformation.

When an order is done by possaibly more than one agent.
In the fact table we admit only one agent.
What if we want to admit more agents?
There are several options.

*Solution 1. Change the granularity*
4. change the granularity of the fact
	1. instead of having a single row per order, we split based on the contribution of agent
	2. it requires to rethink all the dw design

*Solution 2. Auxiliary table*

Instead of a fk to the agent, we may have a fk to the group of agents in the order.

![[Pasted image 20250205215032.png]]

There is a problem.
So far, every reference to the fact table is towards a single row. Not anymore with this solution (?).
It may break for optimization of star join queries.

chatgpt-> queries joining Order and GroupMembers may produce multiple rows per fact, leading to incorrect aggregations if not handled carefully.


*Solution 3. Traditional many-to-many*

A table AgentOrder, typical many-to-many intermediate table.
However, this is very problematic for the idea behind the star join.

![[Pasted image 20250205215402.png]]

*Solution 4. Bridge table (star join safe) *

Similar to recursive hierarchies.
With a bridge table.

Group is a dimension, which allows for the star join.
The non-standard part of the query consists of obtaining the agents from the group of agents.

In the previous design (solution 2 with auxiliary ta), joining Order and GroupMembers created multiple rows per fact, which could lead to incorrect aggregations.
Here, the Order table remains one row per fact, and the allocation logic is handled separately in AgentGroup.

![[Pasted image 20250205215658.png]]

![[Pasted image 20250205215856.png]]

















# dsd12
A DW to support Analytical CRM Analysis. Wrap up on DW design. [Exercises at home for the lesson 14](https://didawiki.di.unipi.it/lib/exe/fetch.php/mds/dsd/dsd12.assignments.pdf "mds:dsd:dsd12.assignments.pdf (157.6 KB)").

starting from 25:00

We conclude the DW Design with a more complex DW that is CRM.

The CRM is made of
5. operational CRM
6. analytical CRM

![[Pasted image 20241224160247.png]]

We can do 4 types of analysis.
7. Sales and Marketing Analysis
	1. Sales
	2. Market
	3. Channel
	4. Promo Campaign
8. Profitability Analysis
	1. Customer
	2. Product
	3. Market
	4. Campaign
	5. Channel
9. Service Quality Analysis
	1. Product return
	2. Order fulfillment
10. Customer Analysis
	1. Customer segmentation
	2. Customer retention
	3. Customer satisfaction
	4. Customer attrition (or churn)

## 1. Sales and Marketing Analysis

This lines can be seen as dimensions of data marts.
For example, we can think of a data mart with the fact table "*sales*" with dimensions such as "Product, Customer, Date, Channel, Order".

![[Pasted image 20241224161004.png]]

Another example is "*Marketing Analysis*".
The new fact can be "contact".

![[Pasted image 20241224161041.png]]

What about sales and marketing analysis?
Here we can see the customers that used the promotion.

![[Pasted image 20241224161110.png]]

## 2. Profitability Analysis

Also *Profitability Analysis*.
Note that
11. Total Cost = Product Cost + Returns Cost + Promotion Cost 
12. Margin = Revenue - Returns Value – Total Cost 
13. Margin % = Margin / (Revenue - Returns Value)

![[Pasted image 20241224161256.png]]



## 3. Service Quality Analysis

We explore *Return Analysis*.

![[Pasted image 20241224161559.png]]

Also *Order fullfillment analysis*

![[Pasted image 20241224161818.png]]

## 4. Customer Analysis

How to categorize customers in a given month?
14. New:  with at least an order last month and no order in the past
15. Constant:  with at least two orders per month for three months in the last four months
16. Occasional:  with at least one order in the last four months, but not as for typology Constant or New
17. Inactive:   with no order in the last four months, and not Constant in the last 12 months
18. Churn risk:  with no order in the last four months after being Constant at least once in the last 12 months.

![[Pasted image 20241224161915.png]]


## DW Example

![[Pasted image 20241224162257.png]]










