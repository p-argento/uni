There are two approaches for solving an unconstrained minimization optimization problem. [S](https://indrag49.github.io/Numerical-Optimization/introduction-to-unconstrained-optimization.html#algorithms-for-solving-unconstrained-minimization-tasks)
1. **Line Search Descent Method**
2. **Trust Region Method**
Trust-region methods are in some sense dual to line-search methods: trust-region methods first choose a step size (the size of the trust region) and then a step direction, while line-search methods first choose a step direction and then a step size. [S](https://en.wikipedia.org/wiki/Trust_region)

# Line Search
(Do no confuse linear search with line search)
In optimization, the line search strategy is one of the two basic iterative approaches to find a local minimum of the objective function $f:\mathbb{R}^n\rightarrow\mathbb{R}$. 
The line search approach first finds a descent direction along which the objective function $f$ will be reduced and then computes a step-size that determines how far $x$ should move along that direction. 
The *descent direction* can be computed can be computed by various methods, such as gradient descent or quasi-newton methods. 
The *step-size* can be determined either exactly or inexactly.
[S](https://en.wikipedia.org/wiki/Line_search)