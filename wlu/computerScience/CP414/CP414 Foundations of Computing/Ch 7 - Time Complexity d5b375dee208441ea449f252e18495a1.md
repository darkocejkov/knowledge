# Ch 7 - Time Complexity

- Decision Problems are given some instance to *solve*, which is I, and answer with either “yes” or “no”. We can measure the size of any problem input/instance, as the number of bits required to specify the entire (or encode) the instance I.

- Algorithms solve decision problems in **polynomial (finite) time** if it always will find an answer for every instance, with a maximum time complexity of $O(n^k)$, where *k* is some pos. integer, and *n* is the size of the problem instance. Essentially, this is the maximum bounding time that puts problem solving algorithms into a complexity class called **P**, which is the set of all algorithms that solve problem in *polynomial time*.
    - The class **P** is only the set of polynomial-time DECISION problems.

- Let’s think about some examples, like graph cycles.
    - Does some graph G contain a cycle?
        - we can solve this by running a BFS / DFS search algo. and look for NON-tree edges. If some non-tree edge is found, then there exists a cycle, otherwise no cycle. The algorithm can always decide the problem, and the runtime is expressed as $O(|V| + |E|)$, the number of nodes + number of edges.
    - Does some graph G contain a Hamiltonian Cycle (passes through every vertex EXACTLY once)?
        - There is no polynomial time algorithm to decide this. The only option we have is to *brute force* all the combinations of vertices and edges to see if there exists some configuration of a path that is a Hamiltonian cycle. This means that there are $n!$ combinations, so we have a maximum bound of $n!$, which is not polynomial.
    - 0-1 Knapsack problems, which give some n-tuple as output, instead of a decision (yes/no), of the subset of all items which maximizes the profits, and fits in the knapsack?
    - Rational Knapsack?
        - There exists a polynomial time algorithm
    
- If we have 2 problems $P_1, P_2$, which are not necessarily decision problems, then some hypothetical algorithm B that solves $P_2$ is called an **oracle** for $P_2$.
    - If A is some algorithm for $P_1$ that solves it, and B is an oracle for $P_2$, and B is used as a subroutine in A, then A is a **turing reduction** from $P_1$ to $P_2$.
        - $P_1 \le ^T P_2$
            - essentially saying that P1 is NOT harder than P2, and if P2 has a solving algorithm, then there must be a solving algorithm for P1.
    - A is a polynomial-time Turing reduction if the run time of A is polynomial, given that B has a *unit cost* running time.
        - $P_1 \le^T_P P_2$
            - if P2 has a polynomial time algo, then P1 must also be solved in polynomial time.

- If we have two subset-sum problems (SubS-D, decider) and (SubS-F, finder) which both take the same input, but do not output the same answers. SubS-D is a decision problem, it answers (decides) whether or not there is a subset of integers within an array that sums to an input target sum. The finder, finds the subset of values that sums to the target sum S.
    - These problems are polynomial-time Turing **equivalent**
        - $SubS-D \le^T_P SubS-F$
        - $SubS-F \le^T_P SubS-D$
            - which essentially means that they are both poly-time reducible to each other
    

## CLIQUE problems

- are ones in which we look at *subgraphs* within a graph, and try and determine if there are sets of vertices such that each pair is connected by an edge - essentially looking at complete subgraphs.
- A clique *size* is determined by the number of vertices in a clique.

- There are three different questions we can try and look for:
    - Decider (graph, integer)
        - Does there exist a clique within this graph of size integer? (yes, no)
    - Optimizer
        - What is the **size** of the largest clique within this graph? (int)
    - Finder
        - What is the set of vertices that forms the largest clique (set)
- These three questions are all poly-time reducible to each other.
    - Because the decider is reducible to the optimizer, we can implement the decider as a function that uses the optimizer as a subroutine (black-box)
    - The optimizer is then reducible to the decider.
    - The finder is reducible to the optimizer
