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
u\geq0 &\text{dual feasibility}\\
u g(x)=0 &\text{complementary slackness}
\end{cases}$$ Respectively
1. stationarity: the gradient of the Lagrangian with respect to optimization variable must be zero at an optimal point (necessary condition)
2. primal feasibility: all the original problem constraints must be satisfied by the solution
3. dual feasibility: Lagrange multipliers corresponding to inequality constraint must be non-negative
4. complementary slackness: for each inequality constraint, either the Lagrange multiplier is zero (inactive constraint) or the constraint itself is active (holds as equality)
	1. The penalty term (u * g) should be zero - essentially this means that with a properly chosen 'x' and 'u', this penalty term will not interfere with finding the optimal value of our minimization problem.

The KKT conditions are necessary conditions for optimality. This means that an optimal point will satisfy these conditions, but a point satisfying these conditions might not always be a guaranteed optimum (especially in non-convex problems).

When the primal problem is convex, the KKT conditions are also suﬃcient for the points to be primal and dual optimal. (Boyd, Vandenberghe)

It reduces solving an optimization problem to solving a bunch of equations and inequalities and as you can imagine this is extremely useful for designing general purpose optimization solvers.

### Interior Point Method
It is a way to solve the KKT Conditions.
There are two techniques behind IP.

**First Issue: KKT(t)**
We solve a modified version of KKT conditions, called KKT(t) where $t\geq0$ is a parameter that controls the degree of perturbation.
We keep all the equations the same, except for the last one, that becomes $$u\ g(x)=-t$$ Hopefully, when t is small, $x(t)\approx x^*$ , meaning that when $t\rightarrow0 \Rightarrow x(t)\rightarrow x^*$ .

![](_myMedia/Pasted%20image%2020240215181203.png)

The modified KKT are much easier to solve.
In fact, we get $u$ from the last equation $$u=\frac{-t}{g(x)}$$ Then the first equation with gradient becomes $$\begin{align}
&\nabla f(x) + \frac{-t}{g(x)} \nabla g(x)=0 \\
&\nabla\bigg(f(x)-t\ log(-g(x))\bigg)=0 \\
\end{align}$$ To solve this gradient, just need to minimize the function $$\min_{x\in\mathbb{R^n}}f(x)-t\ log(-g(x))$$ In the optimum point obtained, all the KKT conditions are satisfied:
1. gradient is zero because is the necessary condition
2. if g were positive $log(-g(x))$ would be +inf (or it does not exist?), so $g(x)\leq0$ is satisfied
3. $u\geq0$ because of 2) and 4)
We are back in unconstrained optimization, where we can use methods like [Newton Method](OP/web_based_studying/Newton%20Method.md).

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




# Transcript of The Karush–Kuhn–Tucker (KKT) Conditions and the Interior Point Method for Convex Optimization - YouTube

> Gemini-generated

**Duality in Convex Optimization**

**Introduction**

In the previous video, we discussed the meaning of duality for convex sets and convex functions. In this video, we'll examine the concept of duality as applied to convex optimization problems and see how it can help us design efficient algorithms to solve them.

**An Illustrative Example**

Imagine you're the captain of a ship in the middle of the ocean. Using sophisticated equipment, you determine that rain is approaching from a direction 'c' (for example, c equals the vector \[1, 1]). You decide to steer the ship in the opposite direction as much as possible. However, the sea is infested with sharks, except within a safe circular region with a radius of one unit.

