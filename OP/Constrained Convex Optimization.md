Some notes about Convex Optimization from [this playlist on youtube](https://www.youtube.com/playlist?list=PLqwozWPBo-FuPu4d9pFOobsCF1vDGdY_I) of Visually Explained.

Outline
1. What is Mathematical Optimization
2. Convexity and the Principle of Duality
3. [The KKT Conditions and the Interior Point Method for Convex Optimization](https://www.youtube.com/watch?v=uh1Dk68cfWs)

# 1. What is Mathematical Optimization
### What is a linear problem?
- It is a problem with linear objective function and linear constraints.
- $f$ is represented as a vector $c$ , so we move along that direction to find the minimum.
- Constraints are represented as hyperplanes.
### Least Squares Problem
- it is a classic example of linear problem
- it is about fitting a model, meaning that we want to find a vector $[x_1,x_2,...]^T$ so that $Ax=b$
- the objective function measures the error in the linear model as $min||Ax-b||^2$
	- note that it is quadratic
- $x$ can be the vector with the parameters of a neural network

# 2. Convexity and the Principle of Duality
### Convexity is related to set, functions and optimization problems.
- convex set
	- if segment connecting to points in the set is always included in the set itself
- convex function
	- if the epigraph (region above the function) is a convex set
	- note that you can build convex functions using known convex function and adding scalars
- convex optimization problem
	- if $f$ convex, LINEAR equality constraints and convex inequality constraints
	- why linear equalities? because $h_i=0$ means $h_i\leq0$ and $h_i\geq0$ but they can be both convex only if the constraint is actually a line
### Dual definitions
- convex set (dual)
	- if the positive region of all supporting hyperplanes (those that have the set in their positive set) contains the whole set
	- so we can see the convex set as a polyhedra defined by infinite  inequalities represented as hyperplanes
	- note that the issue in optimization is not about linearity or non-linearity, but between convexity and non-convexity
- convex function (dual)
	- $f$ is convex if the graph of $f$ is always above the tangent hyperplane
	- it is connected to taylor, where a small part of a section can be approximated using tangent hyperplanes 
	- and, with taylor in mind, if $\nabla f=0$ then the point is a min because $f(x)\geq f(x_0)+0\ \forall x$ because $f(x)$ is always above the horizontal hyperplane

# 3. KKT Conditions and Interior Point
See [Transcript of The Karush–Kuhn–Tucker (KKT) Conditions and the Interior Point Method for Convex Optimization - YouTube](OP/docs/Transcript%20of%20The%20Karush–Kuhn–Tucker%20(KKT)%20Conditions%20and%20the%20Interior%20Point%20Method%20for%20Convex%20Optimization%20-%20YouTube.md)
### Penalty function
It is a function that penalize for not satisfying a constraint $$min\ f(x)+P(y)$$1 ) an approach of $P(y)$ is the zero-penalty function, for example for the constraint $y<0$ is $$P(y)=\begin{cases} \infty &\text{if\ $y>0$} \\ 0 &\text{if\ $y\leq0$} \end{cases}$$Here we get rid of constraint and it works, but the function is not continuous anymore

 2 ) another approach is the linear function $$P(y)=u\times y$$It is smooth, but poor in terms of function's shape

3 ) a better approach is $$P(y)=max(u\times y)$$Using this last approach, let's go through an example, moving the max of the penalty function outside in the main problem. What we got is a min-max problem. $$\begin{align}
&\min_x\ x_1+x_2+P(x_1^2+x_2^2-1) \\
&\min_x\ x_1+x_2+\max_{u\geq0}\ U(x_1^2+x_2^2-1) \\
&\min_x\ \max_{u\geq0}\ x_1+x_2+\ U(x_1^2+x_2^2-1)

