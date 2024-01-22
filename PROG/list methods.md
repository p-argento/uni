The list data type has some more methods. Here are all of the methods of list objects:

## list.append(_x_)
Add an item to the end of the list. Equivalent to `a[len(a):] = [x]`.

## list.extend(_iterable_)
Extend the list by appending all the items from the iterable. Equivalent to `a[len(a):] = iterable`.

## list.insert(_i_, _x_)
Insert an item at a given position. The first argument is the index of the element before which to insert, so `a.insert(0, x)` inserts at the front of the list, and `a.insert(len(a), x)` is equivalent to `a.append(x)`.

## list.remove(_x_)

Remove the first item from the list whose value is equal to _x_. It raises a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError") if there is no such item.

## list.pop([_i_])

Remove the item at the given position in the list, and return it. If no index is specified, `a.pop()` removes and returns the last item in the list. (The square brackets around the _i_ in the method signature denote that the parameter is optional, not that you should type square brackets at that position. You will see this notation frequently in the Python Library Reference.)

## list.clear()

Remove all items from the list. Equivalent to `del a[:]`.

## list.index(_x_[, _start_[, _end_]])

Return zero-based index in the list of the first item whose value is equal to _x_. Raises a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError") if there is no such item.

The optional arguments _start_ and _end_ are interpreted as in the slice notation and are used to limit the search to a particular subsequence of the list. The returned index is computed relative to the beginning of the full sequence rather than the _start_ argument.

list.count(_x_)

Return the number of times _x_ appears in the list.

list.sort(_*_, _key=None_, _reverse=False_)

Sort the items of the list in place (the arguments can be used for sort customization, see [`sorted()`](https://docs.python.org/3/library/functions.html#sorted "sorted") for their explanation).

list.reverse()

Reverse the elements of the list in place.

list.copy()

Return a shallow copy of the list. Equivalent to `a[:]`.