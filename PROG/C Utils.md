# 0. UNIX
...



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
Note the use of *CURLY BRACKETS*!

Do not access values outside the memory, it will cause segmentation fault.

Example
![[Pasted image 20240902174120.png]]

Example. Reads 7 integers from the terminal and prints them in reverse order.
![[Pasted image 20240902174324.png]]

> In C, the name of an array (e.g., A) represents a pointer to its first element. So when you pass an array to a function, you’re actually passing the address of the first element of the array. If you have `A[3]`, passing A to a function is like passing `&A[0]`. Technically, the pointer itself is passed by value.

![[Pasted image 20240902182025.png]]

*ATTENTION*
![[Pasted image 20240902183533.png]]
If the array was not in the heap, it would have been deallocated after the function activation (losing the Activation Record).

# 3.  Functions, Stack and Visibility

## 1. Functions

They must be declared before main, but can be defined later.
![[Pasted image 20240902174456.png]]

Example
![[Pasted image 20240902174756.png]]

> in C you CANNOT define functions within other functions

## Visibility rules
... easy

## Stack
**Activation of a Function** means calling a function, this Involves: creating a new stack frame (activation record AR, including the space for the return values), passing arguments, executing the function code, handling the return, and cleaning up.






# 4. Pointers and Memory allocation
## 1. Pointers

![[Pasted image 20240902181727.png]]

![[Pasted image 20240902181848.png]]






## 2. Memory allocation

C has primitives to control the dynamic allocation of memory  Incluse in stdlib.h

MALLOC
Type casting the void * returned by malloc to int * ensures that the pointer is treated as a pointer to an integer.
![[Pasted image 20240902182420.png]]
![[Pasted image 20240902182514.png]]

CALLOC
• calloc stands for “contiguous allocation.” It allocates memory for an array of num elements, each of which is size bytes long.
• Unlike malloc which allocates garbage, calloc initializes the allocated memory to zero.
![[Pasted image 20240902182625.png]]

REALLOC
![[Pasted image 20240902182714.png]]

FREE
![[Pasted image 20240902182741.png]]

*ALWAYS USE FREE() even inside functions to avoid memory leaks*






## 3. Pointers and functions
Parameters in C are usually passed by value.



# 5. User-defined types
## 1. Bidimensional arrays

![[Pasted image 20240902183735.png]]


## 2. User data types

![[Pasted image 20240902184017.png]]

![[Pasted image 20240902183913.png]]

Size of a struct is the sum of the sizes of its primitive data.

NESTED STRUCTS use pointers to know the sizeof elements
![[Pasted image 20240902184239.png]]

Also struct can be dynamically allocated:
![[Pasted image 20240902184329.png]]

TYPEDEF
![[Pasted image 20240902184359.png]]
Which means
![[Pasted image 20240902184419.png]]



ENUM
![[Pasted image 20240902184513.png]]

## 3. Concatenated lists

![[Pasted image 20240902184539.png]]
![[Pasted image 20240902184606.png]]






# 6. Libraries and strings
## 1. Libraries

![[Pasted image 20240902184630.png]]

![[Pasted image 20240902184717.png]]

![[Pasted image 20240902184734.png]]



## 2. Strings

TLDR
In C, a string is essentially an array of characters ending with a special character called the null terminator ('\0'). This null terminator is used to indicate the end of the string.

string on stack
```c
char str[] = "Hello";
str[0] = 'J'; // Now str is "Jello"
```

string on heap
```c
char *str = (char *)malloc(6 * sizeof(char)); // Allocate memory for 5 characters + null terminator
strcpy(str, "Hello");
str[0] = 'J'; // Now str is "Jello"
```

(NOT A STRING) a string literal, also constant string is
```c
char *str = "Hello"; // add const as best practice
```










![[Pasted image 20240902184814.png]]

CONSTANT Strings CANNOT be modified.
![[Pasted image 20240902184853.png]]

![[Pasted image 20240902184919.png]]



![[Pasted image 20240902185019.png]]

To include also *white spaces*, instead of scanf
![[Pasted image 20240902185104.png]]

Manipulating stings
![[Pasted image 20240902185149.png]]

USE FUNCTIONS IN string.h
![[Pasted image 20240902185213.png]]
![[Pasted image 20240902185226.png]]


STROK
![[Pasted image 20240902185250.png]]
![[Pasted image 20240902185304.png]]
![[Pasted image 20240902185311.png]]





