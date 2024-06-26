# Analysis of algorithms
## The Sorting Problem
Input: sequence `A[1,n]` of n elements
Goal: permutation `A'[1,n]` of A (without creating a new element) such that $$A'[i]\leq A'[i+1]\qquad\forall i\in[1,n-1]$$All the books about algorithms are 1-based (NOT 0-based like python). Keep this in mind when turning pseudo-code into real-code.

What is the idea for ordering a vector?
Never use an external number to replace a number which was supposed to be removed. It is a patch and it is wrong.
Swap the number to be removed with the last one and remove the last one.

> Try to implement a sorting algorithm with the min.

Instead of creating a new array, it is a better idea to divide the array in sorted and unsorted sub-arrays. Each time a min is computed, the number goes to the left and the index of the unsorted sub-array is increased by 1 (started from 0).
This algorithm is called *selection sort*.

Iterating the array n times and swapping each time the consecutive element if smaller. It is called *bubble sort*. Never use this, it is one of the worst.

Another approach is place each number in its correct position. Start with a one-number array and increasingly add items in the right position. This is *insertion sort*.

--21.02.24--

The complexity of an algorithm is the number of steps required in order to find a solution.

## Properties of Algorithms
Properties
1. in-place
2. correctness
3. stability

*In-place.*
It is an "in-place sort", meaning that modifies the original array.
It doesn't need extra space for creating a new array.
We process the array and when the i-th term is not sorted, it will be moved backwards to its correct position, comparing with each antecedent until we found the smaller or equal.

Pseudocode.
i is the antecedent, j is the item to be moved.
```pseudocode
InsertionSort(A)
	for j=2 to length
		key = A[j]
		// insert key in already sorted A[1,i-1]
		i = j - 1
		while i > 0 and A[i] > key
			A[i+1] = A[i]
			i = i - 1
		A[i+1] = key
```

> Always simulate. Design an example and run the algorithm step by step. I strongly encourage you to try more examples.

Running Example.
> Do not believe in comments. You must simulate.


Let's prove the *correctness of this algorithm*.
There are no automatic tools to check correctness,  we must use a proof.
"unit testing" means defining some examples, especially with marginal cases like empty array. The larger the set for testing is, the better is the confidence in the correctness of the algorithm.

We can use a "loop invariant".
1. find a property which is valid for every iteration of the algorithm.
2. using this property you should be able to check correctness.
3. the goal is to prove that after the loop the array is sorted.
Definitions
1. loop invariant: a property that holds for every iteration of the algorithm
2. initialization: the property holds before the loop starts
3. maintenance: the property holds after every iteration
4. termination: the property holds after the loop terminates

Loop invariant for Insertion Sort.
At iteration j, `A[1,...,j-1]` is sorted.

Idea of *stability*.
1. if we look at the array before and after being sorted, and we focus on different occurrences of the same values, then those occurrences preserve their relative order
	1. $...n_1...n_2...n_3... \rightarrow ...n_1n_2n_3...$

## RAM Model
What does it mean? It means finding a mathematical formula which is able to tell us how many steps the algorithm requires. What does a step mean?
We need to agree on a *computer model* that should be
1. simple enough to make analysis possible
2. precise enough to give meaningful analysis
There a lot of computational models, each one analysing a different aspect like memory. We focus on the easiest, which is called RAM Model.
It allows to remove algorithms that are very inefficient. But to compare two algorithms that looks efficient, the only way is testing.

*RAM Model*
CPU takes data from a memory. Afterwards the result will be stored again in memory.
In our model, all the operations have the same cost (like sum and square root) and access from memory has always the same cost. But in real life this is far from being true.
Then, there are registers (increasingly bigger):
1. CPU registers of memory
2. L1 cache (KB)
3. L2 cache (MB)
4. L3 cache (MB)
5. RAM (GB)
6. Disks (TB)
Accessing data in different registers costs differently, increasingly more expensive.
CPU performs operations between (at most 2) values in memory and saves the result back in memory.

