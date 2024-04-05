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

## Function attributes
They are `__attribute__`.
The `__name__` for example can be used to show which task are executed during a pipelline, maybe in combination with tqdm. It looks very professional.

You can add your attributes to the functions.


## Lambda functions

next lesson on monday
