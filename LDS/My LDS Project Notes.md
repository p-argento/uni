*MOVED TO GITHUB*

## 14/11
I want to understand the structure of the dataset.
In particular, I want to understand
1. each feature, so that I can fill missing values
2. how the 3 files are related to each other, so that I can do a join and work with a unique operational table, that will be later divided into dimensional tables for the analysis
3. looking at the BQ, if I can have an idea of the solution and if it possible to anwer
4. think of additional data to be integrated
	1. can I use flows in the lds dataset? are they useful?
	2. what if I use a tesselletion and set maybe the avg salary of the neighborhood.
	3. POIs from OSM. How do they can be useful for insurance purposes?

I found the following resources online:
1. [crashes description](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data)
Crash data shows information about each traffic crash on city streets within the City of Chicago limits and under the jurisdiction of Chicago Police Department (CPD). Data are shown as is from the electronic crash reporting system (E-Crash) at CPD, excluding any personally identifiable information. Records are added to the data portal when a crash report is finalized or when amendments are made to an existing report in E-Crash. Data from E-Crash are available for some police districts in 2015, but citywide data are not available until September 2017. About half of all crash reports, mostly minor crashes, are self-reported at the police district by the driver(s) involved and the other half are recorded at the scene by the police officer responding to the crash. Many of the crash parameters, including street condition data, weather condition, and posted speed limits, are recorded by the reporting officer based on best available information at the time, but many of these may disagree with posted information or other assessments on road conditions. If any new or updated information on a crash is received, the reporting officer may amend the crash report at a later time. A traffic crash within the city limits for which CPD is not the responding police agency, typically crashes on interstate highways, freeway ramps, and on local roads along the City boundary, are excluded from this dataset.

2. [people description]()
This data contains information about people involved in a crash and if any injuries were sustained. This dataset should be used in combination with the traffic Crash and Vehicle dataset. Each record corresponds to an occupant in a vehicle listed in the Crash dataset. Some people involved in a crash may not have been an occupant in a motor vehicle, but may have been a pedestrian, bicyclist, or using another non-motor vehicle mode of transportation. Injuries reported are reported by the responding police officer. Fatalities that occur after the initial reports are typically updated in these records up to 30 days after the date of the crash. Person data can be linked with the Crash and Vehicle dataset using the “CRASH_RECORD_ID” field. A vehicle can have multiple occupants and hence have a one to many relationship between Vehicle and Person dataset. However, a pedestrian is a “unit” by itself and have a one to one relationship between the Vehicle and Person table.

3. [vehicles description](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Vehicles/68nd-jvt3/about_data)
This dataset contains information about vehicles (or units as they are identified in crash reports) involved in a traffic crash. This dataset should be used in conjunction with the traffic Crash and People dataset available in the portal. “Vehicle” information includes motor vehicle and non-motor vehicle modes of transportation, such as bicycles and pedestrians. Each mode of transportation involved in a crash is a “unit” and get one entry here. Each vehicle, each pedestrian, each motorcyclist, and each bicyclist is considered an independent unit that can have a trajectory separate from the other units. However, people inside a vehicle including the driver do not have a trajectory separate from the vehicle in which they are travelling and hence only the vehicle they are travelling in get any entry here. This type of identification of “units” is needed to determine how each movement affected the crash. Data for occupants who do not make up an independent unit, typically drivers and passengers, are available in the People table. Many of the fields are coded to denote the type and location of damage on the vehicle. Vehicle information can be linked back to Crash data using the “CRASH_RECORD_ID” field. Since this dataset is a combination of vehicles, pedestrians, and pedal cyclists not all columns are applicable to each record. Look at the Unit Type field to determine what additional data may be available for that record.

And here's the instructions for [officers](https://idot.illinois.gov/content/dam/soi/en/web/idot/documents/transportation-system/manuals-guides-and-handbooks/safety/illinois-traffic-crash-report-sr-1050-instruction-manual-2019.pdf).

![[Pasted image 20241114164152.png]]

This in particular, may be the reason for the duplicates in people.
However, the column REPORT_TYPE in Crashes contains only ON SCENE and NOT ON SCENE (DESK REPORT), meaning that the amended have been removed. There is something strange here.


