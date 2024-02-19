from https://www.youtube.com/watch?v=T9UcK-TxQGw


## SVM from scratch
Idea: Use a linear model and try to find a linear decision boundary (hyperplane) that best separates the data. The best hyperplane is the one that yield the largest separation/margin between both classes. So we choose the hyperplane so that the distance to the nearest data point on each side (support vectors) is maximized.

This code implements the training loop of an SVM using stochastic gradient descent with a hinge loss function and L2 regularization. The goal is to find a decision boundary that maximizes the margin between two classes while penalizing misclassifications.


```python

import numpy as np

class SVM:

  

def __init__(self, learning_rate=0.001, lambda_param=0.01, n_iters=1000):

self.lr = learning_rate

self.lambda_param = lambda_param

self.n_iters = n_iters

self.w = None

self.b = None

  

def fit(self, X, y):

  

# use np array

n_samples, n_features = X.shape

  

# now we want to make sure y is within -1 and 1

# so y is -1 if <= 0 and 1 otherwise

y_ = np.where(y <= 0, -1, 1)

  

# init weights (better if randomized)

self.w = np.zeros(n_features)

self.b = 0

  

# update rule for weights

for _ in range(self.n_iters):

for idx, x_i in enumerate(X):

  

# condition

condition = y_[idx] * (np.dot(x_i, self.w) - self.b) >= 1

  

if condition:

self.w -= self.lr * (2 * self.lambda_param * self.w)

self.b = self.b

else:

self.w -= self.lr * (2 * self.lambda_param * self.w - np.dot(x_i, y_[idx]))

self.b -= self.lr * y_[idx]

  
  

def predict(self, X):

approx = np.dot(X, self.w) - self.b

return np.sign(approx)

  
  

# %% [markdown]

# ## Testing

  

# %%

from sklearn.model_selection import train_test_split

from sklearn import datasets

import matplotlib.pyplot as plt

  

# %%

# importing example dataset

X, y = datasets.make_blobs(

n_samples=50, n_features=2, centers=2, cluster_std=1.05, random_state=40

)

y = np.where(y == 0, -1, 1)

  

X_train, X_test, y_train, y_test = train_test_split(

X, y, test_size=0.2, random_state=123

)

  

# %%

# defining classifier with the SVM class adn training

clf = SVM()

clf.fit(X_train, y_train)

predictions = clf.predict(X_test)

  

# %%

# testing accuracy

def accuracy(y_true, y_pred):

accuracy = np.sum(y_true == y_pred) / len(y_true)

return accuracy

  

print("SVM classification accuracy", accuracy(y_test, predictions))

  

# %%

# visualizing

def visualize_svm():

def get_hyperplane_value(x, w, b, offset):

return (-w[0] * x + b + offset) / w[1]

fig = plt.figure()

ax = fig.add_subplot(1, 1, 1)

plt.scatter(X[:,0], X[:,1], marker="o", c=y)

  

x0_1 = np.amin(X[:,0])

x0_2 = np.amax(X[:,0])

  

x1_1 = get_hyperplane_value(x0_1, clf.w, clf.b, 0)

x1_2 = get_hyperplane_value(x0_2, clf.w, clf.b, 0)

  

x1_1_m = get_hyperplane_value(x0_1, clf.w, clf.b, -1)

x1_2_m = get_hyperplane_value(x0_2, clf.w, clf.b, -1)

  

x1_1_p = get_hyperplane_value(x0_1, clf.w, clf.b, 1)

x1_2_p = get_hyperplane_value(x0_2, clf.w, clf.b, 1)

  

ax.plot([x0_1, x0_2], [x1_1, x1_2], "y--")

ax.plot([x0_1, x0_2], [x1_1_m, x1_2_m], "k")

ax.plot([x0_1, x0_2], [x1_1_p, x1_2_p], "k")

  

plt.show()

  

visualize_svm()
```
