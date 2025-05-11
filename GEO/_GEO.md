Prof. Pappalardo

## Slides
[[Geospatial Analytics - Module 1]]
[[Geospatial - Module 2,3,4]]

## Geo Labs
[[Geo Labs Notes]]
[Github Geo](https://github.com/jonpappalord/geospatial_analytics)

[[geo ideas]]
## Interesting links

[Didawiki Geo](http://didawiki.di.unipi.it/doku.php/geospatialanalytics/gsa/start)
[[Riccardo Di Clemente]]
[geo conference](https://www.datastories.org/bmda24/BMDA24Accepted.html)

Riccardo di clemente (guest lecture).
Barabàsi (book).
Greg Milner (book on gps).

> The evolution of science is made by tools, like the microscope or phones.

Provide feedback on the book that they are writing.


## Lecture *14/11* didawiki not working

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
For example, regarding time, the ERP do not capture the routines we have, it only captures that I rest.

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


w