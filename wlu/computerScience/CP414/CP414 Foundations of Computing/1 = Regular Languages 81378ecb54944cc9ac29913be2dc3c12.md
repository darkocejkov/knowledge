# 1 = Regular Languages

The real purpose that we are investigating languages is to build a **mathematical model** of computers, called **computational models**. The computer or device that displays this page is some form of a computer,  but any modern or even primitive kind of computer is already too complicated. In essence, they are essentially functions of computions, components that are pieced together to make real computers possible.

# Finite Automata

Think about the simplest kinds of computers, machines even. Something like an automatic door is not something that would be considered a computer, but they have the essence of a computer. Automatic doors can sense, through something like pressure sensors or infrared, something that is about to approach the door. It opens only when it senses someone. It has states, either “OPEN” or “CLOSED”, and things that catalyze or make it change state, like someone standing in the FRONT, BACK, or NEITHER (no one activates the door).

This state diagram to the right has a corresponding state transition table, that describes what state it transitions to based on certain inputs.

“Memory”  in this case is really about keeping track of these states, because we need to know what the current state is, and the input, to really do something.  This automatic only needs 1 bit of memory, to keep track of the state → 0 = Closed, 1 = Open

- Markov Chains are *probabilistic* Finite Automata, both are used to find patterns in data, like speech processing.

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled.png)

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%201.png)

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%202.png)

This is an abstract state diagram called $M_1$, which has three states, whose start state is $q_1$ because there is a floating arrow from outside the system on it. $q_2$ is called the **accept** state because it has a double-circle, and the arrows that point between the three states and to themselves as well are called **transitions**. 

This system in particular processes binary strings like $1101$ (from left → right) and produces an *output.* In this case, the input is **accepted** if the state is in the accept state on the final character of input, otherwise the input is **rejected**.

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%203.png)

This machine has a **predictable** outcome, meaning that there is a pattern to all the inputs that will lead to the accepted state. As long as there is a 1 in the string, AND the last element is a 1, then it will ALWAYS accept that string.

- This doesn’t mean it won’t accept the string $100$ for example, since it will go to q_2, then q_3, then q_2 again. In other words, there is a **language** that consists of all strings that this automata accepts.
- The above definition of automata is not formal, we need to understand how to do so formally in order to have good notation, and the precise rules of automata.

The formal definition of an finite automaton is that it has 5 things:

- $Q$ is a *finite* set of STATES
- $\Sigma$ is a finite set, the ALPHABET of allowed input characters
- $\delta: Q\times E \rarr Q$ is the **transition** function
    - it is the cartesian product of all states to all inputs from the alphabet, and relates it to other states (ie. the transition table)
    - x → 1 → y means that from state *x,* if an input reads as 1, then it moves to state *y*
    - $\delta(x,1) = y$ is that same transition, if the state is x, and a 1 is read, then it moves to *y*.
        - This also means exactly 1 transition exits every state for each possible input symbol
- $q_0$ is the **start state**
- $F \subseteq Q$ is the **set of accept states**
    - since F is a set, then it’s allowable to have an *empty set* of accept states (no states)

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%203.png)

Let’s think about this diagram formally:

- Q = $\{q_1, q_2, q_3\}$
- $\Sigma = \{0,1\}$
- $\delta$
    - $\delta(q_1, 0) = q_1, \delta(q_1, 1) = q_2,$
    - $\delta(q_2, 0) = q_3,\delta(q_2, 0) = q_2,$
    - $\delta(q_3, 0) = q_2, \delta(q_3, 0) = q_2,$
- $q_0 = q_1$
- $F = \{q_2\}$
- If the set A is the set of all strings that is *accepted* by this machine, called M, then “A is the language of machine M”, and $L(M) = A$, or that “M recognizes A” or “M accepts A”.
    - Machines *accept* several strings, but only *recognize* one language. Even if that language has no strings, then $L(M) = \empty$.
    - We can also verbally declare the rules or properties that strings must have to be accepted in set form:
        - A = {w | w contains at least one 1, and an EVEN amount of 0s follow the last 1}

Let’s formalize also what it means for a finite automaton to operate. If $M = (Q, \Sigma, \delta, q_0, F)$ is a finite automaton, and $w = w_1w_2...w_n$ is a *string* where each $w_i$ is a character from the alphabet. the machine M accepts *w* if there is a sequence of states $r_0, r_1,...,r_n$ in the set of states of Q, such that:

1) $r_0 = q_0$

- that is, the first state is the start state

2) $\delta(r_i, w_{i+1}) = r_{i+1}$

