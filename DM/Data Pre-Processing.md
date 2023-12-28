[[DM Project]]
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

Explore (EDA)
1. head(),info(), describe()

Carefully distinguish
1. numerical features
2. categorical features
3. binary features

Basics steps
1. partitioning
	1. train_test_split
2. encoding categorical features
	1. OneHotEncoding
3. normalization
	1. MinMax
4. standardization
	1. StandardScaler



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