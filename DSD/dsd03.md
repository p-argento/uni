Recall of notions of Information Modeling for the *Object Data Model (ODM)*.

In Operational Systems, DB are support applications. The design of the operational db is to optimize transactions. What is modeled in a DB? This is the question today.

## Information modeling

We use a symbolic model to represent the relevant part of the real world that is relevant. We need an appropriate abstraction level with appropriate notation (for example the map of the city).

There are 3 levels in any software system
1. Conceptual data model
	1. What is the problem?
	2. Object Data Model (ODM)
2. Logical model
	1. How to solve it?
	2. Relational Data Model
3. Physical model
	1. how to implement a solution?

What do we need to model in an operational database?
There is concrete knowledge, meaning facts known of the system to be modeled.
1. entity
	1. anything for which certain facts should be recorded, independently from the existence of other entities
	2. for example, Mario is a student
2. property
	1. a fact about an entity which is not meaningful in itself, but only because it describes an entity of interest
	2. "Age of Mario is 22"
3. collection (or class)
	1. set of entities with the same properties
	2. {Mario, Anna,...}
4. relationship
	1. fact which correlates independent entities
	2. "Mario is enrolled at DS"

![[Pasted image 20240920113356.png]]

How to specify common structure?
Abstract knowledge, means the structure of concrete knowledge and the restrictions on admissible values:
1. property type
2. entity type
	1. `Age:int, Name:string`
3. collection type
	1. `{ Age:int, Name:string }`
4. relationships
	1. cardinality
		1. can be one (1) or many (N)
		2. `Is enrolled` at has cardinality (N, 1)
	3. participation
		1. can be total or partial, to specify whether an entity of one collection can have entities of another collection associated to it
		2. if the relationship always exists or no
		3. `Is enrolled at` is total, `HasPassed exams` is partial`

A *data model* is a set of abstraction mechanisms to describe abstract knowledge. The object data model can be seen as an extension of the entity-relation data model. Different names will be used:
1. entity -> object
2. entity type -> object type
3. collection type -> class
4. relationship
5. inheritance
6. property -> (Attribute, Value)
7. property types -> attribute type

![[Pasted image 20240920114739.png]]

In the image on the left
a) is a class
b) has also the attributes
c) has also the attribute types (note that they can be composed)

In the image on the right
a) is a relationship
- (a single arrow means 1, two means N, the bar is the possibility to be zero)
- as a convention, we name the relationship reading from left to right, if it is in both directions
b) the relationship has a property
c) this is another solution, which is transforming the relationship into a class
d) is a relationship connecting objects of the same class

A *schema* is the abstract knowledge of a domain of discourse expressed by using a specific data model. A schema is a symbolic model.

![[Pasted image 20240920115940.png]]

*Inheritance* allows to define classes as extensions of other classes (like in python). For example, we can model the class Students from the already existing class Persons.
There are different possibilities to represent inheritnace.
Cover means that the superclass is fully covered by the subclasses.

![[Pasted image 20240920120741.png]]

A refined schema.

![[Pasted image 20240920120959.png]]













