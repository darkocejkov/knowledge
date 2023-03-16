# 7 = Time Complexity

The classes of *solvable* and *unsolvable* aren’t necessary the limits in “computationally solvable”, because computers, though they may have infinite memory and can go forever, that’s not a reasonable way to gauge (humanly) that something is truly solvable. We need to consider how *time* and *space* requirements of problems affect how we can solve them.

# 7.1 Measuring Complexity

- Given some language, we need to define some ideas about how algorithms for that language use time and space, and certain factors.
- For example, certain cases of input may be the “best-case” input, such as the empty string, because its outcome regardless of accept or reject, is just one operation, reading the empty symbol and halting.
- There also exists **worst-case** analysis, and **average-case-analysis,** which are used more often than “best-case” because the best-case is usually a very small set of input that doesn’t really give a good estimation of how the algo runs.
    - worst-case = longest running time
    - average-case = average of all run times of inputs of particular length
- The **running time** / **time complexity** of a machine is a function $f : \N \rarr \N$ such that $f(n)$ is the max. number of steps that the machine uses on any input of length *n*.
- Run times are usually *expressions* of length and how input length changes given the algorithm, but that’s too narrow. We can use **asymptotic analysis** to understand running times based on certain known classes of run-times, and consider the run time growth from small to large inputs.
    - Thus, as input length grows, then some factor of run-time grows proportionally in some way, and we only want to care about the largest degree that will *dominate* the growth.
        - ie. $6n^3 + 2n^2 + 20n + 45$ is an expression, and the factor $n^3$ is the highest degree, meaning that as $n \rarr \infty$, then $n^3$ grows the most out of all other factors.
    - In *asymptotic notation* or Big-O notation, we use this highest degree to describe the run-time, as $f(n) = O(n^3)$.

# 7.2 The Class P

# 7.3 The Class NP

# 7.4 NP-Completeness