What are the *operation* the CPU is allowed to perform?
Set of elementary operations: $+, -, *, /, \sqrt{}, log, \lceil\ \rceil, \lfloor\ \rfloor, and, or$
The cost of any operations is 1.
But remember that this is irrealistic because $\sqrt{}$  cost is much more than $+$
## Analysis of Insertion Sort
*Constant* means independent of the size of the input. But depends on the machine.
How many times are we executing every constant instruction?
In general, we evaluate a loop condition one time more (when we stop and do not enter the loop).
f(n) is the worst case , among all possible inputs, meaning the worst possible input for the algorithm.
Remember that this type of analysis can be problematic, because most cases can be actually efficient, and the worst case can be marginal.

The magic formula is $cost\times times$
But cost is constant, meaning that depends on the computer.

> try to calculate the f(x) of insertion sort for some arrays.
> What is the best case? What is the worst case?


Being a single line doesn't mean constant operation.
For example, `if 10 in array` costs the length of array.

*What is the running time?*
```pseudocode
InsertionSort(A)
	for j=2 to length
		key = A[j]
		// insert key in already sorted A[1,i-1]
		i = j - 1
		while i > 0 and A[i] > key
			A[i+1] = A[i]
			i = i - 1
		A[i+1] = key
```
$$\displaylines{T(n)=\\
=C_1n+C_2(n-1)+C3(n-1)+C_4\sum_{j=2}^nt_j+C_5\sum_{j=2}^n(t_j-1)+C_6\sum_{j=2}^n(t_j-1)+C_7(n-1)}$$
This is the complexity, the running time.
We always want an overestimation.
But the goal is not giving an estimation of the running time of an algorithm.
The main goal is to compare two solutions. And with this formula is quite hard to compare. Let's try to simplify, by approximating stuff, keep in mind that we want to overestimate.

We declare that there is a $C\geq C_i$ so that $$\begin{align}
T(n)&=Cn+3C(n-1)+C\sum_{j=2}^N+2C\sum_{j=2}^N(t_j-1) \\
&=3C\sum t_j+4Cn-3C
\end{align}$$In bubble sort, we do n iterations, but the cost of swapping is constant. Does the running time depends on the (different) input? No, because it depends only on n and not on swapping or not. The array must be scanned anway.
How can we compare this bubble sort idea with the $T(j)$ of insertion sort? It is still difficult because we do not have $t_j$ in bubble sort.

What we want is the worst time possible. Now, we have one single target.
Observe that $T(n)$ depends on the particular input we use because of $t_j$s.
If we know the typical $t_j$ of your application, you can fix it and calculate.
Otherwise, we use best case and worst case.

*1. Best Case: already sorted*
$t_j=1$ because it is number of times we were evaluating the while loop.
With this fixed input, $$\begin{align}
T(n)&=3C\sum t_j+4Cn-3C \\
&=3Cn+4Cn-3C \\
&=7Cn-3C
\end{align}$$This is a linear function, so the running time of the function is linear.
**Linear time** are really good, in sorting you cannot do better than linear time.
Of course, we must check the array at least once.

*2. Worst Case: reverse order*
> There could be many different worst cases, try to find the easiest

$t_j=j$ because every time we enter is $j-1+1$.
Now, we simplify the formula with the fixed $t_j$ $$\begin{align}
T(n)&=3C\sum t_j+4Cn-3C \\
&=3C\sum_{j=2}^nj+4Cn-3C \\
&=3C(\frac{(n+1)n}2-1)+4Cn-3C \\
&=\frac3 2C(n+1)n+4Cn-6C \\
&=\frac3 2Cn^2+\frac3 2Cn+4Cn-6C \\
&\approx\frac3 2Cn^2
\end{align}$$We used the formula for the sum of N natural numbers (called Gauss formula?)
$$\sum_{j=1}^nn=\frac{(n+1)n}2$$And selected the dominant term in the last step, because we are interested in large input sizes because those are the inputs that can make the algorithm unfeasible. This means that the algorithm runs **Quadratic Time**.

Now, we can compare algorithms, without using many different constants for being precise. It was impossible.

*A better approach*
Is there an easier way avoiding all these calculations?
Yes.

