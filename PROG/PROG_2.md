*What is a fuzzy set?*
Progr4ds.01e.Sets_MultiSets_FuzzySets.pdf

## Tautology
How to prove that a formula is always true?
A tautology is a proposition that is always true, obvious.
Two approaches
1. Use a truth table and checking equivalence
	1. but it grows exponentially
2. build a proof that starts from known tautologies

*If premise if true but consequent is false is the only case when implication is False.*

## 1. Using Equivalence
Two propositions are *equivalent* $P\equiv Q$ if they always have the same truth value.
For example, we can show that the contrapositive $(\neg q \implies \neg q)$ is equivalent to the original proposition $(p\implies q)$. 
We can also show that the converse $(q\implies p)$ and the inverse $(\neg p\implies\neg q)$ are not equivalent to the original implication.

Some well known equivalent propositions.
They can be derived using truth tables.

![[Pasted image 20240222112619.png]]
![[Pasted image 20240222112634.png]]

*DE MORGAN's law* is really important. We will use it a lot.
Geometrically, if something is not in the intersection of A and B, then it is in the union of complementary of A and B, including outside of the circles.
The negation of an intersection is equivalent to the union of negations.

And for *implications*
If premise is false, implication is always true. (We do not always need to check the back of the card)
The first one is really important.
$p\implies q\equiv\neg p\vee q$

![[Pasted image 20240222112657.png]]
![[Pasted image 20240222112707.png]]

## 2. Using Proof

Now we have many laws to construct a proof.
We use substitution principle.

![[Pasted image 20240222114911.png]]

### Modus Ponens
Every human is mortal, Socrates is a man, so Socrates is mortal.
We have an implication and knowing that the implication is true, means that the implication is true.
$(p\implies q)\vee p\implies q$

![[Pasted image 20240222120035.png]]

## Satisfiability
A compound proposition is satisfiable if there is an assignment of truth values to its variables that makes is true.
Being a tautology obviously means being satisfiable.

## Reductio ad absurdum
It is another way to prove.
For example $\sqrt{2}$ is irrational.
To prove P its sufficient to show that denying P results in a contradiction $$P\equiv(\neg P\implies F)$$Another formulation is
...


# Normal Forms
Using De Morgan, we can remove conjunction and disjunction, reducing to
1. conjunctive Normal Form (CNF)
2. disjunctive Normal Form (DNF)

![[Pasted image 20240222122712.png]]

The disadvantage of truth table is the exponential growth, but they are easy.
The proof is shorter, but harder to automate.

### How to convert to normal formulas.
Using laws.
Normal forms facilitate automatic verification.

Example.
![[Pasted image 20240222123201.png]]

An example where the NF is useful is programming, where you cannot use implication, but you must use only and, or, negations. So we need to find equivalent formulae for implications.

# Predicates and Quantifiers

