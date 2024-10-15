*Outline*
First part: 
❏ Lesson 1 - 18/09/2024: course introduction  
❏ Lesson 2 - 25/09/2024: parallel and distributed computing  ❏ Lesson 3 - 27/09/2024: map + reduce paradigm
❏ Lesson 4 - 2/10/2024: spark basics (RDDs)
❏ Lesson 5 - 4/10/2024: laboratory on RDDs
❏ Lesson 6 - 9/10/2024: dataframe API
❏ Lesson 7 - 11/10/2024: laboratory on DataFrames 
❏ Lesson 8 - 16/10/2024: spark SQL
❏ Lesson 9 - 18/10/2024: laboratory on sparkSQL
❏ Lesson 10 - 23/10/2024: Machine learning on RDDs 
❏ Lesson 11 - 25/10/2024: Project guidelines + laboratory on MLlib (RDD)
❏ Lesson 12 - 27/10/2024: Machine learning on DFs
❏ Lesson 13 - 30/10/2024: laboratory on MLlib (DataFrames)

# 1. Distributed Computing and Hadoop
25/09/24

*outline*
1. Difference between Parallel and Distributed Computing
2. The typical Distributed computing issues
3. What is Hadoop
4. How Map-Reduce works
5. How HDFS works
6. Limitations of Hadoop
7. The main difference between Hadoop and Spark

The 3 issues of Distributed Computing are
1. Communication
	1. process of exchanging data between different parts of a system
2. Synchronization
	1. meaning coordination of processes
3. Fault Tolerance
	1. ability of a system to continue operating correctly in the event of failure of one or more of its components, preventing complete system failure

Hadoop is an open-source software framework that solves the issues of distributed computing.
Observe that
1. Hadoop Map-Reduce is the part of Hadoop taking care of the computing
2. Hadoop Distributed File System (HDFS) is the primary storage system used to manage large amounts of data in a distributed environment

![[Pasted image 20241013155951.png|300]]

## Hadoop Map-Reduce
Key-value pairs form the basic data structure in MapReduce.
Keys and values may be primitives like integers, but also complex structures like lists.
For example, in a collection of web pages, keys may be URLSs and values mays be the actual HTML content.

![[Pasted image 20241013160823.png]]

The steps are
1. input splitting
	1. input split into smaller subsets
	2. represented in a `<key,value>` form
	3. key is the identifier  and value is the actual data
	4. this is done automatically by Hadoop
2. map function
	1. takes an input key-value pair
	2. produces one or more key-value pairs
	3. transforms and categorize the input data into a set of intermediate data
	4. if necessary, it changes the key -> *why?*
	5. this function is defined by the user
3. shuffling and sorting
	1. the key-value pairs having the same key are grouped together
	2. grouped pairs are sent to the same reducer in the form `<key,list of values>`
	3. this is done automatically by Hadoop
4. reduce function
	1. processes each unique key and its associated list of values
	2. merges the values to produce a single or smaller set of output values
	3. this function is defined by the user to take in input the `<key,list of values>`

?? The output, which is not handled by Hadoop, is considered an external process, ie merge the results into a single one.

Note that the user is NOT in control
1. of the distribution of the computation among the various nodes, that are machines and processors
2. of the storing of data, which is managed by HDFS, reducing communications to the minimum 

![[Pasted image 20241013160927.png]]

*Word Count Example*

![[Pasted image 20241013163115.png]]

The initial text is split into lines (keys are missing because they are not relevant, they can be the number of the line). The map function returns for each line a set of <key,values> having as a key a single word and as value 1 (not the count, but the constant number 1). The shuffling put together all the pairs having the same key, a.k.a. the same word creating a list of 1s for them. The reduce function sums all the 1s, obtaining the count for a specific word. The final output is the merge of the various counts.

![[Pasted image 20241013163239.png]]
(the doc is a line of the document)

