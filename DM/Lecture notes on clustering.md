



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


---

# Clustering Exercises


*Didactic data mining on didawiki*

*dbscan*
Typically the default value od minPoints = 4, but we use 3.
Place the yellow point into a dot.
1. divide core point, border point and noise point.
2. core point. in the eps distance there are minPoints (included the point) -> the area is dense enough
3. border points are in the neighbourhood of a core point (but are not core points)
4. noise, everything else.

Labeling procedure.
1. start from one core point and colour within the eps
2. go further to find another core point (skip border points)

*hierarchical clustering*
They provide the proximity matrix (pairwise).
> If it's a distance matrix, you look for the MIN distance.
> If it's a similarity matrix, you look for the MAX value.

1. if the distance merge is all the same (starting from the min), merge the points.
2. recalculate the distance matrix but using new clusters as columns
	1. in case of single-linkage, take the MIN distance between clusters
	2. in case of complete-linkage, take the MAX distance between clusters

> *DO THE EXS and test using didactic website*