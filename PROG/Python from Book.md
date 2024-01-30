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
Classes
20. Object Orientation
21. Operator Overloading
22. Inheritance
Extra
23. Iterators and Generators
24. Command Line Processing
25. Regular Expressions
26. File Formats
27. Various Useful Modules


# Built-in Types
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

**Formatting strings**

![[Pasted image 20240120170659.png]]
![[Pasted image 20240123182923.png]]
![[Pasted image 20240122132628.png]]


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
*What then?*
Based on experience, I think the best idea is to create a new empty list and add there the elements we need while iterating the first list (which remains unmodified). If needed, replace the old list with the new one.


**Special operators**
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


**Methods** (usually no return value because they change the list)
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

**List comprehensions**
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
		- If both are deﬁned, then __str__() is used with a print()
		- If __str__() is not deﬁned, by default it is the same as __repr__()

**Methods**
Note on naming the methods with prefixes
- `is` prefix if they return True/False
- `get` prefix to get a value from an object
- `set` prefix to set a value for an object

**Note on classes as parameters**
Objects can be used as parameters for other objects.
However, all object instances are passed to methods and functions *by reference*, exactly like lists, dictionaries, sets. If you want, create a copy() or deepcopy().

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
 
## Inheritance
 To consider whether the relationship between two classes is an inheritance relation- ship, ask yourself whether subclass “is a” superclass.
 For example a car is a vehicle, but a molecule is NOT an atom.

```
class Square(Rectangle):  
    def __init__(self, x, y, w):  
        super().__init__(x, y, w, w)
```

Initializing a rectangle with the square parameters and inheriting all the methods. If necessary, add more parameters and initialize below.
Remember to add the parent class in the definition of the child.


# More Topics
## Exceptions
There are two check when running a program and they lead respectively to:
1. "Syntax Error"
2. "Runtime Error"

When an exception is raised (like `ZeroDivisionError`), if it is not handled the program is stopped and the error displayed. However, an exception can be handled and the program can continue running.

**Exception handling**
```
try:
	print(3/0)
except:
	print("Division by zero!")
```
If the statement after `Try` raises an exception, python executes the "exception handling" after `except` and the program continues. Otherwise, the `except` is just skipped.

To differentiate each `try...except` to understand (and display) errors there are two options
1. Code each `try...except` separately
2. Use `expect` like an if
Here's an example
```
try:
	print( 3 / int(input("Number: ")))
except ZeroDivisionError:
	print("Divided by zero)
except ValueError:
	print("Not an integer")
except:
	print("There is something wrong)
```
The final except is generic.

**Most common exceptions** are
1. `ZeroDivisionError`
	1. division by zero
2. `IndexError`
	1. accessing a list or tuple with an index out of bound
3. `KeyError`
	1. accessing a dictionary element with unknown key
4. `IOError`
	1. any error while accessing a file
5. `FileNotFound`
	1. opening a file that does not exist
6. `ValueError`
	1. error while casting to another value
7. `TypeError`
	1. using a value not supported by that operator

There are two **additional clauses** that can be used
1. *else*
	1. contains the code that it is executed if no exceptions are raised
	2. it is better just to continue the normal coding
2. *finally*
	1. contains the code that is always executed, with or without exceptions
	2. it is used for example to make sure that the file is closed

**Accessing exception information**
1. *as*
	1. it is used to fill the variable after `as` with a tuple of arguments provided when the exeption is raised
	2. to access the tuple use `<variable>.args`
```
try:  
    print(int("Not an integer"))  
except ValueError as ve:  
    print(ve.args)
```

> Remember that all exceptions should be either handled responsabily or should just make the program crash

**File handling exceptions** in the `errno` module
Any problem with files leads to an `IOError` Exception.
The error numbers in the tuple of information of the error are defined in the `errno` module, which can be imported. The module offers constant to use instead of actual numbers.
The most common are
1. `errno.ENOENT`
	1. No such file or directory
2. `errno.EACCES`
	1. Permission denied
	2. also reading from a closed file
3. `errno.ENOSPC`
	1. No more space left on device

**Raising exceptions**
There are two possibilities
1. use `raise` with known exceptions replacing the tuple of arguments
2. create a new exception with classes (how?)
An example of replacing the arguments
```
def getStringLenMax10(prompt):
	s = input(prompt)
	if len(s) > 10:
		raise ValueError("Length exceeds 10", len(s))
	return s

print( getStringLenMax10("Use 10 characters or less: "))
```



# Files
## Text Files
A text file consists of lines of text.
At the end of each line, there's a newline symbol. In python is automatically converted in `\n`.
Word processor document are not text files, they are binary files.

