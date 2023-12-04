# Lagrange Multipliers
---
from [Khan Academy](https://www.youtube.com/watch?v=yuqB-d5MjZA)

![[Pasted image 20231204222813.png]]

The core idea is to the set the gradients proportional to each other because this means that the contour lines of one function are tangent to the contour lines of the other.
$f$ is objective function
$g$ is the constraint

# Lagrangian
---
from [Khan Academy](https://www.youtube.com/watch?v=hQ4UNu1P2kw&t=33s)

![[Pasted image 20231204223609.png]]
![[Pasted image 20231204224809.png]]

In a constraint optimization problem.
The Lagrangian is just a way to encapsulate all the equations of Lagrange Multipliers into one, which is $$\nabla\mathcal{L}=0$$
Why that? Because for a computer is easier.
And this happens because it is an unconstrained optimization problem.
Basically, we transformed a constrained optimization problem into an unconstrained problem. And now we only need to compute the max of the Lagrangian.