Notice that the reduce function is sure that it is counting the global count for a specific key, a.k.a. a word, because the shuffling grouped them in the whole system, and so no occurrence of a specific word can be processed by another one.

*Iterative Message Passing Example*
...
*Grocery Store Baskets Example*
...
*MapReduce++*
It is a new version of MapReduce with 2 additional, but optional, steps
1. combiner
2. partitioner


## Hadoop HDFS
Hadoop Distributed File System (HDFS) is the primary storage system used to manage large amounts of data in a distributed environment.

This is almost invisible to the users and it is automatically managed by Hadoop. For the user, HDFS is the same filesystem as the one on your personal computer.

Basics concepts
1. data blocks
	1. files in HDFS are broken down into smaller fixed-sized blocks (typically 128 or 256 MB) to be stored across different nodes of the cluster
2. replication and fault tolerance
	1. to ensure reliability and fault tolerance, each data block in HDFS is replicated across multiple nodes (default replication factor of 3)
3. scalability
	1. HDFS is built to scale horizontally, meaning that more storage capacity and processing power can be added simply by adding more Data-Nodes to the cluster
4. write once, read many
	1. data is written once and read many times
5. node types
	1. NameNode (or Master Node)
		1. central component of HDFS and acts as the master server
		2. manages metadata for the file system, including directory structure, file permissions, mapping of file blocks to DataNodes
		3. it keeps track of where all the blocks of a file are located
	2. DataNode (or Slave Node)
		1. worker nodes in HDFS
		2. store the actual data blocks and are resposible for serving read and write requests from clients
		3. DataNodes periodically report the status of the block they store the NameNode

![[Pasted image 20241013170544.png|400]]

For the user, HDFS appears to be the same filesystem as the one in your personal computer, but behind the scenes, the operations of READ and WRITE a file trigger the following sequences of actions.

![[Pasted image 20241013171214.png]]

*HDFS: write*
1. client request to NameNode
	1. the client begins the write process by contacting the NameNode to create a new file in the HDFS namespace
	2. the HDFS sends a list of locations where to write, including the replicas, to be safe in case of a disk fault
3. client initiates Data Writing
	1. the client splits the file into blocks
	2. begins writing these packets sequentially
4. Data Acknowledgement (ie "riconoscimento o conferma")
	1. the DataNodes acknowledge the correct writing of the block
	2. the NameNode updates the metadata with the location of the blocks

*HDFS: read*
1. client request to NameNode
	1.  the client initiates the read request by contacting the NameNode
	2. the client asks for the metadata of the file it wants to read, it includes information about the blocks that make up the file and the DataNodes that store these blocks
2. client contacts DataNode
	1. using the information received from the NameNode, the client directly contacts the first DataNode
	2. the client then reads the block of data from this DataNode
	3. if the DataNode does not answer (eg fault), it will use one of the replicas
3. sequential reading
	1. the clients continues to read each subsequent block from the appropriate DataNode until the end of the file

Note that the actual WRITE and READ are done directly between the Client and the NameNodes without passing through the NameNode to avoid bottlenecks.


## The Pitfalls of Hadoop

Not all problems are suitable for Hadoop.
The reasons are
1. latency and real-time processing
2. complexity of the programming model
3. fixed data flow
4. limited support for interactive and ad-hoc queries

Hadoop vs Spark
...


![[Pasted image 20241013172615.png]]

Problems
1. cumbersome setup and management
2. steep learning curve
3. declining relevance in the cloud era

Summary of limitations
1. security problem
2. ease of use
3. no iterative processing
4. no real time processing
5. slow processing speed
6. small file concerns

Alternative solutions.
One of the most promising alternatives to Hadoop is Databricks, a unified analytics platform built on top of Apache Spark. It provides a fully managed, cloud-based platform for big data processing and analytics, eliminating the need for complex setup and management.

Key benefits of Databricks and Apache Spark include
1. faster processing
2. easier development
3. unified platform


# 2. Spark RDD Basics
27/09/24

