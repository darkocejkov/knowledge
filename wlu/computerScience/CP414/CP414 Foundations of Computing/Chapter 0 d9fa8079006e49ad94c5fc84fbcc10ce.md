# Chapter 0

# Alphabets, Strings, & Problems

Alphabet: $\Sigma = \{0,1\}$

- Strings are any sequences usings the characters in that alphabet
- Languages are sets of strings over a single alphabet, that satisfy some property
    - for example, a language can have the property that all its strings are of odd length:
        - $L1 = \{0,1,000,001,011,100,010,...\}$
    - or strings with an equal number of 0s and 1s
        - $L1 = \{01,10,0011,0101,1010,...\}$
    - An important part about language is that given a property of a language, and a string over an alphabet, can we verify is a string is part of that language
        - “Membership testing”

Why is all this notation important for understanding the fundamental units of computation? Because it allows us to build our own language of pseudo-code, that is free of any concrete languages. Essentially, we build from the ground-up, the logic and language to be able to construct the lowest-level solutions for problems, which will dictate whether or not we can solve those problems with computation.

- Problems in computer science often give us an *instance* about that problem, and to solve it, we need to find its solution through some task
- the instance of a problem is a set of inputs for the specific problem, and the solution is an output which satisfies all properties of the problem
- Algorithms are step-by-step processes that carry out computations given the appropriate input
    - for example, an algorithm for sorting a list, given a list of objects, requires that we carry out *computations* such as *comparisons* to compare numbers based on the scale of the object itself. For example, sorting a list of numbers is inherentely simple, since numbers have order. Number comparison at the lowest levels of hardware are done through adding, which is in itself, a computation.
    - Algorithms solve problems, if for *every instance of that problem*, the algorithm can find a valid solution within a FINITE time. Any problem can be solved through brute force (combinations, for example), given an infinite amount of time.

An important class of problems are **decision problems**, for which they can have any kind of input, but must output either *yes* or *no*, answering the question of the problem. For example “Does this string have *odd length*” or “is this number *prime*”?

- YES instances of problems can have *solution sets* with correspond with a language of strings.
- Input to a problem is like a string that *encodes* the input.
- Membership tests are decision algorithms for the problem in that case.
    - For example, the input to the problem can be all sets of strings of a binary alphabet, and the yes-instances of this problem are specific strings of that language that pass the property of the problem, which are their own solution-languages themselves.
- Decision problems are fundamental to problems themselves, as we can transform any problem into a decision problem for the same input, and they are not restrictive, since understanding the solution to transformed-decision problems, can help inform us on strategies to find solutions for the non-decision variants of problems.

Proof: There are *undecidable* decision problems, meaning that there are problems in which there is no answer

<aside>
❕ Countability

Countable sets are NOT finite sets. Countable sets are INFINITE actually, because there exists a function that can map *each element of the set*  to the set of natural numbers. Essentially, there is a pattern that you can take (the function) to define it’s form. For example, the set of rational numbers, because there is a function that can map those numbers to the rational numbers. Uncountable infinite sets are things like the $\R$ or $\Complex$, because there is no pattern able to *explicitly* write all the reals.

Integers are either even, or odd, so the bijective function can be (2m) for even numbers, and (2m+1) for odd numbers.

This leads to the idea of different sizes of “infinity”, where infinite sets that are countable, are smaller than uncountable infinite sets.

</aside>

<aside>
❕ Cardinality

The number of elements of a set.

</aside>

<aside>
❕ Counting argument

Consider the set of *all decision problems*, which are equivalent to languages over a fixed alphabet, is this set countable? No, it is infinite, or uncountable. Because it is the cardinality of a set of *infinite sets* over an alphabet, since each language is itself, uncountable. This is equivalent to talking about the cardinality of the set of real numbers, which is uncountable.

Now consider the set of all decision algorithms, which are represented by finite strings. This is countable, because each language itself is countable. 

This leads us to see that there are infinite decision problems, but a finite amount of decision algorithms. Functionally, this means that not every problem will have an algorithm for it, so not every problem is solvable, and thus, not every language is decidable.

</aside>

Problems may also have specific *encodings* of alphabets. Consider this alphabet $\Sigma = \{0,1,...,9, \#,(,)\}$. We can take this alphabet and encode it to represent in a string, the connections and layout of a graph. 

- $4\#(1,2)(3,4)$
    - is an example of an unconnected graph, where the first character represents the number of vertices, while each pair after the # represents an edge conecting two nodes.
- If the language $LC$ is the set of all correct encodings of connected graphs, then $33\#99929 \notin LC$ since it does not have correct encoding.
    - This represents a *membership test* for understanding which strings are within the language set, and which are not. If we have a membership test for a language, then there is an algorithm that can solve the related decision problem: “Is this a graph, and if it is, is it connected?”