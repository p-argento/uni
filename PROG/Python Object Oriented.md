## Intro
Remember
- a class is a data type, an object is a value
- every data type is a class
- a method is always called `variable.method()` while a function is `function(variable)`

## Creating a class
Use `class ClassName`.
The keyword `pass` is used to replace a statement, but instead doing nothing.

- `self` is the reference to the object of the class. It must be always included in the methods declarations, otherwise there is a runtime error. In the call of methods it is implicit.

- The initialization method is called `__init__()`
	- It is good practice to create all the attributes in the init, however it is possible to create them also later in the code. Better use inheritance to add extra attributes.
	- it is possible to add default values

- `__repr()__` and `__str__()`
	- 