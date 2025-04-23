This is about Module 1
 
 
 MODULE 1: Spatial and Mobility data
 1. basic concepts
	 1. geographic coordinates systems, vector data model
 2. data types
	 1. trajectory, flows, tessellations
 3. spatial and mobility data
	 1. mobile phone records, gps traces, social media records, POIs, Road Networks
 4. pre-processing mobility data
	 1. filtering, compression, stop detection, trajectory segmentation, trajectory similarity and clustering
 5. (practice) open-source tools for geospatial analysis
	 1. shapely, geopandas, folium, scikit-mobility, osmnx and more




# 1. Introduction

Interesting concepts.

Digital footprints of human activity.
![[Pasted image 20250423171425.png]]

Big data properties
1. volume
2. velocity
3. variety
4. veracity
5. value

> Material  
>● [book] Introduction to geographic information systems, Kang-Tsung Chang, McGraw-Hill ○ Chapter 1  
>● [paper] Human Mobility: Models and Applications, Barbosa et al., Physics Reports  ○ Section 1 (Introduction)




# 2. Fundamental Concepts

## Definitions

Geographic Information System (GIS).
1. it is a computer system for capturing, storing, querying, analyzing and displaying geospatial data.

Fundamental Concepts.
1. Geographic Coordinate System (GCS)
	1. reference system for locating points on the Earth's surface
2. Vector Data Model
	1. representation of spatial features in GIS
3. Trajectory
	1. sequence of points that describe an individual movements
4. Spatial Tessellation
	1. division of space into non-overlapping tiles
5. Flows
	1. movements of groups of people between places


## Geographic Coordinate System (GCS)
reference system for locating points on Earth's surface.

> key concepts
> 1. gcs
> 2. geodetic datum
> 3. wgs84
> 4. nill points
> 5. distance with haversine

It is based on 2 angles
1. longitude (long)
	1. angle E/W from the Prime Meridian (PM)
2. latitude (lat)
	1. angle N/S of the equatorial plane

Meridians



## Distance on the Earth

Straight lines are replaced by *geodesics (great-circles)*.
However, the Earth is only nearly spherical, meaning that great-circle distance are correct to within 0.5%, still this is the formula we use.
Between two points we find the shortest arc on the great-circles which connects them. If they are not antipodal, this great-circle is unique.

To compute the distance between two pointsWe can use
1. spherical law of cosines
2. haversine formula

*1. spherical law of cosines*
![[Pasted image 20250423181407.png]]
where
1. d is the angular distance (central angle) between points A and B

To obtain the actual linear distance measure on Earth
1. compute d from the arccos of the result
2. then multiply it by the Earth's radius $r=111.32\text{ km}$
	1. ie. length of 1 degree at the equator

*2. haversine formula*
An approximation because the Earth is not a perfect sphere.
Generally preferred for computational purposes (especially for small distances) because it's numerically more stable.
It is obtained from the spherical law of cosines.

The haversine function is
$$\operatorname{hav} (\theta) =\sin ^{2}\left({\frac {\theta }{2}}\right)={\frac {1-\cos(\theta )}{2}}$$
And its inverse
$$\operatorname {archav} (\operatorname {hav} \theta )=2r\arcsin \left({\sqrt {\operatorname {hav} \theta }}\right)$$
And the law of haversines is
$$\operatorname{hav} \left(\theta \right)=\operatorname {hav} \left(\Delta \varphi \right)+\cos \left(\varphi _{1}\right)\cos \left(\varphi _{2}\right)\operatorname {hav} \left(\Delta \lambda \right)$$

An example from wikipedia
![[Pasted image 20250423182858.png]]




## Trajectory
sequence of points that describe people's movements.

> key concepts
> 1. definition of trajectory
> 2. definition of point

![[Pasted image 20250423183112.png]]

It is crucial to observe that there is a third dimension that is time!
It is a TIME-ORDERED sequence of points.

## Spatial Tessellation
division of space into non-overlapping tiles.

> 1. definition of spatial tessellation
> 2. characteristics of tessellation
> 3. examples of tessellations (H3, voronoi, ...)

![[Pasted image 20250423183225.png]]

It is a division of space into geometric subspaces.

A tesselation can be
1. regular (equilateral triangular, squared, hexagonal, ...)
2. irregular (buildings, administrative units, ...)
A spatial join can be used to associate a point with the (one and only) tile that contains it.

