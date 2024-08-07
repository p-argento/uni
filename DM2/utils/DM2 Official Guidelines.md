## Outline
There are 4 Modules
- Module 1: Data Understanding & Preparation
	1. Data Understanding
	2. Data Preparation
- Module 2: Time Series Analysis
	1. Time Series Similarity, 
	2. Approximation, 
	3. Motif, 
	4. Shapelets, 
	5. Classification, 
	6. Clustering
- Module 3: Advanced Data-Preprocessing 
	1. Imbalanced Learning, 
	2. Dimensionality Reduction,
	3. Anomaly Detection
- Module 4: Advanced ML & XAI
	1. Logistic Regression,
	2. Support Vector Machines, 
	3. Neural Networks, 
	4. Ensamble Methods, 
	5. Gradient Boosting, 
	6. Rule-based Classifiers

![[Pasted image 20240317114356.png]]


## Dataset
There are 2 datasets for this project: 
1. A tabular dataset [module 1, 3, 4] 
	1. • Extended version of the DM1 dataset: ~100k records, 114 genre classes, additional info about artists (i.e., followers, popularity). 
2. A time series dataset [module 1, 2] 
	1. • Time-series representing the spectral centroids of the song mp3 audio files.
	2. • 10k time series (500 for each of the 20-genre considered) 
	3. • File naming: trackid_genre
## Module 1: Data Understanding and Preparation 
Guidelines
1. Explore and prepare the tabular dataset
	1. Pre-process the dataset and create new variables, if you consider it interesting.
	2. You are allowed to take inspiration from existing notebooks and figure out your personal research perspective (e.g., choosing a subset of variables for the class to predict).
2. Explore and prepare the time-series dataset
	1. Pre-process the dataset to be able to run time series clustering; motif/anomaly discovery and classification.
	2. If the dataset is too big for these tasks, you can use approximations (e.g. SAX, PAA etc)

My Notes
1. see [[My EDA Cheatsheet]]

## Module 2: Time Series Analysis 
### Motifs/Discords
1. Analyze the dataset for finding motifs and/or anomalies.
2. Visualize and discuss them and their relationship with shapelets. 

### Clustering
1. Use at least two clustering algorithm on time series using an appropriate distance. 
2. Analyze the clusters and highlight similarities and differences and visualize the clusters using at least 2 dimensionality reduction techniques.

### Classification 
Define one (or more) classification task and solve it using: 
• KNN with at least two distances 
• Euclidean/Manhattan 
• DTW 
• Shapelets: Analyze the shapelets retrieved 
• At least one other method (rocket, muse, cnn, rnn etc) 

### Sequential Pattern Mining (optional)
Discretize the time-series to run sequential pattern mining (e.g., identify frequent pattern or trends within the time series).

## Module 3: Advanced Data-Preprocessing  

### Outliers 
1. Identify the top 1% outliers: adopt at least three different methods from different families (i.e., density-based, angle-based…) and compare the results. 
2. Visualize the outliers in a 2 or 3d scatter plot using at least one dimensionality reduction technique. 
3. Deal with the outliers in a way you see fit, e.g. by removing them from the dataset or by treating the anomalous variables as missing values and employing replacement techniques. In this second case, you should check that the outliers are not outliers anymore. Justify your choices in every step.

### Imbalanced Learning
1. Define one simple unbalanced classification tasks and solve it with Decision Tree or KNN. 
2. If the dataset is already unbalanced leave it as it is, otherwise turns the dataset into an imbalanced version (e.g., 96% - 4%, for binary classification). 
3. Then solve the classification task using the Decision Tree or KNN by adopting at least 2 techniques of imbalanced learning (Undersampling, Oversampling).

## Module 4: Advanced ML & XAI

### Advanced Classification
1. Solve the classification task defined in Module 3 (or define new ones) with the other classification methods analyzed during the course:
	1. Logistic Regression, Support Vector Machines, Neural Networks, Ensemble Methods, Gradient Boosting Machines. 
2. Always perform hyper-parameter tuning phases and justify your choices (which are the best parameters? which parameters did you test and why?). 
3. Evaluate each classifier with the techniques presented in DM1: accuracy (or precision, recall, F1-score etc), ROC curve (or lift, precision-recall etc). 
4. Besides the numerical evaluation draw your conclusions about the various classifiers
	1. for Neural Networks: what are the parameter sets or the convergence criteria which avoid overfitting?
	2. for Ensemble classifiers how the number of base models impact the classification performance? What is revealing the feature importance of Random Forests?
	3. ...

### Advanced Regression
1. Define a multiple regression task, i.e., using more than one input feature, and solve it using 2 advanced regression approaches (not linear). 
2. Compare and evaluate the approaches using appropriate metrics. 

### Explainability
1. Try to use one or more explanation methods (e.g., TREPAN, LIME, LORE, SHAP, Counterfactual Explainers, etc.) to illustrate the reasons for the classification in one of the steps of the previous tasks.


