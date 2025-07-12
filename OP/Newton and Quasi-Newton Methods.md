Here I want to describe
1. Newton method
2. Quasi-Newton method (BFGS in particular)

## 1. Newton Method

![[Newton Method]]

From Nocedal, Wright
![[Nocedal, Wright - My Notes#2. Newton direction]]

## 2. BFGS
Sources
1. videos on youtube by Folker Hoffman [about Quasi-Newton](https://www.youtube.com/watch?v=VIoWzHlz7k8) and [line search](https://www.youtube.com/watch?v=kM79eCS9cs8)
2. “Quasi-Newton Methods” ([Nocedal and Wright, 2006, p. 135](zotero://select/library/items/XU24DLQI)) ([pdf](zotero://open-pdf/library/items/SZ2KAERJ?page=155))

*main idea*
We begin with the quadratic model of the objective function (aka 2nd order Taylor approximation) $$f(x_k+p)\approx f_k+p^T\nabla f_k+\frac 1 2p^T\nabla^2 f_k p = m_k(p)$$where $B$ is a $n\times n$ symmetric PD matrix that is update at every iteration.

Note that the minimizer of this quadratic problem is $$p_k = -B_k^{-1}\nabla f_k$$ and it can be used as search direction with stepsize $\alpha_k$ that satisfy the Wolfe conditions in the update of $$x_{k+1} = x_k + \alpha_kp_k.$$ Observe that this is very similar to the line search Newton method, but the approximation of the Hessian $B_k$ instead of the true Hessian.

*Davidon and the secant condition*
In order to get the BFGS method, it is worth looking first at the DFP algorithm. It was proposed by Davidon and then refined by Fletcher-Powell.
The idea of Davidon was to use the curvature of previous steps to update $B$. Remember that the Hessian gives the curvature of the function, meaning also how fast the gradient varies. And we already computed the gradient for previous steps.

We want to obtain a new quadratic model for the next iterate$$m_{k+1}(p) = f_{k+1}+p^T\nabla f_{k+1}+\frac 1 2p^TB_{k+1} f_{k+1} p$$but how do we define B? We use some contraints (aka requirements) based on the knowledge of previous steps.

These requirements are
1. symmetry and PD (like H)
2. secant condition
3. closeness to $B_{k-1}$ (this is where the methods differ)

What is the secant condition?
The gradient of $m_{k+1}$ should match the gradient of $f$ at the latest two iterates
1. $x_k$ which requires special attention
2. $x_{k+1}$ satisfied automatically because $\nabla m_{k+1}=\nabla f_{k+1}$ 
The first condition can be written as
$$$$