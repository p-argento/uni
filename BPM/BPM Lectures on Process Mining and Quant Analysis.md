# 23 - Process Mining
slides 23
  
Process mining:  
intro, Event logs, discovery, conformance, enhancement, perspectives, play-in, play-out, replay, overfitting, underfitting, alpha-algorithm, footprint matrix, naive fitness, improved fitness, comparing footprints

Exercises:  
process discovery, performance analysis


## intro, Event logs, 

We try to learn models out of data.
We use event logs data.

Processes are needed to better understand the world data.
Configure and implement software systems which interacts with data.

A process consists of cases.
A case consists of events.
Events within a case are ordered in time (start and end time).
Events can have attributes (eg. activity, time, cost, resource).

An event log is a collection of all the events of a process.
They are ordered sequentially.

![[Pasted image 20250227114819.png]]

An example of event log.
Each event has its own unique id.

![[Pasted image 20250227114908.png]]

We group by case-id instance, then by timestamp.

## discovery, conformance, enhancement, perspectives, 

There a 3 activities that we can perform.
1. discovery
	1. starts from event log to discover the model
2. conformance
	1. check if model match with logs
	2. are there cases that cannot be performed with the model?
3. enhancement
	1. if there is a mismatch, we can try to repair the model or the system

![[Pasted image 20250227115140.png]]

Discovey.
Carried out automatically.
It is possible to obtain different kinds of models from the same event log.

Conformance.
Used to detect violations and why they do happen.

Enhancement.
Two different angles
1. descriptive model
	1. if there is a mismatch, means the model is wrong
	2. -> model repair
2. normative model
	1. if there is a mismatch, means the reality is different from the guidelines

## play-in, play-out, replay, 
There are 3 strategies.

play-in.
Used in mining and discovery.

Replay.
We start from event log and try to use the model to replicate the event.
Will be used in conformance checking.

Play-out.
Ability given a model to produce a synthetic event log.
Will be used to compare models.

*Example of discovery and conformance*

There are elements we are not interested in (separation of concerns).

We use abstraction as letters for activities.
So now a sequence of activities is a miulti-set of traces.

How to extract information?
1. all cases start with a and end with g or h
	1. build the net accordingly adding initial and final place
2. ...
Let's keep guessing.

![[Pasted image 20250227120230.png]]

Now we try to replay the event logs using the model.
Do the logs belong to do the language of our model?

![[Pasted image 20250227120435.png]]

## overfitting, underfitting, 

According to the model, we could capture traces that are not in the logs. This is usually desirable since we want the model to be more general.

![[Pasted image 20250227120633.png]]

Be careful with
1. underfitting
	1. some logs cannot be replayed
2. overfitting
	1. if it replicates the logs but does not add contraints in the sequence of logs (called flower net)

![[Pasted image 20250227120820.png]]

How to measure the conformance?
Count the number of the traces that cannot be executed.
For example 7/10 is better than 2/10.

Question time...
![[Pasted image 20250227121107.png]]

Be careful with inserting splits and joins, if they are not in the trace, it means that they cannot be used.

## alpha-algorithm, footprint matrix,
Process Discovery: $\alpha$-algorithm

A process discovery algorithm is a function that maps an event log L onto a process model M.

![[Pasted image 20250227123209.png]]

For the alpha algo, multiplicity is mot important.

![[Pasted image 20250227123305.png]]

![[Pasted image 20250227123411.png]]

How to measure the fitness? We will describe it next time.

*alpha-algo*

It was one the first algorithms and it still has some limitations.

The alpha-algorithm uses the play-in strategy  to scan the event log for particular patterns,  called log-based ordering relations,  to create a footprint matrix of the log.

Any two logs with the same matrix will derive the same model.

How are the ordering relations derived?
There are log-based ordering relations

1. a is immediately followed by b
	1. a >L b
![[Pasted image 20250227143630.png]]

Then there are 3 possibilities
![[Pasted image 20250227143706.png]]

Given any two pairs of events, there are 4 casas
1. concurrent
2. mutual exclusive
3. a precedes b
4. b precedes a

First, we get all the immediate precedences.
Second, we look for other precedence, mutual exclusion and concurrence.

![[Pasted image 20250227144222.png]]

*footprint matrix*
Now we want to use this information to build the footprint matrix (which is symmetric).

![[Pasted image 20250227144342.png]]

Which are the patterns we look at?
1. a sequence pattern
	1. with sequence pattern
2. xor-split and xor-join
	1. with mutual exclusive pattern
3. and-split and and-join
	1. with parallel pattern

![[Pasted image 20250227144528.png]]

The first 3 steps define the transitions of interest.
The first transitions are those that appear in the beginning of some trace (equivalently for end).

The 4th step is important to get the dependencies among events.
There are decision points.
Intuitively, given two set of transitions A and B, there will be a place s.t. its preset is A and its postset is B.

![[Pasted image 20250227145008.png]]

Step 5. max decision points
We only care about the largest pairs.
I throw away all the pairs that are dominated by others.
This is called maximal decision points.
For example a,b is dominated by a,be.
In the set of decision points, we keep only those that are not dominated by others.

Step 6. places
One place for each pair of maximal decision point.
Starting from maximal decision points,

Step 7. arcs
The place ab will have a as preset and b as postset.

Step 8. net
Obtain the net.

![[Pasted image 20250227145820.png]]

Try the following exercise given the log, check the footprint matrix and the model extracted.
![[Pasted image 20250227145857.png]]

![[Pasted image 20250227145939.png]]

This algorithm is not perfect. It can be redundant.
One particular issue is the short loop, meaning transitions with the same name, the alpha algo cannot detect them.
However, the designer can detect it because there will be a disconnected node.

![[Pasted image 20250227150052.png]]

Another limitation is noise.
Noise is a behaviour that is rare.
Maybe we just want a model that generalize.



## naive fitness, improved fitness, comparing footprints
Conformance checking: fitness measures.

















# 24 - Quantitative Analysis
slides 24

Quantitative analysis (lecture 23):  
Performance dimensions and objectives, KPI, cyle time analysis, Little's law, cost analysis


## performance dimensions and objectives, KPI, 




## cyle time analysis, 


## Little's law, 


## cost analysis








