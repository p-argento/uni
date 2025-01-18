
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
1. a business process model consists of a set oof activity modeles and execution constraints between them
	1. like a blueprints
2. a business process instance represent a concrete case in the operational business of a company consisting of activity instances

![[Pasted image 20250118124805.png]]

![[Pasted image 20250118124839.png]]



## 2. Aggregation abstraction
Granularity levels






## 3. Vertical abstraction
separation of concerns (or subdomains)














# bpm5 - BP Lifecycle
Business Processes Lifecyle:  
levels of business processes, business strategies, operational goals, organizational BP, operational BP, lifecycle, design and analysis phase, identification, modelling guidelines, validation, simulation, verification, configuration phase, platform selection, software architecture, individual enterprise applications, enterprise resource planning system, siloed enterprise applications, enterprise application integration, point-to-point integration, hub-and-spoke integration, enterprise service computing, system workflows, human interaction workflows, testing, enactment phase, event logs, logging, evaluation phase, activity monitoring, mining, administration phase, stakeholders



# bpm6 - EPC
EPC:  
Event-driven Process Chain, events, functions, connectors, EPC diagrams, guidelines, diagram repair, function annotations, EPML, folder-passing semantics, candidate split, corresponding split, matching split, OR-join policies (wait-for-all, first-come, every-time), examples



# bpm7 - BPMN (1)
BPMN:  
Notation, swimlanes, flow objects, artefacts, connecting objects, collaborations







# bpm8 - BPMN (2)
Exercises:  
EPC and BPMN modelling_  
  
BPMN:  
data objects, associations, groups, call acrivities, throwing and catching, choreographies_





# bpm9 - From automata to nets
Slide 8.
From automata to nets:  
Inductive definitions, Kleene star, finite state automata, transition function, destination function, language accepted by an automaton, from automata to Petri nets, places, transitions, tokens_




# bpm10 - Petri Nets (1)
Slide 9 (1).
Exercises:  
BPMN and FSA_  
  
Petri nets basics:  
multisets and markings, transition enabling and firing, firing sequences, reachable markings_  
  
Woped basics



# bpm11 - Petri Nets (2)
slide 9(2)

Exercises:  
Petri nets_  
  
Petri nets basics:  
occurrence graph, modelling with Petri nets, examples and exercises_  
  
Woped basics



# bpm12 - Behavioural and Structural Properties
slide 10.

Exercises:  
modelling with Petri nets_  
  
Behavioural properties:  
liveness, non live transitions, dead transitions, place liveness, non live places, dead places_
(CONTINUES IN LECTURE 13)
deadlock freedom, boundedness, safeness, home marking, cyclicity_  

Structural properties:  
weak and strong connectedness, S-systems, T-systems, free-choice nets_