## Order of growth
Large enough input means $$\lim_{n\rightarrow\infty}f(n)$$*Idea*.
1. forget about lower order terms
2. forget about constants factors
It means that we can do $$\begin{align}
T(n)&=\frac3 2Cn^2+\frac3 2Cn+4Cn-6C \\
&\approx\frac3 2Cn^2 \\
&\approx n^2
\end{align}$$In every algorithm we use a different factor.
This is enough most of the time to compare efficient vs inefficient algorithms.
This is true for large enough input size.
For example, every quadratic algo is slower than any linear algo.

We will use the *notation*$$\begin{align}
T(n)&=3C\bigg(\frac{(n+1)n}2-1\bigg)+4Cn-3C \\
&=\Theta(n^2)
\end{align}$$
Most useful functions in growing order.$$\begin{align}
&\Theta(1) \\
&\Theta(log\ n)=100\ log\ n+3 \\
&\Theta(n\ log\ n) \\
&\Theta(n^2) \\
&\Theta(n^3)
\end{align}$$It is not possible to sort an array in $\Theta(log\ n)$ because it is less than $\Theta(n)$ which is the minimum to check every element of the array.

If you compare two linear time algos, it might be useful to compare also constant factors.

*Time considerations*
If you have logn, it means that there was a preprocessing on the input data.
If you have a linear time algo, it is a super good algo that will finish pretty soon.
If you have nlogn, it will be fast, because logn is small.
NOTE that a nlogn might be faster than n because the constant factor in the linear can be bigger than the (usually) small value of logn.
If you have quadratic, it might take years if n is bigger than one million.
If you have a cubic, it will work only for small n.


> Try to analyze selection sort by yourself



--27.02--
1. analyzing selection sort
2. designing algorithm
3. optimal sorting algorithm


Scanning an array takes $\Theta(n)$ time.
There are two possibilities:
1. scan over elements
2. scan over indexes (better because more general)

If the goal is to compute the sum(A) where `A[1,n]`
```pseudocode
s=0
for e in A: # c(n+1)
	s += e # c(n)
```
$T(n)=2cn+c=\Theta(n)$

In a simpler way.
1. number of time we iterate
2. cost of each iteration
Because we need only the bigger term.

$Log\ n$ is usually around 32.
$n^2$ is really slow already at 100,000
$n^3$ usually unfeasible, unless very efficient for most of the inputs.


## Analysis of Selection Sort 

The idea is check for the smallest and move it in front of the array.
Now the prefix of the array contains the sorted array.

At each iteration i, find the min in the suffix `A[i,n]` and say its position is j.
Swap `A[i]` and `A[j]`.

```pseudocode
SelectionSort(A):
	for i: 1 to A.length
		min_pos = i
		for j: i+1 to A.length
			if A[j] < A[min_pos]
				min_pos = j
		swap(A[i], A[min_pos])
```
Why computing the min in this way? Because I need the index and because I want to inizialize it with an element of the array.

Properties we want
1. inplace
	1. we are sorting the array without using extra space 
2. stable
	1. if two identical values keep the order in the final array
Selection sort is inplace, but NOT stable.
To prove that is not stable is enough to provide a counterexample like `A=[551]`.

How to check correctness?
Carefully design a set of test. Marginal cases included.

Let's analyze the complexity of Selection Sort
```pseudocode
SelectionSort(A):
	for i: 1 to A.length // c(n+1)
		min_pos = i // c(n)
		for j: i+1 to A.length // sum n times of c(n-i) 
			if A[j] < A[min_pos] // sum n times of c(n-i-1)
				min_pos = j // cost dominated by if
		swap(A[i], A[min_pos]) // c(n)
```

$$T(n)=3cn+2\sum_{i=1}^N c(n-1)=n+\frac{n(n-1)}2=n^2+... \Longrightarrow\Theta(n^2)$$
The running time is quadratic regarding the input. So, it is both best and worst case.
Why? There is nothing depending on the input in the final formula (i disappeared).
This is very bad. No matter what, the time is very slow.
While for insertion sort, the best case was linear (or close to linear).
When the input is quite small or the input is almost sort, even python libraries use insertion sort. Nobody uses selection sort.

## Shorthands for analyzing
The hard part is to analyze loops.
Be careful with the difference between parallel and sequential loops.
The trick is starting from the most inner thing and then go to the outer.

If the inner loop is `for j: i to n` it is not better than `1 to n`, it is still quadratic because of the gauss formula. See Selection Sort analysis.

