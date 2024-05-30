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


