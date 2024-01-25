## Intro
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
- `__repr()__`
		- should return a string that contains every information needed to recreate the object
		- always define it
- `__str__()`
		- return a nicely formatted string that explains the most important information on the class
		- it is optional
		- *what is the relationship with print?*

**Methods**
Note on naming the methods with prefixes
- `is` prefix if they return True/False
- `get` prefix to get a value from an object
- `set` prefix to set a value for an object

Objects can be used as parameters for other objects.
However, all object instances are passed to methods and functions *by reference*, exactly like lists, dictionaries, sets. If you want, create a copy().

## Operator Overloading
Polymorphism is a concept that allows a function to have different results depending of the type of its arguments.
Remember to check the type of a variable using `isinstance(variable, type)` that returns True or False.

**Comparisons Overloading**
![[Pasted image 20240125185746.png|400]]

Additionally
- `__bool__` when an object is treated as a condition

**Calculations Overloading**
![[Pasted image 20240125185937.png|400]]

Additionally
- `def __radd__( self, n ): return self.__add__( n )`
	- add the prefix `r` to methods if you want to use a different order than usual, meaning that the class whose method you are calling is on the right of the operator (while usually is on the left)

**Unary Operators Overloading**
![[Pasted image 20240125190405.png]]

**Overloading Operators of Sequence Classes**
It is a special kind of class.
The predefined sequence classes are tuples, lists, dictionaries, sets.
The main characteristic is that elements can be accessed by index or keys.

![[Pasted image 20240125190756.png]]
![[Pasted image 20240125190808.png]]