> The most important thing of the course is to avoid parallel loops.

*Exercise*
Write a function to compute the distinct elements in a list A.
```python
def DistinctPythonic(A):
	list(set(A)) # this is the most pythonic way

def Distinct(A):
	B=[]
	for e in A:
		if e not in B: # here there is an hidden loop
			B.append(e) 
	return B
```
$$T(n)=\Theta(n^2)$$
Solve the same assuming A is sorted.
```python
def Distinct(A): # there is a bug
	B=[]
	for e in A:
		if e not in B[-1]:
			B.append(e) 
	return B
```
It is enough to check the last element of B because B is sorted.
Now, the running time is linear.
But append does not always cost constant time. It is not fully correct.



# Merge Sort

## Recursion
It solves a problem on calling itself for smaller functions.
```pseudocode
f(n)
if n<=1 return 1 // base case
return n*f(n-1) // call the function on a smaller problem
```
"Smaller problem" is required for termination, meaning reaching the best case.
This is the function for n factorial.

```python
def Fib(n):
	if n==0 : return 1
	if n==1 : return 1
	return Fib(n-1)+Fib(n-2)
```
This is not the best way to do it.
It is much better to use an array and sum previous two numbers. This is linear.
While recursion is very inefficient, in particular is $\geq2^n$.
Since there are two calls, this generates a binary tree.

Why using recursion? Because we want to solve a smaller function.
But in Fib function, we just remove one step from the bigger function, so the recursion is not effective. But in mergesort we split in two equally big functions, meaning that the new smaller functions are both much smaller than the bigger one.

> The second exercise is trivial if you know recursion. It can be solved in less than a minute.

## Divide and Conquer
Three main steps
1. divide
	1. divide the problem into a number of sub problems that are smaller instances of the main problem
	2. in Fib `n-1` and `n-2` is the divide step creating sub-instances
	3. difficult to define
2. conquer
	1. solve the sub-instances by calling the function recursively
	2. in Fib is just the call `Fib()`
	3. most of the time is just calling the function
3. combine
	1. combine the solutions of the subinstances to get the solution of the original instances
	2. in Fib is the sum `+`
	3. difficult to define

## MergeSort Algorithm
An optimal sorting algorithm, meaning that you cannot do better.
It use the Divide and Conquer paradigm. Many useful algos follow this approach..
It runs in $\Theta(nlogn)$ time.

Divide and conquer steps.
1. divide
	1. we need to divide an n elements array into sub-instances
	2. the most reasonable way to split is in the middle
2. conquer
	1. sort the two parts recursively
	2. best case? stop if $n\leq1$
3. combine
	1. each recursive call get just two results
	2. merge the two now sorted sub-arrays
	3. how to merge? just compare each time the first elements of the sub-arrays and add the min to the final array (use i and j)
		1. if equal, take the first to guarantee stability

Example of merge with `A=[2,4,5,7]` and `B=[1,2,3,6]`.
In the pseudocode, we use sentinels, meaning that when we reach the end of one of the two arrays, we set the sentinel of that array as $+\infty$ and keep comparing.
In python, we will create another loop.

We create a temporary copy of the array for storing sorted sub-array.
Then we will overwrite the original array with the sorted one.

```pseudocode
Merge(A,p,q,r)
	n1 = q - p + 1
	n2 = r - p
	// let L[1...n1+1] and R[1...n2+1] be new arrays
	for i = 1 r to n1
		L[i] = A[p + i - 1] // copying into temp array
	for i = 1 to n2
		R[i] = A[q + i] // q is the last element of the first part
	L[n1 + 1] = +inf
	R[n2 + 1] = +inf
	// start copying
	i = j = 1
	for k = p to r
		if L[i] <= R[j]: // <= needed for stability
			A[k] = L[i]
			i = i + 1
		else
			A[k] = R[j]
			j = j + 1
	
```

`-1` sometimes is necessary because pseudo-code is 1-based, not 0-based.
In the definition of L and R, we add +1 because we need space for the sentinels.
In the second loop, we do not need -1 because q is the last element of the first part.

> find the bug: <=

> On friday, lab about insertion and selection sort.
> Next week we analyze algos

## MergeSort in LAB

