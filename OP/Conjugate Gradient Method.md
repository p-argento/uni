Sources
1. videos on youtube by Priya Deo on [CG](https://www.youtube.com/watch?v=h4cG8jLGmKg) and [preconditioned CG](https://www.youtube.com/watch?v=zjzOYL4fhrQ)
2. “Conjugate Gradient Methods” ([Nocedal and Wright, 2006, p. 101](zotero://select/library/items/XU24DLQI)) ([pdf](zotero://open-pdf/library/items/SZ2KAERJ?page=121))

There are different algorithms that are worth considering, in order of complexity
1. basic conjugate gradient
2. advanced conjugate gradient
3. preconditioned conjugate gradient
4. nonlinear conjugate gradient (in particular, Fletcher-Reeves)

## 1. Basic CG
The linear conjugate gradient is an iterative method for solving a liner system of equations $Ax=b$ where $A$ is a $n\times n$ matrix PD.

The system $Ax=b$ can also be interpreted as $$min\ \phi(x):=\frac 1 2x^TAx-b^Tx$$ where we observe that the gradient of $\phi$ is equal to the residual of the liner system, ie $$\nabla\phi(x)=Ax-b:=r(x).$$
The idea is to improve the gradient descent because the directions $d_i$ (or $p_i$ in Nocedal-Wright), which are obtained only through the negative of the gradient, can point nearly where it was the previous step, giving very slow convergence.
This is the famous zig-zag shown in quadratic functions when the level sets are elongated ellipses, which are the result of high condition number of Q.

Let's dive deeper in the conditioning problem, which will be useful also for preconditioning.
The conditioning number is $$k(A)=\frac{|\lambda_{max}|}{|\lambda_{min}|}$$which can be seen as the shape of level sets in quadratic functions.
If $A=[1\ 0; 0\ 1]$ is the identity matrix, then $k=1$ and we observe level sets as circles. Here the gradient descent works fine.
If $A=[1\ 0; 0\ 0.1]$, then $k(A)=10$ and we observe level sets as elongated ellipses, see it like the ratio among eigenvalues. Here the gradient descent might get stuck in the direction of the smallest eigenvalue because it is hard to make any progress where the gradient is weak.

Back to the main idea, we do not want to waste steps, therefore we choose directions that are orthogonal with respect to the matrix Q. These directions are called Q-orthogonal or conjugate directions, ie $$d_i^T Q d_j = 0 \quad\text{for } i\neq j$$
