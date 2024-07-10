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

also inspired by [this mooc](https://inria.github.io/scikit-learn-mooc/)

Preprocessing your dataset for machine learning (ML) algorithms involves several steps to ensure the data is clean, consistent, and ready for modeling. Here is a step-by-step guide to help you through the process:

### 1. load the data
```python
import os
os.chdir('/Users/pietro/_DS/DM2')
os.getcwd()

import pandas as pd
df = pd.read_csv('your_dataset.csv') 
```

### 2. inspect the data
```python
print(df.info())
print(df.describe())
print(df.head())

print(df.shape)
print(df['name'].unique())
print(df['genre'].unique().shape)
print(df['genre'].unique())
print(df['genre'].unique().shape)
```
maybe also visualizations like scatterplots
```python
pd.options.display.max_columns = 100
pd.options.display.max_rows = 100
```


I created this useful script to better understand features.
```python
eda = pd.DataFrame(index=df.columns, columns=['nunique', 'unique'])

for column in df.columns:
    # Calculate the number of unique values
    unique_count = df[column].nunique()
    eda.at[column, 'nunique'] = unique_count
    
    # If the number of unique values is less than 20, store the unique values
    if unique_count < 20:
        eda.at[column, 'unique'] = df[column].unique()
    else:
        eda.at[column, 'unique'] = df[column].head(10)

	# check data type
	eda.at[column, 'dtype'] = df[column].dtype

print(eda)
```

and classify each feature if it is
1. numerical (int or float)
2. categorical 
3. bool

```python
print(df['time_signature'].dtype())
df['time_signature'] = df['time_signature'].astype('category')

```

or you can just use an automated EDA like [ydata-profiling](https://github.com/ydataai/ydata-profiling).


### 3. handle missing values (or inf)
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
columns_to_drop = ['id', 'name', 'artists', 'album_name', 'album_release_date_precision']
df = df.drop(columns=columns_to_drop)
```

how to deal with dates?



```python
df['time_signature'] = df['time_signature'].astype('category')

```

### 5. convert categorical data to numeric
Convert categorical variables to numeric using techniques like one-hot encoding.

Isnt' it better to use OneHotEncoding from sklearn.
In particular, it is better for ML tasks because it learn the encoding and then we can be sure it is replicated also in the test set.

```python
df = pd.get_dummies(df, columns=['album_type', 'genre'])
```

```python
from sklearn.preprocessing import OneHotEncoder

X = [['male', 'from US', 'uses Safari'], ['female', 'from Europe', 'uses Firefox']]
enc = preprocessing.OneHotEncoder()
enc.fit(X)
enc.transform([['female', 'from US', 'uses Safari'],
               ['male', 'from Europe', 'uses Safari']]).toarray()
```


How to deal with dates?
you can extract various useful components from this date and include them as features in your analysis.
```python
df['album_release_date'] = pd.to_datetime(df['album_release_date'], errors='coerce')
df['release_year'] = df['album_release_date'].dt.year
df['release_month'] = df['album_release_date'].dt.month
df['release_day'] = df['album_release_date'].dt.day
df['release_day_of_week'] = df['album_release_date'].dt.dayofweek  # Monday=0, Sunday=6
df['release_is_weekend'] = df['release_day_of_week'].apply(lambda x: 1 if x >= 5 else 0)

```

Also target encoding can be used. [See this article](https://towardsdatascience.com/encoding-categorical-variables-a-deep-dive-into-target-encoding-2862217c2753).
Target encoding works by converting each category of a categorical feature into its corresponding expected value. The approach to calculating the expected value will depend on the value you are trying to predict.
For Regression problems, the expected value is simply the average value for that category.
For Classification problems, the expected value is the conditional probability given that category.

*from kaggle*
For large datasets with many rows, one-hot encoding can greatly expand the size of the dataset. For this reason, we typically will only one-hot encode columns with relatively low cardinality. Then, high cardinality columns can either be dropped from the dataset, or we can use label encoding.
As an example, consider a dataset with 10,000 rows, and containing one categorical column with 100 unique entries.
```python
# Columns that will be one-hot encoded
low_cardinality_cols = [col for col in object_cols if X_train[col].nunique() < 10]

# Columns that will be dropped from the dataset
high_cardinality_cols = list(set(object_cols)-set(low_cardinality_cols))

print('Categorical columns that will be one-hot encoded:', low_cardinality_cols)
print('\nCategorical columns that will be dropped from the dataset:', high_cardinality_cols)
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


### 9. remove outliers
Should I repeat normalization?


### 10. feature engineering
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






