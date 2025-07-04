Collage of different notes to create the main reference for basic python stuff.

The notes comes mainly from 
1. [[0. Pythonbook]]
2. [[Advanced Python]]
3. [[Data Structures in Python]].
See also more advanced topics in 
4. [[Understanding Python World]] for more libraries 
5. [[Organizing Python Code]] for details on code organization


> divide et impera:
> 1. add functions
> 2. add variables (maybe temporary)
> 3. create class (if really needed)
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
Tuples `(1,5,9)` and Strings `"hi"` are
- ordered sequences
- fast index access
- repeatable values
- IMMUTABLE
Lists `[1,5,9]` are
- ordered sequences
- fast index access
- repeatable values
- mutable
Dictionaries `dict{"apple":3} ` and `sets {1,5,9}` are
- not ordered
- fast key access
- unique keys

Lists and dictionaries are the two most-used data structures in Python.
Set are much faster then lists.

Lists and tuples are 
*Useful for*
- storing sequences of values
- allowing use of sequences as keys for dictionaries (tuple only)
- returning multiple values from a function (tuple only)
*Best at*
- Random access
- Scanning from left-to-right or right-to-left
- Preserving time ordering
- Inserting and removing elments form the tail
*Bad at* 
- Searching for a key (in operator)
- Inserting and removing elements "in the middle"

Dictionaries and sets are
*Useful for*
- Storing key-value associations
- Counting things
*Best at*
- Searching for a key (in operator)
- Accessing by key
- Scanning elements in arbitrary order
- Inserting and removing elements 
*Bad at* 
- Storing ordered sequences

> Sometimes you keep the same time data in two different collections at the same time, for choosing the best one in terms of performance each time.

> Before implementing, ask yourself what is the best data structure for your task.
> The first question is: list or dictionary?

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

*Create a text of strings.*
Be aware of the difference in terms of efficiency between two methods.
First, the append way is quadratic.
Second, the join way is linear.

```python
text = "\n".join(strings)
```

**Formatting strings**

![[Pasted image 20240120170659.png]]
![[Pasted image 20240123182923.png]]
![[Pasted image 20240122132628.png]]

*strings formatting*
```python
'{name} ha {age} ed è alto {height:.2f}'.format(name=name, age=age, height=height)
```

This was for previous versions.

```python
f'{name} ha {age} ed è alto {height:.2f}'
```

This is the right way in the last version of python.

![[Pasted image 20240709135344.png]]

## Tuples
They are separated by commas, with or without parenthesis.
It is possible to mix data types.
Access tuple's values by its index.
Comparing tuples means checking each element at once.
They cannot be changed.

*tuples unpacking*
Common use of unpacking is returning multiple values from a function.
a, b, c are assigned to the first, second and third element of the tuple.
The number of variables must equal the length of the tuple.
```python
tup = ("hello", [1, 2, 3], 42)
a, b, c = tup
print(a, b, c, sep='\n')
# a, b = tup WRONG
```
 
 THIS is the Python way to swap (idiomatic)
```python
a, b = b, a
```
On the right we create a tuple and we use unpacking to assign on the left.




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

*Initializing a list of lists*
Everyone expect the same type in a list.
Otherwise it is very error prone.

Note that multiplying a list of a list by n creates copies of the lists, meaning that they are shallow copies. But I can still inizialize different lists when initializing the list containing the others, for example with a for loop.
So, for creating a table made by lists:

```python
l = [ [] ] * 10 # wrong

for _ in range(10): # correct
	l.append([])
```

*Modifying a list*
Append and extend take constant time.
Insert, pop and remove take linear time, and should be used very carefully.
Popping the last element, however is pretty efficient.

List comprehensions allow to filter out from a list.

> At the beginning of a task, stop and explain yourself the task using the right terminology.

The rule is easy: The variable is a cell that contains the value or a reference to the object. We copy the content of the variable. Variables of most of types contain a reference (a pointer) to the object, which is stored somewhere else in memory.
Ratio for the rule: avoid expensive copies as much as possible.

The last element of the list is `l[-1]` because it is like `l[len(l) - 1]`.
And so on with `-2,-3` and so on.

## Dictionaries
*Description*
They are very common.
They are unordered, which means no indexing available.
The indexes are the keys, which are of course unique and immutable.
For this reason, any immutable data type can be a key: int, float, strings, tuples.

