## What is DBMS
A set of tools, to manage homogeneous sets of structured data.
It is able to deal with
1. huge amounts of data
	1. otherwise it is excel or simpler tool
2. mission critical data
	1. if an organization loose data (or faith into data) it is a real problem
	2. basically it has to keep data reliable
3. shared data
	1. if two people are updating the data in the same moment, it should happen sequentially, not together
4. queries and updates
	1. if it is only for queries, it is not a dbms, but it is a tool for data analysis
	2. queries and updates can happen at the same time

## DBMS vs Data Analysis
They are two different tools
1. OLTP: On-Line Transaction Processing
	1. support everyday activities of the organization
	2. the collection of data is a "database"
		1. managed by a DBMS
2. OLAP: On-Line Analytical Processing
	1. analysis of collected data to gather information
	2. the collection of data is called "data warehouse"
		1. managed by Decision Support System (DSS)
Do not confuse them. They are really different.
But in both of them, you manage structured data.

![[Pasted image 20240220144807.png]]

> DSS are built on top of DB.
> This course is about DB, that is systems to support OLTP

*Big Data*
Traditional DBMS is not able to able. Why?
DB is able to handle only structured data.
The three Vs of Big Data are Volume, Variety, Velocity.
Big Data application are usually supported by NoSQL systems.
High parallelism is required.

## What a database looks like
It looks like a collection of sets.
These sets must be structured.
A database contains many tables correlated.

![[Pasted image 20240220153214.png]]

Example of a session
1. defining the database
2. schema definition
3. data entry
4. query (and get return)

Usually there is a piece of code inserting code in the db.

## Users of DBMS
1. analyst / designer
	1. defines the schema
2. programmer
	1. write applications (for example to insert data)
3. db administrator (DBA)
	1. manages data structures (consider changing indexing if too slow)
	2. manages user rights (assign username and rights to new users)
4. operator (final user)
	1. use applications
	2. use query tools

## Parts of DBMS
1. engine (or kernel)
	1. different tasks: transactions, DDL, ...
2. tools for the programmer
3. tools for the DBA
4. tools for data access

*Transaction*
A transaction is a piece of code defined by boundaries.
Three actions must be defined
1. begin
2. commit
3. abort
The key concepts are
1. atomicity
	1. in case of failures (any type of failures), it is easy to abort and it is as if the operation never happened
	2. it is all or nothing
2. durability
	1. transaction effects can be recovered after a failure
3. isolation (or serializability)
	1. no interference by concurrent transactions
	2. for example when two actors are playing at the same time

It is not easy to implement atomicity and durability at the same time. Should I write on disk or not?

A transaction is usually defined as an ACID Transaction if it respects Atomicity, Consistency, Isolation, Durability.



