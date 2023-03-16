# 0 = Introduction

# Automata, Computability, & Complexity

> What are the fundamental capabilities & limitations of computers?
> 
- Complexity Theory
    - The difficulty of solving different kinds of problems, classifying problems as **easy** or as **hard** problems.
        - Sorting is easy, there is a logical algorithm to sorting an infinite amount of numbers. No matter how many numbers there are, there is a definite solution to the problem (all numbers are in the specified order), and there is always a method to sort a list of numbers, no matter how large.
        - Scheduling problems, such that no two classes take place in the same room at the same time, are much more difficult. There is no obvious solution, because there are many more variables here to consider, so we cannot tell if it is even possible from a broad sense.
    - Complexity theory is about understanding what makes some problems harder than others, and applying that to a computational lens.
    - There are different properties of problems that can classify them as being computationally hard, some problems have specific areas or variables that make them too hard to solve, and changing those can make the problem easier. We can also think about finding an *approximation* of the solution rather than the true solution to a problem, since approximations are mostly easier. Some problems are also easy most of the time, and are only hard in the worst-cases.
    - Cryptography is a discipline which prefers the hardest problems, because the point of cryptography is to be able to encrypt something so well, with an unbreakable cypher that you cannot solve backwards without the secret key.
- Computability Theory
    - Understanding the limits of computation, by classifying problems that are **solvable** or as **unsolvable** problems by strict computation.
- Automata Theory
    - The models of computers reduced to their most discrete units, coupled with their properties and definitions that make them computers.
    - **Finite Automaton**
        - models that are used for text-processing, compilers, hardware
    - **Context Free Grammars**
        - programming languages, AI

# Mathematical Notation and Terms

- Sets
    - groups of things, can contain any objects, and even other sets. The objects in a set are **elements**
        - $S = \{7, 21, 57\}$
            - $7 \in S$
        - $A \subseteq  B$  means A is a subset of B, if and only if all the elements of A are also elements of B
        - Sets with no regard to the number of occurrences of an element (repeats allowed) is called a **multiset**
        - $\empty$ or $\{\}$ means the **empty set**
    - Some operators include
        - Union ( $A \bigcup B$)
            - represents the combination set of all members/elements of A and B together
        - Intersection ($A \bigcap B$)
            - the *intersection* of A and B is the elements BOTH have in common
        - Complement
            - $\overline{A}$ is the complement of A, which is all the elements that are NOT in A
    - Sequences are ***ordered*** sets of elements
        - $(7,21,57)$
        - *k-tuples* can be finite/infinite *sequences*
    - Power Sets
        - a power set of A for example, is a set containing all the subsets of A
            - $A = \{0,1\}$
            - $Power(A) = \{\empty, \{0\},\{1\},\{0,1\}\}$
    - Cartesian/Cross Product
        - of two sets, A and B ($A \times B$ ), is the set of ALL ORDERED PAIRS, where the first element of each ordered pair is an element of A, and the second of the pair is a member of B.

- Functions
    - are an input-output relationship between objects. Functions take an input, and transforms it to produce an output. The same inputs ALWAYS produce the same output.
        - $f(a) = b$ means that the function of input *a* produces output *b*.
    - functions can also be considered a **mapping** of objects, if $f(a) = b$, then input a maps to output b.
    - the set of all possible inputs to a function is its **domain**, whereas the set of all outputs a function produces is the **range** of the function
        - $f : D \rarr R$
            - a function *maps* its *domain* to its *range*.
        - functions do not have to map all of the domain to the range. If a function does map the domain onto the entire range, it is called an **onto** function.
    - When the domain of a function is a result of a cartesian product of two (or more) sets, then the input to that function is a *k-tuple*, where each element in that tuple is an **argument** to *f*. Functions with *k* arguments, are *k-ary functions*, with the number of arguments being called the “Arity” of the function.
        - k = 1, unary
        - k = 2, binary
    - functions have two main notations
        - infix notation: operator placed BETWEEN arguments
            - a + b
        - prefix notation: operator precedes arguements
            - add(a, b)
    - **predicates / properties** are functions that have a range of $\{ TRUE, FALSE\}$. For example, the property *even* can be either true or false, depending on whether its input is an even number (true) or odd number (false)
        - properties that have domains of *k-tuples* are called **relations**, and are *k-ary relations*. 2-ary relations are binary relations.
            - for example, “<” is a binary relation, as it tests whether $A < B$ is true or false.
        - Rock-Paper-Scissors is an example of a relation, in which both players will simult. pick from the set {ROCK, PAPER, SCISSORS}, and the relation is based on the precedence each element has on the others.
    - Equivalence Relations are special, because they impose the idea that the two objects being compared are equal in some sense. Equivalence relations must satisfy these three conditions:
        - **reflexive**
            - if for every *x,* xRx (x relates to x)
        - **symmetric**
            - if for every x AND y, (xRy) implies (yRx)
        - **transitive**
            - if for every x, y, and z, (xRy) and (yRz) implies (xRz)

