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

## tqdm
It is an external library.
If we are processing a very long loop, how do we know everything is working fine and the loop is not stuck?
The first solution is the print, say every 100 iterations.
The second solution is tqdm, which looks very professional.

```python
from tqdm import tqdm
l = list(range(100000))
for _ in tqdm(range(10000)):
	l.sort()
```

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

## Other generators
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

## String formatting
```python
'{name} ha {age} ed è alto {height:.2f}'.format(name=name, age=age, height=height)
```

This was for previous versions.

```python
f'{name} ha {age} ed è alto {height:.2f}'
```

This is the right way in the last version of python.


## Using zip()
![[Pasted image 20240427190242.png]]

