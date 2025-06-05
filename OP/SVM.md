# News
- 1/09/24: call with Duc, we are fixing the draft of the report so that tomorrow we can send it to frangioni. We decided to split the work for now, duc will do the barrier method and I will do the general purpose solver. We set 20/9 as the deadline to meet again and send everything to frangioni.

- 11/11: trying to find a direction [[Basics of Numerical Linear Algebra]]

- 19/03 working on frangioni's code on IP

# Outline
---

![](Screenshot%202023-12-12%20at%2016.08.31.png)
Project Guideline: [[OP/docs/Guidelines_4_Projects_ODS23.pdf]]
Article linked:  [[FRANGIONI_svm_interior-point-article.pdf]] (online [here](https://epubs.siam.org/doi/abs/10.1137/S1052623400374379?journalCode=sjope8))

**Project 25**
The ML Model is a Support Vector Machine-type approach of your choice (in particular, with one or more kernels of your choice) for multi-class classification, e.g. using the standard One-to-Rest approach.

The first Optimization Algorithm is an algorithm of the class of interior-point methods, applied to either the primal or the dual(or both) formulation of the SVR.

The second optimization algorithm is a general-purpose solver applied to an appropriate formulation of the problem.

No off-the-shelf solver is allowed, save of course for (A2). Specific discussion should be provided about if and how solving one training problem in the One-to-Rest approach (if it is used) may provide useful solution that may help in solving the others.


# Main Sources
---
[[OP/OPTIMIZATION Survival Kit]]

The book:
- "J. Nocedal, S.J. Wright, Numerical Optimization"
	- [[Nocedal, Wright - My Notes]]

In [["Visually Explained" Videos]] some theory.

In [[SVM_MATH from ritvikmat]], find key steps in the theory from youtube.

In [[SVM_IP from Medium]], notes from articles on Medium on SVM with Interior Points.

In [[SVM_CODE from youtube]]

See [paper](/Users/pietro/_DS/OP/SVM_project/articles/survey_piccialli_sciandrone4OR.pdf)

# More resources
---
SVM from Scratch:
- sentdex lessons 20-33 of this [playlist](https://www.youtube.com/playlist?list=PLQVvvaa0QuDfKTOs3Keq_kaG2P55YRn5v)
	- in particular [25](https://www.youtube.com/watch?v=AbVtcUBlBok)-28
- Also Patrick Loeber
	- [here](https://www.youtube.com/watch?v=T9UcK-TxQGw)  and a few years before [here](https://www.youtube.com/watch?v=UX0f9BNBcsY) 
	- it can be used for comparison with Gradient Descent
	- theory [here](https://towardsdatascience.com/support-vector-machine-introduction-to-machine-learning-algorithms-934a444fca47)

Examples on Github:
- [This Repository](https://github.com/MariaLavrovskaya/Nowearetalking) by [MariaLavrovskaya](https://github.com/MariaLavrovskaya) explained in the Medium article.

SVM with One-to-Rest Approach:
- [creating-one-vs-rest-and-one-vs-one-svm-classifiers-with-scikit-learn.md](https://github.com/christianversloot/machine-learning-articles/blob/main/creating-one-vs-rest-and-one-vs-one-svm-classifiers-with-scikit-learn.md)
	- an introduction to multiclass classification with one-vs-rest 
- https://www.geeksforgeeks.org/one-vs-rest-strategy-for-multi-class-classification/
	- another introduction
- [[svm-ovr-cancer.pdf]]
	- looks like a super interesting example especially for (A2)
-  https://www.youtube.com/watch?v=YChPxoJ-Sh4
	- 5 minutes on OneVsRest Approach (maybe useless)

SVM and Interior Points:
- https://www.cs.cmu.edu/~ggordon/10725-F12/scribes/10725_Lecture22.pdf
	- an explanation
- nocedal, wright

New approaches:
- https://cienciasbasicas.udp.cl/cms/wp-content/uploads/2019/06/52.pdf
	- it is a new approach to svm, but maybe it's too much
- https://github.com/gilbertgede/PyIntropt/tree/master
	- implementation of interior point


# Utils
---
[Overleaf](https://www.overleaf.com/project/65dc61340f4e3e332b7dacc7)

```latex
•	Scalars: Denoted by lowercase letters, e.g.,  w ,  b ,  x_1 . These represent single numbers.
•	Vectors: Denoted by boldface lowercase letters, e.g.,  \mathbf{w} ,  \mathbf{x} ,  \mathbf{y} . Vectors represent a sequence of numbers.
•	Matrices: Denoted by boldface uppercase letters, e.g.,  \mathbf{X} ,  \mathbf{D} . Matrices represent a table of numbers (or vectors stacked together).
```




# General-Purpose Solver
---

The idea here is to use the [quadratic solver](https://www.cvxpy.org/examples/basic/quadratic_program.html) from the library CVXPY.
To do so, we need to formulate the SVM problem as a quadratic programming problem.

I am investigating if the formulation of [libsvm](https://www.csie.ntu.edu.tw/~cjlin/libsvm/) can be used, or if I need to do it from scratch. Following this [guide](https://www.csie.ntu.edu.tw/~cjlin/papers/guide/guide.pdf)
This [article](https://www.csie.ntu.edu.tw/~cjlin/papers/libsvm.pdf) , which I believe is the main paper of LIBSVM, mentions the use of a decomposition method for solving the dual problem of the svm, because Q may be too big to be stored. Not our task though, but the definition of the problem is the same.

Among CVXPY solvers, I think OSQP is the best. It is also described in this [page](https://osqp.org/docs/solver/index.html) of oxford.

(Maybe I can try also [scipy](https://docs.scipy.org/doc/scipy/reference/optimize.html) as mentioned [here](https://stackoverflow.com/questions/17009774/quadratic-program-qp-solver-that-only-depends-on-numpy-scipy))




