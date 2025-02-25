
# 13 - Workflow Nets
slide 13.
  
Exercises:  
invariants_  
  
Workflow nets (lecture 15):  
definition, syntax sugar, subprocesses, control flow aspects
 
Workflow nets (lecture 16):  
triggers

(START LECTURE 15 PART 2 MINUTE 27)

![[Pasted image 20250220114249.png]]

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
1. structural analysis, activity analysis, token analysis, net analysis, verification and validation, reachability analysis, 






example of deadlock
![[Pasted image 20250125171014.png]]


## bags, coverability graph

The coverability graph, compared to occurence graph, allow to represent the graph of infinite nets.

Extended bag is like a marking, but for the coverability graph.

## 2. soundness, N*


![[Pasted image 20250125191702.png]]

![[Pasted image 20250125191923.png]]

The second one is similar to liveness.

Boundedness and liveness will not be checked directly on the wf net, but on a variant of it, called N*.
We add one transition to reset the net and repeat any number of times. Note that is not a wf net anymore.

## main soundness theorem,

![[Pasted image 20250125192350.png]]

The proof is divided in 3 parts.
![[Pasted image 20250125192508.png]]

Let's move to the proof of the main theorem.
Generally the wf net N is not live.
The proof is made of 3 steps.
3. if N* is live and bounded -> N is sound
4. if N is sound -> N* is bounded
5. if N is sound -> N* is live

see the proof in lecture 17 part 1.
...

## strong connectedness of N*

![[Pasted image 20250128115402.png]]
->* is not a firing sequence, it just means a connected path.
Since N* is strongly connected, it is live and bounded.

We analyze the wf net using woped.
If it is a wf, woped automatically add an invisible reset?









*exercises*
How to use wf net to represent an orchestration scenario.

![[Pasted image 20250125192755.png]]

![[Pasted image 20250125193008.png]]

The AND-split and AND-join are redundant and not required.


![[Pasted image 20250128111302.png]]
What is the language of a net?
L(N) is the set of firing sequences that lead us from the start to the end.
Sometimes to find all the sets it is enough to change the order of transitions or take alternative paths in xor.
If we cannot reach the end, the L(N) is empty.

*exercises on behavioural properties*
Recall.
![[Pasted image 20250128112048.png]]

![[Pasted image 20250128112246.png]]
If we take the path above, there is no proper condition because there is a left token in p7 below.
![[Pasted image 20250128112946.png]]
A solution would be to always send the letter.






# 15 - Safe Workflow Nets
slides 15

Exercises:  
workflow nets and soundeness, soundness by construction
  
Safe Workflow nets (lecture 17p2):  
soundness (and safeness) by construction

This set of slides is about
6. building a net that is sound by construction
7. we show a technique to build sound wf nets

## The idea of building blocks

THe idea is to find building blocks.
They 
![[Pasted image 20250128120437.png]]

We can replace a transition with a whole new net.
If N and N' are safe and sound, then the result is safe and sound.

![[Pasted image 20250128120637.png]]
![[Pasted image 20250128120705.png]]
![[Pasted image 20250215171455.png]]
![[Pasted image 20250215171547.png]]

You can take any net that is safe and sound and reuse it as a block.
Even if the net looks complicated, we know that is safe and sound if the smaller blocks are.


![[Pasted image 20250128120958.png]]
We can replace some blocks with single transitions.

*exercise*
![[Pasted image 20250128121310.png]]

When we have two parallel branches they may create a state explosion.

We replace
8. a xor block
9. a nested iteration (careful with the direction)

Sometimes it is helpful to desugarize (remove decorations like xor).

![[Pasted image 20250128121744.png]]

![[Pasted image 20250128121756.png]]

![[Pasted image 20250128122336.png]]






![[Pasted image 20250129113134.png]]
The reset transition is there, even if not visible.

> For the project, I expect you to have all the soundness checks green in woped. It doesn't matter if the ones of the structural analysis are not okay, it can happen.
> You will have to design the diagram in bpmn, translate it in wf-net and analyse it.

![[Pasted image 20250129114541.png]]
Look at an optimal situation.

## -> project-like exercise (try it)
![[Pasted image 20250129114815.png]]

![[Pasted image 20250129120407.png]]

In the next lectures we will learn what does it mean
![[Pasted image 20250129120423.png]]




# 16 - S-nets
slides16

