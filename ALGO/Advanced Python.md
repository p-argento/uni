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

