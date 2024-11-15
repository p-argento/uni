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


## Lectures
*14/11* didawiki not working

Predictive vs Generative.
If fine-tuning chatgpt, it can generate trajectories.
However, we do not know how the LLM works.
In mechanicistic models, the generation is explainable by design, because there is a formula that you can understand.

Physics informed AI is a new approach. 

We will see
1. individual models (to generate trajectories)
	1. EPR model (fundamental)
	2. EPR variants
2. collective models (to generate flows between locations)
	1. Gravity
	2. Radiation
	3. Deep Gravity

A flow describes how individuals move from one point to another. The flow is not only a group of people moving together, a flow describes how many objects move from one point to another.

Why should we generate trajectories?
What happens if I close a road? What happens if I limit all the streets to 30 kmh? I need simulations to predict the impact.
There are also privacy concerns.

Why synthetic flows?
One of the most important aspects is to complete data that I do not have in dataset.

Let's dive into individual.

"Exploration and Preferential Return Model (ERP)"
You are more likely to come back up or go to the cinema?
When I return, I go back to an already visited location with a probability based on the number of times I already visited it.
How to explore?
Popular ones, locations near me, friends, ...
Based on the initial ERP model, I am more likely to explore locations near me.
We have seen that the distribution of distances covered by an individual is a power law. This means that picking at random a distance, it will be more likely a short one.

Also the distribution of inter-time is a power law. It is the time between one visited and another.

Looking at CDR, it is not possible to distinguish real data from synthetic one.

Any model can reproduce a limited number of patterns, but not all of them. This means that the ERP model is realistic but not perfect.
For example, regarding time, the ERP do not capture the routines we have, it only camptures that I rest.

> EPR is the only trajectory model you need to know for the exam (?)

Now we move to spatial flows.

The origin-destination matrix is a square matrix, with origins in the rows and destinations in the columns.

The matrix is very sparse. Only a small fraction is realized.
Again, it is a power law. The vast majority of flows are small, and a small flows large. Like the flow between pisa and florence.

Flows
1. decay with distance
2. grow with population
3. grow with opportunities
	1. (jobs, university, hospital, ...)
	2. typically jobs

two main models
1. gravity (G) models
2. intervening opportunities (IO) model

The G model comes from newton law of gravitation.
Tij is the number of people moving from i to j. It is a formula (see slides).

We have singly constrained model and globally constrained model.

How can I fit the parameters of the gravity model?
I apply a Generalized Linear Model (GLM), kind of regression.

Many applications.
How do I validate? train-test ml-style.
It is a predictive model.
It is very good to predict and versatile, but it is not very generalizable.

IO model.
What is intervening opportunities?
It means what I can do closer instead of going further.(?)
Opportunities do not have a precise definition.

Stouffer(1940) defined the IO concept and Schneider(1959) built the model.

The Radiation model is proposed by the same people of ERP. But they do not know the IO model, that is more or less the same.
The traveler choose the closest point with the higher opportunities than the starting point.

The G model uses the distance explicitly, the Radian model do not. It is taken into account indirectly through the concept of IO.

The IO model
1. is parameter free
	1. meaning that we do not need data to train
2. performance is comparable to G
	1. however, at some scales (like cities) it does not work well (very good for states though)

OTHER COLLECTIVE MODELS.
...

MoGAN can be used to generate flows. GAN are usually used with images, but the origin-destination matrix can be treated like one.

LLMs are now used to generate trajectories and flows (there is an obsession).

The Deep Gravity Model (DG) is much better than G.
But we are still far from capturing the real flows in cities.


> You can try to use the models in scikit-mobility and compare them with real flow data





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

If we do not have a precise geometry for cities, we can use bounding boxes (bbox), meaning that we need to build a geometry of the rectangle.

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

To build a geopandas df, you need do actually build a new object, adding the geometry column is not enough.
Remember always to specify the CRS (Coordinates Reference System), because every file uses a different one.

Geoapify is a website where you can find useful datasets, for example the one that we need for the population.

We didn't find any correlation. 
Try to perform your own analysis going deeper.
Does this hypothesis hold.


## Lab on trajectory generation

What do I need to fit the model?

If we have flows of migration within the same state, we have a problem in the gravity model, because are dividing by the distance that is zero.

It might happen that I have some flows towards states that are not defined in the tessellation (like San Marino)' ???

There is a particular gravity model, called single constraint gravity model, where you fix the number of outflow you observe from...
What do you expect from the params?

Be aware that geopandas wants a string for the tessellation, while skmobility uses a number.














