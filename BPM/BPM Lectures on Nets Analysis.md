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


We explore 3 different approaches

![[Pasted image 20250210115252.png]]


## (1) FROM EPC TO WF NETS, net fragments, dummy style, fusion style, unique start, unique end, three transformations

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



## semantics ambiguities

![[Pasted image 20250210115726.png]]

This is easy, but how do we deal with connectors?

![[Pasted image 20250210120032.png]]

![[Pasted image 20250210120120.png]]
One single node is translated into 6 nodes.

![[Pasted image 20250210120145.png]]

Once we have done the translation of all the arcs, we need to take into account the

![[Pasted image 20250210120222.png]]

Example.
![[Pasted image 20250210121517.png]]
Observe that there are two arcs between two places, which is not allowed. So we apply the fusion style.
Then we fix the two different end places.

![[Pasted image 20250210121708.png]]

Now we move to woped and discover that is not sound.
There are 4 unbounded places.

![[Pasted image 20250210121736.png]]

We look at the coverability graph.
We colour in green succesful nodes and in red the failures.
(together with predecessors), the others where we can choose we color in orange.

![[Pasted image 20250210122002.png]]

It means that after following an oragne path, the decision will then impact what happens in the future.

![[Pasted image 20250210122107.png]]

Can we repair the model?
Instead of having an OR join, we use an END.
Now the model is bounded but not live anymore, meaning that we risk a deadlock.
> always remember that there is the deadlock node.

We might try to fix the petri net, but what about the original epc?

## relaxed sound nets, relaxed sound EPC diagrams, 

![[Pasted image 20250211122521.png]]

![[Pasted image 20250211122529.png]]

![[Pasted image 20250211122554.png]]
 If for every transition of the net, there exists an execution in the language of the net (with one token in i and one in o), such that the transition t is used in that execution.
 Meaning that the transition can participate to a sound execution.

![[Pasted image 20250211122800.png]]
There is a transition (O1B) that cannot participate to a sound execution. This net is not relaxed sound then.

However, from the point of view of the EPC.
The EPC diagram is relaxed sound, because the transition of the OR join is translated into many nodes. And at least one of these nodes participate in sound executions.
Therefopre the OR node itself can be part of sound execution.
The underlying petri net however is NOT sound.

The problem is that there is no theroem for relaxed soundness.
![[Pasted image 20250211123135.png]]





## (2) FROM RESTRICTED EPC TO FC NETS, problems with (X)OR joins, OR join policies (wfa, fc, et),

Second attempt.
We consider diagrams with NO OR connectors.

We insert dummy transitions in a preliminary step (step 0).
The we follow the usual 3 steps.


...


![[Pasted image 20250211123536.png]]

The good point is that we can obtain free choice nets using this approach.




## (3) FROM DECORATED EPC TO NETS

![[Pasted image 20250211123943.png]]

![[Pasted image 20250211124358.png]]

...








> for the project, do not use epc diagrams because there will be collaborations.


# 20 - Workflow Systems
slides 20

Exercises:  
free-choice nets, clusters, siphons, traps, SAT encoding_  
  
Workflow systems:  
I/O interfaces, workflow modules, structural compatibility, workflow system, weak soundness_

![[Pasted image 20250211124719.png]]

![[Pasted image 20250211124736.png]]

![[Pasted image 20250211124746.png]]

![[Pasted image 20250211124812.png]]

Note the different between blue places that are input places because they have only outgoing arcs, and they are in the presets of transitions in the net.

![[Pasted image 20250211124929.png]]

After validation of soundness, you can add places in the interface, but it is no longer a workflow net, it becomes a workflow module.

![[Pasted image 20250211125041.png]]

It is not a wf net anymore because there are many initial places and final places.

We can compose modules.

![[Pasted image 20250211125139.png]]

![[Pasted image 20250211125150.png]]

the output places in one side matches the input places in the other side.

![[Pasted image 20250211125239.png]]

![[Pasted image 20250211125303.png]]

The idea is to transform this set of wf modules into a wf net.
We must enforce a unique initial and final places.

![[Pasted image 20250211125440.png]]

![[Pasted image 20250211125528.png]]
![[Pasted image 20250211125643.png]]

We can change the behavior of the auctioning service.

![[Pasted image 20250211125926.png]]
![[Pasted image 20250211125939.png]]

Typically collaborations are not free choice.
Because they wait for others.


*weak soundness*

![[Pasted image 20250211130126.png]]

![[Pasted image 20250211130136.png]]

![[Pasted image 20250211130312.png]]

This is weak sound.


# 21 - BPMN Analysis

Exercises:  
workflow systems_  
  
BPMN:  
from BPMN diagrams to nets
  
![[Pasted image 20250211130655.png]]

Collaboration between 2 or more partners.
BPMN is the best notation because it allows collaboration.

![[Pasted image 20250211130836.png]]

Elements
1. Pools and lanes to assign resposanbilities for the execution of tasks.
2. flow objects
	1. events
	2. tasks
	3. gateways
3. connecting objects
	1. flow relation
	2. message passing relations
4. artifacts
	1. (you can remove them before starting the analysis)

![[Pasted image 20250211131301.png]]

![[Pasted image 20250211131316.png]]

Patient and doctor.

![[Pasted image 20250211131337.png]]

![[Pasted image 20250211131352.png]]
Remember that we need a ? gateway if we need to wait a decision from the other partner.

Now to analyze these diagrams we follow the same strategy we used for EPC.

## BPMN semantics

![[Pasted image 20250211144600.png]]

There are many formal semantics, but use petri nets.
There is the same problem with OR-join that was in EPC.

![[Pasted image 20250211144716.png]]
If the wf net is sound, then the bpmn diagram is sound.

## Translation from BPMN to Petri

![[Pasted image 20250211144755.png]]

![[Pasted image 20250211144817.png]]

The bpmn that we translate are simplified.

![[Pasted image 20250211144903.png]]
![[Pasted image 20250211144955.png]]

![[Pasted image 20250211145024.png]]
Before the translation, it is useful to translate into these.
Be careful in particular with the event-based gate.

![[Pasted image 20250211145138.png]]
Prof suggested not to use some of them.

![[Pasted image 20250211145209.png]]

	How to translate?

![[Pasted image 20250211145232.png]]

![[Pasted image 20250211145245.png]]

![[Pasted image 20250215165146.png]]

![[Pasted image 20250215165205.png]]


The intermediate step is a hybrid diagram with elements of a petrin net.

![[Pasted image 20250211145410.png]]

![[Pasted image 20250211145447.png]]

![[Pasted image 20250215164844.png]]

![[Pasted image 20250215164854.png]]

*example of order process*











# 22 - Diagnosis of Workflow Nets

Diagnosis of Workflow nets:  
Woped, S-components, S-cover, sound f.c wf nets are safe, TP-handles, PT-handles, well-handled nets, well-structured wf nets, Woflan, ProM, error sequences, non-live sequences, unbounded sequences_

![[Pasted image 20250211155844.png]]












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
