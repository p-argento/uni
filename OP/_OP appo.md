2023-09-29
*Multi-objective Optimization*


*Algebra*
If the scalar product is >0 then the cos(a) is >a (because of the geometric interpretation) then the directions of vectors are on the same side.

---

E-6 for gradient norm as a stop criteria 
What is alfa?
The value of the function has to go down, but we don't know about the norm of the gradient .
If the eigenvalues are 1 and 100 then it will take a lot of time to get to minimum using gradient algo.
We are going towards the zero (E-6) of the norm of the gradient.

Can I prove that it is converging? That the norm of the gradient is converging to zero? We saw that it is not always a monotonous descend.

Each gradient direction is orthogonal to the previous one. If all eigenvalues are positive (positively definite matrix). Can I estimate the error? ...
$$biggest \  eignvalue = max\frac{(d^T Q d)}
{||d||^2}
$$
A(x1) is the error at the begging but then it decreases exponentially.
The algo converges $$A(x^{i+1})<r^iA(x^1)$$ Where x^1 is the first known error..

---

# conjugate gradient
Start from anywhere and moves on directions that are orthogonal to one aanother in the spherical space (conjugate).
At each iteration you optimize 
You get the optimal value of the line.
The optimum is the product of the two directoins?
The first iteration is the same as the gradient method. Then it changes directions.

In the matlab algo
ecc->eccentricity->conditioning of the matrix?
rank->do we want 0 eigenvalues?

Look at the convergence plot of algo.
See the difference between gradient and conjugate.
`hold on` to see the result on the same plot.

Look at the `diagPrecond` algorithm.





