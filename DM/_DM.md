
[[DM Project]]
[[DM Clustering]]
[[DM Formulas]]


**Professor's Advice**
Study the book! Available online.
Experiment with dataset online, trying to reproduce the output of notebooks.

# Slides
---
0. Introduction
Exploratory Data Analysis
[[1. Data Understanding]]
[[2. Data Preparation]]
[[3. Data Similarity]]
Clustering
[[4. Clustering Introduction]]
[[5. K-Means Clustering]]
[[6. Hierarchical Clustering]]
[[7. Density-Based Clustering]]
Classification
[[8. Classification Introduction]]
[[9. Instance-based classifiers]]
[[10. Naïve Bayes Classifier]]
[[11.  Classification Model Evaluation]]
[[12. Decision Trees]]
Regression and Pattern Mining
[[13. Pattern Mining]]
[[14. Linear Regression]]


# Outline
---
Module 1: Data Understanding 
• KDD & CRISP 
• Data Understanding 
• Data Preparation 
• Data Similarity 
• Basic Statistics

Module 2: Clustering 
• Taxonomy & Problem Setting 
• Centroid-based Clustering 
• Hierarachical Clustering 
• Density-based Clustering 
• Advanced Approaches • 

Module 3: Pattern Mining 
• Frequent Pattern Mining 
• Association Rules 
• Sequential Pattern Mining 
• Generalized Sequential Pattern 
• Advanced Approaches • 

Module 4: Classification & Regression 
• Problem Setting 
• K Nearest Neighbor 
• Naive Bayes Classifier 
• Decision Tree Classifier 
• Linear Regression


# Project
---
Github repo and Overleaf shared project.
Justify the choices.
Comment the figures.
Use the training file. For classification you can use also the other one.
Use a notebook on Jupyter for each phase of the KDD Process.
There's a notebook with all the details.

**project faq**

Remove outliers and draw the plot again. check the difference. Do it differently for each attribute. Work independently from feature to feature.
K-means is very sensitive to outliers.
Typically consider the IQR (Inter Quartile Range), between 25th and 75th percentile.

Focus on the features more interesting to detect outliers.
USE ALL THE FEATURES for clustering. This is the beauty of kdd algorithms.

Do a PCA, for dimensionality reduction.
If k=2, you can visualise in a scatterplot, loosing however information.
But clustering comes before pca.

# Python
---
3 basic types: int, float, str.
// is the division by integer part.
4 data structures: `list[,], set{,}, tuple(,)`
Difference between list and set? In a set there are no duplicates. And both of them can be composed by mixed data types.

Dictionaries `{'str':int}` or viceversa.
dict.keys and dict-values.

The data frame is the box excluding indexes (can be only one column).
A single column is a series. (try the type() method).
Be aware of the different between data frame and series. 
Each one of them provides different functionalities.


# Appo
---





