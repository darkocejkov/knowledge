# 1.1 - 1.9 Regular Languages

# Finite Automata

- Automata are described either be a 5-tuple that has all of the most important properties of automatons, such as the various states, the start state, and the end states that accept strings, and which alphabet is used. Most importantly, it has a *transition function,* which maps states and letters of the alphabet, to other states. This means that when we are in a current state, and an input symbol is read from the string, the transition function dictates based on the current state and the symbol, what the next state is.
- Finite Automata work to define a set of strings that it accepts. The empty set (accepting no strings) is a valid *language*.
    - The languages that FAs recognize are called **regular languages**
        - they are *regular* because they are recognized by some FA
- membership testing of any string can be done given the FA in terms of its 5-tuple, like its state, transition function, and accepting states, given that all strings are over the same alphabet.
    - All that needs to happen in order to compute membership of any string given the FA, is to compute the sequence of states that the symbols of the string cause. When the string ends, its important to check the state that the FA is in, and if that state is in the set of accepted states, then the string is in the language that is recognized by the FA.

- Constructing languages can be based on the discrete properties that the language has, if we think about the *closure* of languages when we use union (or), intersection (and), etc., then we can take languages which satisfy each property and use the closed operators to create larger or smaller languages piece-by-piece.
    - For example, if language L1 has property that all strings start with A, and L2 has that all strings end with B, then it is possible to find a third language, L3, such that strings must start with A and end with B.
        - To do this, we take the intersection of L1 ^ L2, which means that L3 = L1 ^ L2, all strings in L3 are BOTH in L1 and L2.
    - Or, we can have a language in which it has strings that *either* start with A, or end with B.
        - This either/or means that we take the union of languages (L1 U L2).
- In fact, we can prove that we can take two FAs and combine them into one using operators such as union or intersection. This works on a proof of construction, such that we can take two distinct FAs, and use these closed operators to combine sets of states into *pairs* of states, and similarly for accepting sets of states.
    - For union, we would want to accept a string when *either* automata accepts, so this means that any pairs of states that has accepts in either automata would be an accepting state.
        - with union operations, the number of states is the multiple of the number of states of each FA.
    - For intersection, we would rather want an accept state that only accepts when *both* conditions are satisfied, so the only states that would accept in that case must be the states that contain BOTH accept states of the FAs.
    - The complement FA is one that accepts all strings that the original FA did not accept, so the complement set. In this way, all accept states of a complement FA are states in which they are NOT involved in the accept states of the original.
        - For example, if an accept state in M_1 is q_3, then the accept state(s) in (NOT) M_1 will be all states that are not q_3, such as q_1, q_2, q_4, ...
- $L_1, L_2 \in \R$, where big R is the set of all regular languages
    - $L_1 \bigcup L_2 \in \R$
    - $L_1 \bigcap L_2 \in \R$
    - $\overline{L_1} \in \R$
    - $L_1 \circ L_2 \in \R$
    - $L_1^* \in R$

# Closure & Non-determinism

- Concatenation
    - is the operation of adding any string from one language as a prefix or suffix to a string of another language
    - if language A is the set of strings that end with ‘b’, and language B is the set of strings of odd length, then what is a concatenation of these two sets?
        - for example, “ababababbbb” is a string in language A, while ‘aaa’ is a string in language B. So their concatenation is ‘ababababbbbaaa’, where the ‘aaa’ string is a suffix.
            - if this happens to a set, like in $A \circ B$, then that is the set of all of A’s strings, with B’s strings as suffixes to those strings.
        - when concatenation happens, how can we tell that the resulting concatenation string is part of a regular language, can this string be accepted by some automata?
            - the big problem here is that we don’t know where the bounding is for a string, meaning that we cannot tell when a string from A ends and a string from B starts.

