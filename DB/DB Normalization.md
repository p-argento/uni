Outline
1. functional dependencies
	1. defining a fd
	2. satisfying a fd (for a specific instance)
	3. expressing a fd (in english)
	4. manipulating fd (with the rule)
	5. examples of fd
2. keys and other definitions
	1. schema R
	2. complete fd
	3. superkey (it is a set of A)
	4. key
3. implications vs deductions
	1. implication definition
	2. Armstrong's axioms
	3. deduction (or inference or derivation) using axioms
	4. examples
	5. correctness and completedness of axioms
4. closures
	1. closure of FD
	2. closure of X (set of attributes A)
	3. fundamental theorem
	4. algo for computing closures of X (slow closure)
	5. finding a key
	6. prime attributes
5. equivalence p.17
	1. equivalence of sets of FD
	2. redundant and extraneous attributes
	3. canonical covers
6. decomposition p.22
	1. lossless join decomposition definition
	2. binary decomposition theorem
	3. projection of FD
	4. preservation of FD
	5. bcnf
	6. analysis algo
	7. 3nf
	8. synthesis algo

## Type of exercises
*ex1*
Consider the relational scheme R(A,B,C,D,E) 
with the following FDs: CD->A, CA->B, CD-> E, BA->C 
a) Find one key for R 
b) Knowing that the prime attributes are {A,B,C,D}, tell if the scheme is in 3NF or in BCNF. 
c) Apply the analysis algorithm to the scheme and tell whether the decomposition preserves the dependencies. 
d) Apply the synthesis algorithm to the scheme.

*ex_corrected_20240514*
Consider the following relational scheme (the set of functional dependencies constitutes a canonical cover): R< ABCDE, { AB->C, AC->B, AB->D, D->A, E->B } > 
1. Find at least one key 
2. Knowing that the set of prime attributes is { A,D, E }, check which normal forms are respected by the schema 
3. Apply the synthesis algorithm 
4. Apply the analysis algorithm and tell if the dependencies have been preserved