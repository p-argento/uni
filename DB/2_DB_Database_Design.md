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
		3. NEVER mix the blueprint with the physical object
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

### Library
Library is not a class, because a class is a set that can be empty or contains many items.
> always use plural names for classes

Attributes is interesting only because it describes a class.
Is it an attribute or a class? There's no correct answer, we must ask the librarian.
If I would like to set the languages a-priori, then it is not an attribute anymore, I am creating a dictionary containing all the languages that are allowed, then I should create a class. Otherwise, if the attribute can be whatever, it doesn't need a class, it can be defined a-posteriori when it is written as attribute of a book.
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