## 16/11
To do
1. damage_id
	1. temporary solution, but looks the best for now
2. join people and vehicles
	1. fix the PERSON_ID and CRASH_UNIT_ID



- Prefixes
The prefixes in crashes look random.
Discovered that the prefix P in people is for passengers, while O is for all other PEOPLE_TYPEs.
The vehicle id are just floats.

- IDs
In vehicles
1. no vehicle_id -> pedestrian, bycicle, non-motor vehicle
2. with vehicle_id -> driver (6 nan), parked, driverless
3. ambiguous -> NON-CONTACT VEHICLE(42 nan over 102)

![[Pasted image 20241116181838.png|300]]



Trying to understand better the use of IDs in the 3 tables.
```
Table crash_data {
  rd_no string [pk]
  crash_date string
  posted_speed_limit integer
  traffic_control_device string
  device_condition string
  weather_condition string
  lighting_condition string
  first_crash_type string
  trafficway_type string
  alignment string
  roadway_surface_cond string
  road_defect string
  report_type string
  crash_type string
  date_police_notified string
  prim_contributory_cause string
  sec_contributory_cause string
  street_no integer
  street_direction string
  street_name string
  beat_of_occurrence float
  num_units float
  most_severe_injury string
  injuries_total float
  injuries_fatal float
  injuries_incapacitating float
  injuries_non_incapacitating float
  injuries_reported_not_evident float
  injuries_no_indication float
  injuries_unknown float
  crash_hour integer
  crash_day_of_week integer
  crash_month integer
  latitude float
  longitude float
  location string
}
```


```
Table person_data {
  person_id string [pk]
  person_type string
  rd_no string [ref: > crash_data.rd_no]
  vehicle_id float
  crash_date string
  city string
  state string
  sex string
  age float
  safety_equipment string
  airbag_deployed string
  ejection string
  injury_classification string
  driver_action string
  driver_vision string
  physical_condition string
  bac_result string
  damage_category string
  damage float
}
```

```
Table vehicle_data {
  crash_unit_id integer [pk]
  rd_no string [ref: > crash_data.rd_no]
  crash_date string
  unit_no integer
  unit_type string
  vehicle_id float
  make string
  model string
  lic_plate_state string
  vehicle_year float
  vehicle_defect string
  vehicle_type string
  vehicle_use string
  travel_direction string
  maneuver string
  occupant_cnt float
  first_contact_point string
}
```

Things we want to do within wednesday
1.⁠ ⁠loop over record with a function to fill NA/UNKNOWN/(retrieved) the variables
2.⁠ ⁠⁠join the 3 tables
3.⁠ ⁠⁠sketch datamart

## 17//11

Maybe the join works.

Rileggendo le guidelines, ho notato questo:
“To design the DW schema, since we’re simulating an insurance company, the fact table should capture details about the damage costs reimbursement each client incurs for each crash event.”

Significa che per loro ci sono diversi damage costs (plurale) per ogni cliente (singolare) in ogni incidente. Quindi è praticamente certo che si debba creare una primary key per damage.

Per fare i join ho quindi tenuto sempre sulla sinistra la tabella people (che poi andrebbe chiamata damages). Il join con crashes è su RD_NO, abbastanza facile. Il join con vehicles è più complicato, ma rimuovendo i nan su VEHICLE_ID e facendo il join su quello funziona. Ho infatti rimosso le colonne che dicevamo essere inutili.


## 18/11

Provo a seguire le slide per costruire il data mart.
Gli step sono

*Step 0. Requirements gathering*
Requirements gathering focuses on the study of business processes and on analysis relevant for decision making.

Business questions can be
1. "why is my business not meeting the targets?"
	1. WRONG, not useful
2. "total revenue, by customer, by product"
	1. useful
	2. observe that
		1. "total" is the metric (aggregated)
		2. "revenue" is the measure
		3. "by customer, by product" are the dimensions
3. report
	1. useful, but more difficult

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line