Some examples of tessellation are
1. Uber H3
	1. recursively creates high precision hexagons
	2. each cell is splitted into 7 children
2. S2 Geometry
	1. decompose into a hierarchy of cells ??
3. Voronoi tessellations
	1. for any object there is a corresponding region called Voronoi cell, consisting of all points of the plance closer to that seed than to any other
	2. if I take a point in a cell, its closest central point is the one representing the cell
	3. eg. in mobile phone cells

![[Pasted image 20250423183548.png]]

![[Pasted image 20250423184026.png]]

## Flows
movements of groups of people between places.

> 1. definition of flow

![[Pasted image 20250423184153.png]]

The result of a flow will be a graph where each vertex is a tile and each edge will be labelled with the number of objects moving on that trajectory.

Can trajectories be obtained from flows? NO.
This is why it is better to have a dataset of trajectories, even though they are rare because they are more sensitive to privacy.





## -> homeworks and material
“Homework 2.1” ([“02 - fundamental concepts_24_25”, p. 48](zotero://select/library/items/KBMVVBJK)) ([pdf](zotero://open-pdf/library/items/LPT3QCTM?page=48))



# 3a. Spatial Data Analysis (1)

Content
1. basic terms and concepts from GIS worlds
	1. raster layers
	2. vector data model (and data representation)
	3. data representation model
2. basic spatial data types
	2. raster vs vectorial
3. basic spatial operations
	1. intersection, union, difference
	2. buffering
	3. spatial join
4. simple spatial patters and concentration measures
	1. Moran's I(ndex)
	2. Geary's C

...



## Point spatial patterns

Actually chapter 4 is
4. point spatial patterns and spatial correlation
	1. density
	2. Nearest Neighbors (NN)
	3. Moran's I
	4. Geary's C

The general objective is understand how object are distributed in space.

In spatial point pattern analysis, spatial distribution patterns are typically categorized into three types
1. uniform (discrete) distribution
2. random distribution
3. clustered distribution

![[Pasted image 20241017114922.png]]

As in statistics, we can define
1. a center around which all objects are distributed
2. various dispersion indexes to measure how much they are dispersed around

![[Pasted image 20241017115059.png]]

## 1. Density estimation
How many points (or objects) are in the same place?
Based on the different interpretation of "place", we distinguish
1. global density
	1. computed over all geographical area
	2. eg. number of restaurants per m2
2. local density
	1. computed over all the geographical area
	2. eg. number of restaurants per m2 for each municipality
3. kernel density
	1. density of one cell is computed considering its neighborhood
	2. eg. restaurans in and around municipality

![[Pasted image 20241017115434.png]]

To compute the kernel density
1. define a neighborhood Nc for each cell C
	1. typically the 8 adjacent cells
2. density of C = density of $C\cup N_c$
	1. there is a smoothing effect similar to the "moving average in time series"

![[Pasted image 20241017115710.png|400]]

An alternative is the "weighted kernel density".
The points in the neighborhood have a weight dependent on the distance from C's center.

![[Pasted image 20241017115845.png]]

## 2. (NNs) Random vs Pattern

Two types of analysis
1. Average Nearest Neighbor (ANN)
2. L function (aka standardized Ripley's K-function)

## 3. Spatial Autocorrelation

Autocorrelations is the correlation between values of the same variable (eg temperature) measured in different times or places.
We distinguish
1. different times -> time series -> temporal autocorrelation
2. different places -> geospatial data -> spatial autocorrelation

Tobler's first law of geography.

...


# 3b. Spatial Data Analysis (2)

Content
1. Spatial Interpolation
	1. Thiessen polygons
	2. IDW
	3. Kriging
2. Spatial Regression
3. Spatial Associations: co-location patterns
4. Spatial Trends Detection










# 4. Spatial and mobility data

Sources of mobility data
1. GPS
2. Mobile Phone Records
3. Location-based social networks (LBS)
4. Road Networks and POIs

![[Pasted image 20241017153457.png]]





# 5. Preprocessing Mobility Data

*Content*
Preprocessing trajectories
1. trajectory filtering
2. point map matching
3. route reconstruction
4. trajectory compression
5. semantic enrichment
	1. stop detection / trajectory segmentation
	2. home location detection (GPS & MobPhones)
	3. activity recognition (POI-based)

## 1. Trajectory Filtering
Different types
1. context-based filtering
2. movement-based filtering

## 2. Point Map Matching



## 3. Route Reconstruction



## 4. Trajectory Compression













