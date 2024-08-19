[[17.PDPandICE.pdf]]

## PDP and ICE Plots
[youtube video](https://www.youtube.com/watch?v=dEhbS37Kglc)

Both Partial Dependence (PDPs) and Individual Conditional Expectation (ICE) Plots are used to understand and explain machine learning models. PDPs can tell us if a relationship between a model feature and target variable is linear, non-linear or if there is no relationship. Similarly, ICE plots are used to visualise interactions.

In the plot, we draw a line for each instance in the dataset perturbating one variable (x-axis) and computing the result. for the target variable (y-axis). Then we compute the average, and that line is the Partial Dependence (PDP) and it is easy now to identify the type of relationship. Note that it might be necessary to rescale along the axis to better clarify the shape of the line. In general, if a model does not use a variable to make predictions, its PDP will be flat.  

![[Pasted image 20240817102455.png]]

![[Pasted image 20240817102511.png]]

The short vertical lines in the red part rectangle below are know as a RUG plot. It means that 10% of the dataset falls before the first bar, 20% before the second bar and so on... Here the data is equally distributed, but if you can see that the bars are shifted towards the left. This means that most of the dataset is skewed to the left.

By centering all the individual lines we can get a better interpretation. To center the line, the starting value is subtracted from every point on the line. 
In the plot below, we can clearly see how different instances behave differently by changing a specific value, in particular we can distinguish classic cars, whose value increase with the car age, from normal cars.

![[Pasted image 20240817103854.png]]

In summary,
1. PDP show us a general trend
2. ICE Plots show us how individual instances deviate from this trend

In math terms
1. f is the  
2. S is a set of features
3. C all the features excluded S
4. the average
![[Pasted image 20240817104314.png|300]]

This is actually an approximation of the PD function. And the following is the correct one.
![[Pasted image 20240817104409.png]]


## To do
guarda la 4.3
e prova risultati di 5.3



