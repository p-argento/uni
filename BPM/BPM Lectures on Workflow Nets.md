
# 13 - Workflow Nets
slide 13.
  
Exercises:  
invariants_  
  
Workflow nets (lecture 15):  
definition, syntax sugar, subprocesses, control flow aspects

Workflow nets (lecture 16):  
triggers

(START LECTURE 15 PART 2 MINUTE 27)

Topics
1. definition, 
2. syntax sugar, 
3. subprocesses, 
4. control flow aspects
5. triggers

## 1. definition, 





## 2. syntax sugar, 

There are some decorations.
In woped, you can add decorations for and-split and so on.


![[Pasted image 20250125165054.png]]

Just a professor note.
Use only XOR join.

![[Pasted image 20250125165150.png]]

You can set a transition as a subprocess that is a wf net. It is a transition with double border.

![[Pasted image 20250125165532.png]]






## 3. subprocesses, 
## 4. control flow aspects

Some patterns.

Sequencing 
1. Parallelism (AND-split + AND-join) 
2. Selection (XOR-split + XOR-join) 
3. Iteration (XOR-join + XOR-split) 

Capacity constraints:
1. Feedback loop 
2. Mutual exclusion 
3. Alternating

Explicit choice vs implicit.
Like XOR vs even-based.





## 5. triggers

A decoration that you can add to the transition.

![[Pasted image 20250125170416.png]]










# 14 - Analysis of workflow Nets
slide 14.
  
Exercise:  
modelling with workflow nets_  
  
Analysis of workflow nets (lecture 16):  
structural analysis, activity analysis, token analysis, net analysis, verification and validation, reachability analysis, bags, coverability graph, soundness, N*_
  
Analysis of workflow nets (lecture 17):  
main soundness theorem, strong connectedness of N*

How can we verify the correctness of a WF net?
What does it mean for a wf net to be sound?
We study suitable soundness properties of workflow nets.

What kind of analysis can we do?
1. structural notation
2. behavioural analysis (soundness)

## 1. Types of analysis
1. structural analysis, activity analysis, token analysis, net analysis, verification and validation, reachability analysis, bags, coverability graph

## 2. soundness
3. soundness, N*, main soundness theorem, strong connectedness of N*





example of deadlock
![[Pasted image 20250125171014.png]]


The coverability graph, compared to occurence graph, allow to represent the graph of infinite nets.

Extended bag is like a marking, but for the coverability graph.

![[Pasted image 20250125191702.png]]

![[Pasted image 20250125191923.png]]

The second one is similar to liveness.

Boundedness and liveness will not be checked directly on the wf net, but on a variant of it, called N*.
We add one transition to reset the net and repeat any number of times. Note that is not a wf net anymore.

MAIN THEOREM.

![[Pasted image 20250125192350.png]]

The proof is divided in 3 parts.
![[Pasted image 20250125192508.png]]







*exercises*
How to use wf net to represent an orchestration scenario.

![[Pasted image 20250125192755.png]]

![[Pasted image 20250125193008.png]]

The AND-split and AND-join are redundant and not required.









# 15 - Safe Workflow Nets
slides 15

Exercises:  
workflow nets and soundeness, soundness by construction
  
Safe Workflow nets (lecture 17):  
soundness (and safeness) by construction



# 16 - S-nets
slides16

S-systems (lecture 18):  
fundamental property of S-systems, S-invariants of S-nets, liveness theorem, reachability lemma, reachability theorem, boundedness theorem, workflow S-nets_  

# 17 - T-nets

T-systems (lecture 18):  
circuits and token count on a circuit, fundamental property of T-systems, T-invariants of T-nets, boundedness in strongly connected T-systems, liveness theorem for T-systems, workflow T-nets_  
  
Decision problems and computational complexity (optional reading)  
  
Exercises:  
S-nets properties, T-nets properties_

# 18 - Free-Choice

Free-choice nets:  
Fundamental property of free-choice nets, place-liveness = liveness in f.c. nets, Commoner's theorem, Rank theorem, clusters, stable sets, siphons, proper siphons, fundamental property of siphons, siphons and liveness, traps, Commoner's theorem and its complexity issues, Rank theorem and its complexity issues_  



# 19 - EPC Analysis
slides 19

EPC:  
soundness analysis, from EPC to wf nets, net fragments, dummy style, fusion style, unique start, unique end, three transformations_  

EPC:  
semantics ambiguities, relaxed sound nets, relaxed sound EPC diagrams, from restricted EPC diagrams to f.c. nets, problems with (X)OR joins, OR join policies (wfa, fc, et), from decorated EPC diagrams to nets_  

Exercises:  
workflow net analysis with Woped, properties of free-choice nets, workflow systems_



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





