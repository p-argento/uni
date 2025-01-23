Petri Nets
8. nets-intro
9. petri
10. properties
11. net-matrices
12. invariants
# 8 - From automata to nets
Slide 8. Lecture 9.

From automata to nets:  
Inductive definitions, Kleene star, finite state automata, transition function, destination function, language accepted by an automaton, from automata to Petri nets, places, transitions, tokens_

![[Pasted image 20250118192548.png]]

This is an overview of the basic concepts of Petri Nets.

Why Petri Nets in business process analysis
1. validation -> test correctness
2. verification -> proving correctness
3. performance -> planning and optimization

Definitions
1. an automata (or transition system) is used for sequential protocols (or systems)
	1. but do not capture concurrent behaviour directly
2. a petri net is a mathematical model of a parallel and concurrent system

Notation.
![[Pasted image 20250118193133.png]]

Topics
1. Notation
2. Finite automata examples
3. DFA
4. NFA
5. Reshaping

## FSA Examples
Finite State Automata

Applications.
Finite automata are widely used, e.g., in  protocol analysis,  text parsing,  video game character behavior,  security analysis,  CPU control units,  natural language processing,  speech recognition,  mechanical devices  (like elevators, vending machines, traffic lights)  and many more ...

How to define an automaton?
1. identify the admissible states of the system
	1. mark the error states
2. add transitions from one state to another
	1. no transition to recover from error states
3. set the initial state
4. (optional) mark some states as final states

![[Pasted image 20250118193817.png]]

## DFA
Deterministic Finite Automata

It is important to understand
1. definition of DFA
	1. is a tuple $A=(Q,\sum,\delta,q_0,F)$
2. transition function $\delta$
	1. destination function defined recursively
3. language of A, ie L(A)
	1. for the string processing $w$
4. transition diagram
	1. graph to represent A
5. transition table


![[Pasted image 20250118194102.png]]


![[Pasted image 20250118194125.png]]
![[Pasted image 20250118194230.png]]



## NFA
Non-deterministic Finite Automaton

![[Pasted image 20250118195428.png]]

![[Pasted image 20250118195635.png]]


why??


## Reshaping

Steps
1. get a token
2. forget initial state decoration
3. transitions as boxes
4. forget final states
5. allow for more tokens
6. allow for more arcs

Ingredients
1. token
2. Place
3. Arc
4. Transition

![[Pasted image 20250118195859.png]]

Some facts
1. nets are bipartite graphs
	1. arcs never connect two places
	2. arcs never connect two transitions
2. static structure for dynamic systems
	1. places, transitions, arcs do not change
		1. called passive components
	2. tokens move around places
		1. called active components





# 9 - Petri Nets
Slide 9. Lecture 10.

-> lecture 10

Exercises:  
BPMN and FSA_  
  
Petri nets basics:  
multisets and markings, transition enabling and firing, firing sequences, reachable markings_  
  
Woped basics

-> lecture11

Exercises:  
Petri nets_  
  
Petri nets basics:  
occurrence graph, modelling with Petri nets, examples and exercises_  
  
Woped basics


![[Pasted image 20250118200404.png|300]]

Formalization of the basics concepts of Petri Nets.

Free Choice Nets (book, optional reading) 
https://www7.in.tum.de/~esparza/bookfc.html

Topics
1. Petri nets: basic definitions
2. Petri nets: enabling and firing
3. Petri nets: occurence graph


## 1. Petri nets: basic definitions

Ingredients
1. Places are sort of repositories where we can store something
2. Transitions can be operations
3. Tokens

Multisets.
We can assign a function S that returns 1 if the element is present and 0 otherwise.
The order is not important.
It can appear multiple times.
We use the following notation.
![[Pasted image 20250119180504.png]]


Marking.
A markin is a multiset of places.
It represents the number of tokens in each place.
Meaning 4a+2b is 4 tokens in plance a and 2 tokens in place b.
The state of a petri net is represented with a marking of the tokens in each place.

![[Pasted image 20250118200827.png]]

![[Pasted image 20250119181430.png]]

