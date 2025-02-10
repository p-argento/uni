# 19 - EPC Analysis
slides 19

EPC (lecture19p2):  
soundness analysis, from EPC to wf nets, net fragments, dummy style, fusion style, unique start, unique end, three transformations_  

EPC:  
semantics ambiguities, relaxed sound nets, relaxed sound EPC diagrams, from restricted EPC diagrams to f.c. nets, problems with (X)OR joins, OR join policies (wfa, fc, et), from decorated EPC diagrams to nets_  

Exercises:  
workflow net analysis with Woped, properties of free-choice nets, workflow systems_

![[Pasted image 20250210114338.png]]
We exploit petri nets to analyze epc diagrams.

## EPC diagrams recall

![[Pasted image 20250210114428.png|300]]


## from EPC to wf nets, net fragments, dummy style, fusion style, unique start, unique end, three transformations

How to assign smeantics?
We transform epc diagrams into nets to use woped.

![[Pasted image 20250210114548.png]]

Step 1. Convert each ingredient into a net fragment.
We convert each event into a net fragment.

Step 2. Connects fragments together.
Two options
1. introduce dummy places/transitions
	1. called dummy style
	2. to guarantee the properties of petri nets
2. merge places/transitions
	1. called fusion style

Step 3. Enforce initial and final place.
Add a XOR start.
Add a OR end (sometimes XOR or AND, depends).

![[Pasted image 20250210115252.png]]


Context dependent, means that the way we connect an element depends on the other elements it is attached to.
"(dummy)" means that the dummy nodes are in the epc, while "dummy" means dummy nodes after the translation.



## semantics ambiguities, relaxed sound nets, relaxed sound EPC diagrams, 

![[Pasted image 20250210115726.png]]

This is easy, but how do we deal with connectors?

![[Pasted image 20250210120032.png]]

![[Pasted image 20250210120120.png]]
One single node is translated into 6 nodes.

![[Pasted image 20250210120145.png]]

Once we have done the translation of all the arcs, we need to take into account the

![[Pasted image 20250210120222.png]]








## from restricted EPC diagrams to f.c. nets, problems with (X)OR joins, OR join policies (wfa, fc, et),




## from decorated EPC diagrams to nets_  












# 20 - Workflow Systems
slides 20

Exercises:  
free-choice nets, clusters, siphons, traps, SAT encoding_  
  

  
Workflow systems:  
I/O interfaces, workflow modules, stuctural compatibility, workflow system, weak soundness_



# 21 - BPMN Analysis




Exercises:  
workflow systems_  
  
BPMN:  
from BPMN diagrams to nets_  
  



# 22 - Diagnosis of Workflow Nets

Diagnosis of Workflow nets:  
Woped, S-components, S-cover, sound f.c wf nets are safe, TP-handles, PT-handles, well-handled nets, well-structured wf nets, Woflan, ProM, error sequences, non-live sequences, unbounded sequences_




# 23 - Process Mining
slides 23

Exercises:  
EPC analysis_  
  
Process mining:  
intro, Event logs, discovery, conformance, enhancement, perspectives, play-in, play-out, replay, overfitting, underfitting, alpha-algorithm, footprint matrix, naive fitness, improved fitness, comparing footprints_



# 24 - Quantitative Analysis
slides 24

Exercises:  
_process discovery, peformance analysis_  
  
Quantitative analysis (lecture 23):  
_Performance dimensions and objectives, KPI, cyle time analysis, Little's law, cost analysis_  
  
A final note (with project instructions)
