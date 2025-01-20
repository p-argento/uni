
The topics are
1. bpm1 - Intro  
2. bpm2 - Business Processes  
3. bpm3 - Diagrams Types  
4. bpm4 - Models and abstraction  
5. bpm5 - BP Lifecycle  
6. bpm6 - EPC  
7. bpm7 - BPMN (1)  
8. bpm8 - BPMN (2)  
9. bpm9 - From automata to nets  
10. bpm10 - Petri Nets (1)  
11. bpm11 - Petri Nets (2)  
12. bpm12 - Behavioural and Structural Properties  


# bpm1 - Intro
Course introduction:  
course objectives, textbooks, BPM aim and motivation, models and abstraction_

Just intro and a digression on Euler.

## Eulerian circuit and path

![[Pasted image 20250117161804.png]]
![[Pasted image 20250117161829.png]]



# bpm2 - Business Processes
Introduction to Business Processes:  
Taylorism, work units, processes, terminology, organizational structures, process orientation and reengineering, visual notations_

Ch.1 of Workflow Management: Models, Methods, and Systems Ch.1 of Business Process Management: Concepts, Languages, Architectures

Let's talk about terminology.
The topics are
1. process orientation
2. organizational structures
3. actors
4. cases and procedures
5. process orientation
6. standardization

## 1. Taylorism
Products.
Products are the outcome of some work.
Products are supplied via markets.
There are services and products necessary for the organization.
People are organized in specialized work units.
There might be relatively autonomous divisions.

Process orientation is based on a critical analysis of a concept to organize work units. 
Originally introduced by Frederick Taylor. (!856-1915).
The aim of Taylorism is to improve industrial efficiency.
The management formulates detailed plans and communicate it to the workers.
Taylorism uses functional breakdown of complex work to small granularities.
Fine-grained activities require many handovers of work.

Pitfall of Taylorism.
The steps of a business process are often related to each other.
The handover of work can be a problem because in business organizations that process information the context information is required in every step and plain functional breakdown might be costly.
The complexity might prevent from seeing the overall schema.

Process Orientation serves to capture the activities a company performs, but also to improve the relationship between activities.
The process perspective is instrumental to combine multiple units of work of small granularity into work units of larger granularity to reduce the handover of work.

![[Pasted image 20250117163919.png]]



## 2. Organizational Structures

An organizational structure establish how the work, authorities and responsabilities are divided amongst its staff. Meaning roles and functions.

The most relevant forms of organizational structure are
1. network structure
2. hierarchical structure
3. matrix structure

*1. network structure*
Automomous actors collaborate to supply products or services.
Characteristics
1. non-hierarchical
2. ad-hoc clustering
3. outsourcing
4. dynamic joining of team members

![[Pasted image 20250117173120.png]]

*2. hierarchical*
Also called organization chart.
Structured as a tree.

Characteristics
1. internal nodes are individual nodes/functions,
2. leaves are staff or departments
3. branches are authority relationships

Recall that
1. a tree is a graph such that any two vertices are connected by exactly one path (also called connected acyclic graph)
2. a leaf is a vertex of degree 1
3. a rooted tree is a tree with one distinguished vertex (the root)

![[Pasted image 20250117173556.png]]

*3. matrix structure*
It add (dynamic) functional dimension.

Characteristics
1. one row for each project
2. a project leader is a functional boss
3. each person can have more project leaders

![[Pasted image 20250117173912.png]]


## 3. Actors

An actor can be
1. a principal
2. a contractor
3. both roles at the same time

*1. principal*
A principal is an individual, department or firm that assign (or outsource) the work.
We divide
1. assignment ordered by boss
2. work for customers

*2. contractor*
A contractor is a person (or a machine) who is a task.

*-> contract*
A contract exists between the principal and the contractor.
It is about the deadline, the price, etc.
A communication protocol can be established to exchange information.

![[Pasted image 20250117174828.png]]


## Cases and Procedures

*Case, procedures, tasks*

Definitions
1. case
2. procedures
3. tasks

A case, also called work, job, product, service.
1. a tangible thing produced or modified
2. an intagible case like an insurance

Characteristics
1. typically discrete
2. every case has a beginning and an end
3. each case can be distinguished from any other case
4. each case involves a procedure

Additional definitions.
1. a procedure (also process, project) is a collection of tasks to be carried out and the conditions that determine the order of the tasks.
2. a task is a logical unit of work that is carried out as a single whole.

Cases vs procedures. Economy of scale.
The numbers of procedures in a company is generally finite, but the number of cases can be much bigger.
The number of cases for each procedure should be as high as possible to reduce costs.

*knowledge, resources, activities*

Other definitions
1. knowledge
2. resources
3. activities

A resource is the generic name for a person, machine or group of people or machines that is responsible for the task.