Pre-set of an transition.
It is the set of immediate predecessors.
Consider a transition t, it is the set of incoming places.

Post-set of a transition.
It is the set of output places of t.

Analogously with places.

![[Pasted image 20250119182031.png]]


## 2. Petri nets: enabling and firing

Topics
1. enabling
2. firing
3. patterns (xor, and, or)
4. firing sequence
5. reachable markings
7. more on sequences
	1.  infinite sequence
	2. enabled sequence
	3. prefix of sequences
	4. enabled sequence
	5. projection of sequence

We say that a transition is enablet if the marking M  enables t.
If M->t it means that there are enough tokens in M to enable t.
Two possible notations can be used.

![[Pasted image 20250119182241.png]]

When we have enough tokens, we can fire the transition and the state changes.
The following formula gives a relation between M and M'

![[Pasted image 20250119182406.png]]

Observe that multiple transitions can be executed. They are atomic. Think about it every time: are the enabled transition concurrent or exclusive?

Observe that the number of tokens can change during the execution.

What is the difference with the FSA?
In the FSA the states are finite (finite state...) while  in petri nets the marking can be infinite because the tokens can be increased indefinitely.

![[Pasted image 20250119183118.png]]
The second is more reasonable because the flight and hotel can both be booked, while in the first net the token can go only in one of the states.

Patterns.
1. sequence
	1. easy
	2. ![[Pasted image 20250119183444.png]]
2. XOR
	1. ![[Pasted image 20250119183431.png|200]]
	2. the first will be fired
3. AND
	1. ![[Pasted image 20250119183457.png|200]]
	2. wait for both
4. OR
	1. combination of both
	2. ![[Pasted image 20250119183514.png|300]]

*Woped (tokengame)*

![[Pasted image 20250119183954.png]]
In this example, we created a deadlock.
This happened because of the XOR first and the AND later.



Remember the notation.
that M is the multiset of cases.
![[Pasted image 20250119184351.png]]

![[Pasted image 20250119184420.png]]

We use sigma to denote a sequence of transitions.
![[Pasted image 20250119184643.png]]

If we consider the set of all transitions, the reachable marking is a set of Markings that are 
Remember that epsilon is the empty sequence.
![[Pasted image 20250119184801.png]]

Now, reasoning on petri nets is general more complicated than reasoning on automaton.

![[Pasted image 20250119185349.png]]

***more on sequences***
1. infinite sequence
2. enabled sequence
3. prefix of sequences
4. enabled sequence
5. projection of sequence

*Infinte sequence.*
It means an unbounded sequence.
For example, you might find a recurrent sequence.
![[Pasted image 20250119185408.png]]

*Prefix of sequences.*
Sometimes we want to decompose sequences.
![[Pasted image 20250119192635.png]]
![[Pasted image 20250119192822.png]]
Observe that epsilon is always a prefix.
And that the prefixes of an infinite sequence are finite.

*Enabled sequence.*
sigma can be used both for finite and not finite sequences.
![[Pasted image 20250119192551.png]]
![[Pasted image 20250119192938.png]]
A sequence is enabled iff all the prefixes are enabled.


*Projected sequence*
We may want to project the sequence only on the transitions that are interesting to us.
We can define a projection sigma over the set T' by removing from sigma all the transitions that are not in T'.
![[Pasted image 20250119193423.png]]

![[Pasted image 20250119193634.png]]


## 3. Petri nets: occurence graph
aka reachability graph.

![[Pasted image 20250120173414.png]]

![[Pasted image 20250120174326.png]]

A stands for Arcs.
R is the set of reachable markings.
More specifically.

![[Pasted image 20250120174438.png]]

Nodes is the set of visited nodes.
See the example of traffic light.
![[Pasted image 20250120180046.png]]

How to avoid the two green? Add an additional token that is required to activate green.
![[Pasted image 20250120174941.png]]
How to alternate the nehaviour of the traffic lights?
![[Pasted image 20250120175105.png]]

*woped*
Click the coverability graph.
It is different because, if the occurence graph is infinite, it will be an approximation of it.




