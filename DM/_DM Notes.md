

[[DM Project Notes]]
[[DM Clustering]]
[[DM Classification]]

# TO-DO
---
- [ ] Vedi appunti su slide dell'anno scorso per le prime lezioni


**Professor's Advice**
Study the book! Available online.
Experiment with dataset online, trying to reproduce the output of notebooks.

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



# Decision Tree Classifiers
---
Split until the splitting attributes directly leads to a specific class, in a sense that it does not need to be split again to find a specific class.
For example, if 'home owner=yes' then the class is for sure 'no'.

![[Pasted image 20231122113533.png|400]]

When the slip is not binary, who tells me what is the right split?
There could be more than one tree that fits the same data.

**Comments**
Applied typically for tabular data.
Use greedy algorithm, but it is not possible to grasp the real optimum.

**Hunt's Algorithm**



---





