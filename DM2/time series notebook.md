# Tasks
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

# Additional Notes
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


# Libraries
[tslearn](https://tslearn.readthedocs.io/en/stable/index.html) is a Python package that provides machine learning tools for the analysis of time series. This package builds on (and hence depends on) `scikit-learn`, `numpy` and `scipy` libraries.

[tsfresh](https://tsfresh.readthedocs.io/en/latest/) is a python package. It automatically calculates a large number of time series characteristics, the so called features. Further the package contains methods to evaluate the explaining power and importance of such characteristics for regression or classification tasks.

[sktime](https://www.sktime.net/en/stable/) is a unified framework for machine learning with time series.

[sklearn](https://scikit-learn.org/stable/index.html) 

[matrixprofile-ts](https://github.com/target/matrixprofile-ts/) is a Python 2 and 3 library for evaluating time series data using the Matrix Profile algorithms developed by the [Keogh](https://www.cs.ucr.edu/~eamonn/MatrixProfile.html) and [Mueen](https://www.cs.unm.edu/~mueen/) research groups at UC-Riverside and the University of New Mexico.



# Clustering

### K-Means (using sktime)
from sktime docs
```python
from sklearn.model_selection import train_test_split
from sktime.clustering.k_means import TimeSeriesKMeans
from sktime.clustering.utils.plotting._plot_partitions import plot_cluster_algorithm
from sktime.datasets import load_arrow_head

X, y = load_arrow_head()
X_train, X_test, y_train, y_test = train_test_split(X, y)

k_means = TimeSeriesKMeans(n_clusters=5, init_algorithm="forgy", metric="dtw")
k_means.fit(X_train)
plot_cluster_algorithm(k_means, X_test, k_means.n_clusters)
```

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

### K-Means (using tslearn)
but guidotti used sktime
```python
from tslearn.clustering import TimeSeriesKMeans

model = TimeSeriesKMeans(n_clusters=3, metric="dtw",
                         max_iter=10, random_state=seed)
model.fit(X_train)
```


## Feature-based Clustering (using tsfresh)
```python
from sktime.transformations.panel.tsfresh import TSFreshFeatureExtractor

ts_eff = TSFreshFeatureExtractor(default_fc_parameters="comprehensive", show_warnings=False, disable_progressbar=True) 

X_transform1 = ts_eff.fit_transform(X_train)

```

After the trasformation, on the new array we can apply whatever we want, like DBSCAN.

## Additional experiments using motifs


# Motifs 

## Motif extraction (using Matrixprofile)
```python
from matrixprofile import *

mo, mod  = motifs.motifs(ts.values, (mp, mpi), max_motifs=5)


```


# Classification

## Pre-processing (using sktime)
```python
from sktime.transformations.compose import FitInTransform
from sktime.transformations.series.adapt import TabularToSeriesAdaptor
from sklearn.preprocessing import StandardScaler, MinMaxScaler
from sktime.transformations.panel.compose import ColumnTransformer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
```


## KNN (using sktime)
```python
from sklearn.metrics import classification_report
from sktime.classification.distance_based import KNeighborsTimeSeriesClassifier
```

## Shapelet-based (using sktime)
```python
from sktime.classification.shapelet_based import ShapeletTransformClassifier
```


### Shapelet-based SINGLE STEPS 

We can run the single steps of the `ShapeletTransformClassifier`.
 1) Shapelet Finder 
 2) Shapelet Transformer 
 3) Shapelet Dataset 
 4) ML Model

```python
from sklearn.tree import DecisionTreeClassifier
from sktime.transformations.panel.shapelet_transform import RandomShapeletTransform

rst = RandomShapeletTransform(n_shapelet_samples=10000, max_shapelets=None, min_shapelet_length=3, max_shapelet_length=None, n_jobs=-1) #n_jobs -1 uses all processors

%%time
rst.fit(X_train_scaled, y_train)

%%time
shapelets_distances_train = rst.transform(X_train_scaled)
shapelets_distances_test = rst.transform(X_test_scaled)

clf = DecisionTreeClassifier()
clf = clf.fit(shapelets_distances_train, y_train)
y_pred = clf.predict(shapelets_distances_test)
print(classification_report(y_test, y_pred))

# Each item in the list is a tuple containing the following 7 items:
# (shapelet information gain, shapelet length, start position the shapelet was extracted from,
# shapelet dimension, index of the instance the shapelet was extracted from in fit,
# class value of the shapelet, The z-normalised shapelet array)
shapelets = rst.shapelets
shapelets[0]

# plotting the z-normalized shapelet arrays
for i in range(10):
  plt.plot(shapelets[i][6])
  plt.show()

sh_id = 416
start_position = shapelets[sh_id][2]
instance_index = shapelets[sh_id][4]
z_norm_shapelet = shapelets[sh_id][6]
end_position = start_position + len(z_norm_shapelet)

plt.plot(X_train_scaled[instance_index].ravel(), label='time-series')
plt.plot(np.arange(start_position, end_position), X_train_scaled[instance_index].ravel()[start_position:end_position], linewidth=2, label='shapelet')
plt.plot(np.arange(start_position, end_position), z_norm_shapelet, linewidth=2, label='z-norm shapelet')
plt.axvline(start_position, color='k', linestyle='--', alpha=0.25)
plt.title("The aligned extracted shapelet")
plt.legend()
plt.show()
```


```python
# # brute-force approach (works exactly as the RandomShapletTransform - parameters are different)
# from sktime.transformations.panel.shapelet_transform import ShapeletTransform
# st = ShapeletTransform(min_shapelet_length=3, max_shapelet_length=6, max_shapelets_to_store_per_class=5)
```


## shapelet-based (using tslearn)

[ts learn shapelets](https://tslearn.readthedocs.io/en/stable/auto_examples/classification/plot_shapelet_locations.html#sphx-glr-auto-examples-classification-plot-shapelet-locations-py)

```python
from sktime.pipeline import make_pipeline
from sktime.transformations.series.summarize import SummaryTransformer
from sklearn.linear_model import LogisticRegressionCV
from sktime.pipeline import sklearn_to_sktime
```

```python
from tensorflow.keras.optimizers import Adam
from tslearn.shapelets import LearningShapelets, grabocka_params_to_shapelet_size_dict

from tslearn.datasets import CachedDatasets
from tslearn.preprocessing import TimeSeriesScalerMinMax
```

## more?
feature-based using tsfresh?