![[Pasted image 20250122112300.png]]










# 10 - Petri nets properties
slide 10. Lectures 12-13.

Exercises:  
modelling with Petri nets_  
  
Behavioural properties:  
liveness, non live transitions, dead transitions, place liveness, non live places, dead places_
(CONTINUES IN LECTURE 13)
deadlock freedom, boundedness, safeness, home marking, cyclicity_  

Structural properties:  
weak and strong connectedness, S-systems, T-systems, free-choice nets_

We formalize some interesting properties for Petri nets.
Later on in the course we will see how these properties are connected with the soundness of workflows.

Free Choice Nets (book, optional reading)  https://www7.in.tum.de/~esparza/bookfc.html

From now on, no isolated nodes.

We study two properties
1. behavioural (or dynamic)
	1. how the markings will evolve during computation
	2. depend on the initial marking and the firing rules
2. structural
	1. related to connections, ie the shape of the graph representing the net
	2. less computationally expensive to verify
	3. also provide some behavioural properties

## -> A. Behavioural Properties

We introduce some of the properties of Petri nets that can play an important role in the verificaition of business processes.

Behavioural properties
1. liveness
2. deadlock-freedom
3. boundness
4. cyclicity also called reversibility
Liveness and boundness are the most important

Let's see some notation
![[Pasted image 20250120185956.png]]
We assume that M is reachable from M0

## 1. Liveness

Liveness can be referred to
1. a single transition t
2. the whole net

A transition is live if, at any point of the computation, it is possible to fire t in the future (meaning that it cannot be excluded).
A Petri net is live if all of its transitions are live.

![[Pasted image 20250120191120.png]] 

Liveness Illustrated.
..

Formally.
To check that every transition is live, we want to check that every 
The order of quantitifiers is important.

![[Pasted image 20250121114341.png]]

Examples.
![[Pasted image 20250121114404.png]]

How to check liveness?
1. Write reachable markings
2. for each transition, check that it can be reached from a reachable marking


*dead transition*
A transition is dead if it cannot be fired in the future
![[Pasted image 20250121114638.png]]

A transition can be non-live and non-dead.
Do not confuse them.
![[Pasted image 20250121114653.png]]

Remember that negating existential means universal.
![[Pasted image 20250121114746.png]]
![[Pasted image 20250121114823.png]]
![[Pasted image 20250121114847.png]]


![[Pasted image 20250121114916.png]]

Example
![[Pasted image 20250121115249.png]]
Because if we are in p2 and decide to fire t3, then t1 and t2 cannot be fired again in the future.

*Liveness on the occurence graph.*
The graph can grow very large, so it is not easy.

A transition t is live  iff  From any node of the occurrence graph we can reach a  node with an outgoing arc labelled by t

A transition t is dead (at M0)  iff  There is no t-labelled arc in the occurrence graph

![[Pasted image 20250121115423.png]]

*place liveness*
Move the concept of liveness to places.

![[Pasted image 20250121115525.png]]

![[Pasted image 20250121115548.png]]

![[Pasted image 20250121115558.png]]

![[Pasted image 20250121115629.png]]


![[Pasted image 20250121115642.png]]


![[Pasted image 20250121115654.png]]

![[Pasted image 20250121115731.png]]



*obvious facts*
obvious facts
1. a system is not live iff it has a transition that can  become dead at some reachable marking  
2. a system is not place-live iff it has a place that can  become dead at some reachable marking 
3. If a place / transition is dead at M, then it remains dead  at any marking reachable from M  (the set of dead nodes can only increase during a run)

