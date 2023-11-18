[[11.  Classification Model Evaluation]]
# 8. Intro
Supervised learning refers to problem where the value of a target should be predicted based on the values of other attributes.
Problems with a categorical target attribute are called *classification*.
Problems with a numerical target attribute are called *regression*.

ML definition by Arthur Samuel 1959.
> ML is the field of study that gives computers the ability to learn without being explicitly programmed.

ML definition by Tom Mitchell 1997
> A computer program is said 
> to learn from experience E 
> with some task T
> and some performance measure P,
> if its performance P on task T improves with experience E.

Classification consists in learning a model/function f that maps each attribute set x into one of the predefined class labels y -> $f(x) = y$
The learning is performed on a given collection of records named *training set*.
Each record is characterized by a tuple $(x,y)$.
$x$ -> attribute, predictor, indipendent variable, input
$y$ -> class, response, dependent variable, output

The *goal* is to assign previously unseen records to a class.
A *test set* is used to determine the accuracy of the model.

Base classifiers
- decision-tree-based classifiers
- rule-based classifiers
- instance-based classifiers (nearest-neighbour)
- neural networks
- deep learning
- naïve bayes (and Bayesan Belief) Methods
- Support Vector Machines

Ensemble classifiers
- Boosting
- Bagging
- Random Forests

# 9. Instance-based classifiers
**Definition**
Instance-based learning (sometimes called *memory-based learning*) is a family of learning algorithms that, instead of performing explicit generalization, compare new problem instances with instances seen in training, which have been stored in memory.

**Advantages**
- Adaptation -> for previously unseen data, it store a new instance or throw an old instance away.

**Disadvantages**
- "Lazy learners" -> computation is postponed until a new instance is observed, without building a model explicitly (model free)
	- in contrast, "eager learners" spend time in building the model, but then the classification is faster
- Expensive classification of unknown records -> given n training items, the complexity of classifying a single instance is O(n)
	- we need to compute every time the proximity values between the test instance and the training examples
- Suscetible to noise -> because it is based on local data

**Examples**
- KNN
- Kernel Machines
- Radial Basis Function Network (RBF Networks)

## K-NN
It's the Nearest-Neighbour Classifier.
Basic Idea:
> If it walks like a duck, quacks like a duck, then it's probably a duck.

**Requires**
1. Training Set of stored records
2. Distance metric between records
3. Value of k nearest neighbour to retrieve

**Instructions**, given a training set and a test set.
1. Compute distances from records
2. Identify k nearest records
3. Determine label
	1. (classification) by taking the majority labels of nn
	2. (regression) by computing the average between values

**Choosing the value of K**
- too small -> sensitive to noise points and leads to overfitting
- too large -> neighbourhood includes points from other classes
General practice ->  *$K=sqrt(N)$* where N is the number of samples in the training set.

**How to determine the class**
Majority Voting
-> take the majority vote of class labels among the k-nearest-neighours
Distance-weighted Voting (to reduce the impact of k)
-> use the weight factor $w=1/d^2$ to weight the vote according to the euclidean distance.

**Dimensionality issues**
High dimensional data (curse of dimensionality) -> normalize vectors to unit length.
High differences in the scale measure of attributes -> scale

**PEBLS**
Parallel Exemplar-Based Learning System is a KNN algorithm with K=1.
It is designed to handle nominal attributes.
It measures the distance between two values of a nominal attribute using the Modified Value Difference Metric (MVDM).

The distance between Nominal Attributes Values is: $$d\left(V_1, V_2\right)=\sum_{i=1}^k\left|\frac{n_{i 1}}{n_1}-\frac{n_{i 2}}{n_2}\right|$$$V_1,V_2$ -> the pair of nominal attributes values.
$i$ -> the class to label 
$n_{ij}$ -> number of examples from class $i$ with attribute value $V_j$
$n_j$ -> number of examples with attribute value $V_j$

![[Pasted image 20231117171143.png]]

**Distance between Records**
![[Pasted image 20231117181518.png]]


# 10. Naïve Bayes Classifier
It is a probabilistic framework for solving classification problems.

**Bayes Theorem**
The probability of getting the class variable $Y$,
given the attribute sets $X={X_1,X_2,...,X_d}$, is
![[Pasted image 20231117182459.png|350]]

**Bayes for classification**
By knowing the posterior probability P(Y|X) for every combination of X and Y, a test record X' can be classified by finding the class Y' that maximizes the posterior probability P(Y'|X').
And for the Bayes Theorem, this is equivalent of choosing the value of Y' that maximizes P(X'|Y')P(Y').

**Naive bayes classifier**


**How to estimate probability from data***


**M-estimate of Conditional Probability**


















