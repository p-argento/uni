

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





*28/11*
PRESENTATION OF THE PROJECT

The dashboard should be interactive and able to access a db. Use PowerBI.

For delivery, use the university email.

You can choose only 4 of the assignments with `*`.
Answer using MDX, kind of sql language.

> In the project, if there are more rows in a table than the ones in the fact table, probably there is a error.



In SSAS, Cube>Calculations, you can create new 





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


*12/12*

Dashboards and power bi.

Geographical representation of kpi, time series of changes of indicators, etc.
The definition of the dashboard should be discussed with the domain expert.

Different levels of aggregation you might be interested in.

In the SQL Server Suite, there are two tools
1. SSRS (deprecated)
2. Power BI

![[Pasted image 20241218111822.png]]

Now we show a demo.
We present two alternatives
1. connecting the application directly to the cube
2. what happens if we do not find the aggregations in the DW?

Opens Power BI.
Use the famous string for SSAS and use "dynamic connection".

On the right you have the representation of the data. Exactly like in SSAS to create the MDX queries with drag&drop.
Typically the dashboard is a composition of plots.

For any plot, you can use the arrows above the plots to drill-down. 

Click Visualizza modello on the left sidebar to see the structure of the cube.

Right-click and select ? to see the table with the values of the plot.

To add a new plot, click outside the plot first, otherwise it is replaced.

Now, you can also open the db using lds.di.unipi.it
If you open the db engine (no olap cube), you need to create views (see the folder in SSMS). Click design to see the details.

The same computation in the OLAP.

In some companies, you do not have the cube, but only the dw, so you need to create views.

> You are free to use the tool that you want, for example Tableau.

Let's do some queries. in MDX.

1. for each month, how many products have been purchased in the month by at least 10 distinct customers.
```MDX
with memmber nproducts as
	
SELECT nproducts
on columns,
nonempty(([Time].[The Year].[The Year], [Time].[DayMonthYear].[The Monht])
on rows
FROM [Sales]
WHERE
```

2. for each month, how many products have been purchased in the month, by at least 10 distinct customers
```MDX
with memmber nproducts as
	
SELECT nproducts
on columns,
nonempty(([Time].[The Year].[The Year], [Time].[DayMonthYear].[The Monht])
on rows
FROM [Sales]

```