`assert test_sortedness( SelectionSort(my_list) ), "Must be increasing!"`  
It is useful because it tells you what's wrong. It checks the condition, if false the program terminates and print the error. Use reasonable assertions is a best practice.

> Always write more tests, at least 3,4

You can write a customized comparator.
It is useful for example to reverse order of sorting.
In addition, it is possible to sort using a library function and apply your comparator.

```python
# for sorting in decreasing order
def my_cmp(a, b):
if a > b: return -1
return 1

# shorter version and better because returs zero if same
def my_cmp(a, b):
return b-a # a is before if larger that b
```

> lambda function is an inline function without name and return

```python
import functools

print( sorted(list(range(10)), key=functools.cmp_to_key(my_cmp)) )
```
Remember this. It does the magic. Allows to compare keys using your comparator.

## More on MergeSort
The cost of merge is $\Theta(n1+n2)$.
The next part of the algo is the following.
We only care about the part from p(included) to r(not included).
```pseudocode
MergeSort(A,p,r)
	if p < r
		q = floor((p+r)/2)        // divide
		MergeSort(A,p,q)          // conquer
		MergeSort(A,q+1,r)        //
		Merge(A,p,q,r)            // combine
```

First, we compute the point in the middle.
The we call the function recursively, when we come back the first part is sorted and we have to sort the second part.

Everything is a side effect on the array itself. It in not copying or creating anything new.

> Be prepared to simulate MergeSort in the exam.

When you go down recursively, we are actually comparing the first two elements and sorting them, go the the third and forth, and so on.
Next, we deal we pairs, and sort the couples of pairs.
Each time the pairs are doubled.
How many layers are needed?
$$2^L=n\rightarrow L=log_2n$$
The number of elements is $log_2n$

Is MergeSort stable? Yes
Is MergeSort in-place? No, because Merge copy the two parts before merging.

![[Pasted image 20240530181823.png]]
## Analysis of Mergesort
Let's analyse mergesort.
No difference in input: $$worst case = best case$$

## Analysis of Recursive algorithms

A recurrence T(n) for the running time of a divide and conquer - based algo.
The running time is a recursive function itself.

It is the cost of dividing D(n) + combine C(n) + cost of calling the function on an input of size n (here two times because there are two recursive calls).
- $n/b$ is the size of the subproblem.
- $a$ is the number of subproblems
- $D(n)$ is the cost of dividing
- $C(n)$ is the cost of combining
$$
T(n)=\begin{cases}
O(1) \quad if\ n\leq c \\
aT(n/b)+D(n)+C(n)
\end{cases}
$$
In the specific case of MergeSort is 
$$
T(n)=\begin{cases}
O(1) \quad if\ n\leq c \\
2T(n/2)+O(1)+\Theta(n)
\end{cases}
$$
Can we write a script to compute the number of steps?
```python
def T(n):
	if n<=1: return 10
	return 2*T(n/2) + c*n
```

But this is not satisfactory. We want an easy way to compare algorithms.

Solve recurrences with recursion tree.
I am replacing T(n/2) with the definition.

![[Pasted image 20240530181922.png]]

The cost is the sum of all nodes.
In the case of MergeSort, just draw the tree with logn layers and sum all the nodes.
However, we observe that every level costs $C(n)$.
And then the overall cost is $$\Theta(n\cdot log\ n)$$
## Binary Search
The algo finds the position of a target value within a sorted array.
It is a good principle to divide the largest problem into balanced subproblems
It is the problem of indexing elements to answer queries.
The solution consists in storing elements in an array and keep the array sorted.
The query can be solved with binary search.
We need $log\ n$ comparisons.
It consists in going into the middle of the array and if the element in the middle is lower we can skip the first half and focus on the second.
> This is the power of sortedness.

```pseudocode
BinarySearch(A, p, r, key)
	if p > r return False
	if p = 2r return A[p] = 2*key
	q = ceiling((p+r)/2)                 // divide
	if A[q] == key return True           // doesn't change complexity
	if A[q] < key
		r = BinarySearch(A, q+1, r, key) // conquer
	else
		r = BinarySearch(A, p, q-1, key)
	return r                             // do not forget this return
```

