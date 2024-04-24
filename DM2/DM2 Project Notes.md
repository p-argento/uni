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

[[DM2 Description of Variables]]
## Module 1: Data Understanding and Preparation 
Guidelines
1. Explore and prepare the tabular dataset
	1. Pre-process the dataset and create new variables, if you consider it interesting. You are allowed to take inspiration from existing notebooks and figure out your personal research perspective (e.g., choosing a subset of variables for the class to predict).
2. Explore and prepare the time-series dataset
	1. Pre-process the dataset to be able to run time series clustering; motif/anomaly discovery and classification. If the dataset is too big for these tasks, you can use approximations (e.g. SAX, PAA etc)

My Notes
1. see [[My Data Understanding Cheatsheet]]

## Module 2: Time Series Analysis 
### Motifs/Discords
Analyze the dataset for finding motifs and/or anomalies.
Visualize and discuss them and their relationship with shapelets. 
### Clustering
• Use at least two clustering algorithm on time series using an appropriate distance. 
• Analyze the clusters and highlight similarities and differences and visualize the clusters using at least 2 dimensionality reduction techniques.
### Classification 
Define one (or more) classification task and solve it using: 
• KNN with at least two distances 
• Euclidean/Manhattan 
• DTW 
• Shapelets: Analyze the shapelets retrieved 
• At least one other method (rocket, muse, cnn, rnn etc) 
### Sequential Pattern Mining (optional)
Discretize the time-series to run sequential pattern mining (e.g., identify frequent pattern or trends within the time series).

---mynotes---
The time series are [Spectral Centroids](https://librosa.org/doc/main/generated/librosa.feature.spectral_centroid.html) and therefore it is impossible to get back the wav files.

Use numpy.save for saving matrices that took days to run like dtw.
And then reload using numpy.load
Do not recompute the distance if it was already computed once.



1. trasformations
	1. offset
	2. amplitude scaling
	3. linear trend
	4. noise
2. (distance measures between two ts)
	1. ed
	2. dtw
	3. dtw with constraints
3. approximation
	1. DFT with ed ???
	2. PAA
	3. SAX
4. clustering
	1. hierarchical 
	2. partitional
5. motif and discords
	1. motif discovery using MP
	2. anomaly detection
	3. top-k?
6. classification
	1. knn
	2. shapelet-based


In [[time series clustering]].



## Module 3: Advanced Data-Preprocessing  

### Outliers 
• Identify the top 1% outliers: adopt at least three different methods from different families (i.e., density-based, angle-based…) and compare the results. • Visualize the outliers in a 2 or 3d scatter plot using at least one dimensionality reduction technique. • Deal with the outliers in a way you see fit, e.g. by removing them from the dataset or by treating the anomalous variables as missing values and employing replacement techniques. In this second case, you should check that the outliers are not outliers anymore. Justify your choices in every step.

### Imbalanced Learning
• Define one simple unbalanced classification tasks and solve it with Decision Tree or KNN. • If the dataset is already unbalanced leave it as it is, otherwise turns the dataset into an imbalanced version (e.g., 96% - 4%, for binary classification). • Then solve the classification task using the Decision Tree or KNN by adopting at least 2 techniques of imbalanced learning (Undersampling, Oversampling).

## Module 4: Advanced ML & XAI

### Advanced Classification
• Solve the classification task defined in Module 3 (or define new ones) with the other classification methods analyzed during the course: Logistic Regression, Support Vector Machines, Neural Networks, Ensemble Methods, Gradient Boosting Machines. • Always perform hyper-parameter tuning phases and justify your choices (which are the best parameters? which parameters did you test and why?). • Evaluate each classifier with the techniques presented in DM1: accuracy (or precision, recall, F1-score etc), ROC curve (or lift, precision-recall etc). • Besides the numerical evaluation draw your conclusions about the various classifiers (e.g. for Neural Networks: what are the parameter sets or the convergence criteria which avoid overfitting? For Ensemble classifiers how the number of base models impact the classification performance? What is revealing the feature importance of Random Forests?)

### Advanced Regression
• Define a multiple regression task, i.e., using more than one input feature, and solve it using 2 advanced regression approaches (not linear). • Compare and evaluate the approaches using appropriate metrics. 

### Explainability
Try to use one or more explanation methods (e.g., TREPAN, LIME, LORE, SHAP, Counterfactual Explainers, etc.) to illustrate the reasons for the classification in one of the steps of the previous tasks.


# Our Plan

## Time Series

DM2 project ideas

TS subset per genre (vedi split nome file) -> 20 subset (20 genres)

selezioniamo tracks di generi simili -> similarità fra i due generi -> shape interessanti fra generi (tipo classic che ha stessa struttura di generi moderni)

scegli generi su cui fare il confronto  
1st step: approximation -> SAX or PAA? Or DFT without time? -> se vogliamo mantenere la forma per studio sopra meglio DFT.

se consideriamo shapes -> trasformazioni per preservare shape (offset, amplitude scaling)

Trasformazioni da applicare:

noise smoothing -> ci permette di avere shape smooth da confrontare

data values nel grafico (asse y) come vengono calcolati?
