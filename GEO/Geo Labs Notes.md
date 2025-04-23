Main libraries
1. shapely
2. geopandas
3. scikit-mobility

> You might encounter problems of compatibility. Try to use the yml file on github.

Try QGIS software, it is opensource.

## Speed filter

1. get a trajectory of the city of pisa

```
let first valid point p_valid = (lat, lng, time)
let trajectory T=(p_0, ..., p_{n-1})
let T'=[T[0]]
let speed threshold st = 0
let invalid_points = []

def speed

	for p in range(points ordered):
		d=dist(p_valid, p)
		t=time(p_valid, p)
		s=speed(d,t)
		if s < st:
			newT.append(p)
			p_valid = p
		else:
			invalid_points.add(p)
			
```


To visualize a trajectory, use scikit-mobility using a trajectory dataframe.



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
