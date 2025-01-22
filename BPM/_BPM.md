> All models are wrong, but some are useful

[BPM Didawiki](https://didawiki.di.unipi.it/doku.php/magistraleinformaticaeconomia/mpb/start)
[[BMP Program]]
[[BPM Book Exercises]]

[[BPM Lectures on BP, EPC, BPMN]]
[[BPM Lectures on Petri Nets]]
[[BPM Lectures on Workflow Nets]]


# slides
Intro
1. intro
2. business-processes
3. examples
4. modelling
5. lifecycle
6. epc
7. bpmn-part1-part2
Petri Nets
8. nets-intro
9. petri
10. properties
11. net-matrices
12. invariants
WF Nets
13. workflow-nets
14. workflow-nets-analysis
15. workflow-nets-construction
Properties of nets
16. s-systems
17. t-systems
18. aux-p-np
19. free-choice
Workflows modules
20. workflow-systems
21. bpmn-analysis
22. wfnets-diagnosis
23. process-mining
24. quantitative-analysis





# Orchestration vs Choreography
*Orchestration* is about INTRA-organization process.
No interaction with others.
The focus is on streamlining of internal processes, eliminating invaluable activities and allocating to the right people.
*Choreography* is about INTER-organization process.
B2B process.
The focus is on communication aspects and interoperability.

# Business Process Definition
> A business process consists of a set of activities that are performed in coordination in an organizational and technical environment.
> These activities jointly realize a business goal. Each business process is enacted by a single organization, but it may interact with business processes performed by other organizations. 
> - Weske

> business process management includes concepts, methods, and techniques to support the design, administration, configuration, enactment, and analysis of business processes. 
> - Weske



---


Liveness = every transition can fire in the future.
dead = it will never fire

For places, a place is live if it can become unmarked.

Transition-live and place-live. Similar but not the same.
Transition-live implies place-live.
It is possible to draw a net that is place-live but not transition live.
If a transition does not appear in the coverability graph then it's dead.

Deadlock ???



---