Apache Spark is an open-source distributed computing system.
In python, it is imported as a library and content is generated to give users access to its primitives.

![[Pasted image 20241013183043.png|350]]

## Iterative algorithms
There is an important class of applications, including K-Means, that reuse intermediate results. It is common in iterative machinel learning algorithms and interactive data mining. In MapReduce, the only way to reuse data is to write it to an external stable storage system, eg a distributed file system.

We need a new data structure that is suitable for in-memory computation, but still ensuring fault tolerance without the data replication we have in Hadoop. Spark developers proposed the Resilient Distributed Dataset (RDD).

## Resilient Distributed Dataset (RDD)

A RDD is a fundamental data structure in Apache Spark. It is
1. fault-tolerant
2. distributed/parallel
3. let users explicitly persist intermediate results in memory
4. let users control their partitioning to optimize data placement and manipulate them using a rich set of operators

RDDs 
1. represents an immutable distributed collection of objects
2. is the result of the work done by HDFS to distribute the data across the nodes
3. can be seen as a special kind of list where each item can be of any type or structure we need.

*Characteristics of RDDs*
1. IMMUTABILITY
	1. RDDs are read only, once created they cannot be modified
	2. if you want to change an RDD, you create a new one based on the on the original one with something modified
	3. this allows to reconstruct data in case of a node failure
2. LINEAGE INFORMATION
	1. RDDs keep track of the sequence of information that were used to build them
	2. it is recorded as a directed acyclic graph for each RDD
	3. when a partition of a RDD is lost due to a node failure, Spark can recompute that partition by following the lineage from the original data source, enabling data recovery
3. DATA REPLICATION
	1. for certain types of RDDs, like those created from HDFS data, Spark can leverage the redundant copies available on other nothes
4. CHECKPOINTING
	1. users can explicitly request checkpointing of RDDs
	2. it involves saving the RDDs data to a reliable distributed file system (like HDFS or Amazon S3)
	3. this provides an additional level of fault tolerance by reducing the amount of data that needs to be computed in case of node failures
	4. note that checkpointing is a costly operation in terms of performance and storage, so it should be used judiciously

![[Pasted image 20241015143310.png]]

*Transformations and actions*

Transformations
1. are primitives that create a new RDD from an existing one
2. they are evaluated lazily
	1. meaning that first a sequence of primitives is planned, and not executed immediatly
	2. it will postpone the evaluation until it is absolutely needed
3. new RDDs are produced, since RDDs are immutable

Actions
1. are primitives that trigger the execution of the transformations required to compute the result
2. produce a value back to the user or write data to an external storage system

![[Pasted image 20241015151159.png]]

## PySpark

We usually work in a notebook.

First we create a context to be used for the creation of RDD, Transformations and Actions. `SparkContext` is the primitive to be used, it takes as input the name of the application and where the master machine is using all the possible cores. 
Only one SparkContext should be active per JVM. You must stop() the active SparkContext before creating a new one.

```python
from pyspark import SparkContext
sc = SparkContext(appName="MY-APP-NAME", master="local[*]")
print("done")
```

*Creating an RDD*
To create an RDD, use the primitive `parallelize`.
1. it moves data from the local memory to the distributed storage
2. it triggers the HDFS operations of distributions
3. the data we move must be a list
4. the RDD does NOT contain the actual data, but a reference to the RDD because data is distributed

```python
numbers = [1,2,3,4,5]
rdd_numbers = sc.parallelize(numbers) 
print(numbers)
print(rdd_numbers)
```

The RDD is designed to be very long (bilion of positions), but with small data on each item, it will be optimized by Spark over the nodes.

There is a primitive called `TextFile` that we can invoke over the spark context sc, it reads a local file and creates an RDD by putting in each position of the list a line of text automatically.

```python
shakespeare_rdd = sc.textFile("comedies.txt") 
print(shakespeare_rdd)
```