> Always challenge your implementation. Try to return True, False, and marginal cases.
> Check if it is ceiling or floor by simulating the algorithm.

In binary search there is nothing to combine, but we have to report the result of the call.
When implementing a recursive function, in any point we terminate, we need to return something. 
ALWAYS return something in any termination of the function, included all the if and all the else and the real end.
> The second exercise is a divide and conquer on a binary tree. Do not forget to add a return for each termination.

There's nothing to combine here. We just get the result and report it.

Remember to alway have a best case. Or the recursion will run forever.

## Analysis of Binary Search
The running time is the sum of the cost of each node.
Like all the others recursive algos.

Every recursive algorithm can be translated into a loop.
But recursion is easier.

What is the time complexity
$$T(n)=\begin{cases}
O(1)\quad if\ n<c\\
aT(n/b)+D(n)+C(n)
\end{cases}$$
In BinarySearch
$$T(n)=\begin{cases}
O(1)\quad if\ n<c\\
1T(n/2)+O(1)+O(1) = T(n/2)+O(1)
\end{cases}$$
Combine is constant because is just the return.

Now, we need to use the recursion tree.
Just expand each node with the cost of the operation and the new call of the function.
Then we can generalize.
In this case, we have logn notes, each one with constant cost.
Then, the running time of Binary Search is logn.

The one on the right is a different algo. We call it stupid binary search.

![[Screenshot 2024-03-06 at 10.10.05.png]]

If the cost is not constant, we cannot multiply by logn but we have to sum each node.

Let's analyze a stupid binary search.

![[Pasted image 20240306102534.png]]


# Quick Sort

> Cormen 7.1, 7.2, 7.3

Still based on divide and conquer. As well as comparisons.
For MergeSort
1. divide in costant time
2. combine in linear time
In quicksort
1. divide in linear time
2. combine in constant time
We spend all our time on dividing.

We have a subarray to solve.
I want to partition the array based on a pivot.
Why the median is a great pivot? Because we want the subproblems to be balanced.
We would like to compute the median, but it is costly, so we choose it randomly.

## Partition algorithm
Will do on friday. When we will implement.
It runs in linear time.


## Pseudocode

```pseudocode
QuickSort(A, p, r)
	if p < r
		q = Partition(A, p, r)    // divide
		QuickSort(A, p, q-1)      // conquer
		QuickSort(A, q+1, r)      // conquer
		
		
```

QS is inplace.
QS in NOT stable because of the partition.

## Analysis of QuickSort
The max and the min of the array are not good pivot.
*Best case*
Every time the pivot is the median of `A[p...r]`
Meaning that we have (almost) n/2 on one side and n/2 on the other.
$$T(n)=\begin{cases}
O(1)\quad if\ n\leq1\\
2T(n/2)+\Theta(n)
\end{cases}$$
Meaning nlogn, since it is the same as MergeSort.

*Worst case*
If the pivot is the first or last element.
What is the recurrence?
There are two subproblems, one with one element and costant time, the other with n-1 element and linear time. We will spend a lot of time to make little progress.
$$T(n)=\begin{cases}
O(1)\quad if\ n\leq1\\
T(n-1)+\Theta(n)
\end{cases}$$

Basically, in the worst case, quicksort degenerates in selection sort, because it looks for the min every time in the whole array.
Then, the intuition is that the running time is the same of selection sort, meaning $\Theta(n^2)$.
We are spending linear time to gain just one element, meaning very little progress.

Let's build the tree. 
Formally, we have two subproblems, but one is constant because terminates immediately, so we skip it.
The worst possible problem is $T(n-1)$, it cannot be $T(n)$ otherwise we are not making any progress and the algo doesn't terminate.

![[Pasted image 20240306110857.png]]

Why do we care about QS? 
Because a combination of a good and a bad call is a good one.

## Quicksort Lab

![[Pasted image 20240308093421.png|400]]
So
- p = first element of the array to be partitioned
- r = last element of A
- i = last element of array with elements SMALLER than pivot
- j = first element of array with elements GREATER than pivot

![[Pasted image 20240308093435.png]]
In quicksort, first select a random element in the array for the array and move to the end position r.
If the function stops because of too many function calls, there is probabily a problem with the pivot.
When we swap the elements to move something into the light grey zone we loose stability.
If greater, means that stays in the dark grey zone, so we do not need to do anything.
If there are no dark grey, in the end, the pivot swap with itself.