An activity is the performance of a task by a resource.


## Process Orientation


Keywords
1. Hammer & Champy (1993)
	1. collection, input, output
2. Johansson et al. (1993)
	1. recipient, linked 
3. Davenport (1993)
	1. structure, ordering, time, space, begin, end,  measurement, ownership
4. Rummler & Brache (1995)
	1. production, support and managerial processes

*collection, input, output*

Introduced by Hammer & Champy in "Reengineering the Corporation".

A business process is a collection of activities that take one or more kinds of input and create an output that is of value to the customer.

Shift of logic from product perspective to process perspective.

Characteristics of processes
1. definability
	1. clearly defined boundaries, including input and output
2. collection
	1. wrap up a collection of tasks

*recipient, linked*

In "Business Process Reingeneering".

A process is a set of linked activities that take an input and transform it to create an output.
The output should be useful and effective to the recipient.


*structure, ordering, time, space, begin, end,  measurement, ownership*
Davenport in 1993 with "Process Innovation".

A process is a specific ordering of work activities across time and space, with a beginning and an end.

Additional important definitons
1. measurement
2. ownership

Process that are clearly structured are amenable to measurement in a variety of dimensions, like cost, time, output quality, customer satisfaction.

Ownership must be seen as an additional dimension. 
It is crucial to define the responsible for design and execution.


![[Pasted image 20250117182309.png]]

*production, support and managerial processes*

We distinguish
1. production (or primary) processes
2. support (or secondary) processes
3. management (or tertiary) processes

Production
1. customer-oriented
2. generate income for the company

Support
1. support primary processes
2. for example maintenaince, financial admin

Managerial
1. fix objectives
2. allocate resources

![[Pasted image 20250117183047.png]]


## Standardization

Visual language offer an important communication mean.
The natural choice is nodes and arrows, meaning oriented graphs.


# bpm3 - Diagrams Types
Exercises:  
Alice-Bob car selling scenario
Examples:  
Orchestration diagrams, collaboration diagrams, choreography diagrams

## (insurance claim example)

Be careful with ambiguities.
![[Pasted image 20250117183438.png|300]]

We distinguish
1. orchestration diagrams(single-viewpoint)
2. collaboration diagrams (multiple-viewpoints)
3. choreography diagrams (global-viewpoint)

## 1. Orchestration Diagrams

Orchestration is about describing and executing a single view point model. Like a conductor who centrally controls the musicians in an orchestra.

Business process models are performed in a single organization by definition.
The ordering of activities (performance of a task by a contractor) can be controlled by a business process management system as a centralized software component run by the organization.

Example of reseller.
Glimpse of BPMN-like syntax.
1. a pool is a rectangle that encloses a business process
	1. can be divided in lanes to distribute tasks to different actors
2. dotted arcs represent the message flows
	1. they are used for interacting processes that exchange information

![[Pasted image 20250118115249.png]]

## 2. Collaboration Diagrams

It about describing the interactions between autonomous business processes and they can influennce reciprocally.

![[Pasted image 20250118115217.png]]


## 3. Choreography Diagrams

Choreography is about describing a global model (multi-point view). Like dancers who behave autonomously but have their own part in the choreography.

The process choreography represent the interactions of a set of business processes.

Differences
1. wrt orchestration
	1. absence of a central  agent that control activities
2. wrt collaboration
	1. only contrains activities that are related to interactions between participants

![[Pasted image 20250118115200.png]]


# bpm4 - Models and abstraction
Examples and Exercises:  
Travel agency ochestration, coffe break example, buyers and resellers collaborations

Models and abstraction:  
visual modelling, horizontal abstraction, modelling levels, models and instances, a generic process meta-model, aggregation abstraction, granularity levels, functional decomposition, vertical abstraction, separation of concerns, modelling domains, function models, information models, organization models, roles, IT landscape models, process models
vertical abstraction, separation of concerns, modelling domains, function models, information models, organization models, roles, IT landscape models, process models

Ch. 3 of Business Process Management: Concepts, Languages, Architectures

## Business Process Modelling
A business process consists of a set of activities that are performed in coordination in an organizational and technical environment.

Business Process Management includes concepts, methods, and techniques to support the design, administration, configuration, enactment and analysis of business processes.

In modelling, a notation is needed to
1. communicate efficiently
2. refine processes
3. improve processes

How to represent processes
1. visual representations (what we see)
	1. diagrams and charts
	2. for example informal, intuitive, BPMN, EPC, BPEL, ...
2. languages (what machines see)
	1. unambiguous machine syntax
	2. for example process dialects, XML schemas
3. models (what we analyse)
	1. rigorous semantics for scientists
	2. for example automata, Petri nets, workflow nets

![[Pasted image 20250118124238.png]]

