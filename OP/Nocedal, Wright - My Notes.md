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

There are two approaches for solving an unconstrained minimization optimization problem. [S](https://indrag49.github.io/Numerical-Optimization/introduction-to-unconstrained-optimization.html#algorithms-for-solving-unconstrained-minimization-tasks)
1. **Line Search Descent Method**
2. **Trust Region Method**
Trust-region methods are in some sense dual to line-search methods: trust-region methods first choose a step size (the size of the trust region) and then a step direction, while line-search methods first choose a step direction and then a step size. 

> Wikipedia [trust region](https://en.wikipedia.org/wiki/Trust_region) & [line search](https://en.wikipedia.org/wiki/Line_search)

In *line search*, the algo chooses a direction $p_k$ and searches along this direction from the current iterate $x_k$ for a new iterate with a lower function value.
Given the direction $p_k$, how much should we move along this direction? To find the step length $\alpha$ we should solve the following one-dimensional minimization problem
$$\min_{\alpha>0}f(x_k+\alpha p_k)$$
We would like to derive the maximum benefit from the direction $p_k$
> HOW??

However, an exact minimization may be expensive and usually it is not necessary.
Instead, the line search generates a limited number of trial step lengths until found one that loosely approximate the minimum.
At the new point, new search direction and new step length are computed.

(Do no confuse linear search with line search)
In optimization, the line search strategy is one of the two basic iterative approaches to find a local minimum of the objective function $f:\mathbb{R}^n\rightarrow\mathbb{R}$. 
The line search approach first finds a descent direction along which the objective function $f$ will be reduced and then computes a step-size that determines how far $x$ should move along that direction. 
The descent direction can be computed can be computed by various methods, such as gradient descent or quasi-newton methods. 
The step-size can be determined either exactly or inexactly.

The second strategy is *trust region*.
Here, the information gathered about $f$ is used to construct a model function $m_k$ whose behaviour near the current point $x_k$ is similar to that of the actual objective function. Basically, we restrict the search for the minimizer of $m_k$ to some region around $x_k$. It means solving the subproblem:
$$\min_p m_k(x_k+p)\quad\text{where $x_k+p$ lies inside the trust region}$$
Note that $m_k$ is a function (called model function).

If the candidate solution does not produce a sufficient decrease in f, we conclude that the trust region is too large, so we shrink and re-solve.
Usually, the trust region is a ball defined by $||p||_2\leq\Delta$ where the scalar $\Delta>0$ is called trust-region radius.

The model function $m_k$ is usually defined to be a quadratic function of the form: $$m_k(x_k+p)=f_k+p^T\nabla f_k+\frac 1 2 p^TB_kp$$ where
- $f_k$ is a scalar, is the function at the point $x_k$
- $\nabla f_k$ is a vector, is the gradient of the function at the point $x_k$
- $B_k$ is a matrix, is the Hessian $\nabla^2 f_k$ or some approximation
Note that $m_k$ looks like Taylor approximation.

The main difference between line search and trust region is the following.
Line search
- starts by fixing the direction $p_k$ and then identifying an appropriate distance (the step length $\alpha$). 
- major issue: choice of the search direction $p_k$
Trust-region
- first choose a max distance (the radius $\Delta_k$) and then seek a direction and a step, looking for the best possible improvement given the distance constraint.
- major issue: choice of the Hessian $B_k$

## Line search
Line search directions that will be discussed in this section give rise to the following line search methods:
1. steepest descent method
2. Newton method
3. quasi-newton method
4. conjugate gradient

Note that, in general, nonlinear conjugate gradients directions are much more effective that the steepest descent direction, and almost as simple to compute. Comparing with Newton or quasi-newton, the convergence rate is not so fast, but the advantage is that it is not required to store matrices.

### 1. Steepest descent direction
It is the most obvious choice for search direction for a line search method.
It is $-\nabla f_k$.
It is the direction along which f decreases most rapidly.
It can be verified using Taylor.
The direction of most rapid decrease is $$\min_p p^T\nabla f_k$$ which is $p_k=-\nabla f_k$

Note that other descent directions can be used. And it is guaranteed to produce a decrease in f provided that the step length is sufficiently small.

### 2. Newton direction
The most important one, called Line Search Newton method.
It is derived from the second-order Taylor series approximation to $f(x_k+p)$.
$$f(x_k+p)\approx f_k+p^T\nabla f_k+\frac 1 2p^T\nabla^2 f_k p = m_k(p)$$
Assuming $\nabla^2 f_k$ positive definite, we simply set the derivative of $m_k$ to zero (which is the model approximating the function).
We obtain the formula $$p_k=-(\nabla^2 f_k)^{-1}\ \nabla f_k$$The Newton direction is reliable when the difference between the true function $f(x_k+p)$ and its quadratic model $m_k$(p) is not too large.

Note that, with respect to Taylor approximation, we are simplifying some terms, but the perturbation is small and can be ignored.

Step length.
Most line search implementations of Newton's method use the natual step length of 1, and adjust $\alpha$ only when the reduction in the value of f is not satisfactory.

Problems
1. when $\nabla^2 f_k$ is not positive definite, the direction may not be defined
2. the descent property $\nabla f_k^Tp_k<0$ may not be satisfied and therefore the search direction is unfeasible

Convergence.
Typically, the convergence rate is quadratic. Often few iterations.

More in detail in [[Newton Method]]

### 3. Quasi-Newton direction
These search directions are alternatives to Newton method.
They do not require the computation of the Hessian.
However, they still attain superlinear rate of convergence.
In place of the true Hessian, an approximation $B_k$ is used.

...


### 4. Non-linear conjugate gradient direction





## Trust-region
Same directions of line search, but after choosing a radius.












