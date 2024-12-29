[from here](https://learn.microsoft.com/en-us/analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query?view=asallproducts-allversions)

The WHERE clause describes the slicer axis in an MDX query. It acts as something like an invisible, extra axis in the query, slicing the values that appear in the cells in the result set; unlike the SQL WHERE clause it does not directly affect what appears on the rows axis of the query. The functionality of the SQL WHERE clause is available through other MDX functions such as the FILTER function.


## Esempi

```MDX
--total sales
select [Measures].[Store Sales] on columns
from [Sales]

--total sales per country in store
select [Measures].[Store Sales] on columns,
NONEMPTY([Store].[Geography].[Sales Country])  on rows
from [Sales]

--total sales per south east california
select [Measures].[Store Sales] on columns,
  [Store].[Geography].[Sales Country].&[USA].&[South West].&[CA] on rows
from [Sales]

-- total store sales in 1998
select [Measures].[Store Sales] on columns,
 [Time].[The Year].&[1998] on rows
from [Sales]


-- total store sales in 1998 (solution with where without rows)
select [Measures].[Store Sales] on columns
from [Sales]
where [Time].[The Year].&[1998]

-- total store sales after month Jan 1998
select [Measures].[Store Sales] on columns,
 [Time].[DayMonthYear].[The Year].&[1998].&[Q1].&[January].lead(1)  on rows
from [Sales]

-- total sales and total store cost USA for each  customers gender
select {[Measures].[Store Sales], [Measures].[Store Cost]} on columns,
([Customer].[Geography].[Country].&[USA], [Customer].[Gender].&[F])  on rows
from [Sales]

-- total sales and total store cost for each country and  customers gender
select {[Measures].[Store Sales], [Measures].[Store Cost]} on columns,
([Customer].[Geography].[Country], [Customer].[Gender].[Gender])  on rows
from [Sales]

-- total sales and total store cost USA for female customers
select {[Measures].[Store Sales], [Measures].[Store Cost]} on columns,
([Customer].[Geography].[Country].&[USA], [Customer].[Gender].[Gender])  on rows
from [Sales]


-- sales and profit in USA and Mexico
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
 {[Customer].[Geography].[Country].&[Mexico],[Customer].[Geography].[Country].&[USA]} on rows
from [Sales]

-- sales and costs for each month
select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
 ([Time].[The Year].[The Year], [Time].[DayMonthYear].[The Month])
  on rows
from [Sales]

select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
 [Time].[The Year].[The Year] * [Time].[DayMonthYear].[The Month]
  on rows
from [Sales]

select {[Measures].[Store Sales], [Measures].[Profit]} on columns,
 crossjoin([Time].[The Year].[The Year],[Time].[DayMonthYear].[The Month])
  on rows
from [Sales]

-- total sales from Feb 1997 ti July 1997 

select [Measures].[Store Sales] on columns,
[Time].[DayMonthYear].[The Year].&[1997].&[Q1].&[February]:
[Time].[DayMonthYear].[The Year].&[1997].&[Q3].&[July] on rows
from [Sales]

-- return the ordered list of stores wrt the total sales
select [Measures].[Store Sales] on columns,
NONEMPTY(order([Store].[Store Id].[Store Id],[Measures].[Store Sales],desc))  on rows
from [Sales]

-- return the  list of stores with the total sales > 1000000

select [Measures].[Store Sales] on columns,
filter([Store].[Store Id].[Store Id], [Measures].[Store Sales] > 100000)  on rows
from [Sales]

-- return the top 5 stores with highest store sales 
select [Measures].[Store Sales] on columns,
topcount([Store].[Store Id].[Store Id], 5, [Measures].[Store Sales] )  on rows
from [Sales]

-- return the top 5 stores with highest store sales for saturadays 
select [Measures].[Store Sales] on columns,
topcount([Store].[Store Id].[Store Id], 5, [Measures].[Store Sales] )  on rows
from [Sales]
where [Time].[The Day].&[Saturday]

-- total sales per days of Feb 1997 that have more than 1000$ of sales
-- filter and order
select [Measures].[Store Sales] on columns,
order(filter([Time].[DayMonthYear].[The Year].&[1997].&[Q1].&[February].children,
[Measures].[Store Sales] > 1000), [Measures].[Store Sales], desc)
on rows
from  [Sales]

-- total sales per gender in USA and 1998
select  [Measures].[Store Sales] on columns,
[Customer].[Gender].[Gender] on rows
from  [Sales]
where ([Time].[The Year].&[1998], [Customer].[Country].&[USA])

-- total sales and profit per gender in USA and 1998
with member profit_local as
[Measures].[Store Sales] - [Measures].[Store Cost]
select {[Measures].[Store Sales], profit_local }on columns,
[Customer].[Gender].[Gender] on rows
from  [Sales]
where ([Time].[The Year].&[1998], [Customer].[Country].&[USA])


-- total sales, profit and margin (percentage) per gender in USA and 1998

with member profit_local as
[Measures].[Store Sales] - [Measures].[Store Cost]
member margin as profit_local/[Measures].[Store Sales],
format_string ="percent"
select {[Measures].[Store Sales], profit_local, margin} on columns,
[Customer].[Gender].[Gender] on rows
from  [Sales]
where ([Time].[The Year].&[1998], [Customer].[Country].&[USA])


-- percentage of sales over year per month
-- perc_over_year = store_sale_month/store_sale_year
with member sales_year as
([Time].[DayMonthYear].currentmember.parent.parent,[Measures].[Store Sales])
member perc_over_year as
[Measures].[Store Sales]/sales_year,
format_string ="Percent"
select {[Measures].[Store Sales], sales_year, perc_over_year} on columns,
([Time].[The Year].[The Year], [Time].[DayMonthYear].[The Month])on rows
from  [Sales] 

--running sales per month
with member running_sale as
Aggregate(PERIODSTODATE([Time].[DayMonthYear].[The Year], 
[Time].[DayMonthYear].currentmember),
[Measures].[Store Sales])
select running_sale on columns,
([Time].[The Year].[The Year], [Time].[DayMonthYear].[The Month]) on rows
from  [Sales] 

-- set expression
with SET setcomponent as
{[Store].[Sales City].&[Los Angeles], 
[Store].[Sales City].&[San Francisco]}
select[Measures].[Store Cost] on columns,
setcomponent on rows
from  [Sales] 

-- compute the difference of total store sales between 
-- the current month and the previous one
with member diff as
[Measures].[Store Sales] - 
(PARALLELPERIOD([Time].[DayMonthYear].[The Month], 
1, [Time].[DayMonthYear].currentmember), [Measures].[Store Sales])
select {[Measures].[Store Sales],diff} on columns,
[Time].[DayMonthYear].[The Month] on rows
from  [Sales] 
where [Time].[The Year].&[1998]


-- compute the difference of total store sales between 
-- the current month and the previous one (with lag funtion)
with member diff as
[Measures].[Store Sales] - 
([Time].[DayMonthYear].currentmember.lag(1), [Measures].[Store Sales])
select {[Measures].[Store Sales],diff} on columns,
[Time].[DayMonthYear].[The Month] on rows
from  [Sales] 
where [Time].[The Year].&[1998]

-- compute the difference of total store sales between 
-- the current month and the previous one (with prevmember)
with member diff as
[Measures].[Store Sales] - 
([Time].[DayMonthYear].prevmember, [Measures].[Store Sales])
select {[Measures].[Store Sales],diff} on columns,
[Time].[DayMonthYear].[The Month] on rows
from  [Sales] 
where [Time].[The Year].&[1998]

-- compute the difference of total store sales between 
-- the current day and the same day of the previous month 

with member diff as
[Measures].[Store Sales] - 
(PARALLELPERIOD([Time].[DayMonthYear].[The Month], 
1, [Time].[DayMonthYear].currentmember), [Measures].[Store Sales])
select {[Measures].[Store Sales], diff} on columns,
[Time].[DayMonthYear].[Time Id] on rows
from  [Sales] 
where [Time].[The Year].&[1998]

--drillthrough
drillthrough
select  [Measures].[Store Sales] on columns
from  [Sales] 
where [Time].[The Year].&[1998]

-- RANK FUNCTION
-- RANK(member to be ranked, the sets 
-- of elemnts where we need to work for producing the rank , mesure)
-- rank all the months in our cube wrt the store sales
with member RK as
RANK([Time].[DayMonthYear].currentmember, [Time].[DayMonthYear].[The Month], 
[Measures].[Store Sales])
select {[Measures].[Store Sales], RK} on columns,
([Time].[The Year].[The Year],
[Time].[DayMonthYear].[The Month]) on rows
from  [Sales] 

-- for each year rank the months wrt the store sales

with member RK as
RANK(
([Time].[The Year].currentmember, [Time].[DayMonthYear].currentmember),
([Time].[The Year].currentmember, [Time].[DayMonthYear].[The Month]), 
[Measures].[Store Sales]
)
select {[Measures].[Store Sales], RK} on columns,
([Time].[The Year].[The Year],[Time].[DayMonthYear].[The Month]) on rows
from  [Sales] 

--Q0 in slides

select [Measures].[Store Sales] on columns,
nonempty(([Time].[The Year].[The Year], [Time].[DayMonthYear].[Quarter],
[Customer].[City].[City])
) on rows
from  [Sales]  

-- top 5 product categories based on store sales
select [Measures].[Store Sales]  on columns,
topcount([Product].[Product Category].[Product Category],5,[Measures].[Store Sales])  on rows
from [Sales] 


-- top 5 product categories based on store sales considering 1998
select [Measures].[Store Sales]  on columns,
topcount([Product].[Product Category].[Product Category],5,[Measures].[Store Sales])  on rows
from [Sales] 
where  [Time].[The Year].&[1998]








-- top 5 categories in 1998 per quarter and gender

-- generate (tuples of quanter and gender and for each element produce the top 5)

select [Measures].[Store Sales] on columns,
nonempty(generate( ([Time].[Quarter].[Quarter],[Customer].[Gender].[Gender]), 
topcount(
([Time].[Quarter].currentmember,
[Customer].[Gender].currentmember,
[Product].[Product Category].[Product Category]),
5,
[Measures].[Store Sales]))) on rows
from sales
where [Time].[The Year].&[1998]



select [Measures].[Store Sales] on columns,
nonempty(
GENERATE(
([Time].[Quarter].[Quarter], [Customer].[Gender].[Gender]),
topcount(
([Time].[Quarter].currentmember, 
[Customer].[Gender].currentmember,
[Product].[Product Category].[Product Category]),
5,[Measures].[Store Sales])
)) on rows
from [Sales]
where [Time].[The Year].&[1998]

-- for each quarter and customer city return a ratio = sales/cost
with member ratio as
iif([Measures].[Store Cost]=0,0,([Measures].[Store Sales]/[Measures].[Store Cost])),
format_string ='Percent'
select {[Measures].[Store Sales], [Measures].[Store Cost], ratio} on columns,
([Time].[The Year].[The Year], [Time].[DayMonthYear].[Quarter],[Customer].[City].[City]) on rows 
from [Sales] 

-- order stores and months based on the difference between their sales
-- and the sales of the previous month.

with member diff as
[Measures].[Store Sales] - 
([Time].[DayMonthYear].prevmember,[Measures].[Store Sales])
select diff  on columns,
order(([Time].[The Year].[The Year],[Time].[DayMonthYear].[The Month], 
[Store].[Store Id].[Store Id]), diff, desc) on rows
from [Sales]


-- how many cities per sales region had more than 4000 dollars 
-- of total sales in march 1998
with member ncities as
count(filter ([Store].[Sales City].[Sales City],[Measures].[Store Sales]>4000)) 
select ncities on columns,
nonempty([Store].[Sales Region].[Sales Region]) on rows
from [Sales]

-- Adding ALL

with member sales as 
case when [Measures].[Store Sales]=null then 0 
else [Measures].[Store Sales] end
select 
nonempty(([Time].[The Year].[The Year], 
[Time].[DayMonthYear].[Quarter], sales))on columns,
nonempty([Customer].[Geography].[City]) + {[Customer].[Geography].[All]}
on rows
from [Sales]


-- for each month, how many products have been 
-- purchased in the month 
--by at least 10 distinct customers
-- order the result wrt the nproducts in descending order
-- we need to use bdesc and not desc because otherwise the order 
-- follows the hierachy
with member nproducts as
count(filter([Product].[Product Id].[Product Id], 
[Measures].[NCustomers]>=10))
select {nproducts, [Measures].[Store Sales]}
on columns,
order(([Time].[The Year].[The Year],
[Time].[DayMonthYear].[The Month]), 
nproducts, bDESC)
on rows
from [Sales]



```




## Altro
