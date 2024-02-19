[StatQuest 1/3](https://www.youtube.com/watch?v=efR1C6CvhmE)



[StatQuest 2/3](https://www.youtube.com/watch?v=Toet3EiSFcM)
# 1. Support Vector Machines
---
Different steps (increasingly complex classifiers)
1. Maximal Margin Classifiers
2. Support Vector Classifier (or Soft Margin Classifier)
3. Support Vector Machines

Maximal Margin Classifiers are super-sensitive to outlinears and therefore not useful.
We must allow misclassification.
This is an example of the bias/variance tradeoff, that we find across all of machine learning.
Now this is called soft marging.
How to find the best soft margin? Using cross validation.
We are using a Soft Margin Classifier, also called Support Vector Classifier.
The observations on the edge are called support vectors.

With 2-dimensions, the classifier is a point.
With 2-dimensions, the classifier is a line (1-dimension).
With 3-dimensions, the classifier is a plane (2-dimension).
With 4-dimensions, the classifier is a hyperplane.
The classifiers are flat affine subspace, basically they are all hyperplanes.

What if with have data like this?
![[Pasted image 20231201120913.png]]
We use Support Vector Machines.
They add a new dimension to try to draw the hyperplane.

But how do we decide how to transform the data?
SVM use Kernel Functions to systematically find Support Vector Classifiers in higher dimensions.

An example is the Polynomial Kernel, with the parameter d=degrees of polynomial.
With d=2, the PK computes the 2-dimensional relationships between each pair of observations, used to find the Support Vector Classifier (aka hyperplane).
Find a good value for d with cross validation.

Another example is the Radial Kernel, aka Radial Basis Function Kernel or RBF Kernel.
It finds SVC in infinite dimensions.
It behaves like a Weighted Nearest Neighbor Model.
Basically the closest observations have more influence.

How does the Kernel function calculates the relationships?
Using the Kernel Trick.
Basically Kernel function only calculates the relationship between every pair of points without actually transforming the data to the higher dimension.
This reduces the computation required.

# 2. Polynomial Kernel
---
The Polynomial Kernel computes relationship between pair of observations. 
The Polynomial Kernel of a Support Vector Classifier looks like this $$(a\times b+r)^d$$
$a,b$ are two different observations in the dataset
$r$ determines the coefficient of the polynomial
$d$ sets the degree of the polynomial
$\Rightarrow r,d$ are determined using cross-validation

...

If $r=0$, the points get scaled, but they do not change dimension.
For example, if $d=2$, we get $(a\times b)^2=(a^2)\cdot(b^2)$





# 3. Radial Kernel
---
One way to deal with overlapping data is to use a Support Vector Machine with a Radial Kernel.
$$e^{-\gamma(a-b)^2}$$
$\gamma$ scales the squared distance and thus it scales the influence. It is determined using Cross Validation.

It's not possible to visualize it, because the Radial Kernel finds SVC in infinte dimensions.

It behaves like weighted nearest neighbor.
The further two observations are from each other, the less influence they have on each other. If they are really far, we get a number very close to zero.
When we plug values into the Radial Kernel, we get the high-dimensional relationship.

The proof uses the Taylor Series Expansions.
...

The Radial Kernel is equal to a Dot Product that has coordinates for an infinite number of dimensions.



# Coding
---
# Intro
---
We we'll use SVM with RBF Kernel.
The dataset is ["default of credit card clients"](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) from UCI ML Repo.

SVM are one of the best ML methods when getting the correct answer is the priority, rather than understanding why we get that answer.

Expected output
![[Pasted image 20231202161227.png]]

Steps
1. importing data
2. missing data
3. downsampling data
4. formatting data for svm
5. building a preliminary svm
6. optimize parameters with cross-validation
7. building, evaluating, drawing and interpreting the SVM

Comment.
They are great 'out of the box' and then optimize them doesn't give a huge bonus (like classification trees).



