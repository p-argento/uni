## What is DBMS
A set of tools, to manage homogeneous sets of structured data.
It is able to deal with
1. huge amounts of data
	1. otherwise it is excel or simpler tool
2. mission critical data
	1. if an organization loose data (or faith into data) it is a real problem
	2. basically it has to keep data reliable
3. shared data
	1. if two people are updating the data in the same moment, it should happen sequentially, not together
4. queries and updates
	1. if it is only for queries, it is not a dbms, but it is a tool for data analysis
	2. queries and updates can happen at the same time

## DBMS vs Data Analysis
They are two different tools
1. OLTP: On-Line Transaction Processing
	1. support everyday activities of the organization
	2. the collection of data is a "database"
		1. managed by a DBMS
2. OLAP: On-Line Analyitical Processing
	1. analysis of collected data to gather information
	2. the collection of data is called "data warehouse"
		1. managed by Decision Support System
Do not confuse them. They are really different.

![[Pasted image 20240220144807.png]]




