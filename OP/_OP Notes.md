*Todo*
[[_UNI]]
[[MATLAB Tutorial]]
Start from the wrap-up of each set of slide and take schematic notes.



*Project*. No deadline. Send to professor each step, to check. Use whatever language you want (python, c++, matlab, ...) for the report.
Half october to form groups. List of projects. Choose one.
Use a private repo.
Try to use clear functions and API.
It is a plus to design it to be user-friendly, but not expected.
First the report, then the code. Show that you understood what you did in the report.

---
*appo*
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

ADiGator (Automatic Differentiator) in MATLAB produces code to compute derivatives of a function.

---

gradient definition -> the numeartor goes to zero faster than the denomoinator (which is linear). Look at the definition of derivative with the lim.
The numerator is the diffference between the approxiamtion of the function and the real function.

The tomography of alfa is smaller then eps for each value

In R2, the derivative is a number, so easy.
In n diimensions, the derivative is a vector. How do I know if it's zero or if it's increasing?

Vector valued function. 
The Jacobian is the matrix of all mxn. derivatives, which is actually a vector with all the gradients.

The second derivative is the Hessian matrix.
It is the Jacobian of the matrix.

Quadratic functions have the Hessian constant but NOT zero. 
Linear functions have the hessian = 0.
(check)
The second order model gives the curvature.

If the first order is 0, then it cannot dominates, so if second order is 0, then is 0.

In convex functions U, the line connecting dots is always greater than the corresponding function points.

f concave = -f convex

The Hessian is crucial to understand is the function is convex.
Only quadratic functions have a fixed Hessian, that can be tested to see if it's >0 or <0. But for n>2, you have to compute the Hessian for all points, which is impossible.
There are some functions that you can prove that are convex.
(look at the slide).

Convex vs Unimodal.
Typically is not quasi-convex.
Construct convex, so that is easy to minimize.

---
























