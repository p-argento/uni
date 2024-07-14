https://www.gov.uk/government/collections/household-electricity-survey

[[DM2 Project Notes]]

```
** Background **
These problems were taken from data recorded as part of government sponsored study called Powering the Nation. The intention was to collect behavioural data about how consumers use electricity within the home to help reduce the UK's carbon footprint. The data contains readings from 251 households, sampled in two-minute intervals over a month.

** Problems **
ElectricDevices LargeKitchenAppliances RefrigerationDevices
ScreenType SmallKitchenAppliances

We create two distinct types of problem: problems with similar usage patterns
(Refrigeration, Computers, Screen) and problems with dissimilar
usage patterns (Small Kitchen and Large Kitchen). The aim is that
problems with dissimilar usage patterns should be well suited to
time-domain classification, whilst those with similar consumption
patterns should be much harder.

The five problems we form are summarised in the following table.

||	PROBLEM 	|| 	CLASS LABELS 					||
|| Small kitchen 	|| Kettle, Microwave, Toaster 				||
|| Large Kitchen 	|| Dishwasher, Tumble Dryer, Washing Machine 		||
|| Refrigeration 	|| Fridge/Freezer, Refrigerator, Upright Freezer 	||
|| Computers 		|| Desktop, Laptop 					||
|| Screen 		|| CRT TV, LCD TV, Computer Monitor 			||
```


## Ideas

1. after the best classification possible, I could try motifs and discords again
2. many types of problems to be solved
	1. 2 types of usage: similar (non-kitchen) vs dissimilar (kitchen) usage patterns
	2. 5 problems
	3. 14 class labels
	4. 7 class numbers



## To do

today
1. ts notebook
	1. motif/anomalies
	2. clustering
	3. classification
2. better EDA for ts
3. better EDA for tabular data
4. write draft report for the first half

friday
1. feature selection (RFE)
2. try advanced classifiers with default parameters

saturday
2. try task 3 on tabular dataset
	1. anomaly detection
	2. imblearn
3. finish draft report first half

sunday
1. first half of report in latex must be finished
2. must be finished all the raw experiments, included task 4

monday
1. 


## Diario

Start with ts eda.
Try approximations PAA and SAX.

*ts*
- `"pd-multiindex"` - a `pandas.DataFrame`, with row multi-index (instances, time), cols = variables
- `"numpy3D"` - a 3D `np.ndarray`, with axis 0 = instances, axis 1 = variables, axis 2 = time points
Decide to use numpy3d, I face less problems.

I still need to handle.
1. missing values (looks like there are none)
2. duplicates (a lot)
3. flat ts (maybe there are none)

For 


*tabular*
(old)
I created a tabular version of the time series using TSFreshFeatureExtractor.
I got 777 variables. I need to better understand what they are and decide if it is worth to keep them all. Is 'efficient' the correct value for the parameter?
Maybe with tree-based classifiers it is fine to keep them all, while with other distance-based I need to use dimensionality reduction techniques.

(new)
I created two tabular dataset, both starting from X_long
1. using feature_extractor, then manually cleaning
	1. removing rows with +inf, -inf, nan values
	2. removing duplicates
	3. the result is df_cleaned of shape (8841, 562)
3. using extract_relevant_features
	1. it already includes the target variable
	2. the result is df_filtered of shape (8799, 477)

For now, I am using the df_filtered, since the target variable is only the class y.
I tried
1. DecisionTreeClassifier, the accuracy is 0.85
2. RandomForestClassifiers(n=100), the accuracy is 0.91
However, keep in mind that the classes are imbalanced.

*7/7*
I should create another dataset with less and more interpretable features.
Say max 20.
Dataset ideas
1. df_cleaned
2. df_filtered
3. df_interpretable

In addition, I should define more problems to be solved.
In particular a regression task.
1. class (already there)
2. the result of the best clustering algorithm?
	1. this label can be obtained only from unsupervised learning
	2. could represent the 5 problems
3. 

Now, let's try logistic regression and then all the ensembles.
The target is still the 'class' variable.
Steps
1. create balanced datasets
	1. with undersampling -> df_undersampling
	2. with oversampling -> df_oversampling
2. try logistic regression
	1. 
	2. evaluate
4. try

I lost a lot of time trying to balance the dataset with SMOTE to use logistic regression and evaluate it using a multiclass ROC ([not in sklearn](https://scikit-learn.org/stable/auto_examples/model_selection/plot_roc.html#roc-curve-using-micro-averaged-ovr))

It is of crucial importance to better understand how to deal with features and outliers. I discovered using PCA and KMeans that there is something wrong, maybe 4 points (or more) are distorting everything.
I am trying to improve the dataset using the task3 algorithms of advanced preprocessing
1. visualizing features
2. outlier detection
3. imbalance learning
In particular, I need to understand how to
1. visualize
2. remove useless (collinearity) features with RFE and more
3. remove outliers

Found that the 3 crucial outliers clearly visible from PCA and t-SNE are the same. They are {5965, 5789, 6367}.
Now, I will try to understand why using the Isolation Forest.


*8/7*
Too many problems with sktime.
Switching to tslearn for ml tasks.

I created a function to visualize centroid clusters on top of samples of ts.
The DTW Kmeans with K=5 is just great.
Next step is to compare it with class labels.

Oh and evaluate with silhouette ofc.


*10/7*
Still triggered by the dataset.
Pre-processing once and for all.
Time series dataset.
1. Handling rows
	1. handle missing (or inf) values
	2. handle duplicates

*11/7*
[[Consumption Patterns]]

*12/7*
[[Interesting comment about Normalization of Time Series]]

*13/7*
ADVANCED PRE-PROCESSING for df_refined

Anomaly detection
1. ABOD, because the dataset is high dimensional
2. LODA, as an ensemble of HBOS
3. ISOLATION FOREST, because it is the sota
(how to select the 1%?, how to choose method? merge them?)

Feature Selection (not in the guidelines)
1. just use selectFromModel for df_refined
2. what about df_simpler

Imbalance Learning
1. try dt on df_cleaned
2. use dt on df_imbalanced (one class vs the others?)
3. sota for undersampling and try again
4. SMOTE (or ADASYN) for oversampling and try again
5. best oversampling for df_refined

I need a page to store all the results.

*14/7*
I decided to present the results of test.csv only.

An idea to detect the difference between similar and dissimilar pattern could be anomaly detection (isolation forest).


Before testing TS, proper SCALING.
Then, the experiments are
1. motifs
2. clustering
3. classification

Let's list all the things to do before testing TABULAR.
1. NO data cleaning
	1. consider this real-world scenario, no luxury of data cleaning
2. manual feature selection
3. IF DONE, proper scaling

Advanced Pre-Processing
1. 






## 1. EDA

![[DM2 Official Guidelines#Module 1 Data Understanding and Preparation]]


## 2. Time Series Analysis
Steps
1. motifs/discords
2. clustering
3. classification

![[DM2 Official Guidelines#Module 2 Time Series Analysis]]


## 3.  Advanced Data Pre-Processing
![[DM2 Official Guidelines#Module 3 Advanced Data-Preprocessing]]

the notebooks are
1. dimensionality reduction
2. outlier detection
3. imbalanced learning




## 4. Advanced ML
![[DM2 Official Guidelines#Module 4 Advanced ML & XAI]]


