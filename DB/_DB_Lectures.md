# 1. Intro
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


## Essential Features of a good DBMS engine
Features
1. efficiency
2. transaction support
	1. failure resilience, concurrency control
		1. the dbms gives software tools in order to be resilient, but the hardware must be set up (like a second computer somewhere else in case the first one fails because of a fire)
		2. "no free lunch"
3. data distribution
	1. and data replication (not our matter)

## Advantages of DBMS
Advantages
1. physical and logical independence
	1. code should not depends on the structure of the DB
	2. in DBMS, the SQL code would still work if we change organization and indexes
	3. in the future, if you want to modify the logic, just modify the schema mapping the view, but not the actual sql code
2. automatic optimization of declarative code
	1. sql code is declarative, meaning that is faster to code than low-level programming
### Levels of data definition
A DBMS supports three-levels of schemas
1. View level (or external)
	1. limited views offered to the user
2. logical level (or conceptual)
3. physical level (or internal)

## Problems of DBMS
Problems
1. useful only for structured data
	1. if you manage documents, which are not structured, then use a document system
2. defining a schema is difficult and slow
	1. need skills and time, but maybe I want something fast
	2. a data lake or AI tool can be faster to implement
3. expensive and difficult to manage
	1. need to pay the salary of a DBA
4. usually optimized for OLTP load and not for OLAP load
	1. if the goal is analysis, then consider DSS, not DBMS

# 2. DB Design
--21.02--
## Need to design
In the real-world, often a database is born from an excel spreadsheet that was too big. And it is a terrible idea.
Anomalies arise, because of redundancy and redundancy generate errors.
Divide tables.
If I add a new information in one table, but it was already there, then what is the current right data?
If it is a DB, it must reflect the truth. And it must be designed in order to remove redundancy.
## Phases of design
Phases
1. discuss with the user, to understand how he sees the world
2. write a conceptual design (and discuss with user)
	2. the result is the conceptual design, meaning how the user sees the world
	3. use object-oriented language or entity-relationship languages
3. logical design (or relational design)
	1. the result is the logical schema, means defining the computer representation
	2. use relational language

## Conceptual schema
This is the way of reflecting the view of the world of the customer.
Optimization has nothing to do with conceptual design.
Forget about algorithms and data.
By avoiding optimization, you avoid redundancy.
The user must feel at home, it must reflect world and terminology he expects.
Design things that last.
Designing is a process with some rules.
You should understand how the user works, do not just copy it.
You must understand the needs of the users.
Always focus on the main reason, and deliver.
Users can see if you do not understand, they will oversimplify and then the design is just bad.
Check how they actually work for real and talk with everybody, not just the manager.
Collect the documents they produce, to understand how the final output is.

## O-O language
Operators
1. class (or collections)
2. realtionships
3. subcollection links

![[Pasted image 20240221170120.png|300]]

## 1. Classes
What are classes
1. a set of homogeneous entities
2. a class is in the mind of the user, a table is in the computer
3. for example a class
	1. physical
		1. car, books
	2. events
		1. exams, sales, loans
	3. entity models (a "blueprint")
		1. car model, course description
		2. abstract entities
		3. **NEVER mix the blueprint with the physical object**
		4. recognizing these entities is the most difficult part, because the user will describe blueprint and actual entity with the same words
		5. example
			1. database is 6 CFU (blueprint)
			2. this year database is though by Giorgio Ghelli (actual instance)
		6. example
			1. train from pisa to florence (blueprint)
			2. today's train at 7 is late (actual train)

> I will judge you based on the words that you use, because you should not change the words that the user uses. The only exception is to avoid redundancy if the user uses the same word for different things.



There are two different ways of representing a class. The second one is cleaner for the final version of the schema.

![[Pasted image 20240221172556.png]]


## 2. Relationships
While classes are sets, relationship are set of pairs.
Exactly like the mathematical definition, where a relation between sets is just a subset of pairs from the initial sets.
A relationship is also called association.
Associations may or may not have a name. We give a name only if it is meaningful.
Giving a name to an association is optional.

The cardinality of an association is ...
It can be 0, 1 or many.
There are symbols for representing the cardinality.

![[Pasted image 20240221174108.png]]

An hotel have many rooms. A room belong to one hotel.
A room called 5 can be a different entity in different hotels.
For a given hotel, how many bookings?
Model also the corner cases. Like the empty hotel.
**Two arrows is freedom, one arrow is a constraint.**
When in doubt, use from 0 to many.

### Library Example
Library is not a class, because a class is a set that can be empty or contains many items.
> always use plural names for classes to be sure it is a class

Attributes is interesting only because it describes a class.
Is it an attribute or a class? There's no correct answer, we must ask the librarian.
If I would like to set the languages a-priori, then it is not an attribute anymore, I am creating a dictionary containing all the languages that are allowed, then I should create a class. Otherwise, if the attribute can be what ever, it doesn't need a class, it can be defined a-posteriori when it is written as attribute of a book.
A class is a fixed list a-priori, because we care about it.

