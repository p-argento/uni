Prof. Pansanella
[Sharepoint](https://unipiit.sharepoint.com/sites/a__td_65002/_layouts/15/SeeAll.aspx?Page=%2Fsites%2Fa__td_65002%2FSitePages%2FClassHome.aspx&InstanceId=00000000-0000-0000-0000-000000000007)
[[DDAM Lectures]]

if you want, on sobigdata academy there is an interactive part with quizzes.

*Interactive lesson next time*
Do sobigdata quizzes.
Do exercises with lambda functions.
Try all the exercises in the notebook.
Read pyspark docs.

## Syllabus
1. Introduction to Distributed Computing and PySpark
2. Map-reduce paradigm
3. Spark basics and RDDs
4. Data Processing with PySpark: Dataframes and SQL
5. Machine learning with PySpark


## ML with pyspark

We use pipelines, that are concatenation of tranformers and estimators.

The imputer is the transformer handled by spark.
We use the class `Imputer` making an instance with inputCols and outputCols. Then `imputer.fit(df)`, meaning that it will take data from the cols in the instance defined (the default for the imputer is the average). Then `model.tranform(df)`, that will do the work and generate the output.

The advantage is that it can be used with pipelines.

Practically all the algos in spark work with numbers, so when you have strings you need to use indexes that maintain the information. Use `stringIndexer`.

A sparse vector is used to save space. Only non-zero positions are stored, the other are zero by default. It is a dict od `{pos:value}`. The one-hot encoding is stored as a sparse vector.

## Project Ideas

There are 3 main tasks
1. fraud detection
2. customer segmentation
3. geospatial analysis

In Geospatial Analysis
1. speed filtering
	1. for offline transactions, see if the speed in the customer trajectory is reasonable
2. outlier detection
	1. using Isolation Forest or Local Outlier Factor (LOF), to understand the points that differ from usual behaviour
3. segment customers who frequently transact in different regions (e.g., frequent travelers), based on home location