S-systems (lecture 18):  
fundamental property of S-systems, S-invariants of S-nets, liveness theorem, reachability lemma, reachability theorem, boundedness theorem, workflow S-nets_  


![[Pasted image 20250129120513.png]]

![[Pasted image 20250129120818.png]]

## fundamental property of S-systems,
aka fundamental invariant

The number of tokens is always the same.


New notation.
![[Pasted image 20250129120940.png]]

![[Pasted image 20250129121038.png]]

To answer if a marking is reachable, first count the sum of tokens if it is the same.

![[Pasted image 20250129121235.png]]



## S-invariants of S-nets, 

Assignings weights to places.

![[Pasted image 20250129121301.png]]

![[Pasted image 20250129121343.png]]



## liveness theorem, 

![[Pasted image 20250129121407.png]]

strongly means that we can reach every node from any other node.




## reachability lemma, 

![[Pasted image 20250129121655.png]]


## reachability theorem, 

![[Pasted image 20250129121753.png]]

![[Pasted image 20250129121805.png]]


## boundedness theorem, 
## workflow S-nets_  

![[Pasted image 20250129121841.png]]

![[Pasted image 20250129121850.png]]

We can also strengthen the theorem.

![[Pasted image 20250129121931.png]]

*exercises*










# 17 - T-nets

T-systems (lecture 18):  
circuits and token count on a circuit, fundamental property of T-systems, T-invariants of T-nets, boundedness in strongly connected T-systems, liveness theorem for T-systems, workflow T-nets_  
  
Decision problems and computational complexity (optional reading)  
  
Exercises:  
S-nets properties, T-nets properties_


## circuits and token count on a circuit, 
T-systems are less frequent than S-sytem

![[Pasted image 20250129145730.png]]

The computation is deterministic in a T-Net !!
This means that the firing of a transition t in M cannot disable another transition t' enabled at M.
However, concurrent is possible.

![[Pasted image 20250129150652.png]]
A wf net will never be a T-net.
Once we add the reset transition, it can be a T-net.

![[Pasted image 20250129151100.png]]

![[Pasted image 20250129151122.png]]




## fundamental property of T-systems, 

![[Pasted image 20250129151152.png]]


Some markings are not reachable just because the number of tokens is different for some markings.







## T-invariants of T-nets, 

![[Pasted image 20250129151619.png]]

By firing the same number of times ....


## boundedness in strongly connected T-systems, 

![[Pasted image 20250129151651.png]]

![[Pasted image 20250129151701.png]]

![[Pasted image 20250129151825.png]]

![[Pasted image 20250129151927.png]]

## liveness theorem for T-systems, 

![[Pasted image 20250129151940.png]]

![[Pasted image 20250129152126.png]]

![[Pasted image 20250129152150.png]]


## workflow T-nets

![[Pasted image 20250129152344.png]]

*exercises*

![[Pasted image 20250129152539.png]]

![[Pasted image 20250129152645.png]]
We have a characterization that 









# 18bis - P and NP problems

Complexity classes.

A problem is a family of related questions.
A problem instance is a specific question.
A decision problem requires just a boolean answer.

Computational complexity theory.

## Complexity class P

![[Pasted image 20250129152859.png]]

For example, the eulerian circuit is simple.
It can be checked in linear time.

## Complexity class NP

![[Pasted image 20250129153006.png]]

So
10. in P the problems can be checked and solved effectively
11. in NP the problems can be only checked effectively
This means that a P problem is also NP.

Example of Hamiltonian circuit.


![[Pasted image 20250129153236.png]]

How do we know?

## Complexity class NP-complete

Inside the class of NP, there is another class of problems.

![[Pasted image 20250129153336.png]]

