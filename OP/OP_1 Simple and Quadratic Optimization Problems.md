# 0. Outline & Wrap up
---
**Outline**
1. Optimization Problems
2. Optimization is difficult
3. Simple functions, Univariate case
4. Simple functions, Multivariate case
5. Multivariate Quadratic Case: Gradient Method
6. Multivariate Quadratic Case: Conjugate Gradient Method
7. Multivariate Quadratic Case: Factorization

**Wrap up**
1. Optimization problems are difficult, so start with simple problems to get the intuition
2. Use a simpler model, that looks like the real complex function, but that it is not
3. Linear Functions are super easy
4. Quadratic functions can go up to NP-hard

**My Point**
1. Basically trying to optimize simple problems, both univariate and multivariate
2. Then specifically look at the Multivariate Quadratic case, which is the simplest multivariate
3. Next step will be with more complicated UNIVARIATE functions


# 1. Optimization Problems
---
> How to define the optimization problem.
> Which function to use and how to write constraints.

**Changing the function**
Sometimes changing the function $f$ to $f_*$ does not change $X_*$ (which is the min or the max).

**Finding the min or the max?**
It is the same since
$$\min\{f(x):x\in \mathbb{R}\}=-\max\{-f(x):x\in \mathbb{R}\}$$
And also
$$\min\{f(x)+c:x\in \mathbb{R}\}=c+\min\{f(x):x\in \mathbb{R}\}$$
And again
	$$\min\{cf(x):x\in \mathbb{R}\}=c\min\{f(x):x\in \mathbb{R}\}\ (if\  c>0)$$

**Feasible Region**
We can select a feasible solution $X$ for $x\in X$.
Then the problem will be a (Univariate) Constrained Optimization Problem.
*We are however studying the unconstrained case first.*

**How to define the constraint**
Using more functions.
The standard way is to use
1. equality constraints$$g(x)=\delta \iff X=level\ set\ L(g,\delta)$$
2. inequality constraints with $\leq$  (use $-g(x)$ for $\geq$)$$g(x)\leq\delta \iff S( g , \delta ) = \{ x : g ( x ) \leq\delta\}$$

# 2. Optimization is difficult
---
> This section basically explore the cases when the min does not exist or it is not possible to find it. Not very interesting for us, since we will work with functions that have a minimum.

**What if $f_*\ \nexists$***
For example there is no finite lower bound on im(f).
This hardly never happens in data science since the Loss Function we want to optimize is not negative -> $L(w)\geq 0$.

**Do we need the exact solution?**
No, just an $\varepsilon$-approximate solution, called $\varepsilon$-optimum.
$$x_\varepsilon\in\mathbb{R}\ s.t.\ f_*\leq f(x_\varepsilon)\leq f_*+\varepsilon\,(\varepsilon\geq0)$$
It will be as close to the optimal solution as we need.
The cost of the algorithm typically depends on $\varepsilon$.
Optimization needs to be approximate.

**Sometimes it is impossible**
When there are isolated minima. They can be:
1. jumps
2. isolated (narrow) spikes
To avoid this case, we optimize functions that are
1. continuous (to avoid jumps)
2. Lipszitch-Continuous (to avoid also spikes)





# 3. Simple functions, Univariate Case
---
> Linear Univariate Function.
> Quadratic Univariate Homogeneous functions.
> Quadratic Univariate Non-Homogeneous functions.



# 4. Simple functions, Multivariate case
---
> (HERE CHAOS ENTERS THE CHAT)
> We use real functions with one-objective.
> Multi-Objective Optimization.
> Basic Algebra Review.
> Picturing Multivariate Functions is not possible.
> Linear Multivariate function (tomography and optimization).
> Separable (=sum of) Non-Homogeneous Quadratic Function.
> Advanced Algebra Review.
> Homogeneous Quadratic Functions (tomography, graph, level set, optimization).
> Non-Homogeneous Non-Singular Quadratic Functions (optimization).
> Non-Homogeneous Singular Quadratic Functions (optimization)









# 7. Multivariate Quadratic Case: Gradient Method
---




# 8. Multivariate Quadratic Case: Conjugate Gradient Method
---





# 9. Multivariate Quadratic Case: Factorization
---