Let's recall the business questions we have now.
```
6c. For every year, show the total crash damage costs for each incident

7c. A beat is classified as dangerous if the number of crashes within that beat exceeds the average number of crashes across all other beats by more than 10%. List all the beats that meet this criterion.

8c. For each beat, show the primary contributory cause to the crash ordered by the total crash damage costs in percentage.
```




*Step 1. Identify the granularity of the fact*
The first fundamental decision to be taken is the meaning of the fact. What is the grain?

Identifying the grain means deciding the level of detail you want to be made available in the dimensional model. The more detail, the lower the level of granularity. Consider
1. grain is the precision with which the measurements are taken
2. grain determines measures and dimensions and dimensions determine grain

For example, the fact can be
1. an order line, for example the eggs bought
2. a complete order
More detailed grain, often means more space required.

Fact types can be
1. transaction
	1. one fact per transaction, meaning an event that occurs at a specific point in time
	2. for example, a transaction for an individual account of a customer of a bank
2. periodic
	1. one fact for a group of transactions made over a period of time
	2. for example, the amount is the monthly balance for all transaction against an individual account of a customer of a bank
3. accumulating
	1. one fact for the entire lifetime of an evolving event that has a duration and change over time
	2. for example, the lifetime of a mortgage application

> For us, the grain is the damage to user, that is the fact

*Step 2. Identifying the fact measures*
The measures of interest are numeric values that make sense to add. Not everything that is numeric is a measure.

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line

Not everything that is numeric is a measure! A measure is an observation of the performance of a business process. They can always be aggregated, for example the order number cannot and hence is not a measure.

Measure types
1. numeric additive
2. factless (or measureless)
	1. if the measure is missing
	2. for example the complaints
	3. there is ONLY one operation that we can do that is COUNT(\*)
3. numeric non-additive
	1. for example "unit price" or "gross margin"
4. numeric semi-additive
	1. with respect to a dimension, meaning that sometimes the sum makes sense, sometimes it doesn't
	2. "a measure M is semi-additive with respect to a dimension D1 when it cannot be aggregated with the function SUM for groups of data with different values of D1"
	3. for example "monthly balance" cannot be summed by time, but we can sum the "monthly balance" of two people for a fixed month


*Step 3. Identify the fact dimensions*
Identify the dimensions to give fact measures their context.

The Six Ws questions aim to identify the variables determining the measures and possible intervention levers:
Who is it about? What happened? When did it take place?  Where did it take place? Why did it happen? How did it happen?

> The suggested fact dimensions are
> 1. date
> 2. place
> 3. vehicle
> 4. crash
> 5. person
> 6. weather
> 7. cause



*Step 4. Identify Dimensional Attributes*
The dimensional attributes are important for analysis and for reports.

```
'damage_id', 'PERSON_ID', 'PERSON_TYPE', 'RD_NO', 'VEHICLE_ID', 'CITY',
       'STATE', 'SEX', 'AGE', 'SAFETY_EQUIPMENT', 'AIRBAG_DEPLOYED',
       'EJECTION', 'INJURY_CLASSIFICATION', 'DRIVER_ACTION', 'DRIVER_VISION',
       'PHYSICAL_CONDITION', 'BAC_RESULT', 'DAMAGE_CATEGORY', 'DAMAGE',
       'POSTED_SPEED_LIMIT', 'TRAFFIC_CONTROL_DEVICE', 'DEVICE_CONDITION',
       'WEATHER_CONDITION', 'LIGHTING_CONDITION', 'FIRST_CRASH_TYPE',
       'TRAFFICWAY_TYPE', 'ALIGNMENT', 'ROADWAY_SURFACE_COND', 'ROAD_DEFECT',
       'REPORT_TYPE', 'CRASH_TYPE', 'DATE_POLICE_NOTIFIED',
       'PRIM_CONTRIBUTORY_CAUSE', 'SEC_CONTRIBUTORY_CAUSE', 'STREET_NO',
       'STREET_DIRECTION', 'STREET_NAME', 'BEAT_OF_OCCURRENCE', 'NUM_UNITS',
       'MOST_SEVERE_INJURY', 'INJURIES_TOTAL', 'INJURIES_FATAL',
       'INJURIES_INCAPACITATING', 'INJURIES_NON_INCAPACITATING',
       'INJURIES_REPORTED_NOT_EVIDENT', 'INJURIES_NO_INDICATION',
       'INJURIES_UNKNOWN', 'CRASH_HOUR', 'CRASH_DAY_OF_WEEK', 'CRASH_MONTH',
       'LATITUDE', 'LONGITUDE', 'LOCATION', 'UNIT_TYPE', 'MAKE', 'MODEL',
       'LIC_PLATE_STATE', 'VEHICLE_YEAR', 'VEHICLE_DEFECT', 'VEHICLE_TYPE',
       'VEHICLE_USE', 'TRAVEL_DIRECTION', 'MANEUVER', 'OCCUPANT_CNT',
       'FIRST_CONTACT_POINT'
```