This scenario presents a convex optimization problem. Our decision variable is the two-dimensional vector 'x' (representing the ship's position). The objective is to maximize c transpose x (or simply x1 + x2). We have a single constraint: The ship's position 'x' must be chosen from within the unit disk. Since the objective function is linear (and thus convex) and the constraint is defined by a convex function, this presents a convex optimization problem.

**Eliminating the Constraint**

Ideally, we would like to get rid of the constraint. In an unconstrained convex optimization problem, we could visualize the level of the sea tilted according to the objective function. Low sea levels would reflect low objective values, and high sea levels would indicate high objective values. The solution would be to steer the ship in the direction of -c, which aligns with our intuition.

One way to remove a constraint is through a penalty function. A penalty function punishes us for violating a constraint. A natural choice is a function that takes the value 0 for negative arguments and the value plus infinity for positive arguments. Let's call this the zero-infinity penalty function.

Using a penalty function like this raises the 'sea level' outside our safe circle to plus infinity, preventing us from steering the ship into danger – even if the original objective value was lower there. However, while this allows us to remove the constraint, introducing an objective function that can take infinite values presents challenges.

**Approximating the Penalty Function**

Let's approximate the zero-infinity penalty function with a smooth function that doesn't have infinite values. A simple candidate is a linear function (something like u * y, where 'u' is a non-negative slope). Visually, you can see how this linear penalty is a smoother approximation of the original function.

The linear penalty works as follows: if you violate the constraint, you incur a penalty proportional to the amount of violation. If you satisfy the constraint, you are actually rewarded. While being rewarded for 'doing the right thing' might sound appealing, in our optimization scenario this is undesirable as it affects the optimal value - and the impact this has depends on the value of the chosen slope 'u'.

**The Min-Max Problem**

Interestingly, if you consider all possible values of 'u' and take the maximum of the corresponding linear penalties, you recover the original zero-infinity penalty function. Using this maximum as our penalty function results in a min-max problem. A helpful way to understand this is to think of it as a two-person game: an 'x' player and a 'u' player. The 'x' player aims to minimize the problem by picking 'x', while the 'u' player tries to penalize violations of the constraint, thus making the overall term large.

In games like this, it's always advantageous to go second because you know what the first player did. If the 'u' player goes first, the ‘x’ player only needs to minimize the resulting quantity (a convex function without constraints). Now that we know how 'x' should respond, we can plug that back in and maximize with respect to 'u'.

**Let's continue in the next part...**

Absolutely, let's resume the formatted transcript:

**The Dual Problem**

While solving for 'u' gives us a specific solution (x1 = x2 = minus square root of 2 over 2), what we've actually solved is a variation of the original problem called the _dual problem_. The original is termed the _primal problem_. Examining the dual problem offers many benefits – but first, let's generalize its form for convex optimization problems.

Inspired by our example, let's derive the dual of a general convex optimization problem. We begin by removing constraints. For each function in the constraints, we introduce a scalar (representing the slope of our penalty function) and move these functions from the constraints into the objective function. Similar to the example, we take the maximum over the scalars for inequality constraints (where we want cost to be positive) and allow positive or negative slopes for equality constraints (as we want to penalize both positive and negative values equally).

Finally, to arrive at the dual problem, we pull the maximum outside and switch the order of 'min' and 'max'. The quantity within this problem is known as the Lagrangian of the optimization problem, with the dual problem itself referred to as the Lagrangian dual. Let's highlight some keywords:

- **The Dual Problem:** The dual has one variable for each constraint in the primal. These act as 'costs' or 'prices' associated with violating those constraints.
- **Lower Bound:** Unlike in the primal, the 'x' player (minimizing our objective function) gets the advantage of going second in the dual problem. This means the dual problem gives us a lower bound on the optimal value of the primal.
- **Strong Duality:** Often, under mild assumptions, _strong duality_ holds – meaning the optimal value of the primal and dual problems coincide. You can choose to solve whichever is easier and get the correct answer. These assumptions are usually satisfied (and hold for our toy example), so from here on, let's assume strong duality holds.

**The Karush-Kuhn-Tucker (KKT) Conditions**

Now let's explore how using the dual problem can assist in solving convex optimization problems. This leads us to the celebrated KKT conditions. Remember, within the Lagrangian, the 'x' player aims to minimize this quantity. Therefore, at the optimal solution 'x', the gradient with respect to 'x' must be zero. Think of this as a broader version of the condition (grad of f = 0) often used to find minimizers in unconstrained optimization problems.

There's a strong geometric intuition here. For simplicity, let's assume a single inequality constraint. In this case, the KKT condition states that grad f and grad g are inversely proportional to each other. Visualizing this: delimit the feasible region (given by g) with a green line and consider an arbitrary point 'x' within this region. Drawing the gradients of f and g, we realize that:

- Moving 'x' opposite to the gradient of a function would reduce its value. Thus, within the 'green rectangle,' g would stay below zero (no constraint violation), and within the 'yellow region,' we could improve the objective function f. If these regions intersect, it follows that 'x' cannot be optimal - you could still nudge 'x' to improve things. For optimality, these regions shouldn't intersect, which only occurs when gradients of f and g are inversely proportional.

Now is a good time to review: if 'x' is an optimal solution, it must satisfy the gradient condition discussed. However, is this sufficient? Can we assume any 'x' that matches this condition is automatically optimal? Unfortunately, in the general case, this isn't true. We need some additional assumptions on 'x' and 'u' for this to hold. Thankfully, these assumptions are quite intuitive:

1. 'x' must be feasible.
2. The scalar 'u' should be non-negative.
3. The penalty term (u * g) should be zero - essentially this means that with a properly chosen 'x' and 'u', this penalty term will not interfere with finding the optimal value of our minimization problem.

Together, these are the _KKT conditions_, incredibly influential in convex optimization. The significant advantage of KKT is that you essentially transform solving an optimization problem into solving a set of equations and inequalities. This has immense utility when designing general-purpose optimization solvers.

**Interior Point Methods**

While you could attempt to solve for KKT conditions manually in small examples, this quickly becomes complex. Hence, the _interior point method_ comes in – offering a sophisticated way to handle KKT conditions. There are two major insights or techniques at play in interior point methods, valuable in many areas of mathematics beyond optimization:

Absolutely, let's dive deeper into the insights behind the interior point method:

**Insight 1: Perturbed KKT Conditions**

Instead of working with the KKT conditions directly, we solve a modified or _perturbed_ version of them. We'll refer to these as KKT(t), where 't' is a positive parameter controlling the degree of perturbation. Let x(t) denote the solution to these perturbed equations and x* denote the solution to the original equations. The perturbation involves keeping all the KKT conditions the same except for a change in the last equation – instead of a 0 on the right-hand side, we have a negative number, -t. Our hope is that when 't' is small, x(t) and x* are close, so as the perturbation parameter 't' tends toward 0, x(t) converges to x*.

So far, we've discussed _how_ to perform this perturbation but let's now tackle the _why_. **The main objective is that the modified KKT conditions are significantly easier to solve.** When u * g equals -t, we immediately obtain 'u' from 'x' as u = -t / g(x). Substituting this value for 'u' back into the gradient equation reveals something interesting: this quantity is actually the gradient of f minus t * log(-g). (Take a moment to work this out by hand to develop your intuition!).

Solving the gradient equation is now equivalent to minimizing this function. As a bonus: minimizing this function _automatically_ satisfies the constraint g(x) smaller than zero (if g were positive, log(-g) would give plus infinity), and a positive 'u' is also guaranteed. As of now, we're back in the comfortable territory of unconstrained minimization problems, amenable to techniques like Newton's method.

Geometrically, imagine the penalty for violating the constraint is given by the log function, with 't' controlling the severity of this penalty. The challenge: we want to take 't' as small as possible to minimize the impact of the penalty on our objective. Yet, taking 't' too small causes t * log to behave unfavorably like the discontinuous zero-infinity penalty function we encountered earlier, leading to slow convergence and numerical issues in Newton's method.

**Insight 2: Iterative Reduction of 't'**

Here is where the second insight of interior point methods shines: instead of getting 't' small immediately, we start with a large 't' and reduce it step-by-step. Why does this help?

If 't' is very large, the log term dominates, effectively minimizing g(x), which you can achieve using Newton's method. In our toy example, this step would give the center of the disk. More generally, the point you obtain at this stage is termed the analytic center of the feasible region.

Once you have a solution for a given 't', try solving for a slightly smaller 't' (say t' = 0.9 * t). We use Newton's method again, but crucially, initialize it with x(t) – our previous solution. The key property of Newton's method is that when initialized close to the optimal solution, it converges incredibly fast. Since x(t) is designed to be close to x(t'), obtaining x(t') computationally becomes easy.

The interior point method continues these iterations, making 't' smaller and smaller until we reach a 't' that's deemed close enough to 0.

**Recap**

Let's summarize the inner workings of the interior point method applied to a convex constrained problem:

- Via a log penalty (multiplied by a scalar 't'), it transfers constraints to the objective function.
- Starts with a large 't', effectively finding the analytic center of the feasible set.
- By successively lowering 't', it moves along a path formed by the x(t)'s. This is called the _central path_.
- The central path resides in the interior of the feasible region, hence the name _interior point method_.
- The solution returned by the algorithm is ultimately the end of the central path.

**Conclusion**

This video series offers a starting point in understanding the rich field of convex optimization. There's plenty more to delve into when it comes to duality and interior point methods. If you're interested in deeper learning, I highly recommend the freely available (pdf) book by Boyd and Vandenberghe – a resource I also used to prepare this video.