- that is, for any state, it’s transition given the next input, will result in the next state according to the transition function.

3) $r_n \in F$

- meaning that the final state is an element of the accepted states.

M recognizes the language A, if A = {w | such that M accepts w}, which is the language set of all accepted strings of the machine M.

<aside>
❕ A language is called a **regular language** if there is some finite automaton that recognizes it.

</aside>

Designing an automaton has no formula, but a useful trick is to think about the most crucial information that decides whether or not a string is accepted, regardless of the length of the string. You are simply looking for the simplest rule that you can use, to be able to tell whether or not that string is apart of its recognized language.

- for example, how do we define an automaton that recognizes a language for which all the strings are of the binary language, and must have an *odd* number of 1s. That’s really simple.
    - Instead of keeping track of the *number* of 1s, which can be infinite, we know that a number that is not zero is EITHER even OR odd, and not both.
    - if we have two 1’s, and then another appears, we know that there is now an *odd* number, flipping its bit of parity essentially. So, our state diagram would have two states, $q_{even}$ and $q_{odd}$, and only flips between them when a 1 appears on the input, and when a 0 is encountered for either state, then it stays in the same state (looping).
    - What about the empty string $\epsilon$? Since there are ZERO 1’s, then that would make the necessary accepted state $q_{even}$ since 0 is an even number...
        - so we would just need $q_0 = q_{even}$.
    - What are the accepted states?
        - since we are looking for strings whose number of 1’s is *odd*, then $F = \{q_{odd}\}$

Another example of designing automatons is to keep track of the *possibilities* of the problem states. For example, if we want our automaton to detect the substring $001$, we need to keep track of all the possibilities, which are:

- 0
- 00
- 001
- everything else

This means that when we detect 1’s at the start, we don’t transition until we see a 0, and then if we see, in total that has been $01$, which would disqualify that substring from being accepted, so we start over. If, however, we see another 0, so $00$, then we can move to the possibility that we can see either 0’s or 1’s. If we see a 1, then $001$ puts in the accept state, which we don’t leave because we found a substring 001 *anywhere* in the string. If we see more 0’s, then it may become $000000000000$, which still has the possibility of being 001, so we continue reading until we see a 1, so $000000000000000000000001$ is accepted. The only string we want to start over at is $01$, because that totally disqualifies being $001$.

# Regular Operations

Come in the toolbox of operating on languages, based on set theory, as languages are sets of strings over alphabets. If $A$ and $B$ are languages, then we can operates on them using:

- $A \bigcup B$ → union: $A \bigcup B = \{x|x \in A\; or\; x \in B\}$
    - combines both languages into 1 language
- $A \circ B$ → concatenation: $A \circ B = \{xy | x \in A\;and\;y \in B\}$
    - concatenates all the strings of A with all strings of B (all combinations of concatenation)
- $A*$ → star: $A * = \{x_1x_2...x_k|k \ge 0, each \;x_i \in A\}$
    - attaches any number of strings from A to other strings from A (including 0 strings)

ex. $\Sigma = \{a,b,c,...,z\}$ and $A = \{good,bad\}$ and $B=\{boy,girl\}$

- $A \bigcup B = \{good,bad,boy,girl\}$
- $A\circ B = \{goodboy,goodgirl,badboy,badgirl\}$
- $A* = \{\epsilon, good, bad, goodgood, goodbad,badgood,badbad,goodgoodgood, goodgoodbad, goodbadgood,goodbadbad\}$

<aside>
❕ Closed sets

Sets are *closed under an operation* if for that operation using elements of the set, the result of that operation is *also* in the set.

→ the set of natural numbers ≥ 1, but whole, then that set is closed under multiplication or addition, but not under division, since 1/2 < 1.

</aside>

If $A_1$ and $A_2$ are regular languages, then $A_1 \bigcup A_2$ is also a regular language.

- This is proved by understanding that if $A_1$ is recognized by $M_1$ and $A_2$ is recognized by $M_2$, then there are a total of $k_1 \times k_2$ state pairs. The proof is a construction of the machine $M$ that recognizes $A_1 \bigcup A_2$, which is done by constructing M such that transitions are done in *pairs* of inputs, thus, the accept states of M are pairs in which either $M_1$ OR $M_2$ is an accept state.
    
    → if M accepted ONLY WHEN BOTH $M_1$ AND $M_2$ were in their accept states simultaneously, then this would be the *intersection* of regular languages.
    
