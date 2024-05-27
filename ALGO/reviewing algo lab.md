Outline
1. lab_1: basic sorting
	1. selection sort
	2. insertion sort
	3. strange sorting
	4. insertion sort with a comparator
	5. intersection of two lists
	6. faster intersection of two lists
	7. search engine
2. lab_2
	1. binary vector
	2. quicksort
	3. mergesort
3. lab_3
	1. activity selection
	2. fractional knapsack problem
4. lab_4
	1. k-largest elements with sorting
	2. k-largest elements with quickselect
	3. k-largest elements with heap
	4. distinct elements
	5. pareto frontier
5. lab_5
	1. open addressing with linear probing
	2. hashing with chain
	3. dictionary
6. lab_6
	1. groupBy
7. lab_7
	1. static sorted map
	2. binary search tree
8. lab_8
	1. strongly connected components (kosaraju)

4h
- 1h sorting (1, 2)
- 1h (3,4,5,6)
- 1h bst and graph (7,8)

## Sorting

Selection sort $\Theta(n^2)$
For every element, it iterates on the remaining array updating the min, then swap with the element of the first iteration.

Insertion Sort. $\Theta(n^2)$
For every element, it iterates over the previous elements to find correct position of the element, then swap with the element in that position.

QuickSort.
For every iteration
1. choose a pivot randomly and place it in the end of the subarray
2. scan the subarray once and if element is smaller than the pivot, swap with the last element in position m and increase m
3. swap pivot with element in position m
Do it recursively on left and right, leaving alone the pivot, which is already in its correct position. No merge is needed.

MergeSort.
It is the opposite logic of quicksort.
After the split, merge the two subarrays using a simple merge of sorted lists that keeps the sorting.
Do it recursively.


*check search engine*



2. lab_2
	1. binary vector
	2. quicksort
	3. mergesort
ok


1. lab_3
	1. activity selection
	2. fractional knapsack problem

ok

1. lab_4
	1. k-largest elements with sorting
	2. k-largest elements with quickselect
	3. k-largest elements with heap
	4. distinct elements
	5. pareto frontier



1. lab_5
	1. open addressing with linear probing
	2. hashing with chain
	3. dictionary

ok

1. lab_6
	1. groupBy

maybe a list comprehension can improve it, but looks fine

1. lab_7
	1. static sorted map
	2. binary search tree

ok

1. lab_8
	1. strongly connected components (kosaraju)

