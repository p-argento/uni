> divide et impera
## Program
Intro
1. Introduction
2. Using Python
3. Expressions
4. Variables
5. Simple Functions
6. Conditions
7. Iterations
8. Functions
9. Recursion
Data Types
10. Strings
11. Tuples
12. Lists
13. Dictionaries
14. Sets
Files and Binary
15. Operating System
16. Text Files
17. Exceptions
18. Binary Files
19. Bitwise Operators
Objects
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

Methods (most of them return a new string)
- strip()
	- return a new string with removed leading and trailing whitespaces
- upper() and lower()
	- returns a version with al capitals/lower case
- find(substring, index) -index is optional
	- returns the lowest index where substring start
	- if not found return -1
	- the optional parameter index is the starting point of the search
- replace(lookFor, substituteWith)
	- returns a new string with all occurrences replaced
- split(sep) -sep default is a white space
	- returns a list of strings from the original string split by sep
- join(list)
	- returns a string
	- list must(?) be a list of strings
	- the class object is the string representing the separator
		- typically `" ".join(list)`

## Tuples
They are separated by commas, with or without parenthesis.
It is possible to mix data types.
Access tuple's values by its index.
Comparing tuples means checking each element at once.
They cannot be changed.






## Lists
Description
Ordered collection of mixed elements.
Index access of elements.
Like a tuple, but MUTABLE.

Notation
- `list1 = list2` creates an alias, while `list1 = list2[:]` creates a shallow copy
	- **Remember** in a function, a list is passed by reference and therefore the original list is changed
- replace elements using `list[3]` or slices using `list[1:3]`
- insert elements or lists using `list[3:3]`
- `list1 + list2` merges two lists
	- to add an element in this way, you need to add a single-element list

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
	- argument is the element
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

- `fruitbasket["mango"] = 1` will create a new element if the key does not exist, otherwise it will overwrite the existing value of the key. 

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
- get(key)
	- The get() method can be used to get a value from a dictionary even when you do not know if the key for which you seek the value exists
	- add a second argument to replace the return of None if the key does not exist, for example 0.
	- useful because you do not need to check if an item exist (you can simply return 0)

## Sets
They are built using dictionary.keys().
It means that they the items in a set are unique and immutable.
However the set itself is mutable.
Items are not accessible by index nor by keys. Use for loops.
Initialize with { } but without keys.
But for an empty set by assigning a call to the function `set()` to a variable, otherwise it is a dictionary.
When creating a set, it can be immutable using `frozenset()`.

Methods
- add()
	- a single item
	- repeated items are ignored
- update()
	- adding single sequence elements of a list, a tuple, a string
	- means that `update("hi")` will add `"h","i"`
- remove()
	- runtime error if absent
- discard()
	- ignore errors
- clear()
	- removes all element from the set
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



# Object Orientation

Remember
- a class is a data type, an object is a value
- every data type is a class
- a method is always called `variable.method()` while a function is `function(variable)`

## Creating a class
Use `class ClassName`.
The keyword `pass` is used to replace a statement, but instead doing nothing.

- `self` is the reference to the object of the class. It must be always included in the methods declarations, otherwise there is a runtime error. In the call of methods it is implicit.

**Predefined methods**
- initialisation method `__init__()`
	- It is good practice to create all the attributes in the init, however it is possible to create them also later in the code. Better use inheritance to add extra attributes.
	- it is possible to add default values
	- parameters with default values, must be after the others in the declaration
		- or use =None for parameters without defaults
- `__repr()__`
	- should return a string that contains every information needed to recreate the object
	- always define it
	- goal is to be unambiguous
	- used typically for debugging
- `__str__()` is the output of print()
	- return a nicely formatted string that explains the most important information on the class
	- it is optional
	- goal is to be readable since it is the output of `print(class)`
		- if str is absent, repr is used

**Methods**
Note on naming the methods with prefixes
- `is` prefix if they return True/False
- `get` prefix to get a value from an object
- `set` prefix to set a value for an object

Objects can be used as parameters for other objects.
However, all object instances are passed to methods and functions *by reference*, exactly like lists, dictionaries, sets. If you want, create a copy().

**NOTE**
Python determines the type of a variable at runtime, rather than at compile time. As a result, you can pass instances of different classes to a method, and within that method, you can use the properties and methods of that class.

## Operator Overloading
Polymorphism is a concept that allows a function to have different results depending of the type of its arguments.
Remember to check the type of a variable using `isinstance(variable, type)` that returns True or False.

**Comparisons Overloading**
![[Pasted image 20240125185746.png|400]]

Additionally
- `__bool__` when an object is treated as a condition

**NOTE**
There is no need to implement `__ne__(), __lt__(), __le__(),` as they are automatically changed into calls to the methods `__eq__(), __gt__(), __ge__()`.

**Calculations Overloading**
![[Pasted image 20240125185937.png|400]]

Additionally
- `def __radd__( self, n ): return self.__add__( n )`
	- add the prefix `r` to methods if you want to use a different order than usual, meaning that the class whose method you are calling is on the right of the operator (while usually is on the left)
- `__add__()` vs `__iadd__`  (+ vs +=)
	- the main difference is that, when dealing with lists, dict and sets, we should create a deepcopy for + because we probably do not want to modify the original object (with = we are using an alias)
	- with += on the other hand we are changing the original, so its fine

**Unary Operators Overloading**
![[Pasted image 20240125190405.png]]

**Overloading Operators of Sequence Classes**
It is a special kind of class.
The predefined sequence classes are tuples, lists, dictionaries, sets.
The main characteristic is that elements can be accessed by index or keys.

![[Pasted image 20240125190756.png]]
![[Pasted image 20240125190808.png]]


# More interesting functions

- `isinstance()` function in Python is used to check if an object is an instance of a specified class or a tuple of classes. Its primary purpose is to determine the type of an object and check if it matches a given class or classes.
	- `result = isinstance(x, int)`
	- `y = 3.14; result = isinstance(y, (int, float))`


# Notes on Slides


- `print()`
	- Two special parameters
		- `sep` indicates what should be printed between each of the parameters, and by default is a space
		- `end` indicates what print() should put after all the parameters have been displayed, and by default is a newline
![[Pasted image 20240127163131.png|300]]

- `format()`
	- returns a new string which is the formatted version of the input string

- `main()`
	- Before executing the program, the interpreter deﬁnes few special variables If the ﬁle is executed as a whole program, __name__ is set to the value __main__ and main() executed Otherwise main() is ignored
	- `if __name__ == '__main__': main()`
	- it can be used for testing purposes
	- if the file is loaded as a module, main is ignored

- isinstance(var, type)
	- you may want to check values before using them

- scope
	- var is defined also outside a loop
	- var outside a function is not defined
	- global var is defined inside a function
		- but modifies a local copy
		- any variable create is local

- Bool
	- False = None, 0, "", empty dict

- `from sys import exit`
	- python raises a `SystemExit` exception and the program terminate

- break and continue
	- break exits the loop
	- continue skips to the next iteration

- **loop-and-a-half**
	- is a while loop with several if conditions that break (or continue) the loop

- how to modify a string? concatenate (or create a new one)

- When a mutable data structure is passed as a parameter to a function, it is **passed by reference**!

- 