- Essentially, we know this union exists because there is a way to define an automaton that factors both languages at once, using pairs of inputs, almost like running both machines $M_1, M_2$ simultaneously.
- Because the union of two regular languages is ALSO a regular languages, then regular languages are closed under union.

Regular languages are closed under *concatenation*: if $A_1, A_2$ are regular, then so is $A_1 \circ A_2$.

- This proof is in-a-way, similar to the construction of the union automaton. However, since we have *concatenated* the strings, we need to be able to *break them apart* in the machine, since the new concatenation-machine needs to accept when *either* $M_1$ or $M_2$ contain an accepted string as a substring.
- However, there is no way to tell where the boundaries of the strings are, so we need a new technique: non-determinism.

# Non-Determinism

The machines we saw are called **deterministic** because at each step of the computation, there is always a certainty that we will know what the next state will be, based on the next input. This is true for all input cases, it will always be the same output for the same input, ie. there is no choice that needs to be made that would make different iterations of the same input, lead to a different output.

**Non-deterministic** machines are in-fact the opposite, where there is a choice that can be made for the next state at any point in its computation. Every *deterministic* FA is automatically a *non-deterministic* FA

<aside>
❕ The key difference between a DFA (Deterministic) and an NFA (Non-deterministic) is that *every state* of a DFA always has *exactly one* exiting arrow for *each symbol* in the alphabet, meaning that There is a concrete action for each letter in the alphabet. NFAs do not follow this rule, and can have either *more than one* exit for a given letter in each state, or none.

- This means that in DFAs, there must always be an option for every letter to transition the state of the machine.

NFAs can also use the $\epsilon$ character as a transition, which is not part of the alphabet of the language. DFAs must *only* use alphabet letters.

</aside>

- Because of this inherent “choice” to include more than one transition for a single letter, or none even, then the machine computes in *parallel* with these choices. When there exists more than one transition for a letter, the computation “splits” into multiple branches of computation. When there is no transition for a specific letter in the current state, then that copy “dies” - along with the branch that spawned it.
- NFAs also will accept a string input if *ANY* one of the branches of computation accepts the input.
- The empty character $\epsilon$ is something that allows for *automatic branching* without reading from the input. Even if there is just one $\epsilon$ exiting arrow - then the processing splits such that one of the copies goes through the empty transition, while the original stays in the current state.

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%204.png)

Every NFA can be *converted* into a DFA. 

- The formal definition between DFAs and NFAs differ in the **transition function** that is used for NFAs. In this NFA transition function, instead of linking the current state to a symbol to give the next state, it can use the empty character in addition, and can give a **set of the next possible states**, which allows it to branch.
    - $\Sigma_\epsilon$ is the union between the alphabet, and the set containing the empty char/string → $\Sigma \bigcup \{\epsilon\}$.
    - $P(Q)$ is the *power set* of Q, which is the *collection of all subsets of Q*.
    - Thus, transition functions of NFAs have such that $\delta: Q\times \Sigma_\epsilon \rarr P(Q)$. Meaning, that the cartesian product of all states with the alphabet (including the empty string) is mapped onto the power set of states.
    - Formally, an NFA accepts a string $w = y_1y_2...y_m$ where each *y* is a member of the extended alphabet, and the sequence of steps $r_0,r_1,...,r_m$ exists in the set of all states. Then, each step of that sequence must map to the transition function of *sets* of possible transitions.

D & NFAs recognize the same *class* of languages, which means that we have leverage in which form we choose to recognize a language, since some languages are easier in one than the other. However, this also means that machines are **equivalent** if they recognize the same *language*.

<aside>
❕ Theorem 1.39

Every NFA has an *equivalent* DFA.

- This idea is built on the fact that NFAs keep track of different possibilities by branching, so DFAs just need to have additional, deterministic states that allow it to do the same to become equivalent.
- NFA $N = (Q, \Sigma, \delta, q_0, F)$ recognizes language A
- DFA $M = (Q', \Sigma, \delta', q_0', F')$ recognizes language A
- NOT CONSIDERING $\epsilon$:
    - If an NFA has **k** states, then it has $2^k$ subsets of states, with each subset corresponding to *one* of the possibilities that the DFA must remember, so the DFA that is equivalent will have $2^k$ states.
        - Thus, the states of the DFA will be equal to the power-set of states of the NFA, so every state is a *set* of states in the DFA.
    - The transition function of the DFA is such that for any $R \in Q'$, which is a *set* of states, and $a \in \Sigma$, which is a letter in the original alphabet, without the empty string.
        - $\delta'(R,a) = \{q \in Q | q\in \delta(r,a), for\;some\;r \in R\}$ means that the transition function for the equivalent DFA uses a *set* of states as a current state R, and an input from the original alphabet, such that if *q* is an element from the states of the NFA, then *q* follows the transition from a state of that set of states for that same input.
        - Essentially, the union of all these sets, because each state may go to a *set* of states (R).
            - $\delta'(R,a)= \bigcup_{r\in R}\delta(r,a)$ → the transition relation in the new DFA from a state of the original NFA is the union of all of the possible states that original transition can go to.
    - $q_0' = \{q_0\}$, the machine M starts in the same state that the NFA N does.
    - $F' = \{R \in Q' \;|\; R\;contains\;an\;accept\;state\;of\;N\}$, that the machine M accepts a string if one of the possible states that N could be in at this point, is also an accept state.
