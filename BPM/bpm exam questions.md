01-03-25
Answering on paper the questions from telegram.

*to be reviewed*
1. stable sets
2. s-invariants properties

*PETRI NETS*
1. Introduction
	1. marking equation lemma PROOF
	2. monotonicity lemma PROOF
2. Invariants
	1. define S-invariants and fundamental property
	2. s-invariants boundedness theorem PROOF and example
	3. s-invariants liveness theorem PROOF
	4. reproduction lemma of T-invariants PROOF and its relevance in process analysis
3. soundness
	1. workflow net definition
	2. formally express the soundness requirements
	3. draw a net that satisfies no dead tasks, option to complete but fails to satisfy proper completion
	4. main theorem (3 PROOFS)
4. S-systems and T-systems
	1. S-systems: cosa sono, cos'è x e N, proprietà fondamentale,  boundness e liveness con dimostrazione.
	2. s net e boundedness, trasposte in WF net e soundness nelle s net
	3. - S-net: cos’è e cosa ci dice su invarianti, boundedness, liveness, soundness
	4.  T-system: definizione e proprietà fondamentale
5. free-choice nets
	1. what is the Rank Theorem
	2. algorithm to find max unmarked siphon
	3. siphons (definition, properties and algorithm to find max unmarked siphon)
6. diagnosis
	1. TP-handles and PT-handles and discuss potential issues associated with them about soundness
	2. s coverable e s component


*OTHER TOPICS*
1. business process
	1. process lifecycle in business process from design to validation
	2. actors of the business process
	3. business process life cycle validazione, simulazione verifica e ruoli relativi
2. abstraction
	1. describe the different types of abstraction (vertical, horizontal, aggregated) in process modeling
3. EPC
	1. Compare and contrast EPC and BPMN.
	2. What strategies can be used to translate an EPC into a Petri net?
	3. How are OR join policies handled in EPC?
4. cycle time (quantitative analysis)
	1. How do you conduct a quantitative analysis (cycle time and cost analysis) in business process models?
	2. How is cycle time calculated in different process structures (sequential, parallel, XOR, loops)?
	3. What is Little’s Law and what is the assumption?
5. cost analyisis
	1. How can cost analysis be approached, considering factors
	2. rework probability?
	3. Cost analysis (sequenza, parallel, xor, rework con formule)
6. process mining
	1. alpha-algorithm (describe the role of process mining and explain how the alpha algorithm uses the footprint matrix)
	2. footprint matrix (4 types of relations)







*11-03-25*
Collecting questions from telegram

- spiega il progetto
- nel progetto è importante che ogni pool abbia un inizio ed una fine, teoricamente ogni pool potrebbe esser svolto indipendentemente dal resto, la traduzione e l'analisi sound va fatta su ogni pool e non solo sul flusso complessivo.
- definizione Workflow Net
- condizioni Sound con le proposizioni logiche
- disegna una rete che rispetti 'No dead task' e 'Option to complete' ma non rispetti 'proper completion'
- dimostrazione Marking equation lemma
- spiegare le sottofasi dell'Analysis and Design nel ciclo di vita del business process model

- Differenze EPC e BPMN
- Strategie di traduzione EPC in rete di Petri
- Politiche OR join 
- S-Invariant: boundedness con proof 
- S-systems: liveness + disegno di una Snet con t non live
- Rank theorem e siphons
- Legge di Little

- discussione progetto
- refinement e abstraction con esempi su carta (slides 15) anche usando and-split/join ecc.
- Monotonicity lemma 1 con dimostrazione
- Soundness formalmente
- Disegna un net sound ma che non rispetta proper completion
- Cost analysis (sequenza, parallel, xor, rework con formule)
- Termini per trasformare da BPMN a PetriNet
- astrazione (3 tipi)
- PT/TP handles e relativi problemi

- Discussione del progetto con particolare focus su errori
- analisi quantitativa con particolare riferimento alle dimensioni, l'analisi del cycle time e delle differenze con quella dei costi
- Soundness, le tre proprietà che la caratterizzano e come vengono espresse anche in formula.
- Tp e Pt handle, cosa sono, esempio pratico e quali caratteristiche della soundness vanno a violare
- partizionamento verticale e orizzontale 
- S-invariant, cosa sono, cos'è x e N, proprietà fondamentale,  boundness e liveness con dimostrazione.

- discussione del progetto
- s-invariant, cosa sono, proprietà fondamentale, liveness, boundedness
- main theorem workflow net
- disegnare un workflow net non live
- astrazione orizzontale
- time come dimensione nell'analisi quantitativa
- come calcolare il cycle time a seconda delle situazioni 
- legge di Little

