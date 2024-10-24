[LDS Didawiki](http://didawiki.di.unipi.it/doku.php/mds/lbi/start)

## Important Notes

*24-10*

It is better to do most of the operations locally (even rounding numbers), because we do not know the power of the server. Just get the data from the server.

Remember. The cursor is a pointer to the resources that must be reset (or re-execute the query).

--project




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

## Notes from recording of past year
14/10/24
*is it the same this year?*

install version 17 of odbc driver for sql
active vpn

lds.di.unipi.it
-> autenticazione sql tramide id
id: lds
psswrd: pisa

select default database "lbi"