- What about $\epsilon$ arrows?
    - For any state R of the new DFA machine, $E(R)$ is the collection of states (a set), which can be reached from states within R (a set of states) by only going along those empty-arrows, including members of R themselves.
        - $E(R) = \{q\;|\;q\;can\;be\;reached\;from\;R\;by\;traveling\;along\;0\;or\;more\;\epsilon\;arrows\}$
        - thus, $\delta'(R,a)=\{q\in Q\;|\;q\in E(\delta(r,a))\}$.

Corollary 1.40

- A language is *regular* if and ONLY if some *NFA* recognizes it.
    - this is proven through Th. 1.39, where any NFA can be converted into an equivalent DFA. Thus, if an NFA recognizes a language, so does its equivalent DFA.
</aside>

Practically applying the Theorem 1.39 to convert NFAs to DFAs, in example with the NFA $N_4$.

1) States of the DFA are equivalent to $2^k$, where *k* is the number of states in the NFA.

- $2^3 = 8$, so DFA has 8 total states, since it gets ONE for each subset of states of the NFA.
    - $\{\empty,\{1\},\{2\},\{3\},\{1,2\},\{1,3\},\{2,3\},\{1,2,3\}\}$
- Start + Accept states of DFA
    - initial state is $E(\{1\})$, because the start state has an empty arrow, and also the ‘1’ state itself.
        - $E(\{1\}) = \{1,3\}$.
    - New accept state of the DFA is are those containing N4’s accept state:
        - $\{\{1\},\{1,2\},\{1,3\},\{1,2,3\}\}$
            - essentially subsets that contain *any* of the accept states. In thise case, it is all the subsets that contain 1.
- Transition Function
    - this is quite complicated, but the essence of it is that we are trying to map states from the NFA to the subsets of the new states, and we do that by examining each exiting arrow from a state, and its input.
        - State {2} in D goes TO {2,3} on the input of ‘a’, because in the NFA, state two goes to BOTH 2, and 3, and there are no empty arrows to basically automatically move us
            - think of snakes and ladders, with the empty arrows being the snakes OR the ladders, when we ‘arrive’ at a square, if that square has a snake or a ladder, we must take it to the square it leads us to.
        - State {2] goes to state {3] on ‘b’, because state 2 goes to state 3 only once on b, and there’s no empty arrow to carry it further
        - State {1} goes to $\empty$ on ‘a’ since no ‘a’ arrows exit state 1.
        - State {1} goes to state {2} on b
            - We only ‘follow’ the empty-arrows AFTER the symbol is read, meaning if we read ‘b’ on state 1, then it takes us to state 2, which has no arrows, and we don’t consider the empty-arrow of state 1 since we’re now in state 2.
        - State {3} goes to {1,3} on ‘a’, since state 3 goes to 1, and then the empty-arrow carries us back to state 3.
        - State {3} goes to $\empty$ on ‘b’ since it has no exiting arrow for b.
        - State {1,2} on ‘a’ goes to {2,3}, because 1 does not have an ‘a’ transition
            - in this way, the state {1,2} represents the possibility that we are both at state 1 and state 2 at once, through non-determinism. However,  So, if we were on both states 1 and 2, and the input to both would be ‘a’, then state 1 goes nowhere because it has no ‘a’ arrows, and then takes the empty-arrow to 3, while state 2 loops into 2, and then the active state is that {2,3} both active.
        - State {1,2} on ‘b’, goes to {2,3} as well, since 1 → 2, 2 → 3.
        - etc...

NOTES FROM LOOKING AT SOLUTIONS

- The $\empty$ state should always have an (a,b) loop to itself

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%205.png)

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%206.png)

![The NFA N_4 converted into the DFA D.](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%207.png)

The NFA N_4 converted into the DFA D.

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%208.png)

