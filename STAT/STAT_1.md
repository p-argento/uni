## Basics of statistics
An experiment is a measurement of a random process.
The outcome of a measurement takes values in some set $\Omega$ called the sample space.
$\Omega$ can be finite or infinite.
For example, the set of natural number is countably finite: $\Omega=\mathbb{N}={1,2,3,...}$

We can write all the possible combination using the dot product:
- Tossing a coin twice: $\Omega = \{H, T\} \times \{H, T\} = \{(H, H),(H, T),(T, H),(T, T)\}$

The outcome of the experiment can be a tuple with multiple values.

> See a visualization of statistics [here](https://seeing-theory.brown.edu/)


An event is some subset of $A\subseteq\Omega$ of possible outcomes of an experiment.

## Probability Function

A probability function is a mapping from events to real numbers that satisfies certain axioms. Basically how likely is an event to occur.

![[Pasted image 20240220164104.png]]

In particular, additivity can be expanded over a set of possible values by considering each event as isolated. This is called *generalized additivity*.
$P(\{a_1, . . . , a_n\}) = P(\{a_1\}) + . . . + P(\{a_n\})$

P({a}) often abbreviated as P(a), e.g., P(Jan) instead of P({Jan}).
The event is the set containing only Jan.

*Properties of probability functions.*

![[Pasted image 20240220164926.png|500]]

$$\begin{align}
P(A^c)=1-P(A) \\
P(\emptyset)=0 \\
A\subseteq B \Rightarrow P(A)\leq P(B) \\
P(A \cup B) = ...

\end{align}$$

4 ) is the inclusion-exclusion principle.

## Defining probability functions

In data mining we always rely on counting frequencies.
But there are two approaches
1. *frequentist interpretation*
	1. measure the proportion of outcomes
	2. like when tossing a coin $P(A)=|A|/\Omega$
2. *bayesian* (or epistemiological) *interpretation*
	1. measures the degree of belief
	2. iliad and odyseey were written by the same person

### Monty Hall problem
Try it [here](https://math.andyou.com/tools/montyhallsimulator/montysim.htm)
There is a mistake. In this schema the car is always in door 1.

![[Pasted image 20240220170453.png]]



## What if the sample space is countably infinite?

![[Pasted image 20240220170941.png]]

(ii) is called *countable additivity*.
There is an equivalent formulation which is $\sigma$-additivity $$for\ A_1\subseteq A_2\subseteq...\qquad
P(\lim_{n\rightarrow\infty}A_i)=\lim_{n\rightarrow\infty}P(A_i)$$![[Pasted image 20240220171904.png]]

Defining the probability of observing head after n coin tosses lead to a probability fraction. Both properties of probabilities were tested and respected.

> See onenote and check

## Conditional Probability

Example.
What is the probability of R given the assumption L.
If we restrict to seven month in L.

![[Pasted image 20240220172305.png]]

Intuition.
Probability of an event in the resctricted sample space $\Omega\cap L$ .
- a-priori is the probability $P(R)$ without any assumption
- a-posteriori is the probability $P(R|L)$
The probability of an event can be higher or lower after conditioning.

![[Pasted image 20240220173056.png]]

*Properties of conditional probability*

![[Pasted image 20240220173125.png]]

*Multiplication Rule*

![[Pasted image 20240220173135.png]]

Within C, what is the probability that A holds.
Why? Because sometimes it is easier to calculate the conditional probability than the intersection.

![[Pasted image 20240220173154.png]]

The Chain Rule is a generalization of the multiplication rule.

### Example of no coincident birthdays

![[Pasted image 20240220174256.png]]

### Example

The fact that we can reason thinking with different cases is due to the multiplication rule.

![[Pasted image 20240220174741.png]]

## Law of total probability

![[Pasted image 20240220174900.png]]

The events are disjoint and cover all the sample space.

![[Pasted image 20240220174908.png]]


## Independence of Events

![[Pasted image 20240222141351.png]]

Intuition: the fact that an event occurs doesn't change the probability of another event.
The event B must be possible (otherwise makes no sense).
The a-priori probability is P(A) so without the "given B".
For example, a second coin toss in independent from the first one.

*Properties*
Properties:
1. A independent of B iff $P(A∩B)=P(A)·P(B)$
2. A independent of B iff B independent of A (symmetry)
3. A independent of B iff Ac independent of B

> Prove these statements

## Conditional Independence
It combines conditional probability and independence of events.

![[Pasted image 20240222142618.png]]

Removing B does not change the probability.

*Properties*:
1. A conditionally independent of B iff $P(A ∩ B|C) = P(A|C) · P(B|C)$
2.  A conditionally independent of B iff B conditionally independent of A

![[Pasted image 20240222142817.png]]
> The question is: independence implies or not conditional independence?

*How does independence generalize to two or more events?*
![[Pasted image 20240222142933.png]]
An alternative definition is
![[Pasted image 20240222142948.png]]
Note that in the alternative definition we use the product of subsets.

> Show that the two definitions are equivalent.

*It is stronger than pairwise independence.*

