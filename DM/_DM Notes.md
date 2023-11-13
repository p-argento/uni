

[[DM Project Notes]]

[[DM Clustering]]

---

Study the book! Available online.
Experiment with dataset online, trying to reproduce the output of notebooks.

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



---

*project*
Github repo and Overleaf shared project.
Justify the choices.
Comment the figures.
Use the training file. For classification you can use also the other one.
Use a notebook on Jupyter for each phase of the KDD Process.
There's a notebook with all the details.

*Python*
3 basic types: int, float, str.
// is the division by integer part.
4 data structures: list[,], set{,}, tuple(,).
Difference between list and set? In a set there are no duplicates. And both of them can be composed by mixed data types.

Dictionaries{'str':int} or viceversa.
dict.keys and dict-values.


The data frame is the box excluding indexes (can be only one column).
A single column is a series. (try the type() method).
Be aware of the different between data frame and series. 
Each one of them provides different functionalities.

---

 PCA - sostituisci slide DM con quelle nuove e sistema la parte precedente. In arancio i titoli.

$$log_{10}(n)$$ means transforming the number n in his order of magnitude.

---



---

# project faq

Remove outliers and draw the plot again. check the difference. Do it differently for each attribute. Work independently from feature to feature.
K-means is very sensitive to outliers.
Typically consider the IQR (Inter Quartile Range), between 25th and 75th percentile.

Focus on the features more interesting to detect outliers.
USE ALL THE FEATURES for clustering. This is the beauty of kdd algorithms.

Do a PCA, for dimensionality reduction.
If k=2, you can visualise in a scatterplot, loosing however information.
But clustering comes before pca.

---

# KNN
It is the Nearest Neighbour Classification.
It is a instance-based classifier.
You compare the target value with the set of ducks which is nearest. This set is what defines the attributes of "a duck".
> If it walks like a duck, quacks like a duck, then it's probably a duck.

How to choose k?
If K is too small, it leads to overfitting (relying too much of a singular value).
If K is too large, the neighbourhood might include points from other classes.
Set $K=sqrt(N)$, as a general rule of thumb.

How does the voting work?
Weight the vote according to the distance ($w = 1/(d^2)$)

Dimensionality and scaling issues.
Curse of dimensionality -> normalize the vector to unit length
..


Memory-based learning.
..

To find the parameter, divide the train set in train' and validation. Apply the algorithm to find the parameter validated through the validation set. Now use parameter on the whole original train set.

PEBLS.
It is categorical KNN.
Until now, since we rely on Euclidean distance, we can work onyl with continuous attributes.
It uses a distance calculated on the target value.

Lazy-learner means calculus made at prediction time.

For classification you use the mode (majority voting).
For regression you use the average of the set of ducks.

---

# Naive Bayes
> Why naive? Because it's assuming that the attributes are conditionally independent.

In reality, they're not independent.

---

# Classification Model Evaluation

  In the Iris dataset, you have 3 precision, one for each class.
  