\end{align}$$This is the Primal of the problem.
Think of it as a two-players game $x$ and $u$.
$x$ tries to minimize the objective function $f$, while $x$ penalize it if $x$ does not satisfy the constraint, picking large values of $u$.
But who plays first?
If we change the natural order, we obtain the dual. $$\max_{u\geq0}\ \min_x\  x_1+x_2+\ U(x_1^2+x_2^2-1)$$$x$ job is now simpler because this is a convex function without any constraint, so $x$ can just take the gradient of $f$, set it to zero and solve for $x$; then plug the result back in $f$.$$\begin{align}
&x_1=x_2=-\frac 1 {2u} \\
\Rightarrow &\max_{u\geq0}\ -u-\frac 1 {2u}
\end{align}$$Now we maximize with respect to $u$ and, using derivatives, get the max for $u\geq0$, then plug $u$ in $x_1,x_2$ $$\begin{align}
&u_1=\frac 1{\sqrt2}\\
\rightarrow\ &x_1=x_2=-\frac1{\sqrt2}
\end{align}$$

### What is a dual problem in general?
$$\begin{align}
&\min_{x\in\mathbb{R}}f(x)\\
&h_i(x)=0\quad i=1,... \\
&g_j(x)\leq0\quad j=1,...
\end{align}$$
We want to get rid of contraints , so we multiply each constraint by a scalar $u_i,v_i$ that represent the slope of the penalty function, then we move them from the constraints to the objective function. $$\begin{align}
&\min_{x\in\mathbb{R}}f(x)+\max_{u_i,v_i\geq0}\sum_i v_i h_i(x)+\sum_j u_j g_j(x) \\
&\max_{u_i,v_i\geq0}\min_{x\in\mathbb{R}}f(x)+\sum_i v_i h_i(x)+\sum_j u_j g_j(x)
\end{align}
$$This function is called Lagrangian $$L(x,u,v)=f(x)+\sum_i v_i h_i(x)+\sum_j u_j g_j(x)$$ While the min-max problem of the Lagrangian is the DUAL. 
And because strong duality holds, $$\text{primal problem solution = dual problem solution}$$
*Zero-duality gap*
For certain constrained optimisation problems, we have **zero duality gap**. This essentially means that the optimal minima can be achieved by considering either primal or dual problem. This property is exhibited
(1) if we have a convex quadratic objective function and affine constraint functions and
(2) if the Hessian matrix with respect to _x_ is **semidefinite** or **definite**.
SVM is exactly this kind of problem.

*Active Contraints*
An inequality constraint $g(x)\leq0$ is called active when, for a particular solution point $x$ if the equality $g(x)=0$ holds. Active constraints lie directly on the boundary of the feasible region, meaning that they directly influence the position of the optimal solution. A slight change in an active constraint is likely to move the optimal solution.

### KKT Conditions
We want to minimize the Lagrangian, so the NECESSARY condition is $\nabla L(x)=0$ meaning $$\nabla\bigg( f(x)+\sum_i v_i h_i(x)+\sum_j u_j g_j(x)\bigg)=0$$
*A visual explanation*
When taking the gradient with respect to x, Lagrange multipliers $v_i,u_j$ are treated as constants.
Terms with $h_i​(x)$ vanish because at a feasible point, $h_i​(x)=0$.
Taking a simplified Lagrangian with a single active inequality constraint, we get $$\begin{align}
&\nabla\bigg( f(x)+u g(x)\bigg)=0 \\
&\nabla f(x)=-u \nabla g(x)
\end{align}$$Meaning that they are proportional with negative coefficient, so graphically on the same direction but pointing opposite sides.
Remember that following the opposite direction of the gradient means decreasing the value of the function locally. So, we want to find an x in the intersection where both g and f decrease, within the feasible region. But to find an optimum, the region where $\nabla g$ and $\nabla f$ decrease, they should not intersect, but they must be on the same direction, and so proportional to each other. If $g\leq0$ is the region.

*add image*


