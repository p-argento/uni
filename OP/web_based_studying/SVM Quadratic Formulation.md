(using formulas from https://towardsdatascience.com/svm-talking-maths-formulating-support-vector-machine-as-a-quadratic-programming-problem-ab5d30a8d73e)

The goal of this section is to define the SVM as a Quadratic Programming Problem through its dual. Then, the Interior Point method will be used to solve the KKT conditions. In particular, Newton's Method will be used to iteratively go through KKT modified conditions.

## Defining Hyperplane
We define the separating hyperplane as $$f(x)=b+\omega_1x_1+\omega_2x_2+...+\omega_px_p=0$$Some important notes are the following.
The the vector $\beta^T$ is the normal vector, perpendicular to the surface at a given point.
The distance of any point $x$ of the dataset from the hyperplane $L$ (called margin) is $$M=\frac{\omega^Tx+b}{||\omega||}=\frac{f(x)}{||f'(x)||}$$The denominator can be expressed in this way because taking the derivative of $f$ will leave all the betas.

For the data points on the margins, this distance is equal to 1 (since they are exactly on the margin).
If we consider two data points on opposite margins (called support vectors) one with label +1 and the other with label -1, then their distances from the hyperplane must be $$w^T x_1 + b = 1\qquad w^T x_2 + b = -1$$

$$||\omega||=\frac1 M$$ and the margin M can be expressed as $$M = \frac2{||\omega||}$$

## Formulating Optimization Problem
Since we are trying to find the vector $\beta$ defining the hyperplane that maximizes the margin M. For convenience, we will express it with the minimum formulation $$\max_{\omega,b}\frac2 {||\omega||}\longrightarrow \min_{\omega,b}||\omega||$$ In real-world problems, the classes are not separated by a hard margin, meaning a clear distinction made by the hyperplane, but a soft margin must be used.
The soft margin will include in the problem formulation a misclassification error.
We add slack variables $\epsilon_i$ associated to each data point $x_i$ $$\min_{\omega}||\omega||+C\sum_{i=1}^N\epsilon_i$$ Subject to  $$
\begin{align}
&\epsilon_i\geq0 \\
&y_i(x_i^T\omega_i+b)\geq1-\epsilon_i \\
\end{align}$$The idea behind this last constraint is the following.
Let's start with $\epsilon_i=0$.
$y_i=\pm1$ as stated above, so if the left part of the equation is positive, it means that the two terms have the same sign and therefore the point is classified correctly. The higher the value, the higher the confidence. However, if the point falls within the margin, meaning that $u_i(x_i^T\omega_i+b)\leq1$ , we have a problem.
At this point, we add the $\epsilon\geq0$ to relax the constraint.
Now, a point that is misclassified (within the threshold $\geq1-\epsilon_i$) will lead to an a higher $\epsilon_i$ depending on the distance from the margin. The $\epsilon_i$ will then influence the minimization of the objective function by increasing the penalty term, together with the $C$ value, that is defined as $\sum_{i=1}^N\leq C$.

Until now, the SVM problem with soft margin can be written as $$\begin{align}
&\min_{\omega}||\omega||+C\sum_{i=1}^N\epsilon_i \\
\text{subject to }&\\
&\epsilon_i\geq0 \\
&y_i(x_i^T\omega_i+b)\geq1-\epsilon_i \quad\forall i\\
\end{align}$$

## Writing the Lagrangian
From the constrained optimization problem just defined, we write the Langragian to express it as an unconstrained problem. $$\mathcal{L}_p(\omega,b,\epsilon,\alpha,\lambda)=$$