## Actions
Actions
1. are primitives that trigger the execution of the transformations required to compute the result
2. produce a value back to the user or write data to an external storage system

They are
1. `rdd.collect()`
	1. the opposite of parallelize
	2. it gets the data back from the distributed store
	3. WARNING! you can kill the machine if you collect big data
2. reduce
	1. one of the most important actions
	2. it aggregates the elements of an RDD by applying a binary function f(a,b)
	3. the function f(a,b) is usually a lambda function that should be both commutative and associative, because spark decides the order of the elements according to availability of data
	4. for example `numbers.reduce(lambda x, y: x + y)`
3. first
	1. returns the first element of the rdd
	2. used to understand the format and content
4. take (n)
	1. retrieves the first n elements from the rdd
5. TakeOrdered
	1. returns the smallest or largest elements in sorted order
6. TakeSample
	1. returns a random sample, with or without replacement
7. Distinct
	1. returns a new rdd with the distinct values



## Trasformations
Transformations
1. are primitives that create a new RDD from an existing one
2. they are evaluated lazily
	1. meaning that first a sequence of primitives is planned, and not executed immediatly
	2. it will postpone the evaluation until it is absolutely needed
3. new RDDs are produced, since RDDs are immutable

Some transformations are
1. filter
	1. returns a new rdd that contains only those elements that satisfy the specified condition
2. map
3. flatMap
4. sortBy
5. union
6. intersection
7. keyBy
8. groupByKey
9. reduceByKey
10. Join


*example of most frequent words USING RDD*
to compute the 10 most frequent words in a text, stored in comedies.txt, we have to: 
1. read the file as an RDD using SparkContext.textFile()
2. split the text into single words by any non-word character
3. filtering out empty words
4. create key, value pairs of (word,1)
5. sum by key
6. sort by value
7. take the first 10 words

```python
import re from pyspark 
import SparkContext 
sc = SparkContext(appName="MY-APP-NAME", master="local[*]") 
rdd = sc.textFile('/content/sample_data/comedies.txt') 
split = rdd.flatMap(lambda line: re.split('\W+', line)) 
split_nonempty = split.filter(lambda word: word != "") 
words = split_nonempty.map(lambda word: (word, 1)) 
word_count = words.reduceByKey(lambda a, b: a + b) 
top_words = word_count.takeOrdered(10, key=lambda x: -x[1]) 
print(top_words)
```




# 3. (LAB)




# 4. Dataframes
04/10/24

This lesson is about
1. spark dataframes
2. basic operations on data frames
	1. data cleaning, preparation and exploration, pipeline with examples
3. machine learning with pyspark
	1. with MLib dataframe-based
4. machine learning pipeline
	1. with unsupervised and supervised learning

## Spark DataFrames

A dataframe is a distribution of data organized into named columns, It is a powerful abstraction for distributed and structured data.
It is similar
1. to a pandas dataframe in python, but is distributed in the cluster
2. to a SQL table

Key advantages
1. easier to understand
2. optimized for complicated operations

Advantages of DFs over RDDs
1. optimization
	1. schema information enables query optimization and predicate pushdown
2. ease of use
	1. high level of abstraction similar to pandas
3. interoperability
	1. easily interoperate with various data sources and converted to Pandas dataframes
4. integration
	1. integrated with spark ecosystem, eg spark sql or spark MLlib

*example of most frequent words USING DF*

You can transform an RDD into a dataframe using the function `.toDF()` if the RDD is an `RDD[Row]`.

1. map each line of text to be a Row object
2. create a dataframe with a single column "line"
3. split each line into words based on any non-word character and explode the resulting list into separate rows renaming the col "word"
4. filter out empty words
5. group by the word columns and count occurrences
6. order by the count column in descending order
7. limit the result to the 10 most frequent words