- `fruitbasket["mango"] = 1` will create a new element if the key does not exist, otherwise it will overwrite the existing value of the key. 

Special things
- `fruitbasket3 = fruitbasket1 | fruitbasket2` is the pipeline to merge two dictionaries, but the value for a key which is in both these dictionaries is taken from fruitbasket2, as that dictionary is to the right of the pipeline.
- `x:dict[str,int]` is a type hint
- With the introduction of Python 3.7, the ordering that you see when dictionaries are displayed is guaranteed: it is the order in which the items were added to the dictionary. the order of addition is simply stored in a separate data structure next to the dictionary, which is used when you display the dictionary. Dictionaries cannot be sorted or reversed, as they are unordered by deﬁnition.

*Methods*
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

Note that JSON files use a dictionary-like structure and syntax.
They are descriptions.

Ways of iterating over the dictionaries?

*defaultdict*
`Defaultdict` is used to return a default value from default dictionary.
Use `from collections import defaultdict`.
And before using the dict in the loop, assign to it default values of the default dictionary.

Usually, a Python dictionary throws a `KeyError` if you try to get an item with a key that is not currently in the dictionary. The `defaultdict` in contrast will simply create any items that you try to access (provided of course they do not exist yet). To create such a "default" item, it calls the function object that you pass to the constructor (more precisely, it's an arbitrary "callable" object, which includes function and type objects). For the first example, default items are created using `int()`, which will return the integer object `0`. For the second example, default items are created using `list()`, which returns a new empty list object.
- [stackoverflow](https://stackoverflow.com/questions/5900578/collections-defaultdict-difference-with-normal-dict)

In case you want to change default value overwrite default_factory:
```python
d.default_factory = lambda: 1
```

Esercizio con defaultdict
```python
from collections import defaultdict
words_list = ["ciao", "come", "va", "tutto", "bene"]
def group_by_length(words_list):
	d = defaultdict(list)
	for w in words_list:
		len_s = len(w)
		d[len_s].append(w)
	return d
```
Così dovrebbe funzionare perchè se la chiave non ha ancora un valore, viene inizializzata una lista e posso usare append.
		
In alternativa, senza defaultdict
```python
words_list = ["ciao", "come", "va", "tutto", "bene"]
def group_by_length(words_list):
	d = {}
	for w in words_list:
		len_s = len(w)
		if len_s not in d.keys():
			d[len_s] = []
		d[len_s].append(w)
	return d
```

*Let's review the dictionaries.*
1. Creating an empty dictionary
```python
data = {}
# OR
data = dict()
```
2. Creating a dictionary with initial values
```python
data = {'a': 1, 'b': 2, 'c': 3}
# OR
data = dict(a=1, b=2, c=3)
# OR
data = {k: v for k, v in (('a', 1), ('b',2), ('c',3))}
```
3. Inserting/Updating a single value
```python
data['a'] = 1  # Updates if 'a' exists, else adds 'a'
# OR
data.update({'a': 1})
# OR
data.update(dict(a=1))
# OR
data.update(a=1)
```
4. Inserting/Updating multiple values
```python
data.update({'c':3,'d':4})  # Updates 'c' and adds 'd'
# OR from Python 3.9+
data |= {'c':3,'d':4}
```
5.  Creating a merged dictionary without modifying originals
```python
data3 = {}
data3.update(data)  # Modifies data3, not data
data3.update(data2)  # Modifies data3, not data2
# OR from Python3.9+
data = data1 | {'c':3,'d':4}
```
6. deleting items in dictionary
```python
del data[key]  # Removes specific element in a dictionary
data.pop(key)  # Removes the key & returns the value
data.clear()  # Clears entire dictionary
```
7. Check if a key is already in dictionary
```python
key in data
```
8. Iterate through pairs in a dictionary
```python
for key in data: # Iterates just through the keys, ignoring the values
for key, value in d.items(): # Iterates through the pairs
for key in d.keys(): # Iterates just through key, ignoring the values
for value in d.values(): # Iterates just through value, ignoring the keys
```
9. Create a dictionary from two lists
```python
data = dict(zip(list_with_keys, list_with_values))
```

## Sets
They are built using dictionary.keys().
It means that they the items in a set are unique and immutable.
However the set itself is mutable.
Items are not accessible by index nor by keys. Use for loops.
Initialize with {key1, key2,... }. But for an empty set by assigning a call to the function `set()` to a variable, otherwise it is a dictionary.
When creating a set, it can be immutable using `frozenset()`.
They are special dictionaries with no values, just keys.
The current implementation of sets maintain the order, but do not assume it is ordered.


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


# Functions

## Function
In python it is not possible to return nothing.
So, it is actually returned None, if not specified.
The arguments use the assignment rules.

If a function returns more values, it is actually a tuple.
That needs to be unpacked.

Functions are first-class object.
It means that they can be assigned to variables, stored in a data structure, passed as arugments, ...

## Pipeline
A pipeline is a list of functions.
So, we can store functions in a list.
Then we iterate over the list to execute functions on an object.

```python
pipeline = [funct1, funct2, funct3]
text = "some text"
for task in pipeline:
	text = task(text)
```

It is very professional to use it combination with tqdm.
## Function attributes
They are `__attribute__`.
The `__name__` for example can be used to show which task are executed during a pipelline, maybe in combination with tqdm. It looks very professional.

You can add your attributes to the functions.


## Lambda functions
Also called anonymous functions.
They consist of just one expression.
In those cases, it might be better to turn the function into a lambda function to improve readability. It is just a matter of readability.
Basically, you return the result of an expression which takes the arguments.

```python
def my_function(x, y):
    return x * y

equiv_lambda = lambda x, y: x * y
```

In the following example, we use also the ternary operator.
This is one of the most popular use cases of lambda functions.
Since they are anonymous and inline, it is easier to plug them into the bigger function.
And it is immediately clear what is going on.

```python
def my_abs(x):
    if x < 0: return -1*x
    else: return x
    
equiv_lambda = lambda x: x if x > 0 else -1*x
```

Also, showing which is the variable used for sorting

```python
tuples = [(1, 'd'), (2, 'b'), (4, 'a'), (3, 'c')]

sorted(tuples, key=lambda x: x[1])
```

The idea is that you can forget the function after using it.
Exactly like the `_` in the loops.

## Mapping
Force yourself to use `map` and `filter` because they are quite popular in data science.
> Use Kaggle, in particular challenges
> Look at old challenges with topics you like.
> And compare your notebook with the experts' notebook.
> Understand tools and tricks.

Differences with the map function from libreary?
It can accept multiple collections (not lists) as parameters.
It does not materialize the sequence. But you can still do it if needed.

```python
seq = map(lambda x: x - 1, my_list)
# it prints "<map object at 0x13fa99ab0>"
```

This is a promise that this iterable will generate an element after the other. But it is not materialized.
The seq *cannot be called a second time*, it will not be able to produce anything, because the sequence is generated only once, otherwise you need to materialize.
Or you can redefine the map.
What is the reason for this behavior?
Because the map functions takes more iterables as parameters and some of them cannot be repeated. Meaning that everytime can be different, for example random numbers or data from the internet.

If instead of `[]` in a list comprehension you use `()`, you create a generator object.
So, no materialization, but still usable in for loops.

## Filter
Filter is exactly like the function we used to remove from list.
But in a map-like fashion, using iterables.

```python
def my_remove_from_list(fil, my_list):
    new_list = [e for e in my_list if fil(e)]
    return new_list

my_list = [-1, 2, 3]
my_list = my_remove_from_list( lambda x: x % 2 == 0, my_list) # lambda x: True if x % 2 == 0 else False
print(my_list)
```


## Yield

It is used as a return in function.
Each time the function is called, it return the next yield, and then starts again from the previous yield.

```python
def test_yield():
    yield 1
    print("qui siamo dopo il primo valore")
    yield 2
    yield 3

seq = test_yield()
    
for value in seq:
    print(value)
```



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
	- the main difference is that, when dealing with lists, dict and sets, we *should create a `deepcopy()` for + because we probably do not want to modify the original object* (with = we are using an alias)
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

```python
class Square(Rectangle):  
    def __init__(self, x, y, w):  
        super().__init__(x, y, w, w)
```

Initializing a rectangle with the square parameters and inheriting all the methods. If necessary, add more parameters and initialize below.
Remember to add the parent class in the definition of the child.


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
	3. returns the file handle
2. `read()`
	1. it is a method of the handle: `<variable> = fp.read()`
	2. moves the pointer to the end of the file (to be moved for reading again)
	3. returns the complete content of the file as a string
3. `close()`
	1. it is a method of the handle: `fp.close()`
	2. after, the handle is no longer associated with the file
	3. releases the handle

Example
```python
fp = open("text.txt")  # or `open("text.txt") as fp`
print( fp.read())
fp.close()
```
Or in alternative
```python
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
	3. for printing might want to use `print(line, end="")`


**Writing text files**

Methods
1. `open(<filename>, w)`
	1. to open for writing, just use `"w"` as the second argument of `open()
	2. important
		1. If file does not exists, it is created.
		2. If it does exist, it is replaced (DELETING OLD CONTENT)
			1. therefore *always check if the file already exists*
2. `write(<string>)`
	1. it is a method of the handle `fp.write(<string>)`
	2. the argument is the string you want to add in the file
	3. no newline added
3. `writelines(<list of strings>)`
	1. add a list of strings (taken as argument) in the text files
	2. each string MUST end with the newline (not added automatically).
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

`"path"` refers to the file or the pathname.

Methods in the `os.path` module there are useful functions to handle files.
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

More useful functions in the `os` module are (use `os.<function>`):
- `getcwd()`
	- current working directory
- `chdir()`
	- changes directory
- `listdir()`
	- returns a list of all files and dirs in dir
- `system(<command>)`
	- executes a command (must be supported by OS)





**File encoding**
Text files use an encoding to define how characters are supposed to be interpreted. It differs based on OS.
To see your encoding use
```python
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

**Byte string**
First, what is a *byte string*?
- Each character is a byte. Bytes are numbers between 0 and 255.
- Control codecs are displayed as they are, and not converted.
- Remember that illegal characters where ignored in normal strings.
- It is possible to use indexing as with normal strings. However, instead of the character, it is returned the codec for that letter. Like with ord(). It is the int corresponding to the character in the encoding.

Methods
- `bytes(<list_of_bytes>)`
	- It is possible to `bytes()` cast a list of integers. Even a one-element list. It used to convert the code of a character into that character.
```python
bs = bytes([72, 101, 108, 108, 111]) print (bs)
```

- However, it is not possible to convert the byte string obtained into a regular string using `str()`. 
- It must be used `.decode("utf-8")`. With the appropriate encoding. `.encode()` does the opposite.

An example
```python
s1 = b"Hello World!"
print(s1) # b"Hello World!"
for c in s1:
    print (c, end = " ") # 72 101 108 108 111 32 87 111 114 108 100 33 
```

When to use byte strings?
If the file has Unicode characters that cannot be read with normal strings.

**Opening binary files**
Binary refers to all files that are not text files.

- `open("file.txt","b")`
	-  when opening a file, to do it in binary mode add `"b"` as argument of `open()`.

In addition
1. "rb" for binary read
2. "r+b" for reading and writing in binary
	1. note that "r+" is reading and writing
3. "wb" for writing binary
4. "w+b" for reading and writing in binary DELETES OLD CONTENT
![[Pasted image 20240201162744.png]]

**Reading a binary file**
Any file can be opened in binary. However there's no conversion of newline. The concept of lines does not exist. As a consequence, ONLY `read()` can be used.
1. `read()`
	1. an integer argument can be used to select the number of bytes read from file
		1. remember that each character is a byte (also in strings)
	2. returns a byte string
		1. for example `b"Hello"`



**Writing a binary file**
Of course you must supply a binary string.

**Positioning the file pointer**
Method
1. `seek(<byte_pos>, [opt])` 
	1. the first is a relative byte position
	2. the second (optional) is the starting position for counting of the first argument, it can be (with corresponding constants in the OS module)
		1. 0 -> beginning of file (SEEK_SET)
		2. 1 -> current file pointer position (SEEK_CUR)
		3. 2 -> end of file (SEEK_END)
	3. For example fp.seek(5) == fp.seek(5,0). 
	4. If it starts from the end, negative numbers are expected.

2. `tell()` is used to know the current position of the pointer.

```python
h = open(“pippo.txt”,“rb”)
h.seek(5, os.SEEK_CUR)
print(“Current: ”, h.tell())
h.close()
```

## Command Line Processing
You can start a Python program with a list of arguments:
`python <program_name>.py <argument_1> <argument_n>`
The argument are separated from each other by spaces and can be anything. 
Import the `sys` module in order to process command line arguments, otherwise nothing happens.
You get access to the command line arguments supplied via a pre-defined list called `sys.argv` and it is a list of strings, each string being one of the command line arguments supplied.
It contains at least one element `sys.argv[0]` which is the name of the file.




# More Topics
## Exceptions
There are two check when running a program and they lead respectively to:
1. "Syntax Error"
2. "Runtime Error"

When an exception is raised (like `ZeroDivisionError`), if it is not handled the program is stopped and the error displayed. However, an exception can be handled and the program can continue running.

**Exception handling**
```python
try:
	print(3/0)
except:
	print("Division by zero!")
```
If the statement after `Try` raises an exception, python executes the "exception handling" after `except` and the program continues. Otherwise, the `except` is just skipped.

To differentiate each `try...except` to understand (and display) errors there are two options
1. Code each `try...except` separately
2. Use `except` like an if
Here's an example
```python
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
4. `ValueError`
	1. error while casting to another value
5. `TypeError`
	1. using a value not supported by that operator
6. `FileNotFound`
	1. opening a file that does not exist
7. `IOError`
	1. any error while accessing a file
	2. see File Handling Exceptions of `errno` module

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
```python
try:  
    print(int("Not an integer"))  
except ValueError as ve:  
    print(ve.args)
```

> Remember that all exceptions should be either handled responsabily or should just make the program crash

**File handling exceptions** 
Any problem with files leads to an `IOError` Exception.
The first element of args contains a number to understand exactly what's wrong.
These error numbers in the tuple of information of the error are defined in the `errno` module, which can be imported. The module offers constant to use instead of actual numbers.
The most common are
1. `errno.ENOENT`
	1. No such file or directory
2. `errno.EACCES`
	1. Permission denied
	2. also reading from a closed file
3. `errno.ENOSPC`
	1. No more space left on device

An example from ChatGPT
```python
try:
    fp = open(file_path)
except IOError as e:
    if e.errno == errno.ENOENT:
        print(f"Error: No such file or directory - {file_path}")
    elif e.errno == errno.EACCES:
        print(f"Error: Permission denied - {file_path}")
    elif e.errno == errno.ENOSPC:
        print(f"Error: No more space left on the device - {file_path}")
    else:
        print(f"Error: {e}")
```

**Raising exceptions**
There are two possibilities
1. use `raise` with known exceptions replacing the tuple of arguments
	1. the first element is printed
	2. the second element can still be accessed with `.args`
2. create a new exception with classes (how?)
An example of replacing the arguments
```python
def getStringLenMax10(prompt):
	s = input(prompt)
	if len(s) > 10:
		raise ValueError("Length exceeds 10", len(s))
	return s

print( getStringLenMax10("Use 10 characters or less: "))
```

**Assertions**
```python
#if condition returns True, then nothing happens:  
assert x == "hello"  
  
#if condition returns False, AssertionError is raised:  
assert x == "goodbye"

#You can write a message to be written if the code returns False:  
assert x == "goodbye", "x should be 'hello'"
```

## Bitwise Operators
Python is based on Unicode encoding, specifically UTF-8.
A byte is decoded as follows:
1. if the leftmost bit is 0
	1. is an ASCII character
2. if the leftmost is 1
	1. is the start of a sequence of multiple bytes that represents a sequence
For multibyte sequences...



**Characters Encoding**
A byte is made of 8 bit. Therefore the range of numbers that can be represented is 0->255, because 255=(2^8)-1
1. ASCII has 7 bits because the leftmost is fixed to 0
	1. also other encodings use ASCII in the range 0->127
2. Other encodings use 8 bits
	1. they assign different characters in the range 128->255

Python uses UTF-8
1. it is restricted to at most 4-byte sequences
2. when a bit sequence does not express a legal UTF-8 encoding, you get a `UnicodeDecodeErrors`

![[Pasted image 20240201165522.png]]

Numbers
1. integers are represented with two complement method
2. floating points are represented with the scientific notation
	1. mantissa + exponent

**Manipulating bits**
![[Pasted image 20240130231555.png]]


## Iterators

Useful to save space.

`range()` is special, because it allows to iterate over it more than once.
For every other generator, this is not possible.

`enumerate()` already discusses.

`zip()` "pairs" up the elements of a number of lists, tuples, or other sequences to create a list of tuples.

```python
my_list = [3, 4, 6, 7, 8, 9]
strings = ["Bla bla bla", "A a ben", "Warem a ben ben", "Warem a a ben",
           "Warem a ben ben", "Warem ben ben ben"] #"We were so young!"]

for t in zip(my_list, strings): 
    print(t)
print()
```

![[Pasted image 20240427190242.png]]


# Additional Notes from Slides

## Various

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

## Useful things

*use of underscore*
To indicate that you are not interested in that value.
If you save a value, someone will look for the code where you use that variable. So, if you will not use it, just use `_`.
Also the use of `*_` is very interesting, it means "as many _ as needed"

```python
# Not interested in some elements? Use the placeholder _
_, b, _ = tup

print(b)

# Not interested to last elements? Use *_, which means "as many _ as needed"
a, *_ = tup
print(a)

# Guess what
a, *rest = tup
print(rest)
```

Why do we use immutable objects?[¶](http://localhost:8888/lab/tree/L02-Python-DataStructures.ipynb#Why-do-we-use-immutable-objects?)

- Immutable objects are **thread-safe** (means being able to run on multiple code at the same time) so you will not have any synchronization issues.
- It is guaranteed that functions or classes cannot modify the object.
- Immutable object are easier to cache.
- The internal state of your program will be consistent even if you have exceptions.
- Immutable objects are good Dictionary keys and Set elements. Have you ever ask yourself why a list cannot be a key in a dictionary?

Immutability can have a performance cost, since when an object cannot be mutated we need to copy it if we want to write to it.

*Generate vs Materialize*
Python always tries to generate when possible.
Generate is easier in terms of memory.

Never iterate over the position if you can iterate over the elements.
It is less error prone and much more clear.
Also because of reusability of code with objects that do not have indexes, like sets or generators.

> This is the second most important lesson, after not using "in" in loops.

Enumerate generates pairs position-value.
The sequence of pairs is generated by an object, but not materialized.
It can be generated using `list(enumerate(l))`, but it is not what you usually do, because it is used to iterate over it.

So use enumerate if you also need the indexes in the loop.

```python
# sum of even numbers in the CORRECT way
s = 0
for i,e in enumerate(l):
	if i % 2 == 0:
		s += e
# the WRONG alternative is
s = 0
for i in range(len(l)):
	if i % 2 == 0:
		s += l[i]
```



# Interesting Exercices

**Overloading operator for CustomList**
Better not to overload built-in classes.
```python
class customList(list):
    def __init__(self, *args):
        super().__init__(*args)
    def __sub__(self, sub_list):
        new_list = []
        for elem in self:
            if elem not in sub_list:
                new_list.append(elem)
        return new_list

color1 = customList(["red", "orange", "green", "blue", "white"])
color2 = customList(["black", "yellow", "green", "blue"])

print(color1-color2)
print(color2-color1)
```

**Creating docstring for function**
Get it with
- `help(<function>)`
- `<function>.__doc__`
```python
def my_function():
	'''Demonstrates triple double quotes
	docstrings and does nothing really.'''

	return None

print("Using __doc__:")
print(my_function.__doc__)

print("Using help:")
help(my_function)

```

**Use of `*args` and `**kwargs`**
These constructs allow functions to be more flexible and accept different numbers of arguments without explicitly defining them in the function signature.
- `*args` stands for "arguments" and is used to pass a variable number of non-keyword arguments to a function. It collects these arguments into a tuple.
- `**kwargs` stands for "keyword arguments" and is used to pass a variable number of keyword arguments to a function. It collects these arguments into a dictionary.
```python
def example_function(arg1, *args, kwarg1="default_value", **kwargs):
    print(f"arg1: {arg1}")
    print(f"args: {args}")
    print(f"kwarg1: {kwarg1}")
    print(f"kwargs: {kwargs}")

# Example usage:
example_function(1, 2, 3, kwarg1="custom_value", name="Alice", age=25)

```

**Default Values in class definition**
I think in python is better to alway use default parameters for class. It is also useful to define the types, instead of using type hints.
```python
class Person:
	def __init__(self, name="", age=0):
		self.name = name
		self.age = age
```





