## 23-10

> Microsoft sucks

everytime you want to connect, you need the driver installed.
Install odbc driver 17 for sqlserver 

To connect when you are not in the unipi network, you need to use the vpn.

How to set up the connection to the server?
1. Search in windows bar "origini dei dati 64 bit"
2. add sql server 17
3. use the credential 
	1. (you decide the name)
	2. server: `lds.di.unipi.it`
	3. select "with sql server authentication using login and password entered by the user"
	4. insert id: `lds` , password: `pisa`
	5. select `lbi` as default database, you can play there
	6. test the data source

Open excel
1. import from other sources
2. select oledb (for vm) or odb
3. expand lbi and in dbo search for census table

In Access
1. external data
2. ...

If you import data, the origin will not be updated. In access, if you create a linked db, you apply changes automatically to the server side.

SQL Server Tools
1. Select
	1. server type: database engine
	2. name: `lds.di.unipi.it`
	3. auth: `sql server authentication` (NO windows auth, otherwise the username of the pc is used)
	4. login with the credentials of the group, you will access the space dedicated to your group
		1. alternatively, use `lds` , `pisa` 

Start working on the project now and upload the server, because the connection is slow. The server is one and you are a lot.
Organize the code so that you do not loose everything. For example, avoid a very big commit.

If you want to test something, use lbi tables. When you create a new table, use the matricola number in the name to avoid to overwrite other people tables, for example "table_600362".

DO NOT create tables in FoodMart, do it in lbi.

Right-click on the db census and select "view first 1000 rows" to open the default query window.

If you get an error, check the database where you are focused on. There is a drop-down menu on the top-left.

Install pyodbc.
Using spyder, check the python script uploaded on didawiki. You can copy and paste the string, it will be always the same.
Use variables so that you can change the composition of the string. Be aware of how to concatenate the strings.

Test the query in the script "SELECT TOP 10 * FROM census" directly on sql query tool using copy and paste. Avoid complicated queries. The server is a shared resource. Remember JOIN is the most expensive operation.

It is better to have a variable "query" and pass the variable to the function `cursor.execute()`.


## 24-10

It is better to do most of the operations locally (even rounding numbers), because we do not know the power of the server. Just get the data from the server.

Remember. The cursor is a pointer to the resources that must be reset (or re-execute the query).

--project
In the report, 5 pages max for each part. We want to see your implementation choices. How you treat null values.
You should try to design the fastest solution for the assignment, but you can describe alternatives in the report.
It should contain the things that it is not possible to understand from the code.
We expect comments on the process on the data.
Describe also if you integrate more data.
A brief summary of the code.
You can use images.

Better modularization means better code.

exercise for next time.
stratified subsampling.
NEXT TIME YOU WILL DO A LOT OF EXERCISES.



## 29-10

Remember, the sql tool is called "odbc origini dati 64bit".

Pandas is allowed only for the first part of the project.
> Try the exercise of customers also without using pandas!

When opening files, use `open("filename.csv",mode='r', encoding='utf-8-sig')`
Use the csv package for `csv.DictReader`. It will create a list of dictionaries. It means that every row is a dictionary!
> Be sure to understand how a dictionary works.

Remember that when you read a file everthing is a file, but we might need to convert it into a int. Pandas do this for you.

Remember that when working on data, you need to keep only the data you need, and use less loops as possible. But, before knowing the business questions, during cleaning and transformation, you keep all the data. 

> Look at dictionary comprehehnsion

REMEMBER WHEN WRITING CODE
1. use functions for modularity
2. think about exceptions to avoid problem before production

When scanning tables, use `break` if you find what you looked for, in order to speed up the code.





## 30-10 (prima parte)

Showing the solution of the stratified sampling.
There are 2 solutions, but avoid the one server-side.

> What is a cursor? What type of object?

You can use the `csv` library for the project.

"ORDER BY newid()" can be used to add randomness in the data.

Showing slides 07

What is a snowflake schema?


In SQL Management Studio (SSMS), we can create a new diagram with a subset of tables. Just right click on the folder "FoodMart"->"Database Diagram"->"New Database Diagram"

To write a query, select "New Query" from right click. Remember to change the schema in the top left.

Use `FROM [FoodMart].[dbo].[customer]` to specify the complete path for the table starting from the database.

In `Server Objects->Linked Server` there are linked servers, see slide 07.12; usually the folder is empty. This means that we can simulate a distributed query.








