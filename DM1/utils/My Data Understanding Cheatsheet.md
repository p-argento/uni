This page contains some of the basics steps for data understanding extracted from the analysis of the Titanic dataset made by Guidotti.

## From theory
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

## Coding

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