- Non-determinism
    - is something that is necessary to use to prove that there is closure under concatenation and star operations. This is because DFAs must have a choice for all symbols of the alphabet, and because of this, we need to have states to *track* properties of the string. We cannot ‘test’ alternate options in parallel with DFAs, such as the possibility that part of the current string is accepted by some other FA.
    - non-determism is ability of states to either have 0, 1, or > 1 options for *each* symbols in their transitions. This means that at certain points, some inputs cause a *branching* of processing because there are multiple choices. In other inputs, there may be *no* options at all, and the state that results is a *dead state*. There’s also a special character that can cause automatic transitions without reading any input, which is the *epsilon* or empty character.
        - When any state has an empty transition, it will automatically branch to the connected state, and continue processing on the current state as well.
    - In deterministic automata, processing is *linear*, and DFAs only accept when their *final state* is an accept state.
    - in non-deterministic (NFA) finite automata, processing is branched/parallel. So, if the end of the string is reached, and *any one of the branches* is in an accept state, it totally accepts the string.
    - The essence of non-determinism is that we can check different *possibilities* of strings. For example, we can detect if strings have their 3rd last character as a 1, because everytime we see a 1 in the string, we can “branch” and check if the string ends in 2 characters, and if it does, then that branch accepts that string. Otherwise, that branch dies if it doesn’t end, or ends too early.
        - An equivalent DFA would need to *remember* more, rather than test different possibilities by branching. Because DFAs cannot branch, and must have at most 1 transition for *each* symbol in the alphabet, this means that to detect strings that end with the pattern ‘1xx’ such that ‘x’ is either 0 or 1, then we need to keep track of the last 3 characters at all times in the string, because we don’t know when it will end.
        - Essentially, this DFA will need to have 8 states, because there are 8 different combinations possible for the 3 last characters:
            - 000, 001, 100, 010, 101, 110, 011, and 111. Only 4 of these 8 combinations have ‘1’ as their first character, which are ‘100’, ‘101’, ‘110’, and ‘111’, and these states are accepting.
    - Within the formal defition of NFAs, the only difference is the transition function.
        - The alphabet now includes the empty character $\epsilon$, and the transition function maps $\delta(State, Sybol) = P(Q)$, which is the mapping of state symbol pairs to options of the *power set* of the set of state. That means that instead of having at most 1 state being mapped to, we are now mapping to *sets* of states, because one state may have multiple choices for the same symbol, branching to two different states.
        - When there is no mapping for a state, symbol pair to a set of state(s), then it maps to the empty set $\empty$.

- Equivalence of DFAs and NFAs
    - every NFA has an equivalent DFA that recognizes the same language.
    - this is proved by constructing a DFA that exists given an NFA and its properties.
        - constructing such a DFA involves taking the possiblities of sets of states being active at one time and makes them into each a discrete state themselves.
            - Thus, the set of states of the equivalent DFA is the powerset of the set of states of the NFA.
            - the accept states of the DFA are the sets from the powerset, which contain an accept state from the NFA.
            - the transition function requires us to examine the different combinations of active states, and where each input could take us from either active state, thus, the mapping of states is the union of all possible resulting states.

- NFAs for proving closure on concatenation and star operations
    - These operations are more complex in terms of their resulting strings, because they are combinations of strings with other strings, and within one string, must have *entire* strings of another language, or itself, appearing in them. So, it’s more complex because we cannot determine, determinisitically, when one string ends and another starts without prior knowledge, the goal is to accept strings that contain within them a suffix and a prefix string.
        - One way to do this through non-determinism for concatenation, is to branch using empty transitions whenever the first automaton would accept the prefix string, and instead have the accepts in the suffix-detecting automaton. This way, when the first prefix is accepted, it instead branches off to check the possibility that it may end in a concatenated string.
        - Star operation NFAs are similar, except instead of using two different automatons for each language, it uses a single language, so it must use empty transitions to back-track and check for same-language suffixes.
            - It also starts with an addition accepting + initial state, because star-operations allow for the empty string, since the star operation is the power-set of all concatenation possibilities with every string of a single language.
                - { {}, {a}, {b}, {ab}, ... }

- All DFAs are NFAs, which is why we are able to convert any NFA into a DFA.
    - We also cannot show the *complement* of a language using NFAs, because it is parallel in processing. This is also true for set intersection, because the parallism that NFAs have make it impossible to guarantee that all branches should accept.
        - Because we can convert any NFA into a DFA, we can show the complement to the DFA which is recognizes the language complement to the NFA.

# Pumping Lemma

The key idea of proving the pumping lemma is that, given a language that can be either finite or infinite, that there is a specific way for those input strings to be accepted based on the FAs pattern. This is proven by setting up the fact that some arbitrary length called the ‘pumping length’ is equal to the number of states. using this pumping length, we know that strings which are accepted by this FSM go through some order of states, until the accepting state. So, any strings which are greater or equal to the number of states, ie. visiting all states at least once, then because there are a finite amount of states in the FSM, there must be a repeition somewhere for any strings longer than the number of states. 

- this means that any variations of this string, when broken up into three parts, will also accept, because this repetition will continue with the pattern, meaning that the string *can* be “pumped”.