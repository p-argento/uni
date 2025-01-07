UP TO NOW 
Data Warehouse: Data Models and DW Design and Implementation.

STARTING TODAY 
Data Analysis Using SQL.  How to summarize data using SQL?  What if the query takes a long time to produce the answer?

# dsd15 - Analytic SQL (1)
OLAP systems. Data Analysis Using SQL. Simple reports. Examples. Moderately Difficult Reports. Solutions in SQL.

> Maybe read https://en.wikipedia.org/wiki/Data_warehouse

OLAP refers to the technique of performing complex business  multidimensional analysis over the data warehouse.
> We will see how report developers use SQL to write queries!

## Solution to JRS exercise

**EXERCISE AT HOME**

![[Pasted image 20250107120447.png]]

In JRS, Options > Show Logical Plan.

Query 1.
Number of distinct customers by product.
```SQL
SELECT FkProduct, COUNT(DISTINCT(FkCustomer)) AS NCustomers
FROM Invoices, InvoiceLines
WHERE FkInvoiceNo=PkInvoiceNo
GROUP BY FkProduct;
```

Query 2.
Largest invoice revenue by product.
(for every product,  we want to know the total revenue of the invoice containing that product with the highest)

```SQL
WITH TotalByInvoice
	(SELECT FkInvoiceNo AS Invoice, SUM(FkProduct * Qty) AS TotalInvoice
	FROM InvoiceLines
	GROUP BY FkInvoiceNo)

FROM InvoiceLines, TotalByInvoice
WHERE FkInvoiceNo=Invoice
GROUP BY FkProduct;
```





# dsd16 - Analytic SQL (2)


# dsd17- Analytic SQL (3)


# dsd18 - Query Plans


# dsd 19 - DW Indexes

Start of lectures on "Relational DBMS Extensions for DW".
The topics of the lectures from 19 to 23 are
![[Pasted image 20241224104640.png]]

19 -> Index and Storage Structures + Star Query Physical Plan
20 -> Materialized Views
21 -> (functional dependencies and their usage in query optimization)
22 -> Optimization techniques for star queries with grouping and aggregations
23 -> Query rewriting to use materialized views




