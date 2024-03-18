[J. Nocedal, S.J. Wright, Numerical Optimization](https://www.math.uci.edu/~qnie/Publications/NumericalOptimization.pdf)

> People optimize. Nature Optimize.

# Outline
---





# 1. Introduction
---
> What kind of problems are we studying?
> Continuous, Unconstrained, with Local solutions, Deterministic, mostly Convex.

## Continuous and Discrete
We can divide optimization problems in continuous and discrete.
The book focuses on *continuous* optimization problems.
They are "easier to solve because the smoothness of the function makes it possible to use objective and constraints information at a particular point x to deduce information about the function's behaviour at all points close to x.
In discrete problems, for example integer programming problems, the objective function's behaviour can change significantly going from one feasible point to another.

## Constrained and Unconstrained
Self-explanatory. We focus on *unconstrained*.
Remember that unconstrained problems arise also as reformulations of constrained problems. The constraints are replaced by penalization terms added to objective functions that have the effect of discouraging constraints violation.

## Global and Local
Many algorithms for nonlinear optimization seek only a local solution, because they are not alway able to find a global solution.
For convex programming problems, local solutions are also global solutions (see theorem later on). We treat *local* solutions.

## Stochastic and Deterministic
If some quantities are unknown at the time of the formulation, the model cannot be defined. They use the best guess for those quantities, coming from a number of possible scenarios.
We consider *deterministic* optimization problems, when the model is completely known.

## Convexity
Many practical problems posses this property.
> ... it's important but I'll skip it for now...

There are convex sets and convex functions.
Simple instances of convex sets are the unit ball and the polyhedron.
If the objective function and the feasible region are both convex, then any local solution is a global solution.

## Optimization Algorithms
They are iterative.
They begin with an initial guess of the variable x, generate a sequence of improved estimates (called iterates) and hopefully end with a solution.
The strategy from going from one iterate to the next is what makes algorithms different.
Most strategies make use of: objective function $f$, constraint functions $c_i$, possibly first and second order derivatives, sometimes information gathered at previous iterations.

# 2. Fundamentals of Unconstrained Optimization
---
## What is unconstrained optimization
In unconstrained optimization, we minimize an objective function that depends on real variables, with no restrictions at all on the values of those variables.
$$\min_{x}f(x)$$
where $x\in\mathbb{R}^n$ is a real vector with $n\geq1$ components and $f:\mathbb{R}^n\rightarrow\mathbb{R}$ is a smooth function.

*Key idea*.
Usually we lack a global perspective on the function $f$. All we know are the values of $f$ and maybe some of its derivatives at a set of points $x_0,x_1,x_2,...$.
The information about $f$ does not come cheaply, so we usually prefer algorithms that do not call for this information unnecessarily.
> No easy and known functions like in high school.

## What is a solution
The global minimizer can be difficult to find because our knowledge of $f$ is usually only local. Since our algorithm does not visit many points (or at least this is what we want), we usually do not have a good picture of the overall shape of the function.
Definitions of global, local, strictly local, isolated local minimizer.
It is usually difficult to find global minimizer of functions with many steep local minima because the algorithm tends to be trapped at local minimizers.
However, addition global knowledge of $f$ may help in identifying global minima.
And remember that in convex functions every local minima is also a global one.

## Recognizing a local minimum
It might seem that the only way to find out whether a point $x^*$ is a minimum is to examine all points in the immediate vicinity, to ensure that none of them has a smaller function value.
However, when the function $f$ is *smooth* there are more efficient ways.
If $f$ is in particular twice continuously differentiable, we can tell if a point is a minimizer by looking at :
- the gradient $\nabla f(x^*)$
- the Hessian $\nabla^2f(x^*)$

The mathematical tool to study minimizers of smooth functions is:
*Taylor's Theorem*
- The complete formula for twice continuously differential functions is the following, for $t\in (0,1)$:
$$f(x+p)=f(x)+\nabla f(x)^Tp+\frac1 2p^T\nabla^2f(x+tp)p$$
Then, there are important conditions that follows.

*First-order necessary conditions*
- If $x^*$ is a local minimizer
- and if $f$ is continuously differentiable in an open neighbourhood of $x^*$
- $\Rightarrow\nabla f(x)^*=0$

*Second-order necessary conditions*
- If $x^*$ is a local minimizer and $f$
- and if $\nabla^2f$ exists
- and if $f$ is continuously differentiable in an open neighbourhood of $x^*$
- $\Rightarrow\nabla f(x^*)=0$
- $\Rightarrow\nabla^2f(x^*)$ is positive semidefinite

*Second-order sufficient conditions*
- If $\nabla^2f$ is continuous in an open neighbourhood of $x^*$
- and if $\nabla f(x^*)=0$
- and if $\nabla^2f(x^*)$ is positive semidefinite
- $\Rightarrow x^*$ is a strict local minimizer of f

As mentioned, there is an important
*Theorem for convex functions*
- When $f$ is convex any local minimizer $x^*$ is a global minimizer of $f$.
- In addition, if $f$ is differentiable, then any stationary point is a global minimizer of $f$.

## Non-smooth problems
By smooth functions, we generally mean functions whose second derivatives exists and are continuous.
It is possible to find the minimizer of non-smooth funtions by minimizing each smooth piece individually.

## Overview of algorithms
In this section, we describe the main properties of algorithms for unconstrained optimization of smooth functions.

First. All of these algorithms requires a *starting point* $x_0$.
It can be either chosen by the user, for example using domain knowledge, or by the algorithm.

Second. After a series of iterations, the algorithm must *stop* when no progress can be made OR a solution point has been found with sufficient accuracy.

Third. How to move *from one iteration to the other*? The algorithm uses information about the function $f$ at the iteration $x_k$, together, in some algorithms, with information from previous iterates.
There are two fundamentals strategies to move from one iteration to the other:
1. line search
2. trust region

Note that "monotone" algorithms find a new iterate $x_{k+1}$ with a lower value of the function $f$. However, some algorithms are "non-monotone", meaning that they do not decrease at every step, but only after a prescribed number of $m$ iterations.

## Line search vs Trust Region







