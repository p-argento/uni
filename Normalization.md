[source](https://www.codecademy.com/article/normalization)

# Why Normalization
If the data points are on drastically different scales, then machine learning algorithms do not perform well. This is because they work by comparison.
Why using normalization? The goal is to make every datapoint have the same scale, so each feature is equally important..

# MinMax Normalization
For every feature, the minimum value get transformed into 0, the maximum into 1.
Then all the data points get transformed into a value between 0 and 1, using the following formula.

![[Pasted image 20231112220720.png|200]]

Downside? Outliers. They can ruin everything, setting a very bad max or min.

![[Pasted image 20231112221611.png]]

# Z-score Normalization
The mean is zero and all the data points are around the zero.

![[Pasted image 20231112221123.png|200]]

Downside? The datapoints are NOT in the exact same scale.

![[Pasted image 20231112221551.png]]