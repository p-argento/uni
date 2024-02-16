[FRANGIONI_interior-point-article](OP/docs/FRANGIONI_interior-point-article.pdf)

# 1. Introduction

Outline.
1. introducing
2. formally stating general optimization problem
	1. and show specializations of the framework for linear SVM (and Huber Regression)
3. describing interior-point method
	1. and linear algebra requirement
	2. use of block eliminatio for exploit problem structure
4. implementation of linear algebra using out of core calculations
	1. and numerical consi
5. experimental results for several linear SVM formulations
	1. on two large datasets
6. summarizing


# 2. Quadratic Programming Framework

> "The general optimization problem we consider has a quadratic term consisting of a low-rank update to a positive semidefinite matrix and a small number of linear constraints."

**Quadratic Term**
The function to be optimized (or objective function) has quadratic terms, meaning square of variables.

**Low-rank update**
Low rank means that is a matrix with few independent rows or columns.
A low-rank update means making a small change to a matrix in a way that doesn't alter its rank much.
If $A$ is the original matrix, a low-rank update using the matrix $B$ means adding or subtracting a multiple of $B$ to $A$. If $\alpha$ is a small scalar, it looks like $A+\alpha\cdot B$.

**Positive-semidefinite matrix**
It is a matrix with all eigenvalues >= 0 (or non-negative).
It satisfies the condition that, for any vector $x$, the quadratic form $x^TAx$ is non-negative.

**THE PROBLEM**
In the article, it is written as: $$Q=S+RHR^T$$
Typically
- $S\in R^{m\times m}$ is a very large symmetric positive semidefinite (the original matrix)
- $H\in R^{k\times k}$ is a small symmetric positive definite 
- $R\in R^{m\times k}$ 

The convex problem is $$min$$
Its dual form is $$dual$$
Once the dual problem are solved, the hyperplane in the primal problem can be recovered as follows: $$w=A^TDx\qquad\gamma\ is \ the \ multiplier\ on \ e^TDx=0$$

There are many other formulations of the problem reported, each one with its own dual. However, the interior-point method can be applied to any of them, because the duals are in the class of problems considered.

# 2. Huber regression
skipped

# 3. Interior Point
