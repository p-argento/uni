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

## 6. Hashing
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

## 7. Heap
The Heap solves the "Priority Queue" Problem.
We want to support the following operations
1. Insert(S,k) -> insert key k in S
2. Max(S) -> return the largest key in S
3. ExtractMax(S) -> remove the largest key

Solutions
1. (trivial) unsorted array
2. (trivial) sorted array
3. heap
![[Pasted image 20240531165413.png]]

Note that
1. the heap is an implicit data structure, because it is an array that can be seen as a complete binary tree. 
2. the level L has $2^L$ nodes, starting from 0 and excluded the last level that may not be completed
3. the height of the tree is $log_2 n$

Calculate
1. `Parent(i): return floor(i/2)`
2. `LeftChild(i): return 2i`
3. `RightChild(i): return 2i+1`

The main property is the (Max) Heap Property, meaning that $\forall node\ i, A[parent(i)]\geq A[i]$, the parent is never greater than its children.

The consequence is that the max is at the root, so `Max(A): return A[1]`

How to maintain the property? We use the function `MaxHeapify(A,i)`. Calling it on node i means that we assume that both children of i are the roots of valid MaxHeaps. This assumption is VERY IMPORTANT: in MaxHeapify, we only want to fix i, making sure that its two children respect the property of being not bigger than the parent. In the code, MaxHeapify stops when `largest=i`, otherwise swap and call recursively on largest, checking if now the position of the value inserted is okay. The time in the worst case is the height of the tree, which is logn.

How to build a heap? Just apply MaxHeapify to an unordered array. A sorted array is already a valid heap, but we can do better than sorting in nlogn.
```
BuildMaxHeap(A):
	for i = floor(|A|/2) down to 1
	MaxHeapify(A,i)
```
We start the loop from the parent of the last leaf, which in real code is `floor((A.len-1)/2)` because it is zero-based.
It looks like there are n iterations of cost logn, but actually we observe that in the lower levels there are more nodes but the cost is cheaper and viceversa. So, it is actually linear.

Extract-Max(A) consists of
1. `swap(A[1],A[|A|])`
2. `remove(A[|A|])`
3. `Heapify(A,1)`
The complexity is logn.

IncreaseKey(A, i, key).
1. first 



## 8. BST
