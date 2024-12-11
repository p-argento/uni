
[LDS Didawiki](http://didawiki.di.unipi.it/doku.php/mds/lbi/start)

[[My LDS Project Notes]]

> KNOW HOW TO IMPLEMENT A JOIN WITH DICTIONARIES

## Important Notes

*11/12*

(arriving 30 min later)

If you need to display a ratio, is always better to show also the values to compute the ratio as columns.

To retireve the previous mont, you can choose among
1. lag, 
2. prevmember
3. parallelperios

When you do not have any value, you can have null in the report, but we want to avoid null and actually display zero.
You can use two strategies:
1. case when
2. ...

How to shoe the row "All"?
I can use `+ "a set"` to add
Something like
```DMX
with member sales as
case when [Measures].[Store Sales]=null then 0
else [Measures].[Store Sales] end
select
nonempty(([Time].[The Year].[The Year],
[Time].[DayMonthYear].[Quarter], sales)) on columns,
nonempty(([Customer].[Geography].[City]) + {[Customer].[Geography].[All]}
on rows
from [Sales]

```









*4/12*
MDX Queries in SSMS.

Query 10.
```MDX
-- sales and cost for each month (crossjoin)
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
crossjoin([Time].[The Year].[The Year] , [Time].[DayMonthYear].[The Month]) on rows
from [Sales]
```


Query 11.
..


Query 12.
```MDX
-- return the ordered list of stores wrt the total sales
select [Measures].[Store Sales] on columns,
NONEMPTY(order([Store].[Store Id].[Store Id], [Measures].[Store Sales], desc)) on rows
from [Sales]
```

Remeber that the first `[Store Id]` is the hierarchy and the second one is the member ??

Query 13.



In the left panel, there are two tabs: Metadata and Functions.
See the Functions, they are useful.

TIPS
1. ALWAYS START FROM THE QUESTION: WHAT DO I NEED ON COLUMNS AND ROWS?
2. TEST THE QUERY STEP BY STEP.










*3/12*
We introduce MDX.

In FROM the join is not necessary, because we use the cube and the cube should already incorporate the join.

> ORAL EXAM QUESTION: differences between SQL and MDX

In WHERE, we specify the conditions, 

Remember that the entire set of elements defined in the cube is considered as hierarchies, some are flat soma are not flat. (?)

There are a lot of functions that can exploit the tree of hierachies.
Syntax: `[DimensionName].[HierarchyName].[LevelName].[MemberName] `Example: `[Store].[Time].[Quarter].&[Quarter 1]`
Or equivalent.
Syntax: `[DimensionName].[HierarchyName].[Path from root]`
Example: `[Store].[Time]. [All].[2004].[Quarter 1]`

Constructing members.
For example applying a computation to obtain a metric.

OPEN SSMS.
New query > MDX
(DAX is for tables, not cubes)

Query 1.
```MDX
-- total sales
select [Measures].[Store Sales] on columns
from [Sales]
```

Query 2.
```MDX
-- total sales per country in store
select [Measures].[Store Sales] on columns,
NONEMPTY([Store].[Geography].[Sales Country]) on rows
from [Sales]
```

Query 3.
```MDX
-- total sales per south east california
select [Measures].[Store Sales] on columns,
[Store].[Geography].[Sales Country].&[USA].&[South West].&[CA] on rows
from [Sales]
```

`&[USA]` specifies the value and NOT the level!

Query 4.
```MDX
-- total store sales in 1998
select [Measures].[Store Sales] on columns,
[Time].[The Year].&[1998] on rows
from [Sales]
```

This uses the flat hierarchy. But you can use also the DayMonthYear hierarchy.
You should NOT use `WHERE [Time].[The Year].&[1998]` because you loose the labels for the rows.

Query 5.
```MDX
-- total store sales after Jan 1998
select [Measures].[Store Sales] on columns,
[Time].[DayMonthYear].[The Year].&[1998].&[Q1].&[January].lead(1) on rows
from [Sales]
```

Now, we cannot use the flat hierarchy anymore.
Use DayMonthYear and the function `.lead(1)`.
???


Query 6.
```MDX
-- total sales USA for female customers
select [Measures].[Store Sales] on columns,
([Customer].[Geography].[Country].&[USA] , [Customer].[Gender].&[F]) on rows
from [Sales]
```

Query 7.
```MDX
-- total sales and cost for each country and customer gender
select {[Measures].[Store Sales], [Measures].[Store Sales]} on columns,
([Customer].[Geography].[Country], [Customer].[Gender].[Gender]) on rows
from [Sales]
```

With `{}` you create the set ??

Query 8.
```MDX
-- sales and profit in USA and Mexico
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
{[Customer].[Geography].[Country].&[Mexico], [Customer].[Geography].[Country].&[USA]} on rows
from [Sales]
```

With `{}` you create the set ??

Query 9.
```MDX
-- sales and cost for each month (wrong)
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
([Time].[DayMonthYear].[The Year] , [Time].[DayMonthYear].[The Month]) on rows
from [Sales]
```

The operation when we create a tuple is called crossjoin.
You cannot use an hierarchy twice (?).
You need to combine two different hierarchies

```MDX
-- sales and cost for each month (correct)
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
([Time].[The Year].[The Year] , [Time].[DayMonthYear].[The Month]) on rows
from [Sales]
```
















*28/11*
PRESENTATION OF THE PROJECT

The dashboard should be interactive and able to access a db. Use PowerBI.

For delivery, use the university email.

You can choose only 4 of the assignments with `*`.
Answer using MDX, kind of sql language.

> In the project, if there are more rows in a table than the ones in the fact table, probably there is a error.



In SSAS, Cube>Calculations, you can create new 








*27/11*

We create a new dimension. Right-click on Dimensions on the right.
Any time you access the data, what is the finer granularity? The more detailed information that you have? Select "the_date".

Now, on the right we have the "Date View", which is a smaller part of the bigger view. Here, we see the available attributes.
If I drag-and-drop "the_month" to Attributes, then it is a flat hierarchy.
But if I want a multi-level hierarchy?
In the "time_id" the date is already there.

You can click "Browser", to see...

Now, we create the hierarchies in the window in the middle, using drag-and-drop.

In "Attribute Relationship", we can see the functional dependencies.
It looks like we do not have any fd.
You can create a relationship.
But be aware, that the design of the db allows that relationship.

Remember that in Browser you can always see the flat hierarchy, for example using only the months.

After selcting a dimension, for example "the_month". Set "AttributeHierachyVisible" to False to hide a dimension in the Properties windows bottom left. 


You can set up an ordering.
First create the realtionship.
Then, in the properties window.
Use OrderBy=
And OrderBy="Month_of_the_year"
Now, refresh and see the browser.

Now, apply the same for "the_day".
Go in "time_by_day".
If there is the attribute we need, create the relationship first.


Crea calcolo denominato.
```
CASE the_day
WHEN "Monday" THEN 1
WHEN "..." THEN ...
```
Do it for all days of the week.
Now, we move the new column in the Dimension Structure>Attributes.

Of course, you need to create all the dimensions.
> The professor will upload the cube.



NOW WE CREATE A SPECIAL TYPE OF DIMENSION.
Some dimensions are recursive. You can have recursive hierachies.
We a tool to have this possibility.
In FoodMart, we have `product_child_parent` table.
We want to create a "New Relationship" from `sales_fact`.
Select `product_id` as Origin Column and `child`.
It is recursive because a parent has a child and a child has a parent (?).

We can create a new dimension.

...



NOW WE CREATE THE CUBE.

Check on Properties that the AggregateFunction is set to "Sum" or to "Count" in the specific table.

> For tomorrow, import the cube that she uploads and we will do some exercises linking the cube to excel. Then we will start the MDX language.





















*26/11*
Start of OLAP.

Foodmart is a snowflake.

Showing slides on dwandolap. Nothing interesting.
Showing slides on ssas. Let's see.

In Excel you can access the olap cube directly and exploit that.
In microsoft, there are also reporting services, but PowerBI substituted it.

We will need a structure for our code, 3 layers.
1. ROLAP or MOLAP ??
2. MDX, to exploit hierarchies
3. DAX ?

![[Pasted image 20241126095710.png]]

IMPORTANT.
We define the name of the project using the student_id.
We construct the cube 
There is no login and psswrd. We use the HTTP.
The only way to avoid conflicts is to have a different name at server side.

In SSMS.
Select Analysis Services.
There is a string you need to exploit, in order to access server side the cube.
`http://lds.di.unipi.it/olap/msmdpump.dll`

See many cubes. We will create a cube with the same structure.
1. Data Cube
	1. -> Food Mart
2. Data Source View
	1. I create a view on this data
3. Cubes
4. Dimensions
	1. ...
	2. ProductParentChild is a recurrence dimension that we will see.

Create a new Analysis Services Project. USE THE NAME LIKE `Foodmart_cube_studentid_2024`

After creating the connection to access foodmart.
In "Impersonation Information", we will NOT use the windows account credentials, but the HTTP.
Now the connection is ready, and we will create views.

Clicking on the just created view, we can see al the tables.
Right-click on one table and select "Explore Data".

![[Pasted image 20241126103655.png]]

To create a ssis-like derived column, right-click on the table and select "Create Named Calculation". For example, for creating the "customer_name" use `fname + ' ' + lname`.
If you explore the table, you can see the new colum, but everything is at client side.

Remember to paste the string for the HTTP in the Properties window, in Destination>Server










*21/11*

We see the solution of the dissimilarity index exercise.
Remember that the join is the most costly operation we do.
This is the reason why we try to filter out rows at the very beginning, in this case the year.
So, first we look for the year in the other table (stores?) using vlookup, then conditional split to select `the_year==1998`.
Now, we can search the gender in customer with vlookup, then conditional split the gender. We assume that there are only males and female, so we use the condition `gender==M` as condition. If there's other, then we need to add another condition with females.

The goal is to have a derived column with all the variables we need for the final formula.
> see ssis

Be aware of the stores that appear only in one branch or in no one of them.

"Multicast" node is the opposite of the split.
It means take an input and replicate as output.

In order to perform the join, we need a proxy key for every record (fake key), with all 1s on left and right.(?)
You still need to sort (?).

...

We reached the end of the exercise.

Now, see the ex of yesterday.
Every night, we check if the customer is new, etc..
We are dealing with type ? errors.
Our process is quite inefficient, because we need to read the entire customer table every time.
We usually use agents, in the CDC Proceess.
See SQL Server Agents in SQL Management Studio (on the left).
The idea is that we can associate the agent to a table we want to monitor.

First, we create the table and activate the agent.
Then, say to the agent to monitor the table.
```
-- SQL Server agent must be running
EXEC sys.sp_cdc_enable_table
@source_schema = 
...

```

When you activate the agent, in Tables>System Tables you can see the tables that are being listened.

Every night, the agent need to understand if it is a type 1 or type 2 update.
Note that sometimes the agent can have problems on the server side.

If there is a change after the activation of the agent, it automatically generates two rows with the same id  ???

Back in SSIS.
In Control Flow, we add the node "CDC Control Task - Initial Load Start", then we link it to "CDC Control Task - Initial Load End".
The idea is to connect the process to the table.
Set variable "CDC_State" (?).
Set table_to_store as "cdc_states", or just use the wizard if you do not do it.
Set State Name as

We learned how to populate and change the census.
We need a node to populate everything in the initial loading.
Set "CDC Control Operation" as "Mark initial load end".
The message we give to the system is that we already finished the loading.

After the initial loading, in order to capture tha changes, we need:
1- CDC Control Task - 
Data is already there, so we need to understand the changes after the initial load that we need to apply to the table.
Set "CDC Control Operation" as "Get processing range".
Where to store changes? In the same table as before "cdc_stores".

2- Attività flusso di dati
We need to capture the changes, so we move to the Data Flow Tab.
Use the node "CDC Source".
Set the CDC enabled table that you are monitoring.
Set the variable containing the CDC_state.

If you see the table CDC_state, you see that there are some automatically generated columns to identify the changes like `_$...`

We need to understand if the change is an update, a new row, etc.
We use the node "CDC Splitter". It works like a conditional split.
The splits are
1. UpdateOutput
	1. to node "For update"
2. InsertOutput
	1. to node "For insert into"
3. DeleteOutput
	1. to node "For deletion"
All the destination nodes are "flat files destination". ??


3- CDC Control Task
Set "CDC Control Operation" as "Mark Processed Range".

With this lecture, the part on SSIS is finished.
On tuesday we start with the OLAP Cube.
You need to understand the main concepts.


*20/11*
until now it is
![[Pasted image 20241120164002.png|300]]

exercise
1. read the table
2. if customer name is equal, do nothing because the customer already exists.
3. if customer name is different (same customer id)
	1. for example "rosi" > "rossi"
	2. we do not need an update of type 2, but type 1 is enough
How to change the workflow to address the change of the customer name?
1. we use "conditional split" node
	1. added after the lookup
	2. it is an if condition
> during the oral exam, I want to see the optimal solution in your workflow. Thing about different solution and show the optimal.

The workflow now is
1. read table
2. add customer_name
..
4. in OLE DB Command, we need to add the connection to lbi, then in the tab "Component Properties" of the node, add the SQL Command.
```
update customer_dim
set customer_name = ?
where customer_id = ?
```
We need also to map the elements in the workflow with the question marks. The new value, that is the one coming from the derived column, not from the lookup
We also need to update the date_start and date_end.
data_start of the new record is GETDATE(), as well as date_end of the previous record that is GETDATE(). Remember that GETDATE() get today's date.
So, we update with OLE DB Command the date.

Map "new_columns for customer_dim.date_start" with "Param 0" (?).
...
We add a new OLE DB Destination with appropriate mapping.

What if we have a different name and a different address?

> We update the database during the night so that in the following morning I can see an updated dashboard to take decisions (goal oriented). For this reason, it is important to prioritize the information needed for the analysis. (maybe the misspelling of the name is not that important and we can postpone that)

So we prioritize type 2 changes.

EXERCISE.
Work on foodmart, from didawiki, exercise on dissimilarity index.






*19/11*

...

How to define the workflow to update the table?
1. read flat file
2. use OLEDB command.

```
update [dbo].[census_monreale]
set age =     // this is the update command
where id = ?
```

Create table.
1. create table "customer_dim"
	1. using sql ms
2. create surrogate key
	1. remember how to set up server side
3. create customer_id
	1. we need to create a surrogate key because the customer_id is not a primary key 
	2. type 2 errors?

Populate table.
1. read customer_dim
	1. use lookup
2. use "derived column" node
	1. to set default values for non-null
	2. you can use GETDATE() for the dates
3. if not in the table, insert the new customer.











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

Try to produce a single workflow with everuything














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

???
![[Pasted image 20241120175504.png|400]]







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