- This illustrates a key-point about the fact that the ‘harder’ problems of optimization and finding are poly-time reducible if we have some efficient polynomial-time decider algorithm that can be used to reduce the others.
    - HOWEVER, there does NOT exist a real algorithm that decides cliques in polynomial time, so in reality, those three problems are equally as difficult.

## Travelling Salesperson problem

- Hamiltonian Cycle on some graph given edge weights, finding the path that takes the least cost.
- Three problems:
    - Optimization
        - Finding the Hamiltonian cycle with *minimal* total weight
    - Optimal Value
        - Finding the minimal total weight of ham. cycles
    - Decision
        - Does there exist a ham. cycle, whose weight is $\le$ a given target weight?
- There is no poly-time algorithm for the decider.
- However, they are poly-time reductions
    - $TSP-Optimal Value \le^T_P TSP-Decider$
    - $TSP-Optimization \le^T_P TSP-Decider$

- Certificates are some form of extra information which makes it easy to verify that some instance is a yes-instance.
    - The cert. verification algorithm shows that $V_{er}$ is an algorithm that verifies certificates specifically for yes-instances of problems. Then, $V_{er}(I,C)$ outputs “yes” if I is a yes-instance and C is a valid certificate for I, however, if it outputs “no”, then it is the case that:
        - either I is no-instance, or
        - I is a yes-instance and C is not a valid certificate

## Complexity Class **NP**

- Cert. Ver. Algo. is said to solve a decision problem P provided that for every yes-instance I, there exists a certificate C such that Ver(I,C) outputs “yes”, and for every no-instance I, and for every certificate C, Ver(I,C) outputs “no”
- The complexity class NP is the set of all decision problems such that have poly-time certificate ver. algorithms solving them.
    - $\Pi \in NP$ if the decision problem $\Pi$ is in the complexity class NP
- It’s important to note that we do not require to *find* a certificate for a yes-instance in poly-time, we are “given it”. So, the importance is the ability to **verify** a certificate.

## Certificate Algorithm for Subset Sum

- A certificate would consist of an array B, which is an array of the same size of the input array, but whose elements are *bits* either 0 or 1. This bit-set is a representation of the original set, whose elements are included in the subset-sum if the corresponding bit-element is 1.
- For 1 to n, we subtract from S (target sum) a[i]*b[i]. We return the statement S == 0 (t/f).
    - When b[i] is 1, we subtract from S the value of a[i], but not if b[i] is = 0.
- This is an algorithm in O(n) time because it iterates once for every member of the array
    - Thus, $SubS-D \in NP$

- NP can be considered a class of decision problems that have **polynomial-time NON-deterministic decision algorithms**, whereas P is a class of decision problems that have polynomial-time DETERMINISITIC decision algorithms.
    - as in (non-deterministic) polynomial-time means NP

- Non-determinism in verifiers/algorithms looks like a tree graph of doubling, where it continues branching until *n* depth, at which it can express all possible combinations of certificates. If the non-deterministic tree then accepts for any of the generated certificates, then for that node, there exists a valid certificate for a yes-instance.
- Any decision problem in P, is also in NP
    - $P \subseteq NP$
        - this means that for any decision problem in P, we can create some verifier for instances of that problem by making dummy certificates and calling the decider for each certificate - and if the decider outcomes as ‘yes’, then the certificate is valid for that instance, otherwise it is not.
        - This verifier runs in polynomial time - the same time as the decider and verifies yes instances, so therefore, we can always construct verifiers for any decider problems in P, which puts them into NP.
    - This also makes sense on the “non-determinism” level, because any “deterministic” algorithm is non-deterministic, but does not use non-determinism.

- The class NP is unknown whether or not it is equal to the class P, but there are certain special problems which possess unique features that make them harder than P, and these are called NP-complete problems.
    - NP-complete problems all have a special feature that shows:
        - If NP-complete problems have a polynomial time deciders, than ALL problems in NP have polynomial time deciders, and thus $P = NP$
        