true or false?
1. Every transition in the pre- or post-set of a dead place  is also dead  (true)
2. Every place in the pre- or post-set of a dead transition  is also dead (false

Proposition. 
Live systems are also place-live.
![[Pasted image 20250121122526.png]]

Place liveness on the  occurrence graph 
1. A place p is live  iff  From any node of the occurrence graph we can reach a  node with a token in p  
2. A place p is dead (at M0)  iff  All the nodes of the occurrence graph have no token in p

Exercise
![[Pasted image 20250121122823.png]]
Because t need two tokens to be fired, but there is only one. So the net is live place-live because all the places can be visited, but not live because not all the transitions can be visited.

(second part of the lecture 12 is about exercises)




## 2. Deadlock-freedom

*Deadlock-free*
We want the system to be deadlock-free.
The net has always an activity that can be done, meaning that from every reachable marking there is a transition that is enabled.

Remember that `[M>` is the set of markings reachable from M0.

Deadlock freedom on  the occurrence graph  61  A net is deadlock free  iff  Every node of the occurrence graph has an outgoing arc

Questions
1. Does liveness imply deadlock-freedom? YES
	1. Can you exhibit a live Petri net that is not deadlock-free?) NO
3. Does deadlock-freedom imply liveness? NO
	1. Can you exhibit a deadlock-free net that is not live?) YES

We can also prove it by contradiction.
![[Pasted image 20250122115451.png]]

![[Pasted image 20250122115548.png]]


## 3. Boundness

*k-boundedness*
Let k be a natural number  
A place p is k-bounded if no reachable marking has  more than k tokens in place p 

For example if k=2, it means that the tokes in a place can be max 2.

A net is k-bounded if all of its places are k-bounded  In other words, if a net is k-bounded, then k is a  capacity constraint that can be imposed over places  without any risk of causing “overflow”.

*Safe nets*
A place p is safe if it is 1-bounded  A net is safe if all of its places are safe  In other words, if the net is safe, then we know  that, in any reachable marking, each place  contains one token at most

*Boundedness*
A place p is bounded if it is k-bounded for some  natural number k  A net is bounded if all of its places are bounded  A net is unbounded if it is not bounded  (i.e., there is at least one place in which any  number of tokens can appear)

If we do not know the number that bounds.

![[Pasted image 20250122115841.png]]

![[Pasted image 20250122120236.png]]


Boundedness and the  reachability graph
A system is bounded  iff  its reachability graph is finite

![[Pasted image 20250122120256.png]]
![[Pasted image 20250122120310.png]]


## 4. Cyclicity (or reversibility)

*home marking*
if it always possible to always go back there.

A marking M is a home marking if it can be  reached from every reachable marking 

*cyclic net*
A net is cyclic (or reversible) if its initial marking  is a home marking

*Orthogonal properties* 
Liveness, boundedness and cyclicity are  independent of each other  In other words, you can find nets that satisfy any  arbitrary combination of the above three properties  (and not the others)

![[Pasted image 20250122120533.png]]

First system. (looks like producer and comsumer)
P2 is not bounded. The others are bounded.  But the net is not safe.
It is cyclic because it is always possible to go back to p1.
It is deadlock-free because we can always do something.
It is live.

![[Pasted image 20250123163411.png]]


## -> B. Structural Properties

We do not include tokes anymore.

The properties we study are
1. connectedness
2. s-nets
3. t-nets
4. free-choice nets

Definition.
1. net system
	1. denotes a petri net WITH a given initial marking
	2. we study behavioural properties of net system
2. net
	1. denotes a petri net WITHOUT specifying the initial marking
	2. we study structural properties of nets

Other definitions.
1. path
2. circuit
3. undirected path

![[Pasted image 20250122121227.png]]

## 1. Connectedness

1. A net (P,T,F) is weakly connected
	1. if there is an undirected path between any two distinct nodes
	2. (meaning that) iff it cannot be splitted in separated components 
2. A weakly connected net is strongly connected
	1. there is a path between any two distinct nodes
	2. (meaning that) iff  for every arc (x,y) there is a path from y to x



## 2. S-nets vs T-nets vs free-choice nets

Definition
1. conflict
	1. if from a place we need to choose among different transitions
2. synchronization
	1. if a transition needs the tokens from different places to be enabled

![[Pasted image 20250122122145.png]]
How long should we wait for the token to enable t2? Should we just enable t1?

We want to avoid this kind of problems. So we study S-Nets.

*S-Nets*