Something that is very important is to *optimize* this DFA. We can see that the states {1} and {1,2} have no arrows pointing to them, so we can remove them, because in theory, this means that we can never end up at these states, and so we will never need to use their exiting arrows.

**Finite State Transducers** - are DFAs that output **strings** and not just accept or reject strings, ie. it transforms the input string into the output string. On the right is two examples of FSTs, and its pretty obvious here the transitions are not just single characters, but they are a “formula” for changing the input character. They are in the format (input/output), and whenever an input symbol is read, it takes the transition that matches the input rule for a machine transition, and the machine outputs the output character in sequence.

So, for example, machine $T_1$ gets 2212011 as input, it goes into states q1 → q2 → q2 → q2 → q1 → q1 → q1, so the output string is this same order of sequence, which makes it:

- 1 → 1 → 1 → 1 → 0 → 0 → 0

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%209.png)

Using NFAs to prove things like closure under union makes it much easier, as if there are NFAs that exist which recognize each a language, then their union is just the NFA of both of those NFAs using epsilon arrows, because under union, the total NFA should accept when *either* constituent NFA accepts.

- This construction of an NFA makes it much easier to prove that regular languages are closed under concatenation

<aside>
❕ Regular Languages are closed under Union, Concatenation, and Star operations

</aside>

![NFA that shows the proof of closure under concatenation of two languages A1 and A2, recognized by N1 and N2.](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2010.png)

NFA that shows the proof of closure under concatenation of two languages A1 and A2, recognized by N1 and N2.

![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2011.png)

Proving that they are closed under concatenation:

- This method uses the joint-NFA with a bit of a twist. if N1 recognizes language A1, and N2 recognizes A2, then to show that $A1 \circ A2$ is also a regular language, we need to show that there is an NFA that recognizes this concatenation of languages.
- Instead of branching to *both* at the same time, this technique uses the fact that strings from A1 are at the beginning and concatted with strings of A2. So, the NFA N on the left shows that using the NFA N1 that describes A1, the accept states of N1 become branching states into N2, which is basically like determining if the string is a part of language A1, and then branches to N2.
    - For example, if A1 was {ab, aba, abab, ababa} and A2 was {a, aa, aaa, aaa}, then $A1 \circ A2 = \{aba, abaa, abaaa...\}$, then this NFA N looks for the first parts of the concatenation which coincide with strings from A1, then strings from A2.

- This method of constructing an NFA to prove closure also works for the star operation $A*$.
- If A1 is recognized by N1, then A1* is recognized by N, which has a new initial state which also accepts, and back-links using empty chars. to proceed back to the original starting state of N1.
    - As such, whenever N1 would complete its processing and accept a string, the star-set operation needs to continue to look for other concatenated A1 strings alongisde that A1 string.
    - This is because the star operation is almost like the power-set of concatenation of a language, in which the empty string exists, and the different combinations of concatenations exist as well.

# Regular Expressions

- Math Expression: $(5+3)\times 4$
    - describes a single number, using the different math operations (+, -, x, /).
    - Regular expressions are similar to math expressions, but are meant to describe **patterns** or **languages.**

- For example: $(0 \bigcup 1)0^*$
    - this is the regular expression that describes the language consisting of all strings that *start* with 0 OR 1, followed by *any number of zeroes*.
        - this is because 0 and 1 are shorthand for their sets, $\{0\}, \{1\}$.  So, $\{0\}\bigcup\;\{1\}=\{0,1\}$.
        - $0^* = \{0\}^* = \{0,00,000,0000,...\}$
        - the use of parentheses is similar in how math, multiplication is implied. Here, in regex, concatenation is implied.

Formal Definition of a Regular Expression: R is a regex if R is:

- *a* for some *a* in the alphabet $\Sigma$
- $\epsilon$
    - represents the language of a *single string: the empty string* = $\{\empty\}$
- $\empty$
    - represents a language tha has *zero* strings.
- $(R_1\bigcup R_2)$
- $(R_1 \circ R_2)$
- $(R_1^*)$
    - where $R_1, R_2$ are themselves regular expressions
- (This defintion is not a *circular* definition that defines a regex R in terms of itself, but rather an *inductive definition*, because R1 and R2 are always smaller than R itself)

- If $\Sigma = \{0,1\}$, then we can describe it using regex via $(0 \bigcup 1)$, which also describes strings of length 1 over the alphabet, because each character of the alphabet, is itself, a string of length 1.
    - $\Sigma^*$ describes *any* string over an alphabet
    - $\Sigma^*1$ describes strings that end in 1
    - $(0\Sigma^*)\bigcup(\Sigma^*1)$ describes all strings that *start* with 0, OR end in 1
        - 0100001...
        - ...100101
        - 10 or 100 are not in the language for example.

