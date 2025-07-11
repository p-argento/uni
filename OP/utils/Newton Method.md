from 'Visually Explained' on [youtube](https://youtu.be/W7S94pq5Xuo?si=73TWt1LsX74cKrlh)

**Focus**
Focusing on unconstrained optimization.
How to find the minimum of a function that depends on millions of variables?
The Newton Method belong to the class of Iterative Optimization Algorithms.

**The algorithm.**
Start from a random point $x_0$.
$$x_{k+1}=x_k+d_k$$
We can calculate the function in $x_k$ and $x_{k+1}$ to see if the function is decreasing, but how do we know $k$?

How a function varies in the neighbourhood of a point? Multivariable Calculus is the answer.
The gradient of a function tells us the direction of the biggest increase, that's why the Gradient Descent Algorithm picks -gradient as a descent direction.
Higher order derivatives are also useful, like the Hessian which contains information on the curvature of the function.

**Key idea**
Think in one variable, but then everything generalize.
The derivative is the slope of the tangent line, so we could minimize this linear function going to the right or to the left.
For how much? Let's use the stepsize $\alpha$ (not too big and not too small)
$$x_{k+1}=x_k-\alpha \ f'(x_k)$$
But far away from $x_k$ the linear function is not the function.
Newton method is based on using also the second derivative in $x_k$, like taylor series, optimizing this quadratic function.
Meaning that the stepsize $\alpha=\frac1 {f''(x_k)}$.

**From one variable to multi-variable**
So from one variable
$$x_{k+1}=x_k-\frac{1}{f''(x_k)}f'(x_k)$$
To multi-variable
$$x_{k+1}=x_k-\nabla^2f(x_k)^{-1}\ \nabla f(x_k)$$
Where the first derivative is replaced with the gradient and the inverse of the second derivative with the inverse of the hessian, which is a matrix.

**Good news**
*Quadratic Convergence.*
It means that after every iterations we double the number of the exact digits in our approximation.
Starting with 1 digit, you get 1,2,3,6,12,23,...

**Bad news**
*Starting point*
With different starting point you get different results.
*Scalability with $n$ variables.*
We need $n^2$ memory units just to store the Hessian.
We need ~$n^3$ operations to compute the inverse of the Hessian.
With 10 variables is fine. But what about 10k?
Consider that a single-thread CPU performs 1e10 flops (floating point operations) per second, and a GPU 1e12.

Quasi-Newton Methods avoid to compute the Hessian and its matrix.


## From Wikipedia
---
from [wikipedia](https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization)


Given
$${\displaystyle \min _{x\in \mathbb {R} }f(x)}$$
And using a sequence of second-order Taylor approximations of $f$ around the iterates.
$${\displaystyle f(x_{k}+t)\approx f(x_{k})+f'(x_{k})t+{\frac {1}{2}}f''(x_{k})t^{2}}$$
The next iterate is defined as to minimize the quadratic approximation in t. If the second derivative is positive, the quadratic approximation is a convex function of t, and its minimum can be found by etting the derivative to zero.
$${\displaystyle \displaystyle 0={\frac {\rm {d}}{{\rm {d}}t}}\left(f(x_{k})+f'(x_{k})t+{\frac {1}{2}}f''(x_{k})t^{2}\right)=f'(x_{k})+f''(x_{k})t}$$
The minimum is achieved for
$${\displaystyle t=-{\frac {f'(x_{k})}{f''(x_{k})}}}$$
Putting everything together, the iteration performed by Newton is
$${\displaystyle x_{k+1}=x_{k}+t=x_{k}-{\frac {f'(x_{k})}{f''(x_{k})}}}$$

## Example 

![[Pasted image 20240318144325.png]]

Basically, at every step we approximate the function with a parabola, then find the minimum of that parabola. We iterate again using the minimum found to build the second-order taylor approximation, that is again a parabola with a minimum.

![[Pasted image 20240318144712.png]]

Also
![[Nocedal, Wright - My Notes#2. Newton direction]]
