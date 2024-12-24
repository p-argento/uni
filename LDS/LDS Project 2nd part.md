[Google Doc with Server Logs](https://docs.google.com/document/d/1jRtPixDMGV7qE6ob_1iVFkb5yuY8RICmUtpvUlNvrlA/edit?pli=1&tab=t.0)

## 20-12

*PYODBC*

Best practices
1. when opening files, use `open("filename.csv",mode='r', encoding='utf-8-sig')`
2. use the csv package for `csv.DictReader`, it will create a list of dictionaries. It means that every row is a dictionary!
3. when working on data, you need to keep only the data you need, and use less loops as possible
4. when scanning tables, use `break` if you find what you looked for, in order to speed up the code
5. during cleaning and transformation, you keep all the data (before knowing the business questions)
6. use functions for modularity
7.  think about exceptions to avoid problem before production

Maybe ignore maybe not
1. ?? "ORDER BY newid()" can be used to add randomness in the data.
2. ![[Pasted image 20241220183853.png]]

New ideas 
1. improve columns
	1. aggregate address data
2. define the data staging area with the joined table, with intermediate, partially processed data




*SSIS*

Recall the ETL.

-> Extract:
1. access data sources (Local, distributed, file format, connectivity standards)

-> Tranform:
1. Selecting data  n remove unnecessary, duplicated, corrupted, out of limits (ex., age=999) rows and columns, sampling, dimensionality reduction 
2. Missing data  n fill with default, average, filter out 
3. Coding and normalizing  n to resolve format (ex., CSV, ARFF), measurement units (ex., meters vs inches), codes (ex., person id), times and dates, min-max norm, ... 
4. Attribute Splitting/merging  n of attributes (ex., address vs street+city+country) 
5. Managing surrogate key  n generation and lookup 
6. Aggregating data  n At a different granularity. Ex., grain “orders” (id, qty, price) vs grain“customer” (id, no. orders, amount), discretization into bins, ...  
7. Deriving calculated attributes  n Ex., margin = sales – costs 
8. Resolving inconsistencies – record linkage  n Ex., Dip. Informatica Via Buonarroti 2 is (?) Dip. Informatica Largo B. Pontecorvo 3 
9. Data merging-purging  n from two or more sources (ex., sales database, stock database)

-> Load:
1. Data staging area 
	1. Area containing intermediate, temporary, partially processed data
2. Types of loading: 
	1. Initial load (of the datawarehouse)
	2. Incremental load 
		1. Types of updates: append, destructive merge, constructive merge 
	3. Full refresh

> Remember to upload (and update) the dimensions tables first and the fact table later

Be careful with data types (see [data types documentation](https://learn.microsoft.com/en-us/sql/integration-services/data-flow/integration-services-data-types?view=sql-server-ver16&redirectedfrom=MSDN))
1. Data type from sources are mapped into SSIS types  
2. SSIS transformations works on SSIS types 
3. SSIS types are mapped to destination data types

Important
1. check that all the data types are okay (use utf-8 or utf-8-sig)
2. need to set the auto increment of the key server side
	1. for both the fact table and the dimensions?
3. check that in the population of tables in ssis is correct
	1. dimensions first, fact later
	2. does it take care of type 1 and type 2 errror? (see slide on SCD)
4. 