A model is a simplification of reality
Given a complex problem, we use abstraction to derive general rules and concepts.
We divide
1. horizontal abstraction
	1. separation different modelling levels
2. aggregation abstraction
	1. separation at different granularity levels
3. vertical abstraction
	1. separation at different subdomains

## 1. Horizontal abstraction
Modelling Levels

Definitions
1. a business process meta-model (M2)
1. a business process model (M1)
	1. consists of a set oof activity modeles and execution constraints between them
	2. like a blueprints
3. a business process instance (M0)
	1. represent a concrete case in the operational business of a company consisting of activity instances

![[Pasted image 20250118124805.png]]
![[Pasted image 20250118154636.png]]

![[Pasted image 20250118155539.png]]
![[Pasted image 20250118155555.png]]
![[Pasted image 20250118155621.png]]



![[Pasted image 20250118124839.png]]



## 2. Aggregation abstraction
Granularity levels

It is related to functional decomposition.
A single artefact at the higher level of granularity can be decomposed in multiple elements of a lower granularity level.
In other words, a high-level business function can be decomposed into finer-grained functions.


![[Pasted image 20250118154219.png]]

![[Pasted image 20250118155725.png]]



## 3. Vertical abstraction
separation of concerns (or subdomains)

The guiding principle is the Separation of Concerns (SoC).
It means to separate a system into distinct features that overlap in functionality as little as possible.

> It is what I sometimes have called the separation  of concerns, which, even if not perfectly possible,  is yet the only available technique for effective  ordering of one's thoughts, that I know of.  It does not mean ignoring the other aspects,  it is just doing justice to the fact that from this  aspect's point of view, the other is irrelevant.
> EWD447 ~ Dijstra

![[Pasted image 20250118160330.png]]

???




# bpm5 - BP Lifecycle
Business Processes Lifecyle:  
levels of business processes, business strategies, operational goals, organizational BP, operational BP, lifecycle, design and analysis phase, identification, modelling guidelines, validation, simulation, verification, configuration phase, platform selection, software architecture, individual enterprise applications, enterprise resource planning system, siloed enterprise applications, enterprise application integration, point-to-point integration, hub-and-spoke integration, enterprise service computing, system workflows, human interaction workflows, testing, enactment phase, event logs, logging, evaluation phase, activity monitoring, mining, administration phase, stakeholders

Ch. 1, 2 of Business Process Management: Concepts, Languages, Architectures


## Levels of business processes

![[Pasted image 20250118161435.png]]






## What is the BP Lifecycle

Comparison of BP Lifecycle wrt
1. waterfall
	1. a sequential sw design process flowing downwards
2. Extreme Programming (XP)
	1. made of planning-feeback loops to be responsive wrt changing requirements
3. Plan-Do-Check-Act (PDCA)
	1. management method for control and continuous improvement of products

![[Pasted image 20250118161838.png]]
![[Pasted image 20250118161932.png]]
![[Pasted image 20250118162125.png]]
![[Pasted image 20250118162144.png]]




## Steps of the BP Lifecycle

![[Pasted image 20250118161838.png]]

Steps
1. design&analysis
	1. design
		1. bp identification
		2. bp modelling
	2. analysis
		1. validation
		2. simulation
		3. verification
2. configuration
	1. system selection
	2. implementation
	3. test and deployment
3. enactment
	1. opeartion
	2. logging
	3. maintenance
4. evaluation
	1. process mining
	2. business activity monitoring
5. administration and stakeholders
	1. administration
	2. stakeholders

## 1. Design and Analysis


## 2. Configuration

Different proposals
1. ...

In the 90s, a fixed a standard for Workflow (Wf) representation and execution, the Workflow Management Coalition (WfMC).

Defintions
1. a workflow 
	1. is the automation of a business process in whole or in part
	2. during which documents, information, or tasks are passed from one participaltn to another
	3. according to a set of procedural rules
2. a workflow management system
	1. is a software system that defies, creates, and manages Wfs execution
	2. we divide
		1. single-application workflow
		2. multiple-application workflow
		3. system workflows
		4. human-interaction workflows


## 3. Enactment


## 4. Evaluation

Execution Logs are crucial.
They can be used for Process Mining to find better systems.

## 5. Administration and Stakeholders


# bpm6 - EPC
EPC:  
Event-driven Process Chain, events, functions, connectors, EPC diagrams, guidelines, diagram repair, function annotations, EPML, folder-passing semantics, candidate split, corresponding split, matching split, OR-join policies (wait-for-all, first-come, every-time), examples

Ch.4.3 of Business Process Management: Concepts, Languages, Architectures

![[Pasted image 20250118181732.png]]

This chapter is an overview on the Event-Driven Process Chains (EPC) notation.

