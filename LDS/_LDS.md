[LDS Didawiki](http://didawiki.di.unipi.it/doku.php/mds/lbi/start)

## Important Notes
*14/11*
Open
- SQL Server Management Studio
- Visual Studio with SSIS

Exercise
1. search for "oledb source" in toolbox.
	1. select the connection
	2. create the empty temporary table with only the name
2. populate the table
	1. we want the distinct names from the source
		1. to obtain it, we use the node "sort", selecting the tick "remove rows with duplicates"
3. we want a workflow that adds a customer only when it is not present
	1. we need the node "lookup" to update when there is no match
	2. how? we connect to lbi and select 2024_customer

What happens if we change one value and run the workflow?
```
update[dbo].[2024_customer]
set customer='Anna'
where surrogate_key=1
```

When we want to a new task, we go in control flow.
> Is data flow the more detailed sequence of tasks for the bigger tasks?

What do we need to do?
The final result should be a table with distinct customer (?)
Steps
1. read table sales_description
	1. sales_description is a view and cannot be updated
	2. connect oledb in foodmart
2. do lookup in the new table with surrogate key
	1. we want to capture the matching
	2. lookup ("ricerca in italiano") on 2024_customer in lbi
		1. in "columns" connect the customer left-to-right
		2. in "general" specify behavior if no matching error
			1. reason on that, it is a failure, so we select error
3. construct the file
	1. node "destination file flat"
		1. select "output corrispondenza ricerca"
	2. we create a file "SK_table_customer"
	3. we can select only the columns that we want
		1. "ricerca.customer" has no mapping, but we do not need it, so we can eliminate it

We run the entire control flow.

Exercise.
REPLICATE THE SAME PROCESS ALSO FOR PRODUCT NAME.

1. create product table update
2. same surrogate key
	1. remember the auto-incremement in the surrogate key
3. change the first column with instead of nvarchar, go into product table and see the size and type of product name
	1. go in table dbo.product
	2. see that it is nvarchar(255)
















*13/11*
If a question in the project gives a result that is empty or it is nonsense, it still may be correct. The process is what should be correct.
For any question, look at the data and understand if you are really capturing what data is telling. Look at the data and the relations between data, if you miss something there, the problem may be incorrect.
You can try with Pandas and simple SQL the queries you are doing with SSIS to verify if they are correct.

First test in a smaller database, where you can check correctness. Then, go into production.

You are optimizing the data to be explored by a human, not to train a model.

HINT:
To create the schema, do not confuse "damage to user" and "people".
Look at the keys, for understanding the relationship. Capture the dependecies.
The key is not just one value, you have to process this data.
The simplest way is to look at feature names that are similar or the same.
Please, check again the relationship, I am sure you are missing something.

LET'S MOVE TO SSIS.
We create a package for the stratified sampling.
We want to maintain the proportion of the gender attribute.

> Do not use Views, do all work in SSIS

Start from lbi database, do a stratified sampling of 30%.

Use the data flow task node.
1. The first node is OLEDB Source, it should be configurated. 
2. Second, split the data by gender ("suddivisione condizionale").
3. "Campionamento percentuale"
	1. select the output (there is always a default)
	2. you can rename nodes
	3. change the percentage of rows
4. we need to write the result in a file
	1. we have two branches (each one representing an SQL query)
	2. we use "Unione input multipli" to create the final result
		1. no need to sort (differently from "Unione")
5. in the end, we create a file "sampling.txt"
	1. change the language to english
	2. remember to check if the mapping is correct


WHAT IS A SURROGATE KEY?
When you have a snowflake schema, like in foodmart.
Every time a new customer do a purchase, a record is created.
What if the customer change the address, but I want to keep the history? If I change it, I will loose the old information. 
A surrogate key will be valid for every new values. We need an ETL process. We are reading every night from the operational database. What if there is a change? We need to capture the change in the operational database. Do I need a completely new customer with a new city or keep the historical changes with the same customer?

Let's create a workflow with the creation of a surrogate key.

We simulate the scenario where we simulate a new surrogate key for every customer.
(it is the lab exercise in slide 31)
Remember that first you prepare the tables, then update.
When you read a record, you check that the customer exists in the dimensional table (NOT the customer table in foodmart, because it will be there for sure).
We should generate a table to understand distinct customers, let's call it customer_dim, use the tool.
Where do I need to create a table? Go in lbi>Tables>Create New Table.
How is the table composed? Customer_name, surrogate_key.
When creating the table, be sure that the size is compatible
In the Views>Design, you can see the query and the dimensions.
So, we set the size of 100+50+1 for the customer name and surname (do not forget the +1 for the space).
The second attribute is the surrogate_key, of type int.

If we have two different clients running in parallel, the counter that generates the keys can generate the same key at the same time for different values.
Generating the key on the client side is dangerous, so we set up the auto-increment of the key on the server side.
In the new table > increment key (button somewhere).




*6/11*
WATCH LECTURE





*30-10*
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



In SSIS, open a new project and on the right go to "SSIS Packages" to build an ETL process. Is the .dtsx file, it is like a 
Only one project containing different packages?
Each .dtsx is a dataflow (?).
> How many packages do we need to create for the project?

If you open the file of the professor, you get an error because you cannot open it, but you can still read it. 
...
You can create nodes, and then use the toolbox on the left to add tools.
Double click on the node if there is a problem, for example in OLEDB node you need to configure the connection.

Use the blue arrow to link the nodes.

Remember to change the path. NOT the computer, but the connection to the server. Use "English (USA)" local settings.

Configurate both the connection manager and the mappings.
Check that all the inputs are associated with an output.
Drag&Drop if needed.

> In the project.
> In assignment 1, you can use pandas and whatever you want but you CANNOT modify the file.
> From Assignment 2 on, you can modify the data, but you CANNOT use pandas.


Use "encription: optional" in the login Management Studio.






*29-10*
Remember, the sql tool is called "odbc origini dati 64bit".

Pandas is allowed only for the first part of the project.
> Try the exercise of customers also without using pandas!

When opening files, use `open("filename.csv",mode='r', encoding='utf-8-sig')`
Use the csv package for `csv.DictReader`. It will create a list of dictionaries. It means that every row is a dictionary!
> Be sure to understand how a dictionary works.

Remember that when you read a file everthing is a file, but we might need to convert it into a int. Pandas do this for you.

Remember that when working on data, you need to keep only the data you need, and use less loops as possible. But, before knowing the business questions, during cleaning and transformation, you keep all the data. 

> EXAM QUESTION: Can you implement a join in python (using dictionaries)? 

> Look at dictionary comprehehnsion

REMEMBER WHEN WRITING CODE
1. use functions for modularity
2. think about exceptions
	1. to avoid problem before production

When scanning tables, use `break` if you find what you looked for, in order to speed up the code.









*24-10*

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


*23-10-24*
> Microsoft sucks

everytime you want to connect, you need the driver installed.
Install odbc driver 17 for sqlserver 

To connect when you are not in the unipi network, you need to use the vpn.

How to set up the connection to the server?
1. Searc in windows bar "origini dei dati 64 bit"
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

*tomorrow*
in the first hour, pellungrini willl teach. We will start from the query with params.
We also present the projects and explain the different tasks.
See the test published. The credentials will be sent. 


## Exam
Ruggieri first. Then Monreale. Write it in the notes on valutami.
Better oral exam with the group.

## Project
Write the name in the spreadsheet.
Database release in mid-october.
First deadline beginning december.
Second (and last) deadline December 27.

Be prepared to download a VM of 60GB to use MS on Mac.
*is there an open source source to do ALL these tasks?*

You can use spyder, pycharm (I suggest you NOT to use jupyter, because it is better to be efficient, using functions and cleaning data once).
DO NOT use duplicated code for each code, I DO NOT want to see copy and paste. Use functions to reduce the number of lines of code. Image that the professor is another developer that wants to run your code. Add comments in every part of the code.

Do the exercises in the slides about python. You will be evaluated in the efficiency of the code.

Use exceptions !! and handle them.

Do all exercises.
Try the VPN.
Install management studio.