> if in the test you find ambiguity, justify your choices (especially in the oral)

Attributes or relationships?
If I want attributes for the event, it is much better to have a class than an association.
As with attributes and 


> Try to draw the library, adding all reasonable attributes
> 1. book
> 2. loans
> 3. clients
> 4. subjects
> 5. state
> 6. 

--27.02--
> Cardinality is what students always get wrong.
> When in doubt, choose 0 to many.

What if one class in structured as a tree? For example in the subjects of the library we have science, that includes math, that includes geometry, calculus, ...
They are sentences, basically a set of pairs.
Called ciclic association, or recursive association.

Using more subjects is wrong.
It is redundant.
It is different than the mind of the customer.

Every loan is for one book.
Be aware of the fact that the librarian might use the same word "book" meaning both the blueprint and a physical copy of the book.
But you cannot be ambiguous.
And never use the name of an attribute for a class.
"The book is not the title"

## Subclass
Whenever you have a subset of a class for which we plan to collect more information.
Then you specify extra information.
"A student is a person".
"A copy is NOT a book". (the book is the blueprint, while the copy is a physical entity)
The subclass is a subset relationship with extra attributes.
Define a subclass only when you have extra attributes.

Use cases for subclasses
1. overlapping subsets $\rightarrow$
2. non-overlapping subsets
3. overlapping cover $\Rightarrow$
4. non overlapping cover (called partition)
*Note the different notation.*

> Do exercises published


## Telephone calls example
[[Telephone call example text]]

What about corner case?
Ask the manager. Because everything should be there from the initial design.
But be prepared, because the client will call you saying that the system is shit, if it doesn't allow that specific marginal case.
In these cases, use a name in the relationship.

Unless you have a constraint, allow freedom.
Basically, when you do not know, do not use limitations.

If the customer want to choose the offer from an apriori list, this is enough to choose the representation of offers as a class.

Should we use a subclass "Presented Offers"? NO.
It is not a feature of the offer, it is a relational feature between offers and calls.
In addition, we do not have extra attributes.
An offer presentation is not an offer, because an offer is a blueprint, an offer presentation is an event.
"Offer presentation" from being a relational features, becomes a class with the degree of interest as an attribute.
It is interesting to note that the relations becomes unary going out from "offer_presentation", but to-many entering the "offer_presentation"

> When in doubt in using an attribute or a relation, use a relation.

The call is done by the employee, not the name of the employee.
Never use a value to represent an entity.


# Logical Design

A table is a set of lines (or records).
It has a name and a set of column names (or fields or attributes).
A type is also defined for each attributes.
There can be constraints. Like a salary must be positive.

The key constraint, where every line of an attribute must be unique. There could many key constraint.
A foreign key constraint is also called an inclusion constraint (or subset constraint). It means that every value that appears in the column must appear in the column connected. It is a relation of subset $A\subseteq B$.
The foreign key looks like an association in concept design. But here I use a value to represent the association.

Every relation has
- extensional aspect, the content of the table, the rows
- schema, descriptional aspects
I always build a database in the sequence
1. build the schema
2. fill with content

The content of a table is a set of lines.
The order is irrelevant.
Usually a define at least one key constraint, to avoid repetition of rows.
The extension of a table is a set, not a multiset.
The notation is very similar to conceptual schema.
Now the arrow is just one. An arrow does not denote an association, but a foreign key, that is just an attribute.
The primary key is underlined. And I put a star next to the primary key.

I can have a ciclic association. It will just be a foreign key that relates to its own table. Every field in the table may contain the special type null. 
> what is the meaning of null?

## From conceptual schema to relational
1. Add an artificial primary key to any collection which needs one.
	1. People use unique identifiers, but i suggest you to add your own.
2. translate associations and inclusions into foreign keys
3. translate multivalued attrivutes into tables
4. flatten complex attributes

How it works?
*One-to-many*
If the association is one in at least one direction (1-N), then choose the unary direction and represent that as a primary key.
I take the unary arrow doesn't change, the other one disappears.

![[Pasted image 20240301215441 1.png]]

*Many to many.*
Understand that every instance is just a pair.
Every many to many produces a new table.
It can be very long, but just two columns with the two foreign keys.
It is symmetrical.

![[Pasted image 20240301215719 1.png]]

If you had an association with attributes.


How do I group all employees of the same group? Scan, because tables are not sorted.

*Subclasses*
The arrow becomes a foreign key. 

![[Pasted image 20240301220242 1.png]]

How do we represent this with a relational schema?
A foreign key into persons.
Each family lives in exactly one flat.
The relationship between land owners (tax-payer) and flats is many to many hence it generates a new table.

> exercise. try both conceptual and logical schema.

[[medical center exercises]]