A Petri net is called S-system if every transition has  one input place and one output place.

(S comes from Stellen, the German word for place) 

This way any synchronization is ruled out 
The theory of S-systems is very simple.


*T-System*

A Petri net is called T-system if every place has one  input transition and one output transition  This way all choices/conflicts are ruled out 

T-systems are concurrent (meaning synchronization exists) but essentially deterministic.
T-systems have been studied extensively since the  early Seventies.


*Free-choice nets*

The aim is to avoid that a choice between transitions  is influenced by the rest of the system.

Easiest way:  keep places with more than one output transition apart  from transitions with more than one input place 
In other words,
1. if (p,t) is an arc, then it means that  t is the only output transition of p (no conflict) 
2. OR  p is the only input place of t (no synch)

But we can study a slightly more general class of nets by  requiring a weaker constraint.

A Petri net is free-choice if  
1. for any pair of transitions
	1. their pre-sets are either disjoint or equal 
2. or, equivalently, if  for any pair of places 
	1. their post-sets are either disjoint or equal


![[Pasted image 20250122122836.png]]

![[Pasted image 20250123163823.png]]

# 11 - Nets as Matrices
Slide 11. Lecture 13.

Nets as matrices:  
markings as vectors, incidence matrices, Parikh vectors, marking equation lemma, monotonicity lemma_

(in lecture 14)
Nets as matrices:  
monotonicity lemma 2 and a corollary, boundedness lemma, repetition lemma_  

This is about a more convenient way to represent petri nets using linear algebra.

Topics
1. markings as vectors
2. incidence matrices
3. Parikh vectors
4. marking equation lemma
5. monotonicity lemma
6. monotonicity lemma 2 and a corollary
7. boundedness lemma
8. repetition lemma

## 1. markings as vectors
![[Pasted image 20250123110316.png]]
![[Pasted image 20250123110356.png]]




## 2. incidence matrices


It is entirely determined by the net.

Instead of a graph, we use the matrix PxT

-1 if consuming a token
+1 if producing one token

![[Pasted image 20250123111823.png]]

It will tell how many tokens are produced for each place, looking at rows.

![[Pasted image 20250123111914.png]]

*vending machine example*

Think column-wise. Look at transition and fill the places in the rows with the number of tokens the produce or require when the transition is fired.

![[Pasted image 20250123112103.png]]

*firing*
A sequence of firing is summing the column vectors of transitions to markings.

![[Pasted image 20250123112245.png]]


## 3. Parikh vectors

Can any firing sequence can be seen as a vector?

![[Pasted image 20250123112355.png]]

sigma assign the value corresponding to the number of times each transition is fired.

We can define the paroikh vector recursively.

![[Pasted image 20250123113028.png]]

## 4. marking equation lemma


First fact.
What if I multiply the incidence matrix to the parikh vector of a single transition. I get the column vecotr with the tokens in each place.

![[Pasted image 20250123113205.png]]

Second fact.
![[Pasted image 20250123113244.png]]
![[Pasted image 20250123113300.png]]



![[Pasted image 20250123113329.png]]

Essentially with the parikh vector we are allow to add one by one the transitions appearing in the sequence as many times as needed.

![[Pasted image 20250123113640.png]]

Marking equation  lemma: consequences  63  The marking reached by any occurrence  sequence only depends on the number of  occurrences of each transition  It does not depend on the order in which  transitions occur  Every fireable permutation of the same  transitions leads to the same marking



## 5. monotonicity lemma

Everything that can be done with less resources, can be done with more resources. The extra resources are just presets (L).

![[Pasted image 20250123113837.png]]

![[Pasted image 20250123114035.png]]

## 6. monotonicity lemma 2 and a corollary
(lecture 14)

Reminders
1. infinite sequence
2. enabledness







## 7. boundedness lemma
## 8. repetition lemma


# 12 - Invariants
Slide 12. Lecture 14?

Exercises:  
behavioural properties, structural properties_  
  
Invariants:  
S-invariants, fundamental property of S-invariants, alternative characterization of S-invariant, support, positive S-invariants_








