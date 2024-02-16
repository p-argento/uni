(using formulas from https://towardsdatascience.com/svm-talking-maths-formulating-support-vector-machine-as-a-quadratic-programming-problem-ab5d30a8d73e)

The goal of this section is to define the SVM as a Quadratic Programming Problem through its dual. Then, the Interior Point method will be used to solve the KKT conditions. In particular, Newton's Method will be used to iteratively go through KKT modified conditions.

## Defining Hyperplane
We define the separating hyperplane as $$f(x)=\beta_0+\beta_1x_1+\beta_2x_2+...+\beta_px_p=0$$Some important notes are the following.
The the vector $\beta^T$ is the normal vector, perpendicular to the surface at a given point.
The distance of any point $x$ of the dataset from the hyperplane $L$ (called margin) is $$M=\frac{\beta^Tx+\beta_0}{||\beta||}=\frac{f(x)}{||f'(x)||}$$The denominator can be expressed in this way because taking the derivative of $f$ will leave all the betas.
Now, we arbitrarily set $$||\beta||=\frac1 M$$ and the margin M can be expressed as $$M = \frac2{||\beta||}$$


## Formulating Optimization Problem
Since we are trying to find the vector $\beta$ defining the hyperplane that maximizes the margin M. For convenience, we will express it with the minimum formulation $$\max_{\beta}\frac2 {||\beta||}\longrightarrow \min_{\beta}||\beta||$$ In real-world problems, the classes are not separated by a hard margin, meaning a clear distinction made by the hyperplane, but a soft margin must be used.
The soft margin will include in the problem formulation a misclassification error.
We add slack variables $\epsilon_i\geq0$ and 

$$\min_{\beta}||\beta||+C\sum\epsilon_i$$ This i
 

What are the constraints?

...

## Writing the Lagrangian


