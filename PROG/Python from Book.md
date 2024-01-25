## Program
Day 19
1. Introduction
2. Using Python
3. Expressions
4. Variables
5. Simple Functions
6. Conditions
7. Iterations
8. Functions
9. Recursion
10. Strings
11. Tuples
12. Lists
13. Dictionaries
14. Sets
15. Operating System
16. Text Files
17. Exceptions
18. Binary Files
19. Bitwise Operators
20. Object Orientation
21. Operator Overloading
22. Inheritance
23. Iterators and Generators
Extra
24. Command Line Processing
25. Regular Expressions
26. File Formats
27. Various Useful Modules

## Naming Conventions
Always use snake_case.
Except for
- GLOBAL_VARIABLES
- ClassNames
- ExceptionNames

## Formatting strings

![[Pasted image 20240120170659.png]]
![[Pasted image 20240123182923.png]]
![[Pasted image 20240122132628.png]]


## Built-in Types
[Here](https://docs.python.org/3/library/stdtypes.html)
1. Truth Value Testing
2. Boolean Operations — and, or, not
3. Comparisons
4. Numeric Types — int, float, complex
5. Boolean Type - bool
6. Iterator Types
7. Sequence Types — list, tuple, range
8. Text Sequence Type — str
9. Binary Sequence Types — bytes, bytearray, memoryview
10. Set Types — set, frozenset
11. Mapping Types — dict
12. Context Manager Types
13. Type Annotation Types — Generic Alias, Union
14. Other Built-in Types

| DATA STRUCTURE | ORDERED | MUTABLE |
| ---- | ---- | ---- |
| string | y |  |
| tuple | y |  |
| list | y | y |
| dictionaries |  | y |
| set |  | y |

| strings | list | dictionary | set |
| ---- | ---- | ---- | ---- |
| - strip()<br>- upper()<br>- lower()<br>- find()<br>- replace()<br>- split()<br>- join() | - append()<br>- extend()<br>- insert()<br>- remove()<br>- pop()<br>- index()<br>- count()<br>- sort()<br>- reverse() | - copy()<br>- keys()<br>- values()<br>- items()<br>- get() | - add()<br>- update()<br>- remove()<br>- discard()<br>- clear()<br>- pop()<br>- copy()<br>- union()<br>- intersection()<br>- difference()<br>- isdisjoint()<br>- issubset()<br>- issuperset() |

To remember it:
Tuples `(1,5,9)` and Strings `"hi"` and Lists `[1,5,9]` are
- ordered sequences
- fast index access
- repeatable values
- IMMUTABLE (except lists)
Dictionaries `dict{"apple":3} ` and Sets {1,5,9} are
- not ordered
- fast key access
- unique keys

Mixing types?


Lists and dictionaries are the two most-used data structures in Python.

## Strings

Methods
- strip()
	- ?
- upper(), 
- lower(), 
- find(), 
- replace(), 
- split(),
- join()


## Lists
Description
Ordered collection of mixed elements. Index access of elements.
Like a tuple, but MUTABLE.

Notation
- `list1 = list2` creates an alias, while `list1 = list2[:]` creates a shallow copy
	- **Remember** in a function, a list is passed by reference and therefore the original list is changed
- replace elements using `list[3]` or slices using `list[1:3]`
- insert elements or lists using `list[3:3]`

**What is the best way to iterate through a list to modify it?**

![[Pasted image 20240122164805.png]]
![[Pasted image 20240122171223.png]]

Special operators
- +
	- concatenate two lists (remember to assign the result)
	- to append an element, made it looks like a list ->  +\[element]
- *
	- multiply a list by an integer to create quickly a list with equal numbers
- in
	- test existence of element in a list
- del (is actually a keyword)
	- delete an element by index
	- similar to pop() but no return value
	- can be used also to remove a slice
- is
	- check if the id() of two element is the same


Methods (usually no return value because they change the list)
- append(element) or `list[len(list):]= [element]` or `list += [element]`
	- append an element
- extend(list)
	- append a list
- insert(index, element) or `list[3:3]`
	- easy
- remove(element)
	- remove the first occurrence
	- if not in the list -> runtime error
- pop(index=len(list))
	- RETURNS the element
	- removes by index, if not specified it is the last one
- index(element)
	- returns the first occurrence of an element
	- if not found -> runtime error
- count()
	- RETURNS integer
- sort(reverse=False, key=function)
	- change the order of the list
	- the key function is applied to each item of the list and can also return tuples, for example to handle mixed types lists
	- key function is without parenthesis and can it is better to use an anonymous function
- reverse()

List comprehensions
![[Pasted image 20240125001726.png]]


## Dictionaries
Description
They are very common.
They are unordered, which means no indexing available.
The indexes are the keys, which are of course unique and immutable.
For this reason, any immutable data type can be a key: int, float, strings, tuples.


Special things
- `fruitbasket3 = fruitbasket1 | fruitbasket2` is the pipeline to merge two dictionaries, but the value for a key which is in both these dictionaries is taken from fruitbasket2, as that dictionary is to the right of the pipeline.
- `x:dict[str,int]` is a type hint
- With the introduction of Python 3.7, the ordering that you see when dictionaries are displayed is guaranteed: it is the order in which the items were added to the dictionary. the order of addition is simply stored in a separate data structure next to the dictionary, which is used when you display the dictionary. Dictionaries cannot be sorted or reversed, as they are unordered by deﬁnition.

Methods
- copy()
	- `fruitbasketalias = fruitbasket
	- `fruitbasketcopy = fruitbasket.copy()`
- iterating through the dictionary (return an iterator)
	- keys() provides an iterator that lists all the keys of a dictionary
	- values() provides an iterator that lists all the values of a dictionary
	- items() provides an iterator that lists all the key-value pairs of a dictionary as tuples.
	- NOTE that iterators can be used into `for` loops or with `max(),min(),sum()` otherwise they must be casted to a list
		- If you wonder why Python seems to prefer iterators instead of lists: the answer is that iterators are more general and use much less memory. They are “lazy” methods, as they only provide an item when it is requested.
- get()
	- The get() method can be used to get a value from a dictionary even when you do not know if the key for which you seek the value exists.

## Sets
They are built using dictionary.keys().
It means that they the items in a set are unique and immutable.
However the set itself is mutable.
Create an empty set by assigning a call to the function `set()` to a variable.
When creating a set, it can be immutable using `frozenset()`.

Methods
- add()
	- a single item
	- repeated items are ignored
- update()
	- adding single sequence elements of a list, a tuple, a string
- remove()
	- runtime error if absent
- discard()
	- ignore errors
- clear()
- pop()
	- no argument, pop randomly
- copy()
- union()
	- or |
	- set1.union(set2)
- intersection()
	- or &
- difference()
	- or -
- isdisjoint()
- issubset()
- issuperset()