KKT conditions $$\begin{cases}
\nabla f(x)+u\nabla g(x)=0 &\text{necessary condition for stationarity}\\
g(x)\leq0 &\text{primal feasibility}\\
u\geq0 &\text{dual feasibility (or multipliers conditions)}\\
u g(x)=0 &\text{complementary slackness}
\end{cases}$$ Respectively
1. stationarity: the gradient of the Lagrangian with respect to optimization variable must be zero at an optimal point (necessary condition)
2. primal feasibility: all the original problem constraints must be satisfied by the solution
3. dual feasibility: Lagrange multipliers corresponding to inequality constraint must be non-negative
4. complementary slackness:
	1. If g(x) < 0 (the constraint is inactive), then u must equal 0. In this case, the constraint doesn't directly impact the optimal solution.
	2. If g(x) = 0 (the constraint is active), then λ may be non-zero. The constraint is actively shaping the optimal solution.
	3. It is significant for identifying active constraints and simplifying calculations (allows to eliminate Lagrange multipliers corresponding to inactive constraints, reducing the complexity of the calculations needed to find the optimal solution)

The KKT conditions are necessary conditions for optimality. This means that an optimal point will satisfy these conditions, but a point satisfying these conditions might not always be a guaranteed optimum (especially in non-convex problems).

When the primal problem is convex, the KKT conditions are also suﬃcient for the points to be primal and dual optimal. (Boyd, Vandenberghe)
There are other problems when KKT conditions are sufficient.

It reduces solving an optimization problem to solving a bunch of equations and inequalities and as you can imagine this is extremely useful for designing general purpose optimization solvers.

### Interior Point Method
It is a way to solve the KKT Conditions.
There are two techniques behind IP.

**First Issue: KKT(t)**
We solve a modified version of KKT conditions, called KKT(t) where $t\geq0$ is a parameter that controls the degree of perturbation.
We keep all the equations the same, except for the last one, that becomes $$u\ g(x)=-t$$ Hopefully, when t is small, $x(t)\approx x^*$ , meaning that when $t\rightarrow0 \Rightarrow x(t)\rightarrow x^*$ .

![](Pasted%20image%2020240215181203.png)

The modified KKT are much easier to solve.
In fact, we get $u$ from the last equation $$u=\frac{-t}{g(x)}$$ Then the first equation with gradient becomes $$\begin{align}
&\nabla f(x) + \frac{-t}{g(x)} \nabla g(x)=0 \\
&\nabla\bigg(f(x)-t\ log(-g(x))\bigg)=0 \\
\end{align}$$ To solve this gradient, just need to minimize the function $$\min_{x\in\mathbb{R^n}}f(x)-t\ log(-g(x))$$ In the optimum point obtained, all the KKT conditions are satisfied:
1. gradient is zero because is the necessary condition
2. if g were positive $log(-g(x))$ would be +inf (or it does not exist?), so $g(x)\leq0$ is satisfied
3. $u\geq0$ because of 2) and 4)
We are back in unconstrained optimization, where we can use methods like [Newton Method](Newton%20Method.md).

*Geometric interpretation*
The scalar t controls the degree of penalty given by the logaritmic function.
We want a t as small as possible, so the penalty term doesn't affect the objective function too much. But not too small, otherwise the function $t\ log(-g(x))$ is not continuous (see zero-penalty function above) and Newton method would be extremely slow to converge and cause numerical issues.

**Second Issue: Iterative reduction of t**
Start with a big t and make it smaller and smaller.
$$\min_{x\in\mathbb{R^n}}f(x)-t\ log(-g(x))$$
Why? If t is big, the penalty is dominant. And because log is increasing, this is the same as minimizing g(x) for example with Newton's Method. 
In the initial example, it will give the center of the circle (feasible region), generally called "analytical center of the feasible region".
Once you have a solution for a specific t, try to solve for a slightly smaller t, like t'=.9t using again Newton Method, but now x(t) is specified as a starting point for Newton's Method (if Newton is initialized with a point close to the actual solution, then it is super fast).
Iterate until a t close enough to zero is reached, through what is called as "central path", that falls in the interior of the feasible region.