- Another shorthand that becomes useful is the notion of $^+$, such as $R^+$, which is short for $RR^*$.
    - If $R^*$ is the language of all strings that are ZERO (0) or more concatenations of strings from R (which include the empty string), then $RR^*$ is the language of all strings that are ONE (1) or more concatenations of strings from R.
        - $R^+ \bigcup \epsilon = R^*$.
    - $R^k$ is then shorthand for the concatenation of *k* R’s with each other.

<aside>
❕ Order of Operations of Regex:

- 0) Anything in Parentheses
- 1) Star
- 2) Concatenation
- 3) Union
</aside>

<aside>
❕ Language that a regular expression describes

- If R is a regular expression, then the language or pattern it describes is L(R)
</aside>

- Here are some examples of regular expressions and their languages
    - $0^*10^*$ describes strings that contain a **single** 1.
    - $\Sigma^*1\Sigma^*$ describes strings that have *at least* ONE 1.
    - $\Sigma^*001\Sigma^*$ describes strings that contain the string ‘001’ as a substring.
    - $1^*(01^+)^*$ describes strings in which every 0 is followed by *at least* one 1.
    - $(\Sigma\Sigma)^*$ is all strings of an even length
    - $(\Sigma\Sigma\Sigma)^*$  length of strings are multiples of 3.

- Identities of regular expressions
    - $R \bigcup \empty = R$
        - adding the empty language to any other language does not change it
            - $R \bigcup \epsilon$ = $\{...R, \epsilon\}$, which means that adding the empty string to a *language* changes it
    - $R \circ \epsilon = R$
        - joining the empty string with any other string does not change it
            - $R \circ \empty = \empty$.

- Regex & Finite Automata
    - FAs recognize languages, and regex generates or describes languages. It’s not surprising that regex that be *converted *****to FAs based on the language that they describe, and vice versa.

![(ab U a)^*](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2012.png)

(ab U a)^*

- To convert DFAs into GNFAs
    - add new start that proceeds to the original start with an empty string transition
    - add new accept state with empty string transitions from all previous accept states
    - merge transitions that go in the same directions (a,b) = (a U b)
    - add the empty set transition to states which had no connections

- Convert GNFAs to Regex
    - This process is essentially just combining and merging states and forming the regular expressions
        - Because a GNFA must have at least 2 states, start and accept, then we know that we can construct an equivalent GNFA using regular operations on the transitions until we have two states left, giving us the single regular expression that the GNFA recognized.
            
            ![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2013.png)
            
    - the simplest way to do this, is to take out a state, and repairing each other the transitions such that the *same* language is recognized.
        
        ![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2014.png)
        
        - This is the general formula of the regular expression after removing a start that is not a start or accept state.
            - Since every non-start/accept state has a loop, we know that it references the *star* operation in this case. We concatenate that with the incoming arrow from q(i), and the outgoing arrow from the ripped state itself, which is regular expression R3. Then, if we were to fix the ripped link from q(i) → q(rip) → q(j), this means that we need to merge $R_1R_2^*R_3$ with $R_4$, because a regular expression would be matching (or going from the start to the accept) on the condition that it matches $R_1R_2^*R_3$ OR $R_4$, meaning that would be a union.
            - More algorithmically explained:
                - concatenate the loop with the incoming arrow and the outgoing arrow
                - union those concatenations with the arrow that goes from the start to the accept.

<aside>
❕ Theorem 1.54

A language is regular *if and only if* some regular expression describes it.

</aside>

This is proven both ways:

- If a language is described by a regular expression, then it is regular
    - This is true because there is always a way to convert a regex into an NFA that recognizes that language, and if a language is recognized by some NFA, then it is by definition, regular.
    - also, in the cases of regular expressions being closed under unions, concatenations, and star operations, then any regular expression that contains those remain closed, and their language is still regular because of this.

- NEW TYPE OF FINITE AUTOMATA JUST DROPPED 🔥
    - Generalized Non-Deterministic Finite Automaton (GNFA)
        - A NFA that uses *regex* as transition conditions rather than single members of the alphabet.
        - this is possible because the regex allows for reading *blocks* of input characters rather than just one at a time.
    - Conditions of a GNFA:
        - Start state must have transitions to *all other states*, but no incoming arrows from other states
        - Only 1 (ONE) accept state, which has transitions incoming from all other states, and goes to no other state.
            - The accept state cannot be the start state
        - all other states that are not starting or accepting, must have one arrow loop to itself, and has a transition from itself to every other state.

