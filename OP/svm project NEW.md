# Utils
[Overleaf](https://www.overleaf.com/project/65dc61340f4e3e332b7dacc7)

```latex
•	Scalars: Denoted by lowercase letters, e.g.,  w ,  b ,  x_1 . These represent single numbers.
•	Vectors: Denoted by boldface lowercase letters, e.g.,  \mathbf{w} ,  \mathbf{x} ,  \mathbf{y} . Vectors represent a sequence of numbers.
•	Matrices: Denoted by boldface uppercase letters, e.g.,  \mathbf{X} ,  \mathbf{D} . Matrices represent a table of numbers (or vectors stacked together).
```



# News
- 1/09/24: call with Duc, we are fixing the draft of the report so that tomorrow we can send it to frangioni. We decided to split the work for now, duc will do the barrier method and I will do the general purpose solver. We set 20/9 as the deadline to meet again and send everything to frangioni.

# General-Purpose Solver

The idea here is to use the [quadratic solver](https://www.cvxpy.org/examples/basic/quadratic_program.html) from the library CVXPY.
To do so, we need to formulate the SVM problem as a quadratic programming problem.

I am investigating if the formulation of [libsvm](https://www.csie.ntu.edu.tw/~cjlin/libsvm/) can be used, or if I need to do it from scratch. Following this [guide](https://www.csie.ntu.edu.tw/~cjlin/papers/guide/guide.pdf)
This [article](https://www.csie.ntu.edu.tw/~cjlin/papers/libsvm.pdf) , which I believe is the main paper of LIBSVM, mentions the use of a decomposition method for solving the dual problem of the svm, because Q may be too big to be stored. Not our task though, but the definition of the problem is the same.

Among CVXPY solvers, I think OSQP is the best. It is also described in this [page](https://osqp.org/docs/solver/index.html) of oxford.






(Maybe I can try also [scipy](https://docs.scipy.org/doc/scipy/reference/optimize.html) as mentioned [here](https://stackoverflow.com/questions/17009774/quadratic-program-qp-solver-that-only-depends-on-numpy-scipy))









