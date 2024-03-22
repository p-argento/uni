## LIsts vs Sets
Set are much faster.
Sets can be used to return multiple values from a function. Even different types.
## Unpacking Tuples
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
## Use of Underscore
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

## Why do we use immutable objects?[¶](http://localhost:8888/lab/tree/L02-Python-DataStructures.ipynb#Why-do-we-use-immutable-objects?)

- Immutable objects are **thread-safe** (means being able to run on multiple code at the same time) so you will not have any synchronization issues.
- It is guaranteed that functions or classes cannot modify the object.
- Immutable object are easier to cache.
- The internal state of your program will be consistent even if you have exceptions.
- Immutable objects are good Dictionary keys and Set elements. Have you ever ask yourself why a list cannot be a key in a dictionary?

**Immutability can have a performance cost**, since when an object cannot be mutated we need to copy it if we want to write to it.