Topics
1. what is an EPC
2. EPC Diagrams
	1. ingredients
	2. requirements
	3. examples
	4. guidelines
3. EPC Semantics
4. EPC Sample Diagrams

## 1. EPC Definition

Definition
1. an event-driven process chain (EPC) is an ordered graph of events and functions
2. it provides various connectors that allow alternative and parallel execution of processes
	1. specified using logical operators such as OR, AND and XOR
3. major strength
	1. simplicity and easy-to-understand notation


## 2. EPC Diagrams

*1. Ingredients*

Blocks
1. event -> hexagon
	1. passive element
2. function -> rounded rectangles
	1. active element to describe task or activities
3. logical connectors -> logical symbols in circle
	1. describe logical relationship between branches
	2. can be splits or joins
4. control flow -> dashed arrows
	1. connecting events with functions expressing causal dependencies

![[Pasted image 20250118183240.png]]

*Requirements*

The graph must be weakly connected (eg no isolated nodes)

Furthermore
1. events
	1. have at most one incoming and one outgoing arch
	2. have at least one incident arch
	3. there must be at least one start event and one end event
2. functions
	1. have exactly one incoming and one outgoing arc
3. connectors
	1. have either one incoming arc and multiple outgoing arcs (or viceversa)

Tools
1. yED
2. VisualParadigm Online
3. ARIS Express
4. EPC Markup Language (EPML)

*Guidelines*

Other contraints are sometimes imposed
1. unique start/end event
2. no direct flow between two events
3. no direct flows between two functions
4. no event is followed by a decision node

It is safe to drop most constraints. Implicit dummy nodes might always be added later if needed to guarantee alternation.

Other ingredients
1. organization units -> ellipses with a vertical line
	1. determines the person or the organization responsible for a specific function
2. information, material, resource object -> rectangles linked to function boxes 
	1. represent objects in the real worlds
3. supporting system -> rectangles with vertical lines on its sides
	1. technical support

## 3. EPC Semantics

Folder-passing semantics
1. the current state of the process is determined by placing folders over the diagram.
2. a transiction relation explains how to move one state to the next state
	1. be careful with logical connectors

![[Pasted image 20250118184838.png|300]]

The behaviour for join connectors can be ambiguous.

Designers can further annotate EPC diagrams, called decorated EPC. In particular
1. corresponding split
	1. which node separated the flows we are joining
2. applicable policy
	1. how to trigger outgoing flow

Types of split (for a join node)
1. candidate split
	1. any split nodes whose outputs are connected to the inputs of the join
2. corresponding split
	1. chosen candidate split
3. matching split
	1. if corresponding is the same type as the join node

OR-join policies (assume every join is tagged with a policy)
1. wait-for-all (wfa)
	1. if an or-join has a matching split, it should wait the completion of all activated path
2. every-time (et)
	1. trigger the outgoing path on each input
3. first-come (fc)
	1. wait for the first input and ignore the second

OR-join assumption
1. if it has a matching split
	1. uses wfa
2. if it has not a matching split
	1. is decorated with a policy
		1. wfa is okay with any corresponding split
		2. et/fc are okay with corresponding XOR split

XOR-join assumptions
1. if it has a matching split
	1. it blocks if both paths are activated and  it is triggered by a unique activated path
	2. ANY POLICY WOULD CONTRADICT THE EXCLUSIVITY OF XOR
	3. we assume always a matching split for the xor, even an implicit one


## 4. EPC Sample Diagrams

![[Pasted image 20250118185552.png]]

...






# bpm7 - BPMN (1)
BPMN:  
Notation, swimlanes, flow objects, artefacts, connecting objects, collaborations

Ch.4.7, 5.7 of Business Process Management: Concepts, Languages, Architectures  Ch.3, 4 of Fundamental of Business Process Management. M. Dumas et al.

![[Pasted image 20250118191552.png]]

We overview the BPM Notation.

The topics will be
0. BPMN history
1. BPMN basics
2. BPMN key features
3. More on BPMN
4. BPMN semantics

## 0. BPMN history

The goal is to define a graphical notation that is readily understandable
1. by business analysts (initial draft of processes)
2. by technical developers (process implementation)
3. by business people (process management)






## 1. BPMN basics
## 2. BPMN key features




## 3. More on BPMN
## 4. BPMN semantics













# bpm8 - BPMN (2)
Exercises:  
EPC and BPMN modelling_  
  
BPMN:  
data objects, associations, groups, call acrivities, throwing and catching, choreographies_







# bpm9 - From automata to nets
Slide 8.
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





# bpm10 - Petri Nets
Slide 9

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















# bpm10 - Petri nets properties
slide 10.

-> lecture 12

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



## 1. Behavioural Properties











## 2. Structural Properties