```python
from pyspark.sql import SparkSession 
from pyspark.sql import Row 
from pyspark.sql.functions import explode, split, col 
spark = SparkSession.builder.appName("WordCount").getOrCreate() 
rdd_rows = rdd.map(lambda line: Row(line)) 
df = rdd_rows.toDF(('line',)) 
words_df = df.select(explode(split(col("line"), r"\W+")).alias("word")) 
words_df = words_df.filter(words_df.word != "") 
word_count_df = words_df.groupBy("word").count() 
top_words_df = word_count_df.orderBy(col("count").desc()).limit(10) top_words_df.show()
```


## Spark Context vs Spark Session

What is SparkContext
1. Core Entry Point
	1. SparkContext is the original entry point for Spark functionality
	2. it allows interaction with Spark's cluster, RDDs and low-level APIs
2. RDD focused
	1. primarly used for creating and managing RDDs, which are distributed collections of objects

What is SparkSession?
1. Unified Entry Point
	1. introduced in Spark 2.0
	2. provides a single point of entry to all Spark functionalities, incuding working with dataframes and sql (it was previously split across multiple contexts)
2. Higher-level APIs
	1. emphasizes Dataframe and Dataset APIs, which are optimized and easier to use than RDDs

When we use the DataFrame API, we use SparkSession!

![[Pasted image 20241015181827.png]]

## RDDs vs DataFrames

![[Pasted image 20241015183046.png]]

## Creating a DataFrame

Many different ways
1. from RDDs (more common?)
	1. using `.toDF()`
	2. eg `df = rdd_rows.toDF(('line',))`
2. from RDDs (alternative)
	1. using `pyspark.sql.SparkSession.createDataFrame(data,schema,samplingRatio,verifySchema)`
	2. the schema can be inferred or specified
3. from iterables
	1. using `pyspark.sql.SparkSession.createDataFrame(data,schema,samplingRatio,verifySchema)`
4. from Spark Data Sources

*1. Creating a DF from RDDs using .toDF()*
See example of most frequent words

*2a. Creating a DF from RDDs inferring the schema*
The RDD has to be of any kind of SQL data representation (row, tuple, int, boolean)
1. create suitable RDD
	1. skipping the first row of the file (header)
2. pass the RDD as it is to the createDataFrame function


```python
lines = sc.textFile(‘people.csv’)
header = lines.first() 
lines_without_header = lines.filter(lambda line: line != header) 
parts = lines_without_header.map(lambda l: l.split(','))
people = parts.map(lambda p: Row(p[0], p[1])) 
peopledf = spark.createDataFrame(people)
peopledf.show()
peopledf.printSchema()
```

How to print?
Use the function `df.printSchema()` to obtain information about the inferred schema.
> will it be printed correctly??

To sum up
1. have an `RDD[Row]`
	1. if you want the schema to be correct, assign a name to each element of the Row and cast the elements to the correct data type
2. use createDataFrame(RDD) to create the DataFrame


*2b. Creating a DF from RDDs specifying the schema*
We can define a schema using StructType() which consists of a list of StructField. Each StructField specifies
1. name of the field
2. data type
3. whether the field can be none or not

[Comprehensive list of all types](https://spark.apache.org/docs/late st/sql-ref-datatypes.html)

```python
from pyspark.sql.types import *
schema = StructType(
					[StructField("name", StringType(), True), 
					StructField("age", IntegerType(), True)])
```

A schema can also be defined as a DDL formatted string `"column_name: data_type"`
1. eg `schema = “name: string, age: int”`

Once the schema has been defined, the DataFrame can be created passing the schema with `createDataFrame(rdd, schema)`


*3. Creating a DF from RDDs inferring the schema*


## DataFrame basic operations tutorial

1. select
2. filter
3. groupby
4. aggregations (sum, avg, ...)
5. sort
6. alias
7. distinct
8. drop
9. withcolumn
10. join


## Machine Learning with Spark

Important things...


ML Pipeline with classification

1. load (create a dataframe)
2. train-test split
3. training (.fit())
4. prediction (.transform())
5. evaluation

Clustering
(no train-test split)












# 5. (LAB)
















