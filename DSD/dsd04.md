3 Steps
1. Dimensional Fact Model (DFM)
	1. we see today
2. Relation Data Model (RDM)
	1. to describe a solution
	2. we aim at simplicity rather than normality
3. Multidimensional Model (called CUBE)
	1. with the possibility to navigate the data

We assume to have business questions like this:
![[Pasted image 20240924092047.png]]

Typically arriving at this form requires an effort, because managers speak in natural language.
Be sure that what is available is used and what is useful is available.

In a data model for conceptual design, we have
1. facts
	1. rectangle in the middle
2. measures
	1. quantitative values that are specific of the fact, attached to the fact
3. dimensions
4. dimensional attributes
	1. for example, "date" is a dimension with dimensional attributes like "day","month","quarter","year",...

A dimension without attributes is called degenerate. In the example, it is "OrderNo".

Remind also the concept of hierarchies.
That we represent connecting attributes with arrows.
![[Pasted image 20240924094022.png]]

## Steps for designing a DFM schema

*Step 0. Requirements gathering*
Requirements gathering focuses on the study of business processes and on analysis relevant for decision making.

Business questions can be
1. "why is my business not meeting the targets?"
	1. WRONG, not useful
2. "total revenue, by customer, by product"
	1. useful
3. report
	1. useful, but more difficult

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line


*Step 1. Identify the granularity of the fact*
The first fundamental decision to be taken is the meaning of the fact. What is the grain?

Identifying the grain means deciding the level of detail you want to be made available in the dimensional model. The more detail, the lower the level of granularity. Consider
1. grain is the precision with which the measurements are taken
2. grain determines measures and dimensions and dimensions determine grain

For example, the fact can be
1. an order line, for example the eggs bought
2. a complete order
More detailed grain, often means more space required.

![[Pasted image 20240924095720.png]]

Fact types can be
1. transaction
	1. one fact per transaction, meaning an event that occurs at a specific point in time
	2. for example, a transaction for an individual account of a customer of a bank
2. periodic
	1. one fact for a group of transactions made over a period of time
	2. for example, the amount is the monthly balance for all transaction against an individual account of a customer of a bank
3. accumulating
	1. one fact for the entire lifetime of an evolving event that has a duration and change over time
	2. for example, the lifetime of a mortgage application


*Step 2. Identifying the fact measures*
The measures of interest are numeric values that make sense to add. Not everything that is numeric is a measure.

Remember that
1. a metric is an aggregation of a collection of facts
2. a measure is a quantitative value attached to a fact
3. a fact is an order line

Not everything that is numeric is a measure! A measure is an observation of the performance of a business process. They can always be aggregated, for example the order number cannot and hence is not a measure.

Measure types
1. numeric additive
2. factless (or measureless)
	1. if the measure is missing
	2. for example the complaints
	3. there is ONLY one operation that we can do that is COUNT(\*)
3. numeric non-additive
	1. for example "unit price" or "gross margin"
4. numeric semi-additive
	1. with respect to a dimension, meaning that sometimes the sum makes sense, sometimes it doesn't
	2. "a measure M is semi-additive with respect to a dimension D1 when it cannot be aggregated with the function SUM for groups of data with different values of D1"
	3. for example "monthly balance" cannot be summed by time, but we can sum the "monthly balance" of two people for a fixed month


*Step 3. Identify the fact dimensions*
Identify the dimensions to give fact measures their context.



*Step 4. Identify Dimensional Attributes*
The dimensional attributes are important for analysis and for reports.



*Step 5. Identify the Dimensional Attribute Hierarchies*
Attribute hierarchies is a natural way to support interactive exploration of facts.

Users understand them intuitively, because they are used to look at a summarized report and then to decide to look at a more detailed one.


*ASSIGNMENT AT HOME*: university exams