- Polynomial Time computable functions are those in which a function exists such that some poly. time Turing Machine exists, that halts with only f(w) on the tape, on some input *w*, meaning that it finishes in polynomial time.
- Polynomial time mapping reducible languages are languages in which $A \le_P B$ if a polynomial time computable function exists for every *w:*

$$
w \in A \iff f(w) \in B
$$

- which means that *f* is a poly time reduction of A to B.
    - A is not harder to decide than language B.
    - essentially, yes-instances of A are mapped to yes-instances of B.
    - This means that we can map instances of A to an instance of B by some function, and use a decider of B to produce an answer for the instance of A.

- $Clique \le_P Vertex-Cover$
    - We can find some time reductive function that maps instances of Clique (complete subgraphs) to Vertex Cover instances, and if we have some polynomial time decider for clique, that automatically means that clique has some polynomial time decider.

- Polynomial Time transformations have 2 important properties
    - $P_1 \le_P P_2$, and $P_2 \in P$, that means that $P_1 \in P$
        - essentially since P1 is not harder than P2, and P2 has a poly-time decider that puts it into complexity P, then P1 must also be in P.
    - $P_1 \le_P P_2$ and $P_2 \le_P P_3$, then $P_1 \le_P P_3$
        - the transitive property of poly time transformations.

- Languages are NP-complete if it has the two following conditions:
    - it is in NP
    - and every A in NP, is polynomial time reducible to B
        - essentially that any other problem in the same complexity class is not harder to solve than each other.

- Thus, if we have any language that is NP-complete, and B has a polynomial time decider, than P = NP
    - however, this does not imply that NP-complete actually exists, so we need some examples of problems that are NP-complete to know that NP-complete set is not empty.

## Satisfiability problem (NP-Complete)

- variables can be either TRUE or FALSE (boolean), True = 1, False = 0.
- boolean operations AND, OR, NOT
- boolean formulas are expressions that combine boolean variables and operations to outcome to a single boolean value
    - this value depends, like a function, on the different possibilities of the input variables
- boolean formulas are **satisfiable** if some assignment of 1s and 0s makes the formula evaluate to 1.
    - essentially, is there any combination of 0s and 1s that makes the formula evaluate to true?
- thus, the satisfiability problem is a test to whether or not a boolean formula is satisfiable?
    - that is for any arbitrary formula, can we find any combination of input possibilities to find a configuration that evaluates to true?

- Any problem in NP-complete, is then reducible to the SAT problem.
    - that is, we can create a formula between any NP-complete problem and the SAT problem to show that if the SAT problem has a decider in poly-time, then all other NP-complete problems are poly-time reducible, and thus P = NP.

## Cook-Levin Theorem

- SAT is NP-complete
- thus, since we know that SAT is NPC, then to show any problem A is in (or is not in) NP-complete, its sufficient to show that
    - A is in NP
    - $SAT \le_P A$

## 3SAT problem

- special case of the SAT problem, where formulae are in special forms.
    - Literals are boolean variables, either normal or negatived
    - Clauses are several literals connected with ORs.
    - Conjunctive-Normal-Form (CNF) is a form that formulas than be in, it it combines several clauses connected by ANDs
    
    $$
    (x_1 \lor \neg x_2 \lor \neg x_3 \lor x_4) \land (x_3 \lor \neg x_5 \lor x_6) \land (x_3 \lor \neg x_6)
    $$
    
    - A 3CNF formula is even more specific, in which all clauses have 3 literals.
    
- Thus, the 3SAT problem is one in which we judge the satisfiability of 3CNF formulas.

- 3SAT is NP-Complete
    - must show that 3SAT is in NP
    - and that SAT $\le_P$ 3SAT
        - To show some polynomial time transformation we need to construct some time transformation such that it does not take exponential amounts of time
        - this is shown easily by the fact that any formula not in CNF can be converted into 3CNF by some transformation algorithm, and that transformation itself is in polynomial time.
    

NP-Complete Problems

- SAT
- 3SAT
- Vertex Cover (VC)
- HAM
- TSP-D
- Clique
- Subset-Sum