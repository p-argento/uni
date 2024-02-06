# Outline
---
![[Screenshot 2023-12-12 at 16.08.31.png]]

Project Guideline: [[Guidelines_4_Projects_ODS23.pdf]]

**Project 25**

The ML Model is a Support Vector Machine-type approach of your choice (in particular, with one or more kernels of your choice) for multi-class classification, e.g. using the standard One-to-Rest approach.

The first Optimization Algorithm is an algorithm of the class of interior-point methods, applied to either the primal or the dual(or both) formulation of the SVR.

The second optimization algorithm is a general-purpose solver applied to an appropriate formulation of the problem.

No off-the-shelf solver is allowed, save of course for (A2). Specific discussion should be provided about if and how solving one training problem in the One-to-Rest approach (if it is used) may provide useful solution that may help in solving the others.

(Reference to article: [[FRANGIONI_interior-point-article.pdf]] (online [here](https://epubs.siam.org/doi/abs/10.1137/S1052623400374379?journalCode=sjope8)))



# Math Background
---
[[_OP Survival Kit]]
[[Lagrangian]]

The book:
- "J. Nocedal, S.J. Wright, Numerical Optimization"

Key steps in the theory from [[SVM (ritvikmath)]]
1. [Lagrange Multipliers](https://www.youtube.com/watch?v=6oZT72-nnyI)
2. [The math](https://www.youtube.com/watch?v=bM4_AstaBZo)
3. [Soft margin](https://www.youtube.com/watch?v=IjSfa7Q8ngs&list=PLvcbYUQ5t0UH2MS_B6maLNJhK0jNyPJUY&index=70)
4. The Polynomial Kernel
5. [The RBF Kernel](https://www.youtube.com/watch?v=Q0ExqOphnW0&list=PLvcbYUQ5t0UH2MS_B6maLNJhK0jNyPJUY&index=59)
6. [The Dual Problem]((https://www.youtube.com/watch?v=6-ntMIaJpm0&list=PLvcbYUQ5t0UH2MS_B6maLNJhK0jNyPJUY&index=59)
7. [The Kernels](https://www.youtube.com/watch?v=OKFMZQyDROI&list=PLvcbYUQ5t0UH2MS_B6maLNJhK0jNyPJUY&index=57)


My [[SVM on Medium]] about these articles on **Medium** on SVM Talking maths:
1. [Quadratic Programming and Cholesky factorisation](https://medium.com/@marialavrovskaya/svm-talking-maths-quadratic-programming-and-cholesky-factorisation-968a493db10b)
2. [Formulating Support Vector Machine as a Quadratic Programming problem](https://towardsdatascience.com/svm-talking-maths-formulating-support-vector-machine-as-a-quadratic-programming-problem-ab5d30a8d73e)
3. [Using Interior Point Methods for SVM Training](https://towardsdatascience.com/svm-talking-algos-using-interior-point-methods-for-svm-training-d705cdf78c94)


# Coding
---
SVM with sklearn:
- [[SVM in Python (StatQuest)]]

SVM from Scratch:
- sentdex lessons 20-33 of this [playlist](https://www.youtube.com/playlist?list=PLQVvvaa0QuDfKTOs3Keq_kaG2P55YRn5v)
	- in particular [25](https://www.youtube.com/watch?v=AbVtcUBlBok)-28
- Also Patrick Loeber looks interesting
	- [here](https://www.youtube.com/watch?v=T9UcK-TxQGw) 
	- and a few years before [here](https://www.youtube.com/watch?v=UX0f9BNBcsY) 

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

New approaches:
- https://cienciasbasicas.udp.cl/cms/wp-content/uploads/2019/06/52.pdf
	- it is a new approach to svm, but maybe it's too much



