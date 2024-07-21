Each algorithm will be described as
1. idea
2. steps
3. parameters

# Neural Networks

## Perceptron
*Idea*
A single layer network that contains only input and output nodes, with sign as the activation function.
*Algorithm*
1. initialize weights
2. until conditions are not met
	1. calculate predictions
		1. $y_{pred} = f(w^k, x_i)$
	2. update weights
		1. $w^{k+1} = w^k + \lambda * [y_i-y_{pred}] * x_i$
*Params*
1. $\lambda$ is the learning rate, usually 0.1 or 0.001
2. epochs

## Deep Neural Networks
*Idea*


*Algorithm*
1. ...
2. until stopping conditions are met
	1. calculate predictions $$y_{pred}=f( w_jx_{ij})$$
	2. calculate the error (usually Sum of Squared Residuals) $$E=\frac 1 2 \sum_{i=1}^N\bigg(y_i-f(\sum_j w_jx_{ij})\bigg)^2$$
	3. update weights $$w_j^{(k+1)}=w_j^{k}-\lambda \frac{\delta E}{\delta w_j}$$
It is a 2-step process
1. forward pass
	1. computing the network output $o_i$
2. backward pass
	1. computing the loss function gradients and update




*Params*
For each layer, we can set
1. activation function
	1. relu, tanh, softmax

