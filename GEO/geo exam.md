---

---
## doubts
1. check matplotlib
2. predicates for sjoin
3. 


## sources of data
land
[geodatasets](https://geodatasets.readthedocs.io/en/latest/introduction.html)
[geojson.xyz](https://geojson.xyz/)
[natural earth data](https://www.naturalearthdata.com/downloads/110m-cultural-vectors/)


## oral questions
---

Overview of preprocessing techniques for trajectories
Compression methods for trajectories
EPR model 
Overview of clustering techniques

---

⁃ What measure can we use to evaluate the predictability of the trajectory of an agent? (—> entropy)
 ⁃ What are the different methods for alternative routing?
 ⁃ What are the different models to predict a flow? (—> Gravity and IO)
 ⁃ What are the different types of spatial and mobility data and describe them briefly. (—> GPS, MPR with CDR, XDR and CPR)


Both professors and both assistants were present, each of them asks about 2 questions

- Definition of trajectory, what measures can be defined on them (jump length, radius of gyration etc), what distribution they follow, what we conclude based on this observation
- Point pattern analysis, overview of methods to identify the type of point distribution (random/clustered/uniform)
- Pattern-based trajectory prediction
- EPR model, how it works in general; how does the algorithm choose between the two phases? (randomly, we externally set some parameter that controls how likely it is to choose one or the other). Is it possible that an exploration phase chooses to explore a location that was actually already visited before?(yes but the probability is so low it's basically impossible)
- Models to predict flows, describe the main differences
- Write main equation of the Gravity model; after this, I was asked to reason on how the free parameters would be set if the model were trained on three different types of datasets (daily mobility, relocation, airplane trajectories).

- The final question is to develop the solution to solve some specific task. We did not write any actual code, only specify the main steps. My task was: given a dataset of various individual trajectories, find a way to identify the means of trasportation used (bike, car, bus, etc. or walking). As I proposed some ideas they would also give some hints and ask how I would change my solution based on them.

---

geographic information system
what is a trajectory (good ) 
what is spatial tessellation (rivedi terza regola) 
what is a raster layer, and rasterization
what is vectorization
moran's ()
spatial interpolation 
Voronoi tessellation (definizione ) - bravo 
Interpolation methods
gps traces and formats
mobile network systems
types of mobile phone records
trajectories filtering
route reconstruction
trajectories compression (bene)
ramer-douglas-peucker
driemel
individual mobility network
gyration
epr
spatial flows (definition) 
generating spatial flows
local trajectory patterns
Markov models
hidden Markov models
predicting the next value using Markov models
pattern based predictions

mini projects:
transfer learning, models from another context
suppose you have 2 cities, 1 (A) with a lot of gps data and another (B) where you don't have data other then opestreetmap, gps, etc (but no trajectories).
Want an estimation of the matrix of flows in city B using the data of city A
given answer:
gravitation model 

estimate car autonomy (number of km) based on the usual geographical area he goes around in. 
answer:
POI on the petrol station
we have the trajectories of the car and we can find the stops at the petrol stations
find distance between one stop to petrol station and another
the teacher said that we have 1 year of records
answer: so we can find the max distance between petrol station and another

added question: where should we place a new petrol station?
answer: Voronoi tessellation from existing one