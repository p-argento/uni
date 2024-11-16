*14/11*
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


*16/11*
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



