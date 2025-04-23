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


## Trajectory
sequence of points that describe people's movements.

> key concepts
> 1. definition of trajectory
> 2. definition of point



## Spatial Tessellation
division of space into non-overlapping tiles.

> 1. definition of spatial tessellation
> 2. characteristics of tessellation
> 3. types of tessellations (H3, voronoi, ...)


## Flows
movements of groups of people between places.

> 1. definition of flow


## -> homeworks and material














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
4. Spatial Trends






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













