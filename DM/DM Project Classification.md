There is an orange cluster characterized by high values of explicit and spechiness.
Then a green one with low energy, low loudness, high acousticness.
A red one, with high duration, high n_beats, high n_bars.

### (gpt) Clustering Numerical and Binary data
Certainly! When working with a dataset that contains both numerical and binary features, applying clustering separately to these different types of features can be a strategy to consider. This approach recognizes that numerical and binary features often have distinct characteristics, and their contributions to the clustering process might be better understood when treated separately.

Here's a more detailed explanation:

1. **Clustering Separately:**
   - Instead of applying k-means clustering to the entire dataset, you can perform clustering separately on the numerical features and the binary features. This allows the clustering algorithm to operate on each feature type independently, capturing the inherent structures within numerical and binary spaces.

2. **Numerical Features:**
   - For numerical features, you might choose to use standard k-means clustering with the Euclidean distance metric, as these features often have a continuous range of values. The clustering algorithm can identify patterns based on the magnitudes and distances between numerical data points.

3. **Binary Features:**
   - Binary features, on the other hand, are limited to two values (0 or 1). The Euclidean distance may not be the most suitable metric for binary features. Instead, you can explore alternative distance metrics, such as Hamming distance or Jaccard similarity, which are specifically designed for binary data. These metrics measure dissimilarity based on the number of differing bits or the overlap of binary values, respectively.

4. **Combining Results:**
   - Once you have performed clustering separately on numerical and binary features, you can combine the results. This integration could involve merging the cluster assignments or conducting further analysis to understand how clusters in one feature type relate to clusters in the other.

5. **Interpretability:**
   - Separating clustering for different feature types may enhance interpretability. You can gain insights into the distinct patterns within numerical and binary spaces, potentially leading to a better understanding of the overall dataset structure.

6. **Experimentation:**
   - As with any data analysis approach, it's crucial to experiment and evaluate the impact of these choices on the clustering results. Considerations such as the number of clusters, normalization methods, and distance metrics should be tailored to the specific characteristics of your dataset.

In summary, the idea is to recognize and leverage the unique characteristics of numerical and binary features by applying clustering separately to each type. This approach can lead to more meaningful insights and a better understanding of the underlying structures in your data.

 


# Pre-processing
From sklearn doc
- [6.3. Preprocessing data](https://scikit-learn.org/stable/modules/preprocessing.html#)
    - [6.3.1. Standardization, or mean removal and variance scaling](https://scikit-learn.org/stable/modules/preprocessing.html#standardization-or-mean-removal-and-variance-scaling)
    - [6.3.2. Non-linear transformation](https://scikit-learn.org/stable/modules/preprocessing.html#non-linear-transformation)
    - [6.3.3. Normalization](https://scikit-learn.org/stable/modules/preprocessing.html#normalization)
    - [6.3.4. Encoding categorical features](https://scikit-learn.org/stable/modules/preprocessing.html#encoding-categorical-features)
    - [6.3.5. Discretization](https://scikit-learn.org/stable/modules/preprocessing.html#discretization)
    - [6.3.6. Imputation of missing values](https://scikit-learn.org/stable/modules/preprocessing.html#imputation-of-missing-values)
    - [6.3.7. Generating polynomial features](https://scikit-learn.org/stable/modules/preprocessing.html#generating-polynomial-features)
    - [6.3.8. Custom transformers](https://scikit-learn.org/stable/modules/preprocessing.html#custom-transformers)

Basics steps
1. explore (EDA)
	1. head(),info(), describe()
2. partitioning
	1. train_test_split
3. encoding
	1. OneHotEncoding
4. normalization
	1. MinMax
5. standardization
	1. StandardScaler

Carefully distinguish
1. numerical features
2. categorical features
3. binary features

## Normalization 
(also called, **Min-Max normalization**) is a scaling technique such that when it is applied the features will be rescaled so that the data will fall in the _range of [0,1]_
![[Pasted image 20231222171925.png]]
## Standardization
(also called, **Z-score normalization**) is a scaling technique such that when it is applied the features will be rescaled so that they’ll have the properties of a standard normal distribution with **mean,_μ=0_ and standard deviation, _σ=1_**. This scales the features in a way that they _range between [-1,1]_
![[Pasted image 20231222171959.png]]

## Encoding Categorical Features
OrdinalEncoder and OneHotEncoder


## Discretization
(otherwise known as quantization or binning) provides a way to partition continuous features into discrete values.



**Converting Dataframe to NumPy Array**: `X = df.values` converts the features DataFrame into a NumPy array. This is a common practice because scikit-learn's models generally work with NumPy arrays, although they also accept DataFrames.
Preparing Target Variable: `y = np.array(frame['target'])` takes the target variable ('target' column) and converts it into a NumPy array.
# KNN

## Model fit
```
clf = KNeighborsClassifier(n_neighbors=5, metric="euclidean", weights="uniform")
clf.fit(X_train_norm, y_train)
y_test_pred = clf.predict(X_test_norm)
```

## Performance Evaluation
Evaluate
1. accuracy
2. score
3. classification report
	1. precision, recall, f1-score
4. confusion matrix
5. roc curve
6. precision recall curve

```
print("Accuracy:", accuracy_score(y_test, y_test_pred))

# score: Return the mean accuracy on the given test data and labels.
# KNeighborsClassifier.score is doing (y_test_pred == y_test).sum() / len(y_test)
clf.score(X_test_norm, y_test)

```

```
print(classification_report(y_test, y_test_pred))
```

## Advanced Performance Evaluation
These methods provide an estimate of the model's performance metrics (like accuracy, precision, recall) based on multiple rounds of training and validation.
For example
1. Repeated Holdout
2. Cross-Validation
## Hyperparameters tuning
1. Grid search.
Systematically build and evaluate a model for each combination of algorithm parameters specified in a grid. Provides the best set of hyperparameters for a model.