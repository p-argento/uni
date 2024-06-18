This is about Exploratory Data Analysis and data Pre-Processing.

# From guidotti

This page contains some of the basics steps for data understanding extracted from the analysis of the Titanic dataset made by Guidotti.

Checklist for Data Understanding
• Determine the quality of the data. (e.g. syntactic accuracy)
• Find outliers. (e.g. using visualization techniques) 
• Detect and examine missing values. Possible hidden by default values. 
• Discover new or confirm expected dependencies or correlations between attributes. 
• Check specific application dependent assumptions (e.g. the attribute follows a normal distribution) 
• Compare statistics with the expected behaviour.

Useful tips from guidelines of dm2 project.
1. Explore and prepare the tabular dataset
	1. Pre-process the dataset and create new variables, if you consider it interesting. You are allowed to take inspiration from existing notebooks and figure out your personal research perspective (e.g., choosing a subset of variables for the class to predict).
2. Explore and prepare the time-series dataset
	1. Pre-process the dataset to be able to run time series clustering; motif/anomaly discovery and classification. If the dataset is too big for these tasks, you can use approximations (e.g. SAX, PAA etc)

```python
import numpy as np
import pandas as pd
from matplotlib import pyplot as plt

df = pd.read_csv('tabular/tracks.csv')
df.head(10)
df.tail(5)
df.dtypes
df.info()
df.describe(include="all")

df.isnull().sum()

df.corr() #method : {‘pearson’, ‘kendall’, ‘spearman’}
# df['var1'].corr(df['var2']) 


```







# from sklearn
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




# from chatgpt
(using full spotify dataset as input)
Preprocessing your dataset for machine learning (ML) algorithms involves several steps to ensure the data is clean, consistent, and ready for modeling. Here is a step-by-step guide to help you through the process:

### 1. load the data
```python
import pandas as pd
df = pd.read_csv('your_dataset.csv') 
```

### 2. inspect the data
```python
print(df.info())
print(df.describe())
print(df.head())
```

### 3. handle missing values
```python
df.isnull().sum()
# Drop rows with missing values
df = df.dropna()
# Or, fill missing values with a specific value or strategy
# df = df.fillna(0)  # Example: filling with 0
```

### 4. remove unnecessary columns
First, understand correlations and dependencies.
Identify and drop columns that are not useful for your ML models.
```python
columns_to_drop = ['id', 'name', 'artists', 'album_name', 'album_release_date', 'album_release_date_precision']
df = df.drop(columns=columns_to_drop)
```

### 5. convert categorical data to numeric
Convert categorical variables to numeric using techniques like one-hot encoding.
```python
df = pd.get_dummies(df, columns=['album_type', 'genre'])
```

### 6. normalize numerical features
```python
from sklearn.preprocessing import StandardScaler

numeric_columns = df.select_dtypes(include=['float64', 'int64']).columns
scaler = StandardScaler()
df[numeric_columns] = scaler.fit_transform(df[numeric_columns])
```

### 7. handle boolean values
```python
df['explicit'] = df['explicit'].astype(int)
```

### 8. remove duplicate rows
```python
df = df.drop_duplicates()
```

### remove
### 9. feature engineering
```python
# Example: create a new feature 'track_duration_min'
df['track_duration_min'] = df['duration_ms'] / 60000
df = df.drop(columns=['duration_ms'])
```

### 10. split features X and target y
```python
X = df.drop(columns=['popularity'])  # Assuming 'popularity' is the target variable
y = df['popularity']
```

### 11. split training and test sets
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

```







