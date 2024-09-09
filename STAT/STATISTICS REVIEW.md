
# Slides
1. Probabilities and Independence
2. R Introduction
3. Bayes' Rule and applications
4. Discrete Random Variables
5. (null)
6. Recall on calculus
7. R data access and programming
8. Continuous Random Variables
9. Expectation and Variance
10. Moments. Functions of Random Variables
11. Distance between distributions
12. Simulation
13. Power Law's and Zipf's Law
14. Law of large numbers. The central limit theorem.
15. Graphical summaries. Kernel Density Estimation.
16. Numerical summaries

17. Data preprocessing in R. Estimators.
18. Unbiased estimators. Efficiency and MSE
19. Maximum Likelihood Estimation
20. Linear Regression. Least Squares Estimation.
21. Non-linear, and multiple linear Regression
22. Issues with linear regression. Logistic Regression.

23. Statistical Decision Theory
24. (null)
25. (null)
26. Confidence Intervals: mean, proportion, linear regression.
27. Bootstrap and resampling methods.
28. (null)

29. Hypotheses testing. One-sample t-test and application to linear regression.
30. Classifier performance metrics in R.
31. Two-sample tests of the mean and applications to classifier comparison.
32. Multiple-sample tests of the mean and applications to classifier comparison.
33. Fitting distributions. Testing independence/association.








# 23. Statistical Decision Theory
(or Probabilistic Classifiers)

> Which hypothesis is the most probable given the observed data?
1. use MLE
2. use MAP (Maximum A Posteriori)

A probabilistic classifier is a function that returns the probability of having a class c given some predictive features w. It means $f_{\theta}(c|w)=P(C=c|W=w, \theta)$.

Params theta of the probabilistic classifier are found using ML maximization, that is asymptoptically minimizing the KL Divergence.


> Which is the most probable class value given w and $\theta$?

Bayes Decision Rule is optimal


> Which is the most probable class value given w only (ie without fixing the params?)









