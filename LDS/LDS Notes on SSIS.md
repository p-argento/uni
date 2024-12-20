## 30-10 (seconda parte)

In SSIS, open a new project and on the right go to "SSIS Packages" to build an ETL process. Is the .dtsx file, it is like a 
Only one project containing different packages?
Each .dtsx is a dataflow (?).
> How many packages do we need to create for the project?

If you open the file of the professor, you get an error because you cannot open it, but you can still read it. 

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



## 6/11
WATCH LECTURE

![[Pasted image 20241120175504.png|400]]




## 13/11

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












