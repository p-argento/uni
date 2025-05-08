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
	2. distances on earth
2. Vector Data Model (see NEXT LESSON)
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

![[Pasted image 20250430162547.png]]

![[Pasted image 20250430162600.png]]





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
2. then multiply it by the Earth's radius
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

## Raster Layers
Pixelized version of Earth.

Usually the map is made of both raster and vector layers together.

## Vector Data Model
Purely geometrical description (NO raster NO vectorial).

It is more practical for data analysis.
It uses discrete geometrical objects to represent spatial features.
1. data types
	1. using points, lines and polygons on an empty space
2. data properties
	1. structuring the properties and spatial relationships of these geometric objects
3. data format
	1. coding and storing vector data in digital data files

Vector Data types and properties
1. point (0-dimension)
2. line (1-dimension)
3. polygon (2-dimensions)

Data format (see “Data Format Examples” ([pdf](zotero://open-pdf/library/items/REJBJS4Y?page=15)))
1. google KML
2. GeoJSON
3. Shapely (Python Library)

![[Pasted image 20250423191948.png]]

Terminology (alert!)
1. (spatial) features (better call them *geometries*)
	1. are objects (points, polygons, etc) in a layer
	2. they are "features" of space, but the term can be confusing
2. (non-spatial) *attributes*
	1. are other variables
	2. eg. the temperature
	3. DO NOT call them features


Data representation model
(representing geometric object on computer):
1. geo-relational data model
	1. stores geometries and attributes separately (different tables)
	2. associating attributes to objects may require joins
2. object-relational data model
	1. stores geometries and attributes together


## Spatial Operations
> 1. intersection, union, difference
> 2. buffering
> 3. spatial join

Operations more oriented to manipulate geometries or manage the non-spatial attributes.
1. overlays
	1. from set theory
	2. operations
		1. intersection $A\cap B$
		2. union $A \cup B$
			1. Warning: some tools (e.g. QGIS) return a multipolygon. Here union just added a polygon. Solution (if it is a problem): “dissolve” operation
		3. difference $A-B$ or $A/ B$
2. buffers
	1. expanding the shape by a given amount
	2. equivalent to replace each point in the geometry by a circle
	3. eg. buffer of 10 km
2. spatial join
	1. joining attributes of geometries
	2. merging the information of two objects if they match
		1. ie. intersect, contains, equals, touches
	3. can be inner or outer join




## Spatial point patterns
> 0. utilities
> 1. density-based
> 2. location-based

Actually chapter 4 is
4. point spatial patterns and spatial correlation
	1. density estimation
	2. Nearest Neighbors (NN)
	3. spatial autocorrelation measures

The general objective is understand how object are distributed in space.

In spatial point pattern analysis, spatial distribution patterns are typically categorized into three types
1. uniform (discrete) distribution
2. random distribution
3. clustered distribution

![[Pasted image 20241017114922.png]]

As in statistics, we can define
1. mean center
	1. a center around which all objects are distributed
2. various dispersion indexes
	1. to measure how much they are dispersed around
	2. eg
		1. standard distance
		2. standard deviational ellipse

![[Pasted image 20241017115059.png]]

*1- Density-based Pattern Analysis*
using density estimation
> 1. global/local density
> 2. kernel/weighted-kernel density

How many points (or objects) are in the same place?
Based on the different interpretation of "place", we distinguish
1. global density
	1. computed over all geographical area
	2. eg. number of restaurants per m2
2. local density
	1. computed separately over the small cells of a tessellation
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

**2-Location-based Pattern Analysis**
Random vs Regular Pattern using Nearest Neighbors
1. . Average Nearest Neighbor (ANN)
2. . L-function (aka standardized Ripley's K-function)

Two alternative types of spatial point pattern aalysis
1. Average Nearest Neighbor (ANN)
2. L-function (aka standardized Ripley's K-function)

Sometimes one approach is better than the other, best to use both.

*1 - Average Nearest Neighbor (ANN)*
1. associate each point to its nearest neighbor distance $d_i$
2. compute average $d_i$ values called $d_{obs}$
3. normalize wrt expected $d_{obs}$ over random points $d_{exp}$ meaning $$R=\frac{d_{ops}}{d_{exp}}$$
![[Pasted image 20250430113455.png]]

*2 - L-function (aka standardized Ripley's K-function)*
1. given N points in an aerea of size $A$ and a distance parameter $d$
2. compute all $N(N-1)$ distances between each pair of points
3. compute the fraction $\phi$ of distances that are $<d$
4. compute $L(d)=\sqrt{\frac{A}{\pi}\phi}$

Then see
1. $L(d)=d$ for random points
2. exploring $L(d)$ for various d values allows understanding patters at different spatial granularities

![[Pasted image 20250430114147.png|350]]

## Spatial Autocorrelation
> 1. definition of spatial autocorrelation
> 2. moran's I
> 3. Geary's C

Autocorrelations is the correlation between values of the same variable (eg. temperature) measured in different times or places.
(eg. how much is temperature in one place influenced by temperature around it?)

We distinguish
1. different times -> time series -> temporal autocorrelation
2. different places -> geospatial data -> spatial autocorrelation

Tobler's first law of geography.
"everything is related to everything else, but near things are more related than distant things."

*1. Moran's I*
"I" stands for index; it is the measure of autocorrelation;  
for each point we look at its neighbours, for each pair we compute the displacement and the displacement of the other point ;  
the formula is similar to the standard formula of autocorrelation.

![[Pasted image 20250430153450.png]]

It is the autocorrealtions between values of each point againsta all other points in its neighborhood.
when the two displacements are both positive or both negative the sum will be higher;
the highest is I, the more correlated are nearby values.

An alternative reading of Moran's Index is to see it as the average of several "Local Moran's Indexes".
We can explore Local's I values in a "spatial lag plot", similar to lag plots in time series ("lag" means average value around the reference point).

*Geary's C*
Alternative for Moran's I.
The interpretation is the opposite, low C means low correlation (ie. higher C, more different are nearby values).

![[Pasted image 20250430154052.png]]

Geary's C is less sensitive to linear associations.
Also here a Local C can be explored.

![[Pasted image 20250430154234.png]]


![[Pasted image 20250430154311.png]]



# 3b. Spatial Data Analysis (2)

Content
1. Spatial Interpolation
	1. Thiessen polygons (or proximity interpolation)
	2. Inverse Distance Weighted (IDW) interpolation
	3. Surface Interpolation
	4. Kriging
2. Spatial Regression
	1. difference with interpolation
	2. spatially lagged exogenous regressors
3. Spatial Associations: co-location patterns
	1. co-location patterns
	2. pattern quality measures
4. Spatial Trends Detection
	1. spatial trend definition and examples


## 1. Spatial Interpolation
> 0. spatial interpolation definition 
> 1. Thiessen polygons (or proximity interpolation)
> 2. Inverse Distance Weighted (IDW) interpolation
> 3. Surface Interpolation
> 4. Kriging






## 2. Spatial Regression
> 1. difference with interpolation
> 2. spatially lagged exogenous regressors

## 3. Spatial Associations
>1. co-location patterns
>2. pattern quality measures

## 4. Spatial Trends Detection
>1. spatial trend definition and examples




# 4. Spatial and mobility data
Main sources to describe mobility data

Content
1. Sources of mobility data
	1. GPS
	2. Mobile Phone Records
	3. Location-based social networks (LBS) (aka Checkins)
2. Road Networks and POIs
	1. data format of road networks
	2. data format of POIs

![[Pasted image 20241017153457.png]]
## 1. GPS data
> 1. GPS segments
> 2. Trilateration (how GPS works)
> 3. GPS traces format

Global Positioning System (GPS) is the most famous Global Navigation Satellite System (GNSS). The complete name is actually NAVTEC GPS, it is a US owned utility providing users with positioning, navigation and timing (PNT) services.

*1. GPS segments*

The system is made of 3 main components
1. space segment
2. control segment
3. user segment

1 - space segment
More than 24 satellites, each orbiting at 20k km.
Circling earth twice a day in 6 equally-spaced orbits (4 satellites each)
Broadcasting a gps radio signal, given that a user view at least 4 satellites from any point.

2 - control segment (on earth)
The current Operational Control Segment (OCS) includes
1. a master control station
2. an alternate master control station
3. 11 command and control antennas
4. 16 monitoring sites
The high performance of these satellites constellation is thanks to the team Blackjack.

![[Pasted image 20250505165715.png]]

3 - user segment
GPS is everywhere: cell-phones, wristwatches, bulldozers, shipping containers, ATM's, sports bras, ...

![[Pasted image 20250505165758.png]]


*2. Trilateration (how GPS work)*
Steps for trilaterations.

![[Pasted image 20250505171459.png]]



*3. GPS traces format and precision*
The sampling rate depends on the device, usually from few seconds to 1-2 minutes. However, we often find aggregated data.

![[Pasted image 20250505170241.png|300]]

The spatial precision can be 10m.

![[Pasted image 20250505170408.png]]

Remember that there are are GNSS, not only GPS.
It is a matter of politics.

![[Pasted image 20250505170503.png]]

## 2. Mobile Phone records
> 1. mobile network system
> 2. types of mobile phone records



## 3.  Checkins data
aka Location-based social networks (LBS data).


## 4. Road Networks and POIs data format








# 5. Preprocessing Mobility Data

*Content*
Preprocessing trajectories
1. trajectory operations
	1. trajectory filtering
	2. point map matching
	3. route reconstruction
	4. trajectory compression
2. semantic enrichment
	1. stop detection / trajectory segmentation
	2. home location detection (GPS & MobPhones)
	3. activity labelling / recognition (POI-based)

## 1. Trajectory Filtering
Different types
1. context-based filtering
2. movement-based filtering

## 2. Point Map-Matching



## 3. Route Reconstruction
for trajectory map-matching


## 4. Trajectory Compression



## 5. stop detection / trajectory segmentation
semantic entrichment 1/3


## 6. home location detection (GPS & MobPhones)
semantic enrichment 2/3

## 7. activity labelling / recognition (POI-based)
semantic enrichment 3/3









