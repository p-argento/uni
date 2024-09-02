# 1. Data Types and conditions
## 1. Variables
The primitive data types are
1. int `%d`
2. (signed and unsigned)
3. char `%c`
4. float 
5. double (`%e` for scientific notation eg 1.2e5, 8 bytes)

Attribute `long` for more bytes.

Cast types using `float_sum = (float)sum`

## 2. Printf and scanf
Use `#include <stdio.h>`

Set precision with `%m.d` where m is the minimum size of the field and d the decimal digits
![[Pasted image 20240902172442.png]]

While for scanf
![[Pasted image 20240902172618.png]]

## 3. Conditions
![[Pasted image 20240902172844.png]]
here `&eta` should be `&age`, but observe that age is not a pointer. In fact, scanf needs the address of the value, but it is not necessary for it to be a pointer.



Switch can be used
![[Pasted image 20240902172809.png]]



# 2. Loops and Arrays

## 1. Loops

![[Pasted image 20240902173321.png]]
An example of for
![[Pasted image 20240902173430.png]]
An example of while reading from terminal
![[Pasted image 20240902173535.png]]

Example of do-while
![[Pasted image 20240902173710.png]]
Reads positive integers from the keyboard, until a negative one is read. Beforehand, it is impossible to know how many values will be read, but at least one will be read, thus we use do-while.


## 2. Arrays

It is a simple data structure that allows you to keep in memory a *prefixed number of elements*, all having the *same type*.

![[Pasted image 20240902174028.png]]
Note the use of CURLY BRACKETS!

Do not access values outside the memory, it will cause segmentation fault.

Example
![[Pasted image 20240902174120.png]]

Example. Reads 7 integers from the terminal and prints them in reverse order.
![[Pasted image 20240902174324.png]]








# 3.  Functions, Stack and Visibility

## 1. Functions

They must be declared before main, but can be defined later.
![[Pasted image 20240902174456.png]]

Example
![[Pasted image 20240902174756.png]]







# 4. Pointers and Memory allocation
## 1. Pointers

## 2. Memory allocation


## 3. Pointers and functions



# 5. User-defined types
## 1. Bidimensional arrays

## 2. User data types

## 3. Concatenated lists



# 6. Libraries and strings
## 1. Libraries


## 2. Strings



