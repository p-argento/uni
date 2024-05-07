Causality Ladder
1. observe
2. experiment
3. counter-factual

We could use
1. randomized samples
2. historical data
But they have their problems.

Causal Model Frameworks
1. Potential Outcome
2. Structural Causal mOdel

# 1. Potential Outcome

Causal Effect = Y(1) - Y(0)
But you cannot observe at the same time 0 and 1.
That's why we need counterfactuals.
This problem of causal inference is then treated as a problem of missing data.

We can study the average treatment effect.

Ignorability.
It is important because.
We cannot test the ignorability if we do not have some data.
In the moment you condition on X, Y does not depend anymore on X.
Then ignorability holds.

Identifiability.

We have some assumptions.
We assume that Yi doesn't depend by other treatments.
If all the people have a dog, then maybe you're not happy anymore.
Then consistency (SUTVA in econometrics), meaning that black and white dog are the same.

Propensity Score Matching.
It is more powerful then randomized experiments because we do not have the curse of dimensionality.

Mainly used for estimating average effects of binary treatment.
We need an expert to validate the strong assumptions we make.
It is very manual, not like ML were it is mostly automatic.
We cannot use causal diagrams/graphs.

# 2. Structural Causal Model

There is a set of endogenous and a set of exogenous variables...
Each SCM is associated with a graphical model.

The random part is in the exogenous variable, like the normal distribution.

See causal structures
1. chain
2. collider (one child and different parents)
3. confounder (one parent and different children)

Levels of investigation
1. Causal discovery
2. causal inference

In PO, we only had causal inference.
In SCM, we have additionally the graph, meaning causal discovery, since the graph is not given a priori.

There are some relationships that you can infere from the data, conditioning some variables.

Methods
1. constraint-based
2. score-based
3. functional causal models (at the cost of strong assumptions)

How do we infere using this method?
1. back-door criterium
2. front-door (more complex)