![Example GNFA](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2015.png)

Example GNFA

- Examples of converting DFA → GNFA → Regex
    
    ![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2016.png)
    
    - Here a 2-state DFA is given 2 more states, s (start) and a (accept), and the (a,b) transition loop is converted to a regular expression itself to be 1 arrow instead of 2.
    - We rip out state 2, and use the general formula for maintaining the same language.
        - Since the incoming expression is (b), and the look is (a U b), then we star the loop, concatenate (b)(a U b)*(epsilon) U (empty set)
            - because S has no arrows to A, this represents the empty set transition, which is never used, and so (b)(a U b)*(epsilon) U (empty set) is = (b)(a U b)*
    - We rip out state 1, and star its loop expression, and concatenate that before its outgoing arrow expression.

# Non-Regular Languages

- Not all languages can be recognized by finite automatons, and this is where we gain the tools to prove that some languages cannot be recognized by FAs.
    - Let’s take an example language: $B = \{0^n1^n\;|\:n \ge0\}$.
        - This language doesn’t have a DFA that recognizes it because it specifies all languages for which it has an n-amount of zeroes, followed by an n-amount of ones.
        - Thinking about a DFA, it needs to have states be able to track the number of things, and is possible for a *finite* amount of things to remember. Otherwise, it doesn’t make sense via discrete states to track an infinite number of things, other than things like *parity*. We can track whether there is an even or an odd amount of certain symbols, but we cannot keep track of an infinite series of symbols.
    - This argument of infinite or unbounded memory however, does not disqualify some languages from being regular, because some problems seem to have different concepts.
        - C = the language of strings that has an *equal amount* of 0’s and 1’s is NOT regular, because it needs to count infinitely both the occurrences of 0’s and 1’s.
        - D = language of strings that has an *equal number* of occurrences of ‘01’ and ‘10’ as substrings is regular, which goes past the intuition of counting infinitely.

- The technique to be able to prove non-regularity uses the **pumping lemma**, that all regular languages have a special property, and if we can show that languages do NOT have this property, then it is not regular.

<aside>
❕ Pumping Lemma

The property in question is that all strings in the language can be ‘pumped’ if they are at least as long as a certain value, called the **pumping length**. Which essentially means that *each* of those strings below the pumping length, contain a section that can be *repeated* any number of times with the resulting string remaining in the language.

More formally, is that if A is a regular language, then there is a number *p* (the pumping length) where if *s* is any string within A, of length at least the pumping length *p*, then *s* may be divided into THREE pieces: $s = xyz$ that satisfy the following conditions:

1) for each i ≥ 0, $xy^iz \in A$

2) $|y| > 0$

3) $|xy| \le p$

</aside>

→ $y^i$ represents concatenation *i* times of y.

→ When *s* is divided into these three pieces, either *x* or *z* can be the empty string, but because of condition 2, *y* cannot be empty, because its length must be greater than 0. It’s pretty trivial, but useful to have the third condition, that the concatenation of pieces *x* and *y* have a length that is less than or equal to the pumping length, even if *x* is empty. 

Proof of Pumping Lemma:

- Core Idea:  If M is a DFA that recognizes a language A, then the pumping length can be the *number of states* of the DFA M. Then, any string *s* in A of length ≥ *p* (the number of states) can be broken down into three pieces, *xyz*.
    - What about if *no strings* in A are of length ≥ p? then it is **vacuously true**, because all three conditions hold, since there are no requirements on those strings.
    - If there is a string *s* in A that’s length is ≥ p, then the sequence of states it follows shows the path of computation that string takes, from the starting character to the ending character. Obviously, since *s* is in the language A, then the last state it encounters is an accept state.
        - If the length of *s* is *n* (|s| = n), then the sequence of states *s* takes has length (n+1). Because *n* is at least *p* (n ≥ p), this means that n+1 > p, so then the length of the sequence is greater than the number of states total (pumping length, p).
            - the sequence is length (n+1) because it starts on state 1 automatically, already having 1 more than the length of the string *s*.
        - By the pigeonhole principle, the sequence must have a repeated state,
    - If we then separate the string *s* into three pieces, *xyz*, then this represents three different sequences of states string *s* takes, which are connected. If we precisely seperate it such that *y* is bounded by the *repeated state*, then this forms a cycle in terms of paths.
        
        ![Untitled](repo/wlu/computerScience/CP414/CP414%20Foundations%20of%20Computing/1%20=%20Regular%20Languages%2081378ecb54944cc9ac29913be2dc3c12/Untitled%2017.png)
        
    - The whole purpose of those conditions 1, 2, and 3 on the pumping lemma is that if we were to run the sequence on input *xyyz*, then the sequence of states goes $q_1 \rarr ... \rarr q_9 \rarr ... \rarr q_9 \rarr ... \rarr q_9 \rarr ... \rarr q_{13}$. This means that the cycle of *y*’s processing *repeats*. Logically, because *xyz* is accepted as *s*, **then q13 is an accept, so *xyyz* takes the same sequence with an additional cycle, and ends at q13, and must also accept.
        - It also accepts for any $xy^iz, i>0$. If *i = 0*, then it would make the same sense that $xz$ is accepted, since it “skips” over the cycle that *y* takes, and goes directly to being accepted.
        - the second condition states that the cycle within *y* must contain some number of states greater than 0.
        - the third condition states that the length of *xy* must be ≤ p. This can be achieved because we know that the first *p+1* states in the sequence must contain a repetition because of the pigeonhole principle.

