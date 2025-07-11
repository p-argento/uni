Sources
1. videos on youtube by Priya Deo on [CG](https://www.youtube.com/watch?v=h4cG8jLGmKg) and [preconditioned CG](https://www.youtube.com/watch?v=zjzOYL4fhrQ)
2. “Conjugate Gradient Methods” ([Nocedal and Wright, 2006, p. 101](zotero://select/library/items/XU24DLQI)) ([pdf](zotero://open-pdf/library/items/SZ2KAERJ?page=121))

There are different algorithms that are worth considering, in order of complexity
1. theoretical conjugate gradient
2. practical conjugate gradient
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

Back to the main idea, we do not want to waste steps, therefore we choose directions that are orthogonal with respect to the matrix Q. These directions are called Q-orthogonal or conjugate directions, ie $$d_i^T Q d_j = 0 \quad\text{for } i\neq j$$Suppose we are in a $n$ dimensional feature space, in CG we search $n$ conjugate directions, ie a set of Q-Orthogonal vectors that form a basis for $\mathbb{R}^n$ and therefore are independent.

We can represent $x^*$ as a linear combination of the Q-orthogonal vectors $d_i$ that span through $n$, ie $$x^*=\sum_{i=1}^n\alpha_id_i$$ Through some algebraic steps, we obtain that $$\alpha_k=\frac{d_k^T b}{d_k^T Q d_k}$$

*how to find conjugate vectors*
An example of Q-orthogonal vectors are the eigenvectors, however they are expensive to obtain, so it's better to dynamically generate them using the gradient.


*theoretical algo*
Observe that $\alpha$ is the stepsize for the update of $x$, while $\beta$ is the stepsize for the stepsize of the conjugate directions (which uses the gradient to sum).

![[Pasted image 20250711174701.png]]

in exact arithmetic, the conjugate gradient method will terminate at the solution in at most n iterations. What is more remarkable is that when the distribution of the eigenvalues of A has certain favorable features, the algorithm will identify the solution in many fewer than n iterations.

## 2. Practical CG

We can use some theorems to write the standard form of the CG.

![[Pasted image 20250711175431.png]]

At any given point in Algorithm 5.2 we never need to know the vectors x, r , and p for more than the last two iterations. Accordingly, implementations of this algorithm overwrite old values of these vectors to save on storage. The major computational tasks to be performed at each step are computation of the matrix–vector product Apk, calculation of the inner products pkT ( Apk) and rkT+1rk+1, and calculation of three vector sums.

The CG method is recommended only for large problems; otherwise, Gaussian elimination or other factorization algorithms such as the singular value decomposition are to be preferred, since they are less sensitive to rounding errors. For large problems, the CG method has the advantage that it does not alter the coefficient matrix and (in contrast to factorization techniques) does not produce fill in the arrays holding the matrix. Another key property is that the CG method sometimes approaches the solution quickly, as we discuss next.

## 3. Preconditioned CG

Preconditioning means transforming the solution space to make it easier to solve the problem.
If we have $Ax=b$ with $k(A)$ big, then we transform the problem into $MAx=Mb$ with $k(MA)$ small.
The best conditioned matrix is the identity with $k(I)=1$, therefore we aim at having $MA\approx I$ which means $M\approx A^{-1}$.
There are many preconditioners that can be used such as incomplete LU factorization (ILU) or incomplete Cholesky (for symmetric PD matrices). 

In LU, even if A is sparse, L and U may be dense, therefore we approximate all values that are $\approx 0$ to be $=0$, forcing the sparsity into L and U.
Now, we have $A\approx LU$, therefore, instead of $M=A^{-1}$ we set $M=U^{-1}L^{-1}$.

Remember that not all the matrices can be decomposed in LU, but a permutation matrix P is enough to make it factorizable.
Also, there is no best preconditioner, it really depends on the structure of the problem. 

![[Pasted image 20250711182043.png]]

If we set $M=I$ , we obtain the standard practical CG. Here the main difference, and computational effort, is given by the system $My_{k+1}=r_{k+1}$.

## 4. Nonlinear CG (Fletcher-Reeves)

We have seen that CG can be viewed as a minimization algorithm for the convex quadratic functions. However, it can be expanded to general nonlinear functions.

![[Pasted image 20250711182823.png]]



