Study the book! Available online.
Experiment with dataset online, trying to reproduce the output of notebooks.

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

# K-means
The idea is to divide the dataset in clusters so that the mean of each cluster has a meaning, represent something.
We're studying convex shapes, since with concavities we get weird results, since the mean would be in the hole. But we could also increase the number of clusters to obtain smaller convex shapes.
What is the best k? It is a post-processing choice, because you need to see the difference between the different results.

# Bisecting K-means
From a recursive algo to smaller sets. Starting from a unique cluster, split into 2.

# X-means
New idea for splitting. 
The SSE is always meaningful, it will always be meaningful to split. While with the BIC we can decide how many split at each iteration.
They're greedy algo, simply optimising the next move.

# Hierarchical Clustering
Nested clusters organised as a hierarchical tree.
It is alway a bidimensional tree.
Limited scalability of the problem. So it is used in combination with other methods like k-means (with a large k).
Bottom-up costruction, merging cluster, is the most efficient way.

# Density-based clustering
DBSCAN algorithm.
Based on the notion of density.
We should define the radius around a point. Then we can count the points.

# Cluster validation
How do we find good correlation? Use the law of large numbers, drawing the gaussian for random points and look for correlations far from the mean.

---

# Clustering lab
It is mandatory to normalize data for clustering, since it is based on distances. It might be numbers expressed in different scales, and then the computation of the distance would be biased.
Normalise all the columns in the same way.
Use MINMAX Normalisation for clustering.

Add random_state parameter in KMeans to confront the results in a group, otherwise we get different results.

Silhoutte. (slide) 
A is average distance between points in the same class.
B is minimum average distance ...
It becomes negative if there's something wrong (->-1).
Repeat the computation for all the points.
We're looking for the 'knee'.

How to calculate the centroids?
With df.groupby.mean

If you wnat to use categorical attributes for clustering you need to define a different distance (not euclidean).
If you mix categorical and continuous attributes using euclidean distance is a mistake.
You can use categorical attributes to explore.











