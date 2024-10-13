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


## More on Hadoop
Some facts on Hadoop

Not all problems are suitable for Hadoop.
The reasons are
1. latency and real-time processing
2. complexity of the programming model
3. fixed data flow
4. limited support for interactive and ad-hoc queries

Hadoop vs Spark
1. Hadoop


![[Pasted image 20241013172615.png]]





# 2. Spark RDD Basics
27/09/24





# 3. (LAB)




# 4. Dataframes
04/10/24





# 5. (LAB)
















