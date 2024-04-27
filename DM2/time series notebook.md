## Libraries
[tslearn](https://tslearn.readthedocs.io/en/stable/index.html) is a Python package that provides machine learning tools for the analysis of time series. This package builds on (and hence depends on) `scikit-learn`, `numpy` and `scipy` libraries.

[tsfresh](https://tsfresh.readthedocs.io/en/latest/) is a python package. It automatically calculates a large number of time series characteristics, the so called features. Further the package contains methods to evaluate the explaining power and importance of such characteristics for regression or classification tasks.

[sklearn](https://scikit-learn.org/stable/index.html)

[matrixprofile-ts](https://github.com/target/matrixprofile-ts/) is a Python 2 and 3 library for evaluating time series data using the Matrix Profile algorithms developed by the [Keogh](https://www.cs.ucr.edu/~eamonn/MatrixProfile.html) and [Mueen](https://www.cs.unm.edu/~mueen/) research groups at UC-Riverside and the University of New Mexico.



## Clustering

1. k-means
You could try K-Means based on _**Dynamic Time Warping**_ metric which is much more relevant for time series (see [`tslearn` tuto](https://tslearn.readthedocs.io/en/stable/user_guide/clustering.html)). Saying that, there is an interesting discussion about [Dynamic Time Warping Clustering](https://stats.stackexchange.com/questions/131281/dynamic-time-warping-clustering) that you could read with a [lot of references](https://stats.stackexchange.com/a/131284/242848) that give time series clustering code examples.
Another common approach would be to extract relevant features from your time series and apply clustering techniques to them (see [`sklearn` clustering page](https://scikit-learn.org/stable/modules/clustering.html)). You could extract a lot of [common features for time series](https://tsfresh.readthedocs.io/en/latest/text/list_of_features.html) using [`tsfresh`](https://tsfresh.readthedocs.io/en/latest/index.html) python package.



How to judge clusters? use silhouette, but also centroids and other features (included genre) and motifs. Also matrix profile and ...

Or try a different method based on motifs.
For example, extract top-3 motifs. And use them for clustering.
It is not needed the dtw, since they are very small (use ed).
Use k-means with elbow and evaluate.
You can also extract the centroids.
And check what's in the cluster using external variables coming from the ts from which the motif was extracted.
And then say something like "this motif shape is typical of rock songs".
You will not get pure clusters, but still the percentages are a result.
For example, "this shape is common to all genres".
If it is highly representative, the motif can be used as a shapelet in classification.

use https://dtaidistance.readthedocs.io/en/latest/usage/dtw.html

also useful?
```python
# KMeans distance params 
# https://www.sktime.net/en/stable/api_reference/auto_generated/sktime.dists_kernels.dtw.DtwDist.html
distance_params = {'itakura_max_slope': 0.5, 'window': 3, 'weighted': True}
clusterer = TimeSeriesKMeans(n_clusters=2, metric="dtw", distance_params=distance_params)
```
