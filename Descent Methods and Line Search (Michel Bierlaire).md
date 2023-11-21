From [this playlist](https://youtube.com/playlist?list=PL10NOnsbP5Q7wNrYItE2GhKq05cVov97e&si=Rd85llfgFQAeddFU) on youtube by Michel Bierblaire.


We're investigating a family of algorithms to find the minimum of a function.
The first one is the Gradient Method. It uses $-\nabla f$  as a step, since it it the steepest descent.
Zig-zag behaviour of the algorithm.

Preconditioning.
BY just changing the value before, the algorithm can converge in just one iteration.
We modify the geometry of the function to make the algo faster.

Consider a matrix symmetric postive definite, so that we can calculate the Cholesky factor.
The Cholesky factor is a lower triangular matrix which can be seen as the square root of the matrix.
![[Pasted image 20231121155757.png|400]]