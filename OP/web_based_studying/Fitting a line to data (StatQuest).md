> The only way around is through.
# Least Squares
[Statquest Video](https://www.youtube.com/watch?v=PaFPbb66DxQ)

**Process**
1. We want to minimize the square of the distance between the observed values and the target line
2. We do this by taking the derivative of the sum of squared residuals and finding where it is equal to zero
3. The final line minimizes the sums of square (giving the least squares) between it and the real data.

**Key moment**
The idea is to find the minimum of the function that plots the sum of squared residual based on the slope the target function. The goal is finding the slope of the target function (and the intercept) so that the sum of squared residual is minimum. And this is done by computing the derivative of the sum of squared residuals.

From this
![[Pasted image 20231119162158.png|300]]

To the plot of sum of squared residuals and the corresponding rotation.
Look for the one with the least squares.
If the slope is not zero, than it means there's a correlation to explain one variable with the other.

![[Pasted image 20231118172820.png|300]]



# Linear Regression
[statQuest video](https://www.youtube.com/watch?v=nk2CQITm_eo)

General Linear Models.

3 most important concepts
1. Use least-squares to fit a line to data
2. calculate $R^2$
3. calculate p-value for $R^2$

### Calculating $R^2$
**Around the mean**
Move al the points on the y-axis. 
Then compute the mean of y.
Sum of squares (SS) around the mean is
$$SS(mean)=(data-mean)^2$$
Variation around the mean is the average sum of squares per each instance
$$Var(mean)=\frac{(data-mean)^2}{instances}=\frac{SS(mean)}{n}$$
**Around the line**
Sum of squares (SS) around the line is
$$SS(fit)=(data-line)^2$$
Variation around the line is the average sum of squares per instance
$$Var(fit)=\frac{(data-line)^2}{instances}=\frac{SS(line)}{n}$$

> Reminder
> $$variance=\frac{sums\ of\ square}{number\ of\ things}=average\ SS$$

**Definition of $R^2$**
It tells how much of the variation can be explained by taking into account the independent variable.
$$R^2=\frac{Var(mean)-Var(fit)}{Var(mean)}$$
Since n is the same, we can use the SS instead of the variation.
"The x-variable explains $R^2$% of the y-variable."
If the line is horizontally, then it means that the variance is all expained by the variance of x-variable around its mean.

![[Pasted image 20231119164413.png|500]]

**Multidimensional Regression**
In 3D, we fit a plane instead of a line.
Adding variables will never reduce $R^2$.
It can only increase, since the randomness of other variables like flipping a coin can explain some of the variance of the target variable.
The more parameters we add to the equation, the more opportunities we have for random events to reduce SS(fit), resulting in a higher (and better) $R^2$.
For this reason, we are looking for an "adjusted" $R^2$ that scales by the number of parameters.

**p-value**
We are looking for an "adjusted" $R^2$ that scales by the number of parameters.
The p-value determines how reliable the relationship $R^2$ is.
The Degrees of Freedom (DF) are the extra parameters in the"fit". They turn the SS into variances.
In 2D, the fit line has an extra parameter p (the slope) compared to the mean line, which is only an horizontal line with the y-intercept. The difference is then 2-1=1.
Calculate F.
$$F=\frac{var\ expained\ by\ DF}{var\ NOT\ expained\ by\ DF}=\frac{\frac{SS(mean)-SS(fit)}{p_{fit}-p_{min}
}}{\frac{SS(fit)}{n-p_{fit}}}$$
Calculate the F for many random sets and plot the results.
Then locate the value of the target set and calculate the p-value.
It needs to be small, since the p-value is the number of more extreme values divided by all the values.


# Gradient Descent
[video on GD](https://www.youtube.com/watch?v=sDv4f4s2SB8)

Process
1. Take the Gradient of the Loss Function
2. Pick random initial values for the parameters
3. Plug the parameter values into the gradient
4. Calculate Step Size = Slope x Learning Rate
5. Calculate New Parameters = Old Parameters - Step Size

Stopping criteria usually
1. 1000 iterations
2. step size < 0.001

Loss function
1. The Sum of the Squared residual is just one type of Loss Function
2. Use the Gradient to descend to lowest point in the Loss Function, which, in this case, is the Sum of the Squared Residuals.

The Chain Rule
1. It is the rule to calculate the derivative.

Each step gets smaller the closer we get to the bottom of the curve.

**Why Gradient Descent**
If we were using *Least Squares* to solve for the optimal value for the Intercept, we would simply find where the slope of the curve is = 0.
In contrast, *Gradient Descend* finds the minimum value by taking steps from an initial guess until it reaches the best value.
This makes GD very useful when it is not possible to solve for where the derivative = 0.
And then, it can be used in so many different situations.

> My Point
>But this point might not be the best value, since the derivative is =0 for max, min and saddle.
>And the best value might not be differentiable, so it would not be possible to find it using the derivative.