> Fact Table
> 0. damage
> 	1. 'DAMAGE_CATEGORY', 'DAMAGE',

> Trying to match dimensional attributes based on features
> 1. date
> 	1. 'CRASH_HOUR', 'CRASH_DAY_OF_WEEK', 'CRASH_MONTH', 'DATE_POLICE_NOTIFIED',
> 2. place
> 	1. 'STREET_NO',
       'STREET_DIRECTION', 'STREET_NAME', 'BEAT_OF_OCCURRENCE',  'LATITUDE', 'LONGITUDE', 'LOCATION', 
> 3. vehicle
> 	1. 'VEHICLE_ID' UNIT_TYPE', 'MAKE', 'MODEL',
       'LIC_PLATE_STATE', 'VEHICLE_YEAR', 'VEHICLE_DEFECT', 'VEHICLE_TYPE',
       'VEHICLE_USE', 'TRAVEL_DIRECTION', 'MANEUVER', 'OCCUPANT_CNT',
       'FIRST_CONTACT_POINT'
> 4. crash
> 	1. 'RD_NO', 'CRASH_TYPE', 'REPORT_TYPE', 'NUM_UNITS', 'FIRST_CRASH_TYPE'
> 5. person
> 	1. 'PERSON_ID', 'PERSON_TYPE', 'CITY',
       'STATE', 'SEX', 'AGE',
> 6. weather
> 	1.  'WEATHER_CONDITION', 'LIGHTING_CONDITION', 'ROADWAY_SURFACE_COND',
> 7. cause
> 	1. 'PRIM_CONTRIBUTORY_CAUSE', 'SEC_CONTRIBUTORY_CAUSE',
> 8. injuries
> 	1. 'MOST_SEVERE_INJURY', 'INJURIES_TOTAL', 'INJURIES_FATAL',       'INJURIES_INCAPACITATING', 'INJURIES_NON_INCAPACITATING',       'INJURIES_REPORTED_NOT_EVIDENT', 'INJURIES_NO_INDICATION',       'INJURIES_UNKNOWN', 'INJURY_CLASSIFICATION'     
> 9. road_condition
> 	1. 'POSTED_SPEED_LIMIT', 'TRAFFIC_CONTROL_DEVICE', 'DEVICE_CONDITION',  'ROAD_DEFECT',  'TRAFFICWAY_TYPE', 'ALIGNMENT'
> 10. safety
> 	1. 'SAFETY_EQUIPMENT', 'AIRBAG_DEPLOYED',
	   'EJECTION', , 'DRIVER_ACTION', 'DRIVER_VISION',
	   'PHYSICAL_CONDITION', 'BAC_RESULT', 
   
   
> Updated the schema on [dbdiagram](https://dbdiagram.io/d/LDS_DW-673b86e6e9daa85acade542a)

*Step 5. Identify the Dimensional Attribute Hierarchies*
Attribute hierarchies is a natural way to support interactive exploration of facts.

Users understand them intuitively, because they are used to look at a summarized report and then to decide to look at a more detailed one.


## 19/11

A feasible and interesting idea to integrate data from chicago data portal:
1. import beat boundaries
2. import [crimes](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2/about_data) in the date range
3. add number of crimes (and type?) for each beat
	1. maybe classify the beats as dangerous gives a threshold

Also
1. add holidays in date


## 20/11

Crucial information from chatgpt.





