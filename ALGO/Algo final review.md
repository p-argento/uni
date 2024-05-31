From [classroom](https://classroom.google.com/u/1/w/NjYxNTg1NzIyODc1/t/all), let's review all the topics.

## Outline
1. Analysis of Algorithms
2. Mergesort
3. Quicksort
4. LowerBound
5. Sorting in Linear Time
6. Hashing
7. Heap
8. BST
9. Tree
10. Graph

(and python best practices)

The first 5 are in [[Sorting]].

## 1. Analysis of Algorithms

Simple sorting algorithms

| name        | SelectionSort                                                   | InsertionSort                                 | BubbleSort                                  |
| ----------- | --------------------------------------------------------------- | --------------------------------------------- | ------------------------------------------- |
| description | move to the beginning the min on the subarray at each iteration | move each number back to its correct position | compare with the previous and swap if lower |
| complexity  |                                                                 |                                               | n2                                          |

Properties
1. loop invariant
2. stability
3. 

How to prove the correctness of algorithms?
Use a loop invariant, that is a property that is valid for each iteration of the algorithm. It must be valid before the loop (initialization), after every iteration (maintentance), after the loop (termination). For example, in Insertion Sort, `A[1,...,j-1]` is sorted always sorted.

Stability of an algo means that equal values maintein their relative order.

...

## 5. Hashing
It solves the dictionary problem.
We want to implement the following operations:
1. insert(s,k) -> adds key k to set s
2. delete(s,k) -> removes key k from set s
3. lookup(s,k) -> true if k in S

There are 3 solutions
1. (trivial) direct access table
	1. constant time operations, but $\Theta(|U|)$ space
2. hash table with chaining
3. hash table with open addressing

A good hash function is one that spread the keys on the table.
A reasonable class of functions is:
$h(k)=(ak+b\%prime)\%|T|)$ where $a,b$ chosen at random at the beginning and stored to reuse the function.

The load factor is $\alpha=\frac{|S|}{|T|}$.
It is the expected number of keys per slot.
Lookup and delete takes $O(1+\alpha)$ in expectation.

Values in open addressing can be
1. a key of s
2. none
3. `deleted`

Open addressing uses probe sequences.
1. linear probing
	1. $h(k,i)=(h'(k)+i)\%|T|$
	2. very cache friendly
	3. however clusters might merge creating long runs of entries
2. quadratic probing (used by python dict)
	1. $h(k,i)=(h'(k)+c_1i+c_2i^2)\%|T|$
	2. $c_1i$ is to be cache friendly by staying local
	3. while $c_2i^2$ is to move away avoiding merging of clusters
3. double hashing
	1. $h(k,i)=(h'(k)+ih_2(k))\%|T|$
	2. no local anymore