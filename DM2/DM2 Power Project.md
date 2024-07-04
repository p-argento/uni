https://www.gov.uk/government/collections/household-electricity-survey

[[DM2 Project Notes]]

```
** Background **
These problems were taken from data recorded as part of government sponsored study called Powering the Nation. The intention was to collect behavioural data about how consumers use electricity within the home to help reduce the UK's carbon footprint. The data contains readings from 251 households, sampled in two-minute intervals over a month.

** Problems **
ElectricDevices LargeKitchenAppliances RefrigerationDevices
ScreenType SmallKitchenAppliances

We create two distinct types of problem: problems with similar usage patterns
(Refrigeration, Computers, Screen) and problems with dissimilar
usage patterns (Small Kitchen and Large Kitchen). The aim is that
problems with dissimilar usage patterns should be well suited to
time-domain classification, whilst those with similar consumption
patterns should be much harder.

The five problems we form are summarised in the following table.

||	PROBLEM 	|| 	CLASS LABELS 					||
|| Small kitchen 	|| Kettle, Microwave, Toaster 				||
|| Large Kitchen 	|| Dishwasher, Tumble Dryer, Washing Machine 		||
|| Refrigeration 	|| Fridge/Freezer, Refrigerator, Upright Freezer 	||
|| Computers 		|| Desktop, Laptop 					||
|| Screen 		|| CRT TV, LCD TV, Computer Monitor 			||
```


## Ideas

1. after the best classification possible, I could try motifs and discords again



## To do

today
1. ts notebook
	1. motif/anomalies
	2. clustering
	3. classification
2. better EDA for ts
3. better EDA for tabular data
4. write draft report for the first half

friday
1. feature selection (RFE)
2. try advanced classifiers with default parameters

saturday
2. try task 3 on tabular dataset
	1. anomaly detection
	2. imblearn
3. finish draft report first half

sunday
1. first half of report in latex must be finished
2. must be finished all the raw experiments, included task 4

monday
1. 


## 1. EDA

![[DM2 Official Guidelines#Module 1 Data Understanding and Preparation]]

Start with ts eda.
Try approximations PAA and SAX.


*ts*
- `"pd-multiindex"` - a `pandas.DataFrame`, with row multi-index (instances, time), cols = variables
- `"numpy3D"` - a 3D `np.ndarray`, with axis 0 = instances, axis 1 = variables, axis 2 = time points
Decide to use numpy3d, I face less problems.

I still need to handle.
1. missing values (looks like there are none)
2. duplicates (a lot)
3. flat ts (maybe there are none)

For 


*tabular*
I created a tabular version of the time series using TSFreshFeatureExtractor.
I got 777 variables. I need to better understand what they are and decide if it is worth to keep them all. Is 'efficient' the correct value for the parameter?
Maybe with tree-based classifiers it is fine to keep them all, while with other distance-based I need to use dimensionality reduction techniques.








### REPORT

The time series dataset is made of 8926 records, each one has 96 timepoints and 1 class label.
There are no null points

class
5    2406
2    2231
4    1474
3     851
7     728
1     727
6     509



## 2. Time Series Analysis
Steps
1. motifs/discords
2. clustering
3. classification

![[DM2 Official Guidelines#Module 2 Time Series Analysis]]


## 3.  Advanced Data Pre-Processing
![[DM2 Official Guidelines#Module 3 Advanced Data-Preprocessing]]






## 4. Advanced ML
![[DM2 Official Guidelines#Module 4 Advanced ML & XAI]]