![[Pasted image 20250130171620.png]]
Nice explanation on [stackoverflow](https://stackoverflow.com/questions/1857244/what-are-the-differences-between-np-np-complete-and-np-hard)

If once we find the solution for a problem, every other problem can be solved with any other NP problem.

We will explore the Satisfiability decision problem.

![[Pasted image 20250129153501.png]]


*example*
![[Pasted image 20250129153628.png]]









# 18 - Free-Choice

Free-choice nets (lecture19):  
Fundamental property of free-choice nets, place-liveness = liveness in f.c. nets, Commoner's theorem, Rank theorem, clusters, stable sets, siphons, proper siphons, fundamental property of siphons, siphons and liveness, traps, Commoner's theorem and its complexity issues, Rank theorem and its complexity issues


Today we finish the overview of structural properties that guarantee behavioural ones. Then we will discuss how to encode epc and bpmn into petri nets for analysis. Then process mining and quantititative analysis.

## Recap on Free-choice net

![[Pasted image 20250130105625.png]]

![[Pasted image 20250225204901.png]]

There are many equivalent definitions. The one prof prefer is 
![[Pasted image 20250130105658.png]]

To understand if the net is free-choice, it makes sense to look only at transitions that have a preset place in common. If they share it, it is ok.

![[Pasted image 20250130105956.png]]

## Fundamental property of free-choice nets, 

The choice can be done without excluding any alternative.

![[Pasted image 20250130110115.png]]

When t is enabled, we are free to choose any other transition that will be enabled.

![[Pasted image 20250130110156.png]]



## place-liveness = liveness in f.c. nets, 

![[Pasted image 20250130110216.png]]

It works only the other way round.





## Commoner's theorem, 
for liveness

![[Pasted image 20250130110606.png]]
## Rank theorem, 
for liveness and boundedness

it consists of 6 properties to be checked.
![[Pasted image 20250130110650.png]]

The first two are greyed out because our nets always respect them.

So now we need to show
![[Pasted image 20250130110808.png]]

## clusters, stable sets,

A cluster is the smallest set



So, in the Commoner's theorem, 
The rank, ie the number of independent rows, should be equal to the number of clusters minus 1.

Stable set of markings is a convenient concept.

![[Pasted image 20250130120007.png]]
If M is bold, it means that is a set of markings.

![[Pasted image 20250130120039.png]]
Once we are in the stable set, we cannot escape

![[Pasted image 20250130120105.png]]

Examples...







## siphons, proper siphons, fundamental property of siphons, siphons and liveness,

![[Pasted image 20250130120432.png]]

In order to produce a token in R, we need to retrieve a token from R.

![[Pasted image 20250130120513.png]]
If the siphon is empty, it will remain empty.

![[Pasted image 20250130120744.png]]
Once the tokens get into the trap, it cannot escape. It will be the dual.


![[Pasted image 20250130120922.png]]
If the syphon is empty, the transition attached to it will never be fired.
![[Pasted image 20250130120957.png]]

This explains the third condition of the siphons and rank theorem, ie M0 marks every proper siphon.
Because if this was not true, the net cannot be live



##  traps,

It is the converse of a trap.
The inclusion is  reversed.
The preset of the trap includes
All the transitions that can consume tokens from the set will necessary produce tokens in the set.
Anytime we try to stole tokens from the trap, new tokens will be produced and it will never remain empty.

![[Pasted image 20250130121356.png]]

![[Pasted image 20250130121409.png]]


Examples
![[Pasted image 20250130121434.png]]

![[Pasted image 20250130121622.png]]



## Commoner's theorem and its complexity issues, 
Is it hard to show that a free-choice net is live?

(the proof is not part of the course)

![[Pasted image 20250130121657.png]]
It is not unsolvable, but it is very difficult.

![[Pasted image 20250130125850.png]]

The union of traps is a trap.

![[Pasted image 20250130125926.png]]


![[Pasted image 20250130125950.png]]

If we had an oracle, it would be polynomial time to check.

Let us see the polinomial algo for finding a trap, if R is a siphon.
![[Pasted image 20250130130054.png]]

Q will be guaranteed to be a trap.
![[Pasted image 20250130130209.png]]
so the non-liveness problem for free-choice systems is in NP.

![[Pasted image 20250130130312.png]]

![[Pasted image 20250130130346.png]]
Remember the satisfiablity problem (SAT).

![[Pasted image 20250130130421.png]]

How do we reduce the free-choice net of a formula?
![[Pasted image 20250130130456.png]]


Instead of looking at the formula, it is more convenient to look at the negation.

![[Pasted image 20250130130542.png]]


Let us start with the sample formula and derive the corresponding free-choice net.

?????

![[Pasted image 20250130130835.png]]

![[Pasted image 20250130130859.png]]







## Rank theorem and its complexity issues
Is it hard to show that a free-choice net is live and bounded?

![[Pasted image 20250130131030.png]]

![[Pasted image 20250130131148.png]]

![[Pasted image 20250130131202.png]]


*xercises*