![[Pasted image 20240308104355.png|400]]

*Algo comparison*
Insertion sort is quite efficient in the average case. But quadratic in the worst.
Selection sort is always quadratic.

```python
# this is a jupyter function
%%timeit function()
```

Why are we interested in efficiency?
![[Pasted image 20240308095309.png]]

*How to debug?*
1. prints
2. debugger
3. rubber duck


## Analysis of the average case for QuickSort
It is as good as mergesort in the best case and as bad as selection sort in the worst case.
Selecting a random pivot, the algo is nlogn with high probability.
In particular, the probability of being nlogn is $1-\frac1 n$ meaning that with the increasing of the size of the array will increase the probability, getting close to 1.

*Intuition for the average case*
![[Pasted image 20240317164135.png]]

![[Pasted image 20240317164156.png]]

If you want a formal proof, read it on the Cormen.


# Lower bound
We will prove that nlogn is the best you can hope, based that the algo is working by comparison.
> Typical question for the oral exam

Chapter 8 of Cormen

## Asymptotic Notation

![[Pasted image 20240317164215.png]]

![[Pasted image 20240317164232.png]]

## Lower Bound Proof for Sorting (with comparisons)
The algo is based on comparisons.

What is an alternative approach? Think about the cars, we can use ordered placeholders with cards numbers and using the value of the card to place it in the correct place. 

![[Pasted image 20240317164248.png]]
## Proof of lower bound

![[Pasted image 20240317164304.png]]

![[Pasted image 20240317164329.png]]


*Considerations*
For any algo and input size n, we can draw its decision tree.
Provided the the algo is based on comparisons.
The execution of the algo on an input is a root-to leaf path.
The running time is the length of the path.
The worst case is the longest path.
The best case is the shortest path.
$\Omega$(Height of the tree)

What are the priorities in an algo?
1. correctness 
2. efficiency
3. readability

What is the necessary correctness? Every possible permutation must occur at least once for the algo to be correct. Meaning that the number of leaves is $\geq n!$ , or with a different notation, $\# leaves = \Omega(n!)$

So there is no need to invent an algorithm to draw its dt.

Binary tree of height h as no more than $2^h$ leaves.
Where h is the height of the tree.
Proof
- base case $h=0, 2^0=1$ is the root
- inductive step
	- if true for h, prove it for $h+1$
At $h+1$ we have two nodes for each previous node, so $2^h\cdot h=2^{h+1}$

$2^h \geq n! \Rightarrow h \geq log_2n! \Rightarrow h=\Omega(nlogn)$
we used the Stirling approx for n!
![[Pasted image 20240603165704.png]]


*Main steps of this proof*
1. The main observation is that you can represent even non-existing algo based on comparison into decision tree. And this means changing the question. The height of the tree is the greatest running time.
2. Every leaf is a permutation. All the permutations must be in the leaves. There are at least n! permutations.
3. The height of the tree must guarantee at least n! permutations. Meaning that the number of leaves must be $2^h \geq n! \Rightarrow h \geq log_2n! \Rightarrow h=\Omega(nlogn)$

*What if the input array has duplicates?*
It can be sorted in less than linear time.
It is sufficient a counterproof.
For example a quicksort with a fixed pivot.


# Sorting in linear time
 This is NOT possible of course with comparison-based algo.
 But we will see an algorithm (Radix Sort) that can sort in linear time.

## Unstable Counting Sort
This is the building block of Radix Sort, that we will se next time.

Sort in linear time an array A with n integers, meaning `|A|=n`.
We are leaving comparison-based world and we are forced to sort integers.
If `max(A)=k=O(n)`, meaning that it is not too large.

Example.
`10,10 000,5` means `|A|=3` and `k=10 000`

Counting sort runs in $\Theta(n+k)$
$\Theta$ means that there is exactly a worst case with this time.

This is the only case where Cormen uses zero-based indexes.
Remember that we are sorting integers.

![[Pasted image 20240530180128.png]]

Is it inplace? NO
Is it stable? NO, but Radix Sort needs stability in the building block.

