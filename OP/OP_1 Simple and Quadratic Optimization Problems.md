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

**Linear Univariate Optimality**
In a linear function.
![[Pasted image 20231124174544.png|200]]
If $b>0$ -> $\max=+\inf , \min=-\inf$
If $b=0$ -> $\min=\max=0$
I
t is more interesting to do box-constrained optimization within (P)
$$(P)\ \min\{f(x):x\in [x_-,x_+]\}$$
It is better to use closed interval $[x_-,x_+]$  instead of $(x_-,x_+)$ .
In fact, if the interval is open then $inf\ \exists$ but $min\ \nexists$.
We will just use closed sets and be done with it.

**Quadratic Univariate Homogeneous Functions**
$f(x)=ax^2$
![[Pasted image 20231124174759.png|100]]
Again, unconstrained is easy and depends only on the sign of $a$.
If $a>0\Rightarrow min=0,max=+\inf$
If $a<0\Rightarrow min=-\inf,max=0$
And again closed box-constrained is more interesting.

**Quadratic Univariate Homogeneous Functions**
$f(x)=ax^2+bx$
Basically a homogeneous quadratic + a linear.
Zero is always a root but not the min.

How to find the min? Make $f(x)$ simpler by changing the space of variables.
It means changing the input space so that it becomes homogeneous.
The idea is to use $\bar{x}=-b/2a$ and $z=x-\bar{x}$.
We are translating by $\bar{x}$ horizontally and by $f(x)$ vertically to make $f(x)$ homogeneous. Then the min point is $x*=\bar{x}$.
Remember how to find the vertex of the parabola in high school. There's nothing different.

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


**Multivariate Optimization**
Now we take a big step, using $n$ variables in input. However we stick with real functions, that means we are still getting a real number as output. In formula $f:\mathbb{R}^n\rightarrow \mathbb{R}$.
This assumptions is strong and useful: we can alway say which result we like more because $\mathbb{R}$ has total order.
If we had more than one object, we would call it multi-objective optimization.

**A quick glimpse on Multi-Objective Optimization**
$\mathbb{R}^k$ has no total order, so there is nothing like the best solution.
We can however use the Pareto frontier to define non-dominated ones.
Two solutions.  
1. Scalarization. We can use a parameter to add the function in the other. Like a risk-adjusted return for investment. $\Rightarrow\min\{f_1(x)+\alpha f_2(x)\}$
2. Budgeting. Decide the maximum risk. So we'll use a one-objective function with constraints.  $\Rightarrow\min\{f_1(x):f_2(x)\leq \beta\}$
This is done at modelling stage.

> **Basic Algebra Review**
> Watch 3b1b Linear Algebra playlist on youtube.
> For the Italians, search Gobbino.

**Picturing Multivariate functions**
Not possible.
We need to find the direction $d$ to represent what we need in two dimensions.

**Linear Multivariate Functions**
![[Pasted image 20231124182608.png|400]]
Level sets are lines in $\mathbb{R}^2$ that represents parallel hyperplanes in $\mathbb{R}^n$.
These lines basically are places where the function has the same value for all those point.
$f(x)=f(z)\iff\langle b,x\rangle=\langle b,z\rangle=0\iff b\bot z$

**Tomography**
Think of $b$ as the gradient, which is the steepest way to get higher values of the function. Of course minus the gradient is the way the get the steepest way to descend. All the vectors in the middle give directions in between. This is the idea behind the Gradient Method.
Just imagine the vectors on the 3D figure above and you will get the idea.

**Separable (=sum of) Non-Homogeneous Quadratic Function.**
Special case with $f(x_1,x_2)=ax_1^2+x_2^2$.
It is exactly like the univariate case.

**Non-Separable Homogeneous Quadratic Function**
$f(x)=\frac1 2 x^TQx$
$Q$ is symmetric.

> **Advanced Algebra review**
> This is required to work with the associated matrix of the Quadratic Function.

$\varphi_{H_i}(\alpha)=\alpha^2\lambda_i$
No idea of what that means.

$H_1,H_2$ are the eigenvectors of the $Q$ matrix.
Steepness change with the direction.
One of the eigenvectors is the steepest direction, the other is least steep.

... algebraic stuff

**Optimizing Homogeneous quadratic multivariate function**
It depends on the sign of eigenvalues.
Is the matrix Q positive definite, positive definite, indefinite, etc.?
![[Pasted image 20231124190008.png]]

**Optimizing Non-Homogeneous quadratic multivariate function**
...
wip
...


# 7. Multivariate Quadratic Case: Gradient Method
---
> Multivariate oprimization algorithms (in general, how do they work)
> Gradient method (basic idea)
> Gradient Method for Multivariate Quadratic Functions
> Convergence of the Gradient Method
> Complexity of the Gradient Method
> Stopping criterion
> Is it fast enough?
> If $\lambda_n=0$ 

**Algorithm idea**
It is an iterative procedure.
It start from an initial guess $x_0$ and after some process $x_i\leadsto x^{i+1}$ we get a sequence $\{x_i\}$ that should go towards an optimal solution.
We cannot get to $f_*$ in finite time, but we can get as close as we want.
Does a sequence always converge? If it is monotone, then yes.
Monotone means that the function value at each iteration will be better.
We generally assume minimization.

**Gradient Method basic idea**
Watch a video. There are a lot. This part is not clear at all.


# 8. Multivariate Quadratic Case: Conjugate Gradient Method
---
> Speeding up the gradient method for quadratic functions
> The power of conjugate directions
> The conjugate gradient method for quadratic functions
> Efficiency of the Conjugate Gradient Method
> Preconditioning the Conjugate Gradient Method

**Speeding up the gradient method for quadratic functions**
The Gradient Method only need one iteration when $Q=Identity$.
What if we change the space to get it?
In theory, it is simple if Q is non-singular, which mean non-null eigenvalues.
$[ H\sqrt{\wedge}H^T ][ H\sqrt{\wedge}H^T ] = H\sqrt{\wedge}[H^T H ]\sqrt{\wedge}H^T = H\wedge H^T = Q$








# 9. Multivariate Quadratic Case: Factorization
---
> Using the big guns: direct methods
> Backsolve
> Cholescky Factorization

If Q is dense, Choleski Factorization is the best thing you can do.