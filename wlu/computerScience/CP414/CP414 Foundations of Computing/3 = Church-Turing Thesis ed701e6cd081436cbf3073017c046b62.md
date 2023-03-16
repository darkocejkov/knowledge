# 3 = Church-Turing Thesis

- Finite Automata (FAs) are for problems that can be solved within a *finite* or *limited* memory
- Pushdown Automata (PDAs) are for problems that can be solved within an *infinite* or *unlimited* memory, but require the use of a **stack**, which is limited by only using the *top* of the stack.
- More general models require more robust machines with more capacity for data structures.

# 3.1 Turing Machines

- Developed by Alan Turing
- Similar to FAs, but have a totally unlimited, and unrestricted memory.
    - which is a better model of a general computer than the other automatons
- However, Turing machines cannot solve every problem, which is a nod as to the certain limitations of problem solving with computation.
- It uses an *infinite* tape as a form of unlimited memory, it can read and write symbols from/to the tape, and move around on it.
    - On initial state, the only thing on the tape is the input string. It can write anywhere on the tape, and can move to read or write as it needs.
    - It *accepts* or *rejects* by entering those respective states, but can go infinitely if does not stop. Stopping is called “halting”
- Because we can check any place of input, this allows us to widen the strategies we use to solve problems.
    - For example, if we wanted to check membership of the language $\{w\#w\;|\;w\in \{0,1\}^*\}$, we are allowed to go between input indices.
        - This makes this solution interesting, as the algorithm to check for a string’s membership is to first catch simple things, such as not having “#”. Then, we can mark the tape as our control memory, and use that to go between instances of ‘w’, matching character to character. For each character, we can check if they match - if they do, we can “cross them out” by marking those characters on the tape to know they match.
            - if the end of the string is reached, and all non-# chars are marked, then they all match. However, at any point in the string, if any two characters between instances of ‘w’ don’t match, then we know the string does not long, and rejects.

## Formal Definition

- Like the difference between PDAs and FAs, the main difference in Turing machines is their transition function.
    - It takes the form / mapping of: $Q \times \Gamma \rarr Q \times \Gamma \times \{L,R\}$.
    - when the machine is in a state q, and the head is over a tape *cell* with the symbol $\in \Gamma$ of *a*, then:
        - $\delta(q,a) = (r,b,L)$ means that the machine writes the symbol *b* to replace *a*, and then goes to state *r*.
    - L, R are control symbols that tell the tape-head to either move *left* (L) or *right* (R) after writing.

<aside>
💡 Turing Machine as a  7-tuple $(Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$

Q - set of states

$\Sigma$ - input alphabet that *does not* contain the blank symbol: $\bigsqcup$

$\Gamma$ - *tape* alphabet, which contains the blank symbol $\bigsqcup$ ($\bigsqcup \in \Gamma$), and the input alphabet is a subset of this ($\Sigma \in \Gamma$).

$\delta$ - $Q \times \Gamma \rarr Q \times \Gamma \times \{L,R\}$ is the transition function

$q_0$ - is in the set of states, and is the start state

$q_{accept}$ - is in the set of states, and is the accept state

$q_{reject}$ - is in the set of states, and is the reject state

- $q_{accept} \ne q_{reject}$
</aside>

- On start, the machine receives input on the *leftmost* n squares of the tape (n is the length of the input string).
    - the rest of the tape is blank - blank symbols.
    - the machine’s tape head starts on the first symbol of input.
        - the first blank to appear means that input has ended (since blank is not a member of the input alphabet)
- If any transitions indicate the head to move *left* (L), but the tape is already at the beginning, then the head does not move.
- Computation continues according to the transition function, and will only “halt” (stop) when it enters a *reject* or *accept* state.
    - if neither occur, then it will continue forever.

- Turing operation has three main states of information:
    - current state
    - current tape contents
    - current head location
        - some setting of these three states is a configuration of the Turing machine.
- We can denote some configuration of the machine using this notation:
    - u q v
        - *q* is the current state
        - *uv* is the current contents of the tape
            - but *v* is the current head location
    - for example, the configuration $1011q_701111$ represents:
        - the tape being $101101111$, the current state being $q_7$, and the head currently on the 2nd 0.

- some configuration (C1) can **yield** another configuration (C2) if the machine can *legally* go from C1 to C2 in a single step.
    - $C_1 = uaq_ibv$
    - $C_2 = uq_jacv$
        - means that $C_1$ yields $C_2$
            - this represents the transition $\delta(q_i, b) = (q_j, c, L)$
                - the machine is first in state q_i, and the current tape read is ‘b’, so it yields configuration 2 by moving to state q_j, writing ‘c’ to replace ‘b’, and moves 1 to the left.

- thus, the **start configuration** on some input *w*, will always be $q_o w$.
- an *accepting* configuration is one in which the current state is the accept state
- a *rejecting* configuration is one in which the current state is the reject state
    - these are **halting** configurations, which depend only on the current state, and do not *yield* any other configuration
        - because the machine stops.

- A collection of strings that a Turing machine accepts is the **language** of the machine, or the language **recognized** by it, $L(M)$.
- A language is Turing-recognizable if some Turing machine recognizes it
    - three outcomes are possible for any given string:
        - accept, reject, loop
            - loop represents an outcome where the machine does not *halt* ever.
    - machines fail to accept, when they then either reject, or loop.

- knowing when a machine is done is difficult, because either it takes a long time to stop, or it will never stop.
- Thus, we have Turing machines which *always* stop, called **deciders**, which will halt on every input and never loop.
    - they are ‘deciders’ because they *always* decide to accept or reject, and deciders then “decide” the language that they recognize.
    - languages that can be decided, are called **Turing-decidable** or **decidable**, if some Turing machine decides it.
        - every decidable language, is also recognizable.
        - but not every recognizable language is decidable.

---

## Example: $0^{2^n}$, the language of 0’s whose length are powers of two

- from the beginning, sweep from left to right on the tape
    - mark the first symbol as blank, to know when the beginning is
    - for every *other* 0, cross it off
    - go from right to left, counting the parity of 0’s, if there are an *odd* amount of 0’s left uncross, then we may reject.
    - if the tape has only 1 zero, then we know we can automatically accept
    - return to the left side of the tape by reading until we get to the blank we marked
    - repeat, going from left to right, crossing off every other remaining 0.
- this process cuts the number of zeros in half.
    - thus, this algorithm is *decidable* because it will always reject or accept after at most two runs, and every halving will either tell us if the remaining number of 0’s is even or odd, which means that it is either a power of two, or not.
    -