- Graphs
    - are sets of points that have connections to each other. Points are called **nodes** or **vertices,** and their connections are edges. Not all vertices must have edges to all other vertices.
    - The number of connections/edges a vertex has is its **degree**.
        - two nodes cannot have more than ONE edge, but sometimes some nodes can have a **loop**, meaning that they connect to themselves.
    - Given a graph G with nodes *i* and *j,* the tuple-pair $(i,j)$ denotes that G has an edge between i and j.
    - Subgraphs are graphs whose nodes and edges are a subset of another graph
    - Paths are *sequences* of nodes in a graph, nodes in sequence MUST be connected by an edge.
        - Simple paths do not repeat nodes.
    - This leads us to define if a graph is *connected*, which means that every two nodes have a *path* between them (you can get to any node, starting from any node)
    - Paths become *cycles* if the path starts and also ends with the same node. Simple cycles are one in which there are at least 3 nodes, and the cycle ONLY repeats the first and last.
    - Graphs are called **trees** if they are *connected*, but there are no *simple cycles*.
    - Graphs are *directed graphs* when we use arrows to denote directions of edges, meaning they are “one-way”.

- String & Languages
    - Strings are very important to computer science
    - an **alphabet** is any non-empty finite set, whose elements are **symbols** of that alphabet.
        - $\Sigma = \{0,1\}$
    - a string over an alphabet is a finite seq. of symbols from that alpha, without commas.
        - 01001 is a string over $\Sigma$.
    - if *w* is a string over $\Sigma$, then the length of *w* is denoted $|w|$, and is defined as the *number of symbols* it contains.
        - the empty string has 0 length: “”
    - the *reverse* of a string *w* is obtained by writing the symbols of *w* in reverse order
    - a *substring* of *w* is a string whose symbols are in *w*, and MUST appear in the same, contiguous order
        - “abcdefghijklm” = w, a substring can either be: “abc”, “ghi”, “def”, but NOT “amkb”
    - The **lexicographic order** of string depends on the sequence of the alphabet we use. We can order/sort strings based on the symbols they contain based on lex. order
        - we can also use something called **shortlex order** or **string order** that is a modification to how we sort strings, and that means we can make shorter strings come *before* longer strings
            - if the alphabet $\Sigma = \{0,1\}$, then the shortlex order is: $(\empty, 0, 1, 00, 01, 10, 11, 000, ...)$
    - a string *x* is called a **prefix** of a string *y*, if there is a string *z* such that $xz = y$ (for example, “abcdef” = y, then “abc” + “def” = “abcdef”)
        - *x* is also a **proper prefix** if $x \ne y$.
    - Languages are *sets* of strings, which are *prefix-free* languages if no elements of that language are proper prefixes of another element.

- Boolean Logic
    - the boolean/binary logic values of only TRUE and FALSE
        - can be represented by any two, mutually exclusive symbols like $[0,1]$.
    - Boolean logic relies on dichotomy, answers or situations in things that result in mutually exclusive results, YES/NO, HIGH/LOW, etc.
    - Boolean Operators compare the two values, and output TRUE or FALSE themselves based on the inputs
        - NOT (negation) → (NOT TRUE = FALSE), (NOT FALSE = TRUE)
        - AND (conjunction) → (TRUE AND TRUE = TRUE), (TRUE AND FALSE = FALSE), (FALSE AND FALSE = FALSE)
        - OR (disjunction) → (TRUE OR FALSE = TRUE), (TRUE OR TRUE = TRUE), (FALSE OR FALSE = FALSE)
    - this logic also requires it to use *operands*, which can be any arbitrary state of logic, or some sort of predicate.
        - P = “The sun is shining”
        - Q = “Today is Monday”
            - P and Q → “the sun is shining and today is monday” (result in true only if both are true)
            - P or Q → “the sun is shining *or* today is monday”
            - NOT P or Q → “the sun is NOT shining or today is monday”
    - another operator that is very useful, that can be built by just using NOT, AND and OR is the exclusive OR (XOR)
        - results in true ONLY if either operands are true, BUT NOT BOTH.

# Practice Problems

- Problems From Textbook