Let's write the pseudocode.
Then we will design a stable variant of counting sort.
2
```pseudocode
CountingSortUnstable(A,k)
	let C[0,...k] be a new array
	for i = 0 to k                       // Theta(k)
		C[i] = 0
	for i = 1 to A.len                   // Theta(n)
		C[A[i]] += 1
	j = 1
	for i = 0 to k                       // see below
		for occ = 1 to C[i]
			A[j] = i
			j += 1
```

The time of the two nested loops is
$$\sum_{i=0}^k(\#occ(i)+1)=k+\sum_{i=0}^k\#occ(i)=k$$

## Stable Counting Sort
```pseudocode
CountingSort(A,k)
	let C[0,...k] be a new array
	for i = 0 to k                    // theta(k)
		C[i] = 0
	for i = 1 to A.len
		C[A[i]] += 1                  // theta(n)
	for i = 1 to k
		C[i] += C[i-1]
	for i = A.len down to 1           // theta()
		B[C[A[i]]] = A[i]
		C[A[i]] -= 1
```
The time is $\Theta(n+k)$

It uses prefix sums (also called cumulative sums).
Array C              1,0,3,4,2
Prefix sums P   1,1,4,8,10
Meaning $P[i]=P[i-1]+C[i]$
But we'll use C, to transform C into the prefix sum of itself.
So `C[i]=C[i-1]+C[i]`
Note that starts from 1 because the first value remains the same.

In position i we are storing values smaller or equal to i.
But i is also equal to the index of the last occurence of i.
For this reason, we process the array C backwards.

![[Pasted image 20240530180153.png]]

![[Pasted image 20240603224933.png]]
## Radix Sort
Last lecture about sorting.

We said that Counting Sort runs in $\Theta(n)=\Theta(n+k)$ if $k\in O(n)$, because $c\cdot n$ with constant $c$.

You cannot increase the largest value too much, otherwise it will be slower.
With Radix Sort, we want to fix that.
Radix Sort runs in $\Theta(n)$ if $k\in O(n^c)$ for some constant c.
If for example c =4, it means that we can run in linear time for example for n=1000, meaning $c\cdot n=1000^4$ and we are okay for mostly all array of integers you are dealing with.

We are essentially using Counting Sort more times.

*Algorithm*

![[Pasted image 20240530180210.png]]

We actually need to start from the least significant digit.

![[Pasted image 20240530180225.png]]

*Proof of correctness*
There are 3 possible cases

|        | case 1 | case 2 | case 3  |
| ------ | ------ | ------ | ------- |
| digits | c < c' | c > c' | c == c' |
| c x    | c x    | c' y   | c x     |
| c' x   | c' y   | c x    | c' x    |
The first two cases are handled by the sorting of the digits.
The third case is because of stability.

It is so powerful because just sort the digits, without caring about anything else.
In the previous algo, the grouping was necessary to keep track of the previous iterations.


```pseudocode
RadixSort(A,d)
	for i =1 to d
		use a stable sorting algo to sort A on digit i
```

How many stable algo do you know?
1. InsertionSort  $\rightarrow\Theta(d\cdot n^2)$
2. MergeSort $\rightarrow\Theta(d\cdot nlogn)$
3. CountingSort  $\rightarrow\Theta(d\cdot (n+k))$

Which one to use?
MergeSort inside Radix Sort will be even worst than MS only. Remember that in MS, the worst case is equal to the best case. And it is comparison-based of course, and we want something linear.

In CountingSort, remember that $k$ is the largest number and $d$ is the number of digits in our number.
And this means the largest digit which is 9, with decimal representation of numbers.
So, with decimal representation of numbers, the running time is $\Theta(d(n+10))$ time.
If $d=11$, meaning billions, we have $\Theta(11(n+10))$ time.

*Cool intuition*
Note that there are two costs, one depending on n and the other depending on number of digits. So, we can increase the max number k to do less iterations d. 
In the example, $\Theta(11(n+10))\rightarrow\Theta(6(n+100))\rightarrow \Theta(3(n+10,000))$

How to balance?
It depends on n.

Let's formalize it.
> This is the second most difficult thing after the lower bound.

![[Pasted image 20240530180241.png]]

![[Pasted image 20240530180253.png]]


