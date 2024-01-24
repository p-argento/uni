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
Until now
9. Recursion
10. Strings
11. Tuples
12. Lists
13. Dictionaries
14. Sets
Day 21
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


![[Pasted image 20240120170659.png]]
![[Pasted image 20240123182923.png]]

[[list methods]]

![[Pasted image 20240122132628.png]]

![[Pasted image 20240122164805.png]]

![[Pasted image 20240122171223.png]]

**When iterating through a list where you need to remove items,
BETTER USE `while i < len(list) ` and NOT a for loop .**

## Built-in Types from documentation
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


## Data types comparison
| DATA STRUCTURE | ORDERED | MUTABLE |
| ---- | ---- | ---- |
| string | y |  |
| tuple | y |  |
| list | y | y |
| dictionaries |  | y |
| set |  | y |

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
- strip(),
- upper(), 
- lower(), 
- find(), 
- replace(), 
- split(),
- join()








## Dictionaries
Description

Special things
- `fruitbasket3 = fruitbasket1 | fruitbasket2` is the pipeline to merge two dictionaries, but the value for a key which is in both these dictionaries is taken from fruitbasket2, as that dictionary is to the right of the pipeline.
- `x:dict[str,int]` is a type hint
- With the introduction of Python 3.7, the ordering that you see when dictionaries are displayed is guaranteed: it is the order in which the items were added to the dictionary. the order of addition is simply stored in a separate data structure next to the dictionary, which is used when you display the dictionary. Dictionaries cannot be sorted or reversed, as they are unordered by deﬁnition.
- any immutable data type can be a key. This means: int, float, strings, tuples.
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