- Progetto: discussione e domande sulle proprietà delle net
- Orale:
- Main theorem (parte 2 e 3)
- S-system/net
- T-system/net
- Soundness 
- Process analysis (tempi e costi)

Spiegazione progetto e domandina riguardo ad una implementazione differente rispetto a quello che era stato fatto
1) analisi quantitativa e cycle time, come si computa il costo al variare dei blocchi(sequenze, and, or split, loop)
2) main theorem con prova solo della terza fase
3) traduzione EPC in petri, strategie e stili

Explanation of the project starting from petrinet and semantic analysis of the final workflow net
Oral Exam:
1) Quantitative Analysis(Average Activity cost calculation of both alternation and Parallel loops)
2) Little's law assumption
3) 3 important properties of Soundness 
4) To draw a petri net which holds no dead task, option to complete but doesn't  hold proper completion
5)difference between EPC & BPMN
6)Elements of EPC

-performance analysis (dimensions)
-cycle time analysis (all paths)
-cost analysis 
-little's law
-horizontal abstraction
-soundness
-draw petri net with no proper completion
- epc, elements
-difference epc and bpmn
-marking equation lemma 
-liveness in s-nets

regarding project:
 - description of BPMN diagram;
 - questions on how you would ensure proper completion after slight modifications of diagram;
 - strategy adopted to translate BPMN to Petri Net (whether translating straight up from diagram or trying to follow some net type to ensure soundness, e.g. S-systems, Free-choice systems etc.);

about theory:
 - S-invariants: definition, fundamental property, theorems on boundedness and liveness;
 - Parikh vector and Marking Equation Lemma (proof by induction);
 - Rank theorem: necessary and sufficient conditions and their computational time;
 - definition of syphon and fundamental property; computational cost to ensure syphon condition in Rank theorem;
 - types of costs in business activity, cost analysis through flow analysis, Little's law;
 - business process lifecycle; where EPC/BPMN, translation into Petri nets, process mining take place along the cycle;
 - process mining and validation/enactment: what role processes and models play in the different approaches;

- description of our bpmn diagram and our petri nets
-  if soundness property are verified in our petri net and why
- if our net is a S-net and if it is always sound for this reason 
- how is Woflan and if woflan is faster than woped
- if we made bpmn graph immediately or we thought a bit more 

-s-invariant + fundamentals property 
- s-invariant boundness theorem + proof
- s-invariant liveness theorem + proof
- what is the type of the s-invariant? Positive s-invariant
- draw a net with: no dead task, option to complete but not proper completion
- are there some TP handle or PT handle ? And what are tp and pt handle
- what happens if we add the reset transition 
- draw the previous net with pt handle
- what happens if we add the reset transition 
- BP lifecycle 
- horizontal abstraction
- what level does our network fall into?
- what level does the bpmn language fall into?

- tell me about one of the pools in the BPMN diagram of the project 
- how did you modify the diagram at the end

- s-invariants + fundamental property
- s-invariant boundedness theorem + proof
- s-invariant liveness theorem
- relation between liveness and place-liveness
- rank theorem + clusters
- how does alpha-algorithm work in process mining (not in details)
- horizontal abstraction

- esposizione bpmn graph 
- Esposizione wf net
- spiegare perché il wf module non è free choice 
- marking equation lemma 
- condizioni soundness 
- s coverable e s component
- rank theorem 
- cluster 
- pt handles e TP handles 
- little's law

- monotoniciy lemma con dimostrazione 
- S net ed S invariant 
- WF live and bounded , sound , main theorem  
- EPC
- BPMN 
- errori sul Progetto

- Condizioni soundness 
- Astrazioni verticale orizzontale e aggregata 
- Diverse traduzioni dell’epc 
- Or policy
- Definizione di workflow net
- Theoretical cycle time

- Tante domande sul progetto (se è s-net/t-net/free-choice e perché)
- Relazione liveness e deadlock freedom
- Little's law
- Ruoli business process (soprattutto nel momento della validazione)
- Differenze EPC-BPMN

- descrizione bpmn
- come è stato valutato su woped
- business process life cycle validazione, simulazione verifica e ruoli relativi
- cost analysis
- tipi di costi
- rework probability
- deadlock freedom e boundedness definizione
- s systems 
- t systems 
- marking equation lemma
- boundedness lemma

- descrizione bpmn
- come è stato valutato su woped
- business process life cycle validazione, simulazione verifica e ruoli relativi
- cost analysis
- tipi di costi
- rework probability
- deadlock freedom e boundedness definizione
- s systems 
- t systems 
- marking equation lemma
- boundedness lemma