- In order to *use* the pumping lemma, we often need to assume that a language is regular to obtain a contradiction in proof. To do this, we use the pumping lemma to guarantee that a pumping length *p* exists, such that all strings of length ≥ p can be pumped. We then need to find a string in the language that has length ≥ p, that *cannot* be pumped, and show specifically that it cannot be pumped by considering *all* the different ways of dividing this string into three pieces.
    - the *pumping length* is not a specific value, but rather an arbitrary value based on the conditions and strings within the language we are testing. For example, if we are trying to prove that the language with $0^n1^n$ is not regular, then we can use $0^p1^p$
    - for each of those groupings into xyz, we need to show that $xy^iz \notin B$, by finding a value of *i* such that this occurs.
- If we can find the existence of such a string, then its existence contradicts the pumping lemma *if* the language were regular, so the language *cannot* be regular.

<aside>
❕ Remember, the pumping lemma can only show that language *cannot* be regular if they don’t satisfy the conditions of the lemma, and it doesn’t show that those languages are regular. If we use a regular language with the pumping lemma, it becomes impossibly difficult to show that it is not regular, because it really is, and the fact that you cannot show that it is not regular does not prove that it is.

</aside>

→ The essence of these kinds of contradictory proofs is to use the pattern of the language against itself, to show that, when these patterns have a certain length ≥ p, that we can define these discrete parts that require to be within some bounds of length. If we choose the correct and clever groupings of patterns to these pieces, we can show through “pumping up” or “pumping down”, that $xy^iz \notin A$, based on the pattern itself.

- so for example, if the pattern is $0^i1^j, i>j$, this essentially means that there are at least 1 more 0’s than 1’s in the string. Then, we can show that x = empty, y = all the zeroes, z = all the 1s. Since $xy^0z$ is valid, we can show that a string of all 1’s in (empty + all 1’s) cannot satisfy the condition of having more 0’s than 1’s, and so this string cannot be ‘pumped’ . Therefore, since we assumed that the language is regular, all its strings can be pumped, but we found one that cannot be, showing that the language is not regular through the pumping lemma.

- Closure of non-regular languages
    - Complement (CLOSED)
        - If we have a language L, and L is non-regular, but it’s complement is regular, then the complement of the complement will also be regular based on closure properties of regular languages. However, the double-complement gives us back the original language L, which is non-regular, which is a contradiction. Thus, the complement of non-regular languages IS closed.
    - Union (NOT CLOSED)
        - If L1 and L2 are non-regular, then is it always the case that L1 U L2 is non-regular? By the properties of closure under complement, then if L1 is non-regular, and L2 is the complement of L1, then L2 is also non-regular. But if L1 U L2 = L1 U NOT L1, then that is the language of all strings. This is a regular language, because it is represented by a DFA.
    - Intersection (NOT CLOSED)
        - Similarly, if L1 and L2 are non-regular, then by complement closure, if L2 is the complement of L1 (NOT L1), then L1 V L2 = L1 V NOT L1 = empty set (since no two strings can be in both at once). This is also regular because it can be represented by a DFA.
    - Concatenation (NOT CLOSED)
    - Star (NOT CLOSED)
        - We cannot use the same logic here, but a good frame of reference for this is to remember that if a language is non-empty, and it has AT LEAST 1 non-empty string, then the star of that language is an infinite set/language, because we can concatenate any string to any otherstring, and itself 0 → ♾️ times.
        - If we had a language that is non-regular, then the star of that language would be the language of all strings