**File Handle**
Opening a file creates a "file handle", it is the only access point to the file.
It starts from different point based on how you open the file, basically at the beginning except for appending.
All methods performed on the file are actually performed on the file handle.
The file pointer is moved automatically. Usually it is moved manually only for binary files.

**Buffering and Flushing**
There are two steps for making changes:
1. buffering
	1. changes are temporary stored in memory
2. flushing
	1. sending the buffer to the actual file
	2. it is forced when closing a file
	3. if the file crashes, buffer might not be flushed

**Reading text files**
When accessing a file, if it is not in the same directory, the complete path must be used.

Methods
1. `open()`
	1. two alternative ways
		1. `<handle> = open(<filename>)`
		2. `open(<filename>) as <handle>`
	2. there are two arguments, the second is optional (read only by default)
	3. 
2. `read()`
	1. it is a method of the handle: `<variable> = fp.read()`
	2. moves the pointer to the end of the file (to be moved for reading again)
3. `close()`
	1. it is a method of the handle: `fp.close()`
	2. after, the handle is no longer associated with the file

Example
```
fp = open("text.txt")  # or `open("text.txt") as fp`
print( fp.read())
fp.close()
```
Or in alternative
```
with open("text.txt") as fp:
	print( fp.read())
	# more statements nested
# fp.close() is automatic
```

Additional methods
1. `readline()`
	1. reads characters up to the newline character (included)
	2. returns a string
	3. this is the best for reading large files because handle each line at once
2. `readlines()`
	1. reads all lines
	2. returns a list of strings, which are the lines (including `\n`)
	3. for printing might want to use `print(line, end=""`


**Writing text files**
To open for writing, just use `"w"` as the second argument of `open()`.
Important
1. If it does not exists, it is created.
2. If it does exist, it is replaced (DELETING OLD CONTENT)
	1. therefore *always check if the file already exists*

Methods
1. `open(<filename>, w)`
	1. as already said
2. `write()`
	1. it is a method of the handle `fp.write(<string>)`
	2. the argument is the string you want to add in the file
3. `writelines()`
	1. add a list of strings (taken as argument) in the text files
	2. each string MUST end with the newline.
	3. it is the opposite of readlines()
Note that `writeline()` does not exists since it is the same of `write`

**Appending to text files**
When a file is opened for appending, the file handles is placed at the end of the file. Just use `"a"` as a second argument of `open()`.
Rememember
1. to use `+` to concate strings
2. to add `\n` when needed

It is good practice to create
1. functions for reading (open, read, close)
2. variable for file name

This is good form
![[Pasted image 20240130184522.png]]

**os.path methods**
In the `os.path` module there are useful functions to handle files.
`"path"` refers to the file or the pathname.

Methods
1. `exists()`
	1. true if path exists
2. `isfile()`
	1. true if path is a file
3. `isdir()`
	1. true if path is a directory
4. `join()`
	1. concatenates more parts of a path (*how*?)
5. `basename()`
	1. returns file name from a path
6. `dirname()`
	1. returns directory name from a path
7. `getsize()`
	1. returns an integer representing the number of bytes


**File encoding**
Text files use an encoding to define how characters are supposed to be interpreted. It differs based on OS.
To see your encoding use
```
from sys import getfilesystemencoding
print(getfilesystemencoding())
```
If the text file encoding is different from the OS one, a `UnicodeDecodeError` is displayed. The solution is to add an extra parameter to `open("file.txt", encoding=<encodingname>)`, which is string.
The typical values are
1. `ascii`
2. `latin-1`
	1. includes `ascii`
3. `mbcs`
	1. deprecated
4. `utf-8`
	1. default from python 3.6

## Binary Files

Refers to all files that are not text files.

























# Notes on Slides

- Naming Conventions
	- Always use snake_case
	- Except for
		- GLOBAL_VARIABLES
		- ClassNames
		- ExceptionNames

- `isinstance()` function in Python is used to check if an object is an instance of a specified class or a tuple of classes. Its primary purpose is to determine the type of an object and check if it matches a given class or classes.
	- `result = isinstance(x, int)`
	- `y = 3.14; result = isinstance(y, (int, float))`

- `print()`
	- Two special parameters
		- `sep` indicates what should be printed between each of the parameters, and by default is a space
		- `end` indicates what print() should put after all the parameters have been displayed, and by default is a newline
		- ![[Pasted image 20240127163131.png|300]]

- `format()`
	- returns a new string which is the formatted version of the input string

- how to modify a string? concatenate (or create a new one)

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



- When a mutable data structure is passed as a parameter to a function, it is **passed by reference**!









