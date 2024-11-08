Prof. Pappalardo

[Didawiki Geo](http://didawiki.di.unipi.it/doku.php/geospatialanalytics/gsa/start)
[Github Geo](https://github.com/jonpappalord/geospatial_analytics)

[[Geo labs]]

## News
Try the compression exercise.



## Notes from slides

[[Geospatial Analytics - Module 1]]

[[Geospatial - Module 2,3,4]]




## Introduction
Mobility data and spatial phenomena.

*People*
Riccardo di clemente (guest lecture).
Barabàsi (book).
Greg Milner (book on gps).

The evolution of science is made by tools, like the microscope or phones.
Higher dimensional data are more sensitive to privacy.

Provide feedback on the book that they are writing.

## GIS

Fundamentals concpets
1. Geographic coordinate system
	1. to locate points on Earth
2. Vector data model
	1. representation of spatial features
3. Trajectory
	1. sequence of points
4. Spatial tessellation
	1. division of space in non-overlapping tiles
5. Flows
	1. movements of people
	2. COMPARING WITH TRAJECTORY, the trajectory is a single 

Geographic Coordinate System (GCS).
Be aware of the order used by the library.
Is it (lat,long) or (long, lat)?


## Code fundamentals
See the github.

Main libraries
1. shapely
2. geopandas
3. scikit-mobility

> You might encounter problems of compatibility. Try to use the yml file on github.

## Spatial Data Analysis

Try QGIS software, it is opensource.



bounding box ?

*homework*
eliminate duplicate rows



## Lab on individual mobility

stanford dataset brightkite

Do people in hotels in bigger cities walk more than those who are in hotel in smaller cities?
1. understand check-in data structure
2. discover hotel (think of it as the home location)
	1. call it HGDF (HomeGeoDataFrame)
3. get population and geometry data for cities
	1. you might need to join different geometries


What is the home? We need a Home Detection Algorithm (HDA)
For calls, it is the antenna you use mostly, especially at night.
For gps, we can assume the night.

If we do not have a precise geometry for cities, we can use bounding boxes, meaning that we need to build a geometry of the rectangle.

To compute the amount of walking for each individual, we can use the radius of gyration (rog). However, remember that if the time is too short, it can be unstable (recall the plot in the slides).

> The data should be interpreted, data is not truth, but it depends on how you see and process data. Think about the power law in individual mobility and the work of alessandretti. This is one of the most important messages of the course.

The dataframes we have are
1. HL (home location)
2. POP (population)
	1. with the polygon column
3. ROG (radius of gyration)
	1. uid, rog

We do a spatial join between HL and POP.
Left or right join? Let's keep the inner join.
Now we have
4. df4
	1. uid, geom_x, city, pop, geom_y

A classic join of df4 and df3 leads to
5. df5
	1. uid, geom_x, city, pop, geom_y, rog

Plot scatterplot with rog and pop.

Let's sum up.
1. retrieve the check-in data $C$
2. retrieve population data (and geometry) $P$
3. compute house-hotel location $HL$
4. compute how much individual walked (distances, RoG, ...) $D$
5. spatial join (sjoin of $HL$ and $P$) $SJ$
6. join of $SJ$ and $D$ to get $J$
7. scatterplot

Let's see the skmob implementation.

When we look at the data, we immediately notice the null island.
Always clean data, remember also the speed filter.
We will focus our analysis only on the us, doing a spatial join with the shape of the us.
geojson.io is a website where you can draw a rectangle on the map and get the coordinates. The alternative is to use google map and manually see the coordinates of the rectangle you want.
