- discussione del progetto
- Soundness by construction
- T-system: definizione e proprietà fondamentale
- EPC
- differenze EPC/BPMN

- discussione del progetto
- definizione di soundness
- disegnare un processo che non rispetta la proper completion
- marking equation lemma con dimostrazione
- s-invariant definizione e proprietà
- analisi di costo
- Little's law

- Discussione progetto + qualche domanda sulla struttura dei net (5min)
- 3 condizioni che dicono che una rete è una WF net è condizioni soundness
- Teorema principale della soundness 
- Come si dimostra che se N è sound allora N* è bounded
- Monotonicity lemma
- Nel caso degli S-systems, è possibile che la rete sia unbounded ? 
- Caratteristiche notazione EPC, se avessimo voluto usarla nel progetto che difficoltà (se presenti) avremmo incontrato? 
- Come si rappresenta un event-based gateway in EPC? 
- Cosa si intende con l’attività di Business Process Modeling? 
- Quali caratteristiche devono essere rispettate nel BPMN? 
- È opportuno assegnare dei ruoli di responsabilità per le varie attività?
- Tipi di astrazione + dettagli astrazione verticale

-Main Theorem con dimostrazione di parte 2 e 3
-Condizioni di Soundess
-CTE e TCT e come calcolare costi
-process Mining (a grandi linee)
-S-net, definizione e dire per quali condizioni è bounded e live
-S-Invariants, definizioni e dire quando è bounded e live 
-astrazione aggregata e orizzontale

- definizione di soundness
- disegnare un processo che non rispetta la proper completion
- s-invariant definizione e proprietà liveness (senza proof) e bounded (con proof)
- S-net, definizione e invarianti 
- tp + pt handles 
- Little's law
- Process mining
- astrazione orizzontale

Project discussion (15 min): 
- Pool explanation of BPMN diagram
- Could lanes be substituted with pools?
- Conversion to WF nets
- Potential problems of using EPC instead of BPMN

Theory (15 min):
- EPC in general, OR policies and meanings
- BPMN key features, markers and so on
- S-invariants, properties, liveness and boundedness thms
- Soundness conditions formally and intuitively
- Main theorem, proof of soundness implies liveness of N*
- Quantitative analysis, avg cycle time based on different flow patterns, flaws of flow analysis and Little’s Law

- presentazione di una delle pool degli attori del progetto (versione base + variante) 
- S-net: cos’è e cosa ci dice su invarianti, boundedness, liveness, soundness
- Reti free choice come dire qualcosa sulla liveness + boundedness (-> Rank Theorem)
- Cos’è un cluster e un sifone 
- Algoritmi per risolvere condizione dei sifoni del rank theorem in tempo polinomiale 
- (dopo avermi chiesto se avevo fatto la parte di process mining:) Cos’è e come è costruita la footprint matrix dell’alpha algorithm
- astrazione orizzontale

- s-invariant boundedness e liveness
- t-invariant e reproduction lemma
- s net e boundedness, trasposte in WF net e soundness nelle s net
- rank theorem dimostrazione e codice del 3 quesito 
- quantitative analysis con argomentazione sul cycle time
- foot print Matrix proprietà


- TP-handles and PT-handles, well-handledness and well-structuredness
- Free-choice nets, definition + Rank Theorem conditions. Why is it important? (Because it can be used to prove liveness + boundedness in polynomial time)
- Explain (loosely, no need to write) the algorithm to find the maximal initially unmarked proper siphon in the net
- S-invariants, definition and how they relate to boundedness/liveness of a system
- EPC, what are the main elements
- OR join in EPC, what policies can be used
- Methods to translate EPC diagrams into wf nets, explain main style differences
- Soundness conditions
- Main theorem, what are the three steps of the proof, and explain the proof of N sound => N* live
- α-algorithm, what are the four types of relations among pairs of activities

- What is a workflow net 
- Write down the formulas of 3 requirements of soundness 
- Draw a net that satisfies no dead tasks, option to complete but fails to satisfy proper completion
- Draw 2 nets with pt tp handles, what are the potential problems with them 
- S net properties
- Bpmn vs epc differences 
- Explain footprint matrix
- 3 types of abstraction
- Reproduction lemma

- Project discussion: 
- Comment two pools from bpmn model + carefully explain translations of various connectors and decorations to the workflow net

- Theory: 
- S-nets (definition + properties), S-invariants (definition + theorems on boundedness and liveness).
- Siphons (definition, properties and algorithm to find max unmarked siphon). 
- Soundness (three conditions + draw net without proper completion). 
- Event-based gateway in epc. 
- Description of epc semantics (functions, events, or policies). 
- Quantitative analysis (cycle time).
















