# CP312 — Algorithms (W2020)

---

# Introduction

What are algorithms? How do we define algorithms and their properties, such as efficiency and the strategy behind them, and how different kinds of algorithms yield different properties.

In programming terms, we define algorithms as a sequence of commands that is designed to accomplish a goal; mostly to provide a solution to a complex problem.

Basic algorithms are meant to serve as very efficient and very useful ways to tackle something that is commonly done, sorting and searching. Computer science concepts often use sorting and searching. 

But what exactly is efficiency and how do we notate it? 

Efficiency of any program is measured in two domains:

1. Computing Time / Runtime
2. Memory Requirements

### Runtime

The metric that really defines good algorithms is the runtime, but what units do we measure in? Because there are so many variations to computers and hardware, we must avoid using concrete units like time measured in seconds, so we use a more abstract unit. This unit is structured as a *function* of input. 

This might sound stupid, but we want to understand how algorithms *grow* and perform with different *amounts* of input. 

In example, if you've ever programmed small programs that deal with small amounts of information as input, you might notice that execution times are trivially fast, in the milliseconds. Runtime is not an issue when there is small input, as even the slowest known algorithms can function well with small input. 

Well how large are we talking about? There is no set range for small/large input, but we are interested in understanding how algorithms tend to perform when dealing with many different amounts of input, such as 1000, 100,000, and even 1,000,000,000s of inputs. Again, we use *functions* to define the *profile of efficiency* for any given algorithm.

As such, we can have algorithms that are trivially simple and finish within a **constant** time, meaning that constant algorithm runtimes do not scale with input. This can be as simple as retrieving a single index from an array, or printing. 

The two main kinds of functions that are used to describe algorithms are linear functions (y = mx+b) and exponentials, as well as their inverses, logarithmic.

The basic rules of runtimes is that functions are either:

- Constant
- Linear
- Exponential

Algorithms that are **linear** typically scale 1:1 with input, that is their runtime changes at a *linear* rate with input, this is considered an ***n*** algorithm, as the input of *n* will scale the algorithm. Algorithms that are linear typically follow a very simple, head-on approach of solving the problem.

Otherwise, algorithms that are **exponential** grow exponentially with input, meaning that for small input, their runtimes can be much, much larger than linear functions. These are typically represented by squared (n^2), exponential (2^n), or factorial (n!) functions, and are not suitable for most problems as large input causes an even larger runtime. Some problems are so complex, their only solutions are exponential.

Generally speaking, this notation of efficiency signifies the amount of actions taken based on the size of the input.

If for every one element of input, we do 3 actions, then the number of actions for *n* inputs will be $3n$.

Analyzing runtime complexity can be done by analyzing the number of actions within each iteration of loops and commands

[Iteration Analysis](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Iteration%20Analysis%20dd8f77971f824ae5b90df161719f3bdc.md)

### Memory Complexity

This avenue of efficiency is important for applying algorithms, as programs will generate lots of objects and variables in memory to use to solve their problems. In terms of this course, it is not necessary for us to understand how to deal with memory. 

# Approaches to Algorithms

Algorithms are *steps* to solving a problem, and this problem is defined by the size of the input, whether it is an *n*-size array of numbers, or a *k-*sized linked list, there is a connection between the number of steps we must take to solve the problem, and how much information is provided to the algorithm itself.

There are 2 main approaches to dealing with algorithm design:

1. Iterative → Loops
2. Divide & Conquer → Recursion

### Iteratives

Loops are an integral part to understanding how algorithms scale and grow with the amount of input they are given. Since loops iterate as many times as they are given, they cause the program to repeat steps. This repetition alone is not cause to scale, as it really depends on *how* the loop operates, and whether or not the loop's condition depends on the input.

Not only does a single loop influence the program's runtime, its contents also significantly increase runtime as well. When loops repeat constant-runtime commands, there is very little to scale; however, when loops contain other loops, or functions that are *not constant*, there is a lot of compiling of runtimes that increases overall runtime.

For loops to grow with the size of the input, they must use the size of the input somehow in their iteration limit. For example, if the input is sized as *n*, and a single loop iterates through an *n*-sized array, then it is a linear-runtime loop.

Solving problems iteratively requires data structures that contain the information we must manipulate, and we solve the problem by repeatedly accessing the data structure and using the input information to solve the problem.

### Divide & Conquer

The next approach to dealing with problem solving is quite different, and a little more un-intuitive. The idea behind divide and conquer algorithms use *recursion* as a form of dealing with data structures.

<aside>
💡 Recursion is a method of function-calling in which a function calls itself. All recursive functions must contain a *base case* to be able to catch the base condition to stop infinite calls.

</aside>

Iterative problem solving involves the entire input in its scope, meaning that we do not try and solve small sections of the problem. Recursive problem solving is exactly that, as we create recursive calls to subsets of the input (dividing), solve small sub-problems in those subsets (conquer), and then compare these solved sections to other solved sections, and solve their larger sub-problem.

# Algorithm Properties

These properties are defined by the method we use to solve a problem, and how we utilise space and order of input. 

### In-place Algorithms

The in-placeness of an algorithm is defined by whether or not the algorithm constructs the solution to the problem within the input itself.

For example, if an algorithm is given an array of numbers and asked to sort these numbers ascending, can we somehow use the original array itself rather than creating a new one to store sorted numbers?

(yes, there are sorting algos. that do this).

When algorithms use original data structures to construct the solution, these algos. are called **in-place algos.**

The only importance to note about whether algos. are in-place or not, is to consider how much memory they might end up using.

(if an algorithm is NOT in-place, and must construct 2 NEW arrays to hold over MILLIONS of elements, then we have tripled the memory needed).

### Stable Algorithm

The stability of an algorithm is noted by the ability to maintain the order of identical values.

For example, given an array of numbers to sort in two different ways, can we be sure that identical values would have the same order among themselves?

```python
#the array of student marks, ranked according to their *previous* marks
#thus, the student that got "3" this current time, got the lowest score *last time*
[3, 2, 2, 5, 1, 9, 11] 

#if student *a* got the "2" on the LEFT, and student *b* got "2" on the RIGHT

#stable sorts will maintain the [a, b] subset when sorted by ascending
[1, 2, 2, 3, 5, 9, 11]
```

# Notating Complexities

When dealing with algorithms and trying to label their efficiency, we use functions. However, algorithms cannot always have a single efficiency, because of the nature of problems and the limited steps we can take to solve them.

Algorithms can have cases in which they perform the best, and also those for the worst case, and an average case. For example, if we developed an algorithm to sort an array, and gave this algorithm an already sorted array, it will stop running before the same algorithm given a reverse-sorted array. 

The way we notate this discrepancy is through Big O/Omega/Theta

<aside>
💡 Big O → Worst Case
Big Omega → Best Case
Big Theta → Average Case

</aside>

### Functions

As described before, the types of functions typically used to notate the efficiency of algorithms are:

- Constant
- Linear
- Exponential

We can notate virtually any function using *n* to describe the input

For example, a function with *n* runtime is a linear runtime, while a function with $n^2$ is an exponential function. Things get a little more interesting when we deal with the inverse of exponents, logarithmic functions. 

If we think about it, an exponential function means that for each element we have, we perform a multiple of that amount in actions. So, if we were given an *n-array*, then an exponential algo. would go through the entire array, as many times as there are elements.

On the other side, if we do the opposite by eliminating subsets of the array to access, then we do less actions than there are elements. These are how logarithmic algorithms are born.

So, to describe any algorithm's complexity, we combine this with Big O/Omega/Theta notation to describe all the cases of efficiency for this algorithm.

<aside>
💡 ex. O($n^3$) → Worst case of this algorithm is an exponential runtime

</aside>

### Classes of Cases

Because we have this Best/Average/Worst case format, we can describe and compare algorithms in a standard way. In order to do this, we describe functions of one runtime as classes of functions.

So, for example, an algorithm that is O($n^3$) runtime can be compared to others. For worst cases (O), we use this function as an **upperbounding** for other classes of functions.

<aside>
💡 n < O($n^3$) ; thus n is a member of $n^3$

</aside>

Best cases use a **lowerbounding**, and average cases use a more complicated bounding between curves.

When attempting to classify functions this way, it is always better to have a *tighter bound* to classify functions into.

In order to better visualize and understand algorithmic complexity, check this out: 

[Algorithmic Complexity Cheatsheet](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Algorithmic%20Complexity%20Cheatsheet%208bcdb7ee239c4001a41ae7809052fbea.md)

# Recurrence Relations

These kinds of relations are mathematically driven equations that use previous terms of itself. We can see relations that are not reccurence relations in that of: $y = mx + b$, in which *y* is not defined in previous terms of itself. 

Recurrence Relations are meant to represent a changing series, in which the state of future terms is influenced by previous terms.

Typical RR's can be seen in the form:

$T(n) = T(n-1) + C$

In which the term of T(n) is defined by T(n-1) plus a constant C. Thus, if we wanted to "evaluate" this T(n) term, we must know T(n-1) as:

$T(n-1) = T(n-2) + C$

since we know T(n-1):

$T(n) = [T(n-2)+C] + C = T(n-2) + 2C$

... 

... and vice versa, until we reach 0, 1 as *n*

This applies to algorithms, as *n* is our input size, and we can judge the number of actions based on the current iteration.

Typically, we can construct recurrence relations for any iterative loops given we know their bounds.

Here is an in-depth look at the kinds of recurrence relations we can build from looping commands:

[Loops & Recurrence Relations](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Loops%20&%20Recurrence%20Relations%20f47d8de94e5b4dada17948e63de11c2e.md)

[Heaps & Heap Methods](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Heaps%20&%20Heap%20Methods%205e77de8c9d3c470c9804495846019337.md)

[Graphs](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Graphs%2056de63503f1048dba28ad6b86566c121.md)

---

# Data Structures

This is an overview about the different types of data structures that are used in this course. The overall concept of data structures is a collection of elements, certain data structures depend on a format of inserting and retrieving.

## Arrays

Lists, arrays, and sets all mean the same thing: a collection of elements organized by index numbers. Every element in an array can be referenced by the *index* of the place they hold. In practical programming, all arrays start from index 0, and go up to *n - 1*, where *n* is the total number of elements in the array. Pseudocode arrays start at index 1.

<aside>
💡 [1, 2, 3, 4, 5, 6] → this array has 6 elements in it
→ the first element (1) in this array is located at index 0
→ the last element (6) in this array is located at index 5

</aside>

### Queues

Are array-based data structures that are similar to the way lines form for any event. They are First in, First out structures (FIFO) because the first element to enter the queue, is always the first to leave it. If we had a discrete structure to hold all the elements in a queue, like an array, we would maintain this structure and format by *pushing* elements into the queue *from the back/end,* and *popping* elements out of the queue *from the front*.

### Priority Queues

Based on the queue-format, in which we only add elements to the queue from the back and remove from the front. However, every element is given a *key* which is how we determine *priority* of elements.

Elements are *sorted* by their priority and thus any element with the highest priority are given first attention by removal.

Similar to the way hospital waiting rooms work, patients with the most severe ailments are bumped to the front of the line.

### Stacks

Also are array-based data structures that are exactly what they sound like. Stacks of elements that operate on the same format as a *Pringles can,* and are First in, Last out structures because the first element to go into the stack is always at the bottom, and thus only is taken out once it is the last element in the stack.

## Linked List

Are typically created using *node* objects that have references to other node objects. They are similar to arrays in structure as they create a continuous list of elements that can be referenced in the order they appear from the front.

Node objects and the amount and structure of references determine the type of linked list:

- Singly Linked
- Doubly Linked
- Circular Linked

Singly linked lists are those in which node objects only have a single reference to the *next* node after them, while Doubly linked lists have nodes with two references to other nodes, one for the *previous* node and one for the *next* node. Both these linked lists will have a node that is assigned as the *front*, and we can know which node is the *last* because it will not reference another node.

Circular linked lists are doubly linked lists in which the *last* node's next node is the *first* node, and vice versa.

These references allow for the construction of lists, as the links create an order.

In implementation, to manipulate the elements and order of elements, we manipulate the links to the nodes. For example, to delete a node we simply change the references to it by *skipping* over the node.

## Binary Tree

A tree that maintains the rule of every node having a *maximum* of two children.

In practice, this can be implemented with doubly-linked lists, in which the *previous/next* node references maintain that node's *left/right* children, respectively.

## Binary Search Tree

Are related to binary trees, but maintain an element size rule:

<aside>
💡 Any node's value must be *larger* than it's left child value, and *smaller* than it's right child value.

</aside>

This creates a sorting of the tree, in which the absolute minimal element is accessed by only left children, and the maximal element by only right children.

BSTs can be unbalanced, meaning that we can have only right-children or vice versa, based on the order of insertion.

[Binary Search Tree Methods](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Binary%20Search%20Tree%20Methods%20d999167606f6495397315c992ba9e1d7.md)

## Direct Address Tables

In abstract form, this data structure maintains a *universe* of *keys*, which are typically unique. These keys index a table, which means that there is one row in this table for every key in the universe. Keys reference data, and given a key we can retrieve any data.

In metaphor, it is a filing cabinet of data, in which we have a many drawers, each is dedicated to a single key.

This also means that having lots of keys generates a large table.

## Hash Tables

Similar to *Direct Address Tables*, but are more clever about it. Rather than using unique keys for the whole universe of keys, we use a **hashing function** to generate hash keys for each. Hash values are not exactly unique, and are generated based on the properties of the item we apply the hash function to. This means that similar items can have different hash keys. This helps to maintain a secure table of items that is very fast to access, since we know exactly where to look once we apply the hash function and find the key we want.

Hash keys are not unique, so if by chance, two items have the same key, they **collide**. We can resolve this by using a linked list at every hash key address to hold all the items referenced by this key.

Rather than using one large list for all the items, this hashing creates lots of small arrays that are easy to find because of the function, and are easy to search because they are small.

## [Heaps](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Heaps%20&%20Heap%20Methods%205e77de8c9d3c470c9804495846019337.md)

Similar to binary trees, binary heaps are *trees* in which each *node* has a maximum of two children (hence, binary), and maintains either:

- minimum-node (minheap)
- maximum-noed (maxheap)

In either type of heap, each node's children are constrained to be either less than (maxheap) or greater than (minheap) than the node itself.

They are typically implemented within arrays, because there are universal formula to define the child/parent relationship between indices of an array.

---

# Sorting Algorithms

## Comparison-based

### [Insertion Sort](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Algorithmic%20Complexity%20Cheatsheet%208bcdb7ee239c4001a41ae7809052fbea/Complexities%20e6c04b5ccb734c00b1d43c8dd6220a80/Insertion%20Sort%20a16d20ce377d467398047ba0771c0a9d.md)

Assumes that the first element is already sorted, and the rest are not. As the algo. progresses, it forms the sorted array on the left-side of the array.

Works by comparing the next unsorted element to the already-sorted elements, and shifting the unsorted current element to the correct spot.

```python
def insertionsort(A):
		for j in range(1, lenth(A)): #start from element 2
				key = A[j]
				i = j - 1
				
				while( i >= 0 and A[i] > key ):
						A[i + 1] = A[i] #swap elements
						i = i - 1
		
				A[i + 1] = key #insert key into correct position
```

→ O($n^2$), Omega(n)

→ In-place

### Selection Sort

Is based on *selecting* the *next minimum* element to sort to the left. We start by selecting the first element, and looking through the rest of the array to find an element that is *less than* the current element. If there is such an element, we *swap.* If not, then we increment the element we are currently on.

```python
def selectionsort(A, n):
		for j in range(0, n):
				smallest = j
				for i in range(j+1, n):
						if(A[i] < A[smallest]):
								smallest = i
				swap(A[j], A[smallest])
```

→ O($n^2$), Omega($n^2$)

→ In-place

### Merge Sort

A **Divide & Conquer** approach to sorting, in which the *sub-problems* are unsorted subsets of the larger unsorted set. We tackle this by sorting every pair of values, then every pair of pairs, etc...

Can be done both *iteratively* and *recursively*

<aside>
💡 [8,7,6,5,4,3,2,1]
→ sort [8,7] = [7,8]
→ sort [6,5] = [5,6]
→ sort [4,3] = [3,4]
→ sort [2,1] = [1,2]
= [7,8,5,6,3,4,1,2]
→ merge [7,8] & [5,6] = [5,6,7,8]
→ merge [3,4] & [1,2] = [1,2,3,4]
= [5,6,7,8,1,2,3,4]
→ merge [5,6,7,8] & [1,2,3,4] = [1,2,3,4,5,6,7,8]

</aside>

Iterative → the *merge* function creates a new array, C, which compares two arrays, A and B, for the smaller integers and sorts it into C

```python
def Merge(A, B):
		na = length(A)
		nb = length(B)
		
		i = j = k = 0

		while( (i <= na) and (j <= nb) ):
				if(A[i] < B[j]):
						C[k] = A[i]
						k += 1
						i += 1
				else:
						C[k] = B[j]
						k += 1
						j += 1
```

Recursive → utilizes an iterative merge function, and a recursive *merge-sort* function to organize merging

```python
def merge(A, p, q, r):
			na = q - p + 1
			nb = r - q
	
			let L[1 ... na + 1] and R[1 ... nb + 1] be new arrays
	
			for i = 1 to na:
					L[i] = A[p + i - 1]
		
			for j = 1 to nb:
					R[j] = A[q + j]
		
			L[na + 1] = inf
			R[nb + 1] = inf
	
			i = 1
			j = 1
	
			for k = p to r:
					if L[i] <= R[j]:
							i = i + 1
		
			else A[k] = R[j]:
					j = j + 1

def mergesort(A, p, r): #p = start, r = end
		if( p < r ):
				q = floor((p + r)/2) #midpoint of p+r
				mergesort(A, p, q)
				mergesort(A, (q+1), r)
				merge(A, p, q, r)
```

In this recursive case, mergesort calls itself first on the left half (start to midpoint), then on the right half (midpoint to end) sections of the array A. It fully branches out on the leftmost singletons once it reaches the base case of the start being less than the end.

It basically branches until it reaches the leftmost single element, then stops, and since it returns or does nothing it backtracks to the first left-pair.

Once it reaches this left pair, it merges them in-place. It keeps merging and backtracking until all the first pairs are sorted, and backtracks to merge all pairs of pairs, and onwards.

→ stable

→ O($nlogn$), Omega($nlogn$)

### Quick Sort

Another *divide & conquer* approach to sorting a list, that utilizes a **pivot element,** which is always the *last element* in any partition. The main concept behind quicksort is to use the last pivot element as a midpoint, and put all elements less than the pivot in the indices below it, and all elements greater than the pivot in the indices above.

This creates a semi-sorted list, in which generally the sorting is correctly, in perspective of the pivot.

<aside>
💡 [2,8,7,1,3,5,6,4]
→ 4 is the pivot element
→ once we "partition" this set, we achieve:
[2,1,3,*4*,7,5,6,8]
→ in which we emerge with two subsets [2,1,3] and [7,5,6,8]
→ and we continue to partition each subset with pivots 3 and 8.

</aside>

Eventually as the algorithm continues, we create a tree of branching that results in subsets of single elements, which we backtrack and sort pairs, then sort triples, etc.

![CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/c78c12fa6ea17cfdd7db61f2ebdf7f6f.png](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/c78c12fa6ea17cfdd7db61f2ebdf7f6f.png)

```python
partition(A, p, r):
		x = A[r]
		i = p - 1
		for(j = p to (r-1)):
				if( A[j] <= x ):
						i = i + 1
						swap( A[i], A[j] )
		swap( A[i+1], A[r] )
		return (i+1)
```

→ *r* is the pivot element's index, which is at the end of the subarray. We iterate from the start to the pivot, swapping elements that are less than the pivot to the *ith* index, which creates a less-than subarray to the left of the midpoint, and a greater-than subarray to the right of, and on the midpoint. At the end, we know that the element on the midpoint will be greater than the pivot element, so we swap those elements, and now we have partioned the subarray.

```python
quicksort(A, p, r):
		if( p < r ):
				q = partition(A, p, r)
				quicksort(A, p, (q-1))
				quicksort(A, (q+1), r)
```

→ Quicksort performs the *worst case* when it is given as input an already sorted array. This is because it will partition *n* times down the tree, then backtrack *n* times again. The tree will be *unbalanced.*

→ In-place

→ $O(n^2)$

→ $\Omega(nlogn)$

## Counting-based

These algorithms are not based on comparison sorting, meaning that instead of comparing elements in the array, we use counting techniques to sort arrays.

### Counting Sort

Assumes that we are given an array of *n* values to sort, each element is in the range of [0, k]. Counting sort works better for smaller values of *k* (thus, the variation between numbers is small).

```python
countingsort(A, B, n, k):
		let C[0..k] be new array
		
		for(i = 0 to k):
				C[i] = 0

		for(j = 1 to n): #count occurrences
				C[ A[j] ] = C[ A[j] ] + 1
		
		for(i = 1 to k): #incremental sum
				C[i] = C[i] + C[i-1]
	
		for(j = n to 1): #sort
				B[ C[ A[j] ] ] = A[j]
				C[ A[j] ] = C[ A[j] ] - 1
```

Counting sort constructs an aux. array called C, whose indices correlate to the occurrences of values.

<aside>
💡 C = [w, x, y, z]
→ the 0th element of C is *w*, which is the number of *occurrences* of the value 0 in the original array
→ the 2th element of C is *y*, which is the number of *occurrences* of the value 2 in the original array

</aside>

C is the *counting* array that counts the number of occurrences of values in A, this counting occurs in the *forloop* going from 1 → n.

The next step involves counting from the 0th element to the Kth element in C, and providing the *incremental sum* of each element of C.

The incremental sum refers to the function of summing an element of C to its *left* neighbour. This action adds together the number of occurrences of an *i*th value, plus the (*i-1*)th occurrences. 
This in turn leaves C as a range of indices to place these numbers.

<aside>
💡 C = [0,4,3,1] → 0 zeroes, 4 ones, 3 twos, 1 threes
incremental sum:
C = [0, 0+4, 4+3, 7+1]
→ we use the new summed numbers in the next pair of sums
C = [0, 4, 7, 8]
→ thus, for the value of "1", they range from index 1 → 4, value "2" ranges from indices 5 → 7, and value "3" from 7 → 8.

</aside>

The array B is the sorted array, and the last *forloop* sorts the array A using C *backwards* (starting from the highest on the right to the lowest on the left).

It starts at *n* and progresses down to 1, so it sorts A from the last element to the first. It uses the *value* of this element of A to index C, and inserts the values of A into B based on the range specified within C.

→ Stable

### Radix Sort

Sorts from *least significant digit* to *most significant*

<aside>
💡 ie. given numbers [50, 6, 90, 33, 47, 11] it sorts from the *ones* digit of all these numbers *first*, then by the *tens* digit.
(for a 4-digit → thousand, hundred ten one)

</aside>

This sort is not a comparison sort since it uses *counting sort* as a sub-routine.

<aside>
💡 [50, 6, 90, 33, 47, 11]
LSB (ones)
→ [50, 90, 11, 33, 06, 47]
NSB (tens)
→ [06, 11, 33, 47, 50, 90]

</aside>

The reason it works is because it maintains stability, and thus the order of elements sorted. For example, 50 and 90 are correctly sorted amongst themselves, but in the LSB sort they are not. When they are again sorted by the tens digit, they maintain the same 50, 90 order.

→ Stable

### Bucket Sort

This sort assumes that we have an array of uniformly *distributed numbers* in the range of [0, 1). The violation of this assumption makes this sort useless.

<aside>
💡 A = [0.1, 0.18, 0.11, 0.91, 0.06, 0.55, 0.51, 0.53, 0.44, 0.7]

</aside>

Given this array A, we create an array B whose indices represent the first *tenth* digit, and create linked lists to collect values within this list that have the same *tenth* digit.

<aside>
💡 B = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Each element of B is a linked list that will hold all the values of A whose *tenth* digit (the digit to the *right* of the decimal) match the index.

</aside>

Thus, for the 0th element is a LL that contains only (0.06). The 1st element is a LL that contains (0.1 → 0.18 → 0.11). This roughly sorts the list of numbers, and is similar to Radix sort as we sort by digit bits. We can fully sort this array by doing multiple sorts on each small linked list.

→ Stable

## Structure-based

### Heapsort

Based on the *[heap](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Heaps%20&%20Heap%20Methods%205e77de8c9d3c470c9804495846019337.md)* data structure.

Although heaps in their entirety are not sorted, heaps will always maintain either the minimum or maximum node at their root; which is why any manipulations to a heap must fix any violations to become max/min heaps again.

```python
heapsort(A, n):
		buildmaxheap(A, n)

		for(i = n to 1)
				swap(A[0], A[i])
				maxheapify(A, 1, i-1)
```

We start by building a maxheap from the given array, as we do not know if it is already a maxheap. The next step starts from the end of the array, to the 2nd element (index 1). We swap the root node with the last element of the heap, and maxheapify the new root.

This builds the sorted array backwards in-place, and shrinks the size of the heap down

→ so that elements at the end which are sorted are not re-entered into the maxheap.

→ In-place

---

# Search Algorithms

## Linear Search

The simplest search possible, searching all elements of the array from the first to the last, until the key element is found.

```python
def linearsearch(array, n, key):
			for(int i = 0; i < n; i++):
					if(array[i] == key):
							return i
			return -1
```

→ O(n), Omega(1)

## Binary Search

A more advanced and efficient search, yet requires a *sorted list* to work. It works by knowing that the array is sorted, we start by looking at the midpoint array elements, and deciding to search below the midpoint, or above the midpoint based on the size of the midpoint to the key element.

This kind of search is efficient because every iteration it halves the input, and quickly finds the approximate area the key is in (if at all).

```python
def binarysearch(sortedarray, key):
		low = 0
		high = length(sortedarray)

		while(low < high):
				mid = floor((low+high)/2)
				if(sortedarray[mid] = key):
						return mid
				else if(key > sortedarray[mid]):
						low = mid + 1
				else:
						high = mid - 1

		return -1
```

→ O(log n), Omega(1)

---

# Algorithmic Problems

While rather vague, a "problem" is simply a set of input that has a complicated set of steps to solve. These are problems which can have trivial solutions when given to a human, since there are certain knowledges that can be applied. However, when attempting to write an algorithm that provides a solution, we must think about this: out of the many solutions we can find, how do we know any particular is the *best* one?

<aside>
💡 A solution is a subset of input that satisfies the constraints of the problem. For example, if we are given the problem of solving the shortest path in a maze, which has many paths from the start to the end, how do we know the one we chose is the shortest?

</aside>

### Continguous Maximum Subarray

Given an array of *n* numbers, find a subarray such that the sum of the elements is the largest sum of the whole array

→ contiguous subarray, meaning all elements must be in consecutive indices

<aside>
💡 The array is assumed to be containing both positive AND negative integers.
An array of only positive integers has the trivial solution of the entire array, since the sum only increases.
An array of only negative integers has the trivial solution of the single least negative integer, as the sum of more than one negative integer, is more negative.

</aside>

An approach to solve this can be *brute force*, in which we attempt all subarrays possible and find the best one out of all of them. This is not optimal however, since for every element, we must search the entire array multiple times, making the runtime exponential.

The better approach is to use *recursion* to divide the array into subarrays, and conquer the subproblems.

Given an array, there are two possible cases for the location of the max-sum subarray:

- entirely in either LEFT or RIGHT halves
- crossing between the midpoint

A trick to solving this problem is to understand that checking the crossing between midpoints catches solutions that are found in either half, because we are recursing and dealing with half of the array at a time, we eventually check both halves and crossings simultaneously.

```python
findcrossing(A, low, mid, high):
		leftsum = -inf
		sum = 0
		for(i = mid to low)
				sum = sum + A[i]
				if( sum > left-sum ):
						left-sum = sum
						max-left = i
			
		right-sum = -inf
		sum = 0
		for(j = mid+1 to high):
				sum = sum + A[j]
				if( sum > right-sum ):
						right-sum = sum
						max-right = j
			
	return( max-left, max-right, left-sum+right-sum )
```

→ This aux. function allows us to find the max. sum within halves of the array A. We first check the left-sum by iterating from the midpoint to the start, and sum the elements of A. When the sum increases, we store the maximum index for the increasing sum. Then, we check the right-sum the same way, from the midpoint to the end of the array. What is returned is the two indices of max-left, and max-right, and the addition of the sum.

→ This basically gives a range of elements in [left-sum, right-sum] that results in a large sum.

```python
findmaxsubarray(A, low, high):
		if( high == low ): #base case
				return(low, high, A[low])
		
		else:
				mid = floor((low+high)/2)
				#left division
				left-low, left-high, left-sum =
				findmaxsubarray(A, low, mid)
		
				#right division
				right-low, right-high, right-sum = 
				findmaxsubarray(A, mid+1, high)
			
				#crossing division
				cross-low, cross-high, cross-sum = 
				findcrossing(A, low, mid, high)
			
				if( left-sum >= right-sum AND left-sum >= cross-sum ):
						return ( left-low, left-high, left-sum )
				elif( right-sum >= left-sum AND right-sum >= cross-sum ):
						return ( right-low, right-high, right-sum )
				else
						return ( cross-low, cross-high, cross-sum )
```

→ This recursive function recurses until the base case, of which the low and high indices are the same, meaning that we arrive at single elements of the array as the array itself, of which it returns a range for a possible sum. As it backtracks, it forms a larger range wherever there is an increasing sum, and eventually returns the range and sum.

### Matrix Multiplication

Matrix multiplication is an algebraic operation done only on matrices that share the same number of rows AND columns

<aside>
💡 (m x n) x (n x y) = (m x y)

</aside>

In this problem, we tackle *square* matrices and understand how some solutions to this problem are very inefficient, requiring more optimization.

For example, the iterative approach:

```python
squarematrixmult(A, B, n):
		C = new (n*n) matrix
		for(i = 1 to n): #n
				for(j = 1 to n): #n
						C[i][j] = 0
						for(k = 1 to n): #n
								C[i][j] = C[i][j] + (A[i][k] * B[k][j])
```

→ Through iterative analysis, we see that three nested loops, each of *n* runtime, yield $(n)(n)(n) = n^3$, a really poorly efficient algorithm.

The recursive, divide and conquer approach does not yield any better results:

```python
recursivematrixmult(A, B, n):
		C = new (n*n) matrix
		if(n == 1):
				C[1,1] = C[1,1] * B[1,1]
		else:
				C[1,1] = recursivematrixmult(A[1,1], B[1,1], n/2) + recursivematrixmult(A[1,2], B[2,1], n/2)
				C[1,2] = ...
				C[2,1] = ...
				C[2,2] = ...
```

$T(n) = 8T(n/2) + O(n^2)$ → $O(n^3)$

→ This approach breaks a matrix into 4 sub-matrices, and requires two recursive calls per sub-matrix.

Thus, some dude created the *Strassen Formulae* which reduces any sized matrix multiplication into 10 variables, and we can find any matrix multiplication using 7 commands.

[Strassen Formula](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Strassen%20Formula%20fd5f88a5b6d24edabc86f40d8c7f5048.md)

Using these formula in the following algorithm, we get a *slightly* more efficient solution → $O(n^{log_27})$

<aside>
💡 $log_27$ is slightly smaller than 3, as $log_28 = 3$.

</aside>

```python
Strassen(A, B, n):
		if(n==1):
				C[1,1] = A[1,1] * B[1,1]
		else:
				compute S1 -> S10
	
				P1 = Strassen(A[1,1], S1)
				P2 = Strassen(S2, B[2,2])
				P3 = Strassen(S3, B[1,1])
				P4 = Strassen(A[2,2], S4)
				P5 = Strassen(S5, S6)
				P6 = Strassen(S7, S8)
				P7 = Strassen(S9, S10)

				C[1,1] = P5 + P4 - P2 + P6
				C[1,2] = P1 + P2
				C[2,1] = P3 + P3
				C[2,2] = P5 + P1 - P3 - P7

				return C
```

## Dynamic Programming

Is an approach to problem solving that applies to *optimization problems*, in which we attempt to maximize the outcome given a set of parameters.

In many different problems, solutions often tend to *repeat* calculations or steps. For example, when calculating Fibonacci numbers recursively, we always recurse to find the first fibonacci number, and this happens multiple times per solution. A very obvious answer to this problem is to *store* this result and access it in constant time, rather than calculate it multiple times.

Typical implementations of dynamic programming utilize *matrices* of arrays, which are really fast to access and store (given that we index important values according to the parameters for fast access).

### Memoization & Tabulation

These techniques are how we apply *dynamic programming* to programs. Depending on the type of approach, we can follow these rules:

<aside>
💡 top-down → recursive → memoization
buttom-up → iterative → tabulation

</aside>

Both follow the same concept, but implementation between recursion and iterative programs is different. They store and reference tables of previously calculated function calls. 

### Fibonacci

Recursive Fibonacci algorithms will give the *n*th number of the Fibonacci sequence, given *n*.

<aside>
💡 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...
The next term is Fib. is defined by its previous terms, thus to know Fibonacci's 8th number, we must know the 7th and 6th and their sum.

</aside>

```python
fibonacci(n):
		if( n == 1 or n == 2 ):
				return 1
		return fibonacci(n-2) + fibonacci(n-1)
```

→ this solution is $T(n) = 2T(n-1) + O(1)$ = $O(2^n)$, which is abysmal.

→ We can see that $fib(n)$ is called 15 times, $fib(1)$ is called 3 times, and $fib(2)$ 5 times. We can apply dynamic programming and store these calls to access their values in constant time.

To do this, we must have a good way to reference the answer to the *n*th fibonacci number. The most common way is to create an array with null values, and index the *n*th value of a function call with *n* as a parameter, with the parameter itself.

So, for example, we store $fib(0)$ in index 0, $fib(1)$ in index 1, and so on...

Thus, rather than continuing to recurse on a function call we've done previously, we can check if we've performed it by knowing the parameter and seeing if the array entry is null:

```python
memo = [-inf]
fib(n):
		if(memo[n] != -inf):
				return memo[n]

		if(n == 1 or n == 2):
				return 1

		memo[n] = fib(n-2) + f(n-1)
		return memo[n]
```

→ This version of fibonacci is $O(n)$, which is a large improvement.

<aside>
💡 Remember, *memoization* applies to recursive algorithms. *Tabulation* is an iterative approach in a similar way, looping and storing answers in an array to retrieve calls.

</aside>

### Rod Cutting

This problem centers around maxmimizing revenue gotten by cutting a whole into pieces. Given a rod made of *n discrete pieces*, is there a way to maximize the price we can sell the rod at, if selling different sizes of rods has different prices?

[Rod Cutting](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Rod%20Cutting%203ac25fd0d4cc4df2910bc074fdfcabff.md)

This table shows the different prices we can achieve when we sell rods of different sizes. For example, if we have a rod of length 4, we can split that rod into:

- 4 units of 1 → 1*4 = $4
- 2 units of 2 → 2*5 = $10
- 1 unit of 3, and 1 unit of 1 → 8+1 = $9

Selling these units will yield different gains, and we can see that splitting 4 units into 2, 2 units will give us the most.

Without dynamic programming, a recursive solution is in $O(2^n)$ time.

A problem like this requires storing the *best* solutions of previous calls, so we would determine the maximum between different choices. And for any given division, there are many micro-divisions we can do. We must construct an equation like:

$$
r_n = max_{1<=i<=n}(p_i + r_{n-i})
$$

In which we add together the *indivisble* + *divisible* portions of the rod. As we increase the indivisible portion (no cuts to that portion), then we decrease the divisible portion given a constrained length *i*. 

The *r* in this equation represents the different cases of portions, like previously mentioned, cutting a rod of length 4 has 3 different ways to sell it.

$$
max \begin{cases}i = 1 \rightarrow p(1) +r_{2-1}=1+1\\i=2\rightarrow p(2) + r_0 = 5 \end{cases}
$$

→ thus, $max(2,5)  =5$

→ the best solution for selling a rod of length 2, is to not cut it.

The table we store best solutions for each division is identical to the previous, and we store the solutions indexed to the rod size *i*. A new property of this table hold a value *s*, which is the place that we cut the rod, indexed to the same as the best cost value. This is necessary because to construct a solution, we need to know where the rod was cut, which determines the different sizes.

### Matrix Chain Multiplication

Previously mentioned, matrix multiplication is a very computation-intensive operation. It requires many single operations for knowing even the first cell. Previous attempts at matrix multiplication are not very efficient, requiring $O(n^3)$  and $O(n^{log_27})$ runtimes. This problems requiring calculating the resulting matrix itself, however, we now shift the attention towards finding the best configuration to multiply many matrices together to reduce this unavoidable high cost.

A quick review of matrices sees that any matrix can be of arbitrary size in (rows*columns), or $(x * y)$. Matrix multiplication requires the different matrices to have the *same* number of rows and columns.

<aside>
💡 A = $(p\times q)$
B = $(q\times r)$
→ thus, A has *q* columns, and B has *q* rows.
if C = $A\times B$, then C = $(p\times r)$.

</aside>

Matrix multiplication is also very different from integer multiplcation, as it is not commutative, meaning that:

<aside>
💡 $A\times B\times C \neq A\times C\times B$

</aside>

→ we cannot multiply different matrices themselves

However, MM is associative, meaning that:

<aside>
💡 $A\times (B\times C) = (A \times B)\times C$

</aside>

→ we can change the order in which they multiply.

Given matrices A = [p x q] and B = [q x r], their resulting

A x B = [p x r], but the *number of multiplication operations* is:

<aside>
💡 $p \times q\times r$

</aside>

If we had *m* matrices, how many permutations of orders are there?

$$
\frac{2n \choose n}{n+1}
$$

→ in which n = m - 1

A typical problem this is seen in is when given a *chain* of *n* matrices and their dimensions, find the *best parenthization* to minimize the number of scalar multiplications. This "parenthization" is the way we arrange the parentheses in the multiplication.

Given:

[Chain Matrices](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Chain%20Matrices%2034de41761abb439aa36a1059ffd0846a.md)

We must first notate the different dimensions within variables:

<aside>
⚙ $P_0 = 30$
$P_1 = 35$
$P_2 = 15$
$P_3 = 5$
$P_4 = 10$
$P_5 = 20$
$P_6 = 25$

</aside>

And create two identical tables:

- M → Holds the best number of multiplications
- S → Holds the index of the matrix we "cut" at (parenthesize)

By applying dynamic programming, we find the optimal parenthesizing by minimizing and storing the solutions we come across.

$$
M[i][j] = M[i][k] + M[k+1][j]+p_{i-1}p_kp_j
$$

→ This equation is our way to find the number of multiplications done between matrices. To apply it:

$$
M[i][j] = \begin{cases} 0&\text{i=j}\\ min_{i<=k<j}(M[i][j] = M[i][k] + M[k+1][j]+p_{i-1}p_kp_j) & i < j \end{cases} 
$$

→ Similar to rod cutting, we use the *k value* as an iterator for the different combinations we have.

→ our *k value* ranges between i and j (non-inclusive) and creates our cases.

[M](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/M%20c00c991f2d8e438a9649f1af6b9c5ae2.md)

→ This is an example of the M table. The order we fill it in is (a, b, c, d, ..., o) (diagonally).

→ As we progress, the difference between *i* and *j* increases and creates more permutations of multiplications.

<aside>
⚙ i = 2, j = 4
k ranges between [2, 3], so we calculate the M[i][j] using the minimum function of Min( M[2][2]..., M[2,3] ).

</aside>

→ The *S* table stores the index for best parenthization, indexed the same as M is, and stores the value of *k* for which M[i][j] is minimal.

Once all cells are stored, we can proceed to build a solution by examining the table S and understand the cells represent the *ranges* of parentheses. Thus, cell [1][6] represents the best parenthesization for multiplying matrices 1 → 6. We progress and look at the smaller ranges to find different numbers in the columns.

[Algorithm for Matrix Chains](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Algorithm%20for%20Matrix%20Chains%201dba8844476544fcab510d1db2b54b3e.md)

### Multistage Graphs

Are [graphs](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Graphs%2056de63503f1048dba28ad6b86566c121.md) that contain discrete "stages" of operation. Similar to the depth of trees, these graphs contain nodes in each stage that connect only to the nodes in the *previous stage* and *next stage.*

![https://res.cloudinary.com/practicaldev/image/fetch/s--A-_noYom--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/04l2qwln8pimmu1pqqbf.PNG](https://res.cloudinary.com/practicaldev/image/fetch/s--A-_noYom--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/04l2qwln8pimmu1pqqbf.PNG)

→ Multistage graphs can represent many different kinds of problems that require *stages*. These graphs have no cycles, and are often directional and *weighted.*

Regardless of the specific problem, the main goal of such a graph is to *minimize* the travel from the first node to the last. There are many approaches to this seen much later, but how can we apply dynamic programming to this?

![https://i.gyazo.com/2d14098bb253d5d640f6555063727a47.png](https://i.gyazo.com/2d14098bb253d5d640f6555063727a47.png)

We first create a table, V, that holds all the vertices, and their best cost to reach the goal, and what edge is taken to get the best path.

[Multistage Graph](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Multistage%20Graph%207e0eb3827f9044f39e570745c50327e5.md)

→ An example of a solved multistage graph

Filling in the table is rather simple, as we start from the goal (node 10) and move towards 1. Every node we arrive at, we store the lowest cost to reach 10, and what path we took to get closer to 10.

ie.

Stage 5:

Cost(10 → 10) = 0

Stage 4:

Cost(8 → 10) = 3

Cost(9 → 10) = 8

thus, we note this in table V.

Stage 3:

#because node 5 must go to a node 8 first before 10, we must consider that joint cost

Cost(5) = min(Cost(5 → 8) + Cost(8), inf) = 2 + 3 = 5

Cost(6) = min(Cost(6 → 8) + Cost(8), Cost(6 → 9) + Cost(9)) = min(8, 10) = 8, using node 8

thus, when taking node 6, it is minimal to take node 8 to reach node 10.

...

To construct the minimal path from 1 → 10, we examine the lowest-cost node to take from 1 → 10, which is 4. Best cost from 4 → 10 goes through node 7, from node 7 → 8, node 8 → 10.

→ this gives us (1 → 4 → 7 → 8 → 10), total cost of 12.

### Longest Common Subsequence

This problem is based on two sequences of objects, typically letters, and the goal is to find the longest subsequence that is shared between sequences.

<aside>
⚙ Sequence 1 = A D C K L M N E R P 
Sequence 2 = D E K N G P

</aside>

A subsequence does not require *contiguity*, meaning that the shared letters do not need to be consecutive. They rather *must* be in the *same order* in both sequences.

For example, in the sequences above, a subsequence we can see is:

<aside>
⚙ Sequence 1 = A D C K L M N E R P 
Sequence 2 = D E K N G P
→ E P
→ D K N P
are common subsequences, meaning that *both* sequences contain these letters, in the same order.

</aside>

To dynamically program a solution like this, we must examine if there are any subproblems that can help us solve it. A very simple method to do so is through comparison and branching. If there is no match between letters, we can branch and change the letters we compare in both strings differentially (meaning that we can hold a letter in a sequence, and change the comparison letter in the other sequence). If there is a match, we can increment both sequences and continue comparing until we reach the end of the string.

Like any other problem that can be optimized with dynamic programming, we can see in a full branch that we repeat these subproblems, and then it becomes useful to hold them, indexed, in a table.

For a problem like this, we must construct two tables:

- C, whose rows match the length of seq. 1 + 1, and columns match length of seq. 2 + 1
- B, whose rows match the length of seq. 1, and columns match length of seq. 2

The first row AND column of C (0th row/col) is filled with ZEROES

We evaluate these tables from left → right, row-by-row.

i = 1, j = 1
i = 1, j = 2

...

i = 2, j = 1

In which *i* is an indexer to sequence 1, and *j* is an indexer to sequence 2. The basic rules are as such:

<aside>
⚙ if match:
→ add 1 to previous diagonal
→ label previous diagonal as up-left in B array
if no match:
→ take maximum of previous row/col
→ if that max. is the same, take the top value in C as default
→ label up-arrow in B arrow

</aside>

The equation for this problem:

$$
C[i][j] = \begin{cases} 
0 &\text{i = 0, j = 0} \\ 
C[i-1][j-1]+1 &\text{(i,j > 0) and}& (x_i = y_i)\\ 
max(C[i][j-1], C[i-1][j]) &\text{(i,j > 0) and}&(x_i \neq y_i) \\ \end{cases}
$$

→ in simple terms, if there is a match, we take the left-diagonal value and add 1 to it.

→ if there is no match, we take the max of either:

- cell to the left
- cell to the top
    
    → if the max comes from the top cell, we label that in the B array. if the max comes from the left cell, we label that in the B array.
    

All this algorithm does is label which cells contain a *match* in sequence. We know a cell has common characters when there is a up-left arrow in the B table, otherwise there are left and up arrows. These arrows direct us to the next character in order that is a match.

![CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Untitled.png](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Untitled.png)

To construct the longest common subsequence, we start in the bottom-right cell, and follow the arrows, noting which cells have up-left arrows. These up-left arrows indicate that there is a match between sequences, and we note the character this corresponds to. We follow the left, up-left, and up arrows until we reach a cell that has none, and the LCS is found, except backwards (since we started at the ends of the sequences).

```python
longestcommonsubsequence(string_one, string_two):
		x = len(string_one)  # get string lengths
    y = len(string_two)

    B = [[0 for i in range(0, x+1)]
         for j in range(0, y+1)]  # generate matrices
    C = [[0 for i in range(0, x)] for j in range(0, y)]

    for i in range(1, y+1):  # sequence matching algorithm
        for j in range(1, x+1):
            if(string_one[j-1] == string_two[i-1]):  # match found
                B[i][j] = B[i-1][j-1] + 1
                C[i-1][j-1] = "UL"
            elif(B[i-1][j] >= B[i][j-1]):
                B[i][j] = B[i-1][j]
                C[i-1][j-1] = "UP"
            else:
                B[i][j] = B[i][j-1]
                C[i-1][j-1] = "LE"
```

### 0/1 Knapsack

This problem is similar to the rod cutting problem, as it balances units of items and their prices. In this particular problem, we have solid items (that cannot be split) which have both *weights* and *profits* associated with them. Given a limited capacity bag, how can we *maximize* profits by choosing items to put in this bag?

→ This problem specifically is called 0/1 because every item has the choice to be either:

- 0: excluded
- 1: included

[0/1 Knapsack](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/0%201%20Knapsack%20de9b00928c5442d184f753d3aa4c116a.md)

Given these 5 items with their weights W(i), and profits P(i), how can we max. profits by choosing which items to take into a bag of capacity *10?*

→ We cannot store all items, since 1 + 2 + 3 + 4 + 5 = 15 > 10

→ We must find a combination items as a subset to store in the bag

→ by classic combinations, if every item has 2 choices, then there are $2^5$ possible combinations.

```python
knapsack(n, C): #n = item index, C = bag capacity
		if( n == 0 or C == 0 ):
				result = 0
		else if(W(n) > 0): #W(n) is the weight of an item, P(n) is its profits
				result = knapsack(n-1, C)
		else:
				result = max(knapsack(n-1, C), knapsack(n-1, C - W(n) + P(n))

		return result
```

This recursive solution progresses to find which items are to be included based on the comparison between putting it in, or excluding it.

To apply dynamic programming we store these results in a table T by applying the function:

$$
T_{i,w}=max(T[i-1][w], T[i-1][w-w_i] + p_i)
$$

→ in this equation, we are balancing the maximum between either the previous item, at a certain capacity *w,* OR the previous item at capacity minus current capacity plus the profit of the current item *i*. 

<aside>
⚙ Table T has dimensions $[i+1\times w+1]$, in which i = the number of items and w = the capacity of the bag.
→ ie. if the bag had cap. of 10, then there would be 10 columns for *w*.
Table T also has zeroes in the entire first row and column.

</aside>

[Table T](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Table%20T%20e3a0aa4f596e4517a727b8d8d2eaee01.md)

→ Here we see an example of table T, in which *w* is the horizontal, and *i* is the vertical axis.

We construct the solution by examining the max profit. The bottom-right cell has profit 24, which is the maximum profit seen and is unique to this row, so the max. profit must include item 5.

Because we know the max profit of 24 includes 5, we can subtract the profit of item 5 (24 - 13 = 11) and look at the previous row, item 4. Item 4 has a max profit of 11, but does item 3 also have the same profit? No. This profit of 11 is unique to item 4, so item 4 is included. 11 - 9 = 2, so we examine row 3 and a max profit of 2. Row 3 contains 2, but row 2 and 1 also contain 2. In fact, this max profit of 2 is unique to row 1, because we only consider rows ≤ i, so we know to include item 1.

Thus, the optimal solution contains items: 1, 4, 5. For a max profit of 24.

### Optimal Binary Search Trees

Given 3 nodes to be organized in a binary search tree, in which any node can have a maximum of two children, how do we optimize the order of nodes? With three nodes, there are $\frac{2n \choose n}{n+1}$ total permutations to organize them. Binary search trees are meant to provide efficiency to searching for items within the tree, and given that there are finite items, there is a probability associated with each of them being a search key. This probability increases as nodes become closer to the root node.

Given a 2 trees, and the node probabilities, how do we find which tree is better for searching?

<aside>
⚙ For each node, we perform $depth \times probability$ and add together the *costs*

</aside>

A tree is better than another if its total costs are *higher.*

What about unsuccessful searches? If we are given the probability of an unsuccesful search (which means that the search key would have been at a given node, but it is not) then we can also calculate the costs.

## Greedy Algorithms

These types of algorithms are another approach to finding optimal solutions, and do so in a similar way to dynamic programming. However, the "greedy" approach attempts to find the best local subsolution and build on top of them. This approach leads to *good enough* solutions, sometimes the best, but most often not.

### Activity Scheduling

Given a set of activities who have discrete start and finish times (each of whom $0 \leq S_i<f_i<\infin$), how do we schedule common resources for multiple activities?

We can start by assessing if any activities are *compatible,* which means that their times *do not overlap.* If activity 2 has starting time S2, and finish time F2, then a compatible activity 4 has starting time anything except for in-between S2 and F2.

An easy way to devise when activities are compatible is to sort by finishing time.

[Compatible Activities](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Compatible%20Activities%208225c176a95e4586beb80ec77a38abeb.md)

an example of activities that are compatible is {a3, a9, a11}. This is *a* solution, but not the *optimal* one. The optimal solution contains the *most activities*. To approach this in a greedy way, could use the *earliest starting times* to fit as many activities in. This yields $\{a_3,a_9,a_{11}\}$, but if we were to use *earliest finishing time* we could get $\{a_1,a_4,a_8,a_{11}\}$ which is a better solution.

Rather than attempting to fit in every activity, one-by-one into a schedule, we are using a greedy strategy. This is the basis of any greedy algorithm.

For example, another strategy is to use *shortest activities* to maximize the number of activities occurring in a single day.

```python
greedyactivities(s, f):
		n = s.length
		A = a[1]
		k = 1
		for( m = 2 to n ):
				if( s[m] >= f[k] ):
						A = A.append(a[m])
						k = m
		return A
```

→ we start by using the first element since the array of A is sorted by earliest finishing time

→ we then examine all the activities to see whether there is any activity that is *first* to finish after the current activity *k*. If so, we add that to the solution set.

### Fractional Knapsack

A branch of the 0/1 Knapsack problem, but we use fractional items that do not need to be put in whole. Given a finite capacity bag, and item weights and profits, how to do maximize profits?

Because these items are *fractional*, we can analyze their unit profit, that is, $\frac{profit}{weight}$. This yields some obvious picks, because we can see that some items may have a large profit to weight ratio and should always be taken.

```python
fractionalknapsack(w, p, m, n):
		#w is weight array
		#p is profit array
		#m is bag capacity
		#n is number of items
		for(i = 1 to n):
				cost[i] = p[i] / w[i] #calculate ratio of profit to weight
		sort(cost, descending, w, p) #sort by cost

		i = 1
		total = 0
		
		while( i <= n ):
				if( w[i] <= m ):
						m = m - w[i]
						total = total + p[i]
						i += 1

				else if( w[i] > m ):
						total = total + (cost[i] * m)
						m = 0
						i = n + 1
```

→ we progress by analyzing if the weight of the current item is less than the capacity. If it is, then we can add the entire item and add its profit to the total, and go to the next item.

→ if the weight of the item does not fit in the bag, then we can add in a fraction of the item to get the bag full and maximize profits.

This is a greedy approach since we prioritize items with the highest profit:weight ratio, we will always put entire items whose ratios are the best, and continue using the next best, until we cannot fit a whole item in the bag, and use a fraction to maximize profit.

### Resource Requirements

A problem that deals with serving requests, and allocating resources. Very similar to activity scheduling in that requests have discrete start and end times. A greedy approach to this is to sort by starting and ending times.

```python
resourcereq(s,e,n):
		#s is starting time array
		#e is ending time array
		#n is the number of total requests

		sort(s)
		sort(e)
		count = 0
		resources = 0
		i = j = 1

		while( i <= n ):
				if( s[i] < e[j] ):
						count += 1
						resources = max(resources, count)
						i += 1
				else:
						count -= 1
						j += 1

		return resources
```

This simple greedy approach analyzes whether two requests are compatible by their earliest start and finish times.

### Compression Algorithms

Compression algorithms come in two flavors:

- Lossy
    - more compression, some distortion
- Lossless
    - less compression, no distortion

Certain media are able to use many kinds of compression. Text for example, can only use lossless compression because if we were to lose detail and characters, then the semantics and integrity of the data is destroyed.

Huffman codes are the encoding of DNA sequences, A/C/G/T.

```python
huffman(c):
		n = c.size
		Q = c
		
		for( i = 1 to (n-1) ):
				allocate new node *z*
				z.left = x = extract-min(Q)
				z.right = x = extract-min(Q)
				z.freq = x.freq + y.freq
				insert(Q, z)

		return extract-min(Q) #returns the root
```

Given that A/C/G/T has probabilities of appearance, and that a n-strand is 8*n* bits. We could encode these characters such that the 4 A/C/G/T characters appear in binary

- A = 00 = 45%
- C = 01 = 5%
- G = 10 = 5%
- T = 11 = 45%
    - ACGT strands then require 2 bits.

Since A and T appear the most, we can specify new encodings

- A = 0 (1 bit)
- C = 100 (3 bits)
- G = 101 (3 bits)
- T = 11 (2 bits)
    - space requires (0.45*N*1) + 2(0.05*N*3) + (0.45*N*2)

### Shortest Superstring

Given a list of strings whose order is fixed, and no string is a substring of another, find the shortest string that contains each string in the list as a substring.

<aside>
⚙ AABAC vs. BACCA
→ the ending of AABAC is BAC
→ the start of BACCA is BAC
the shortest super string is thus: AABACCA, concatenating strings such that they overlap to make it shorter than pure concatenation

</aside>

A way to approach this is through graphing the nodes of strings.

<aside>
⚙ BAA vs. ABA vs. AAA vs. AAB vs. BBB

</aside>

→ Because these strings are directional, from left → right, we can impose two different ways to combine some strings.

<aside>
⚙ BAA vs. ABA
→ BAA + ABA = BAABA (1 common)
→ ABA + BAA = ABAA (2 common)

</aside>

We can see that a greedy approach will pick ways that minimize the outcome to create the shortest string, thus picking ways that maximize commonalities between strings.

To graph this, we use directional edges with weights identical to the number of common characters.

BAA → ABA has 1 common

ABA → BAA has 2 common

→ the *tail* of the edge corresponds to the left string

![https://i.gyazo.com/742e9ed2f0891b2bfedfed83cc0da1b1.png](https://i.gyazo.com/742e9ed2f0891b2bfedfed83cc0da1b1.png)

Thus, our greedy approach will pick edges with the *highest* weights and merge the two corresponding nodes to make up a new string and node. The next iteration, we find the commonalities between the new node and existing nodes.

<aside>
⚙ Nodes with no edges are then never picked until the end. The shortest superstring will just append the node since it cannot be merged and shortened.

</aside>

---

# ***Graph Algorithms***

<aside>
💡 [Graphs](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb/Graphs%2056de63503f1048dba28ad6b86566c121.md) → Simple approach to graphs and how to represent them

</aside>

These algorithms cover many different types of ideas in graph theory, and usually look for the best and most efficient ways to traverse a graph.

## Traversal

Traversal algorithms typically use three kinds of variables to maintain the state of nodes in a graph.

- Undiscovered
- Discovered, not explored
- Discovered and explored

The key difference between them is that undiscovered nodes are totally out of the scope of the current node. The current node has no edges to any undiscovered nodes. Discovered nodes are *known* about, they connect directly to the current node, but the *other* connections of discovered nodes are not known. Explored nodes are nodes we have "visited", we have seen all their connections and fully explored them.

The differences between algorithms in traversal is how they pick which nodes to explore next.

### Breadth-first Search (BFS)

Starting from any node *s*, compute the smallest distances from *s* to every reachable node. Produces a *tree.* 

This kind of traversal is typically done using a *queue* structure, called the "frontier", because we store nodes here that are yet to be explored. The key idea is that we explore them in the same order that we discover them.

It is called BFS because it explores the entire *breadth* of a tree *first*. Which just means that it explores all nodes in the same depth/level/layer.

```python
BFS(G, s):
		for( each vertex u element of G.V - {s} ):
				u.color = WHITE #undiscovered
				u.d = inf #unknown distance
				u.pi = NIL #unknown parent
	
		s.color = GRAY #discovered, unexplored
		s.d = 0
		s.pi = NIL
	
		Q = { } #empty set
		enqueue(Q, s)
	
		while( Q !== emptyset ):
				u = dequeue( Q )
		
				for( each v element of G.adjacent( u ) ):
						if( v.color == WHITE ):
						#v is undiscovered
						v.color = GRAY
						v.d = u.d + 1
						v.pi = u
						enqueue( Q, v )
				
		u.color = BLACK #explored
```

→ Even through this algorithm, we see that we only visit/explore nodes which are connected to the current node. Once we explore a node, we "backtrack" and go another way, rather than continuing to explore every node we see.

### Depth-first Search (DFS)

Similar to BFS, Depth-first searching traverses the graph and constructs a *tree*. The main differences between BFS and DFS is that depth-first continues to explore nodes all the way down the depth of the tree/graph. It goes as far as it can until no nodes remain in the path, or until it reaches nodes whose connections are *already discovered*. Once it cannot traverse further down, it backtracks to the previous node that was discovered but not explored, and explores it.

This algorithm can use a *stack*, because it stacks nodes that it discovers, and explores the top of the stack only.

DFS can be applied further to construct a *forest* of trees, assuming that there are nodes that are not discovered, it will pick a new undiscovered node and continue exploring.

If we want to track the iteration/timestamp of discovery and exploration, DFS can track these while it traverses. DFS is also used to [classify](CP312%20%E2%80%94%20Algorithms%20(W2020)%20fa3890396fd24c039a79d4b585d0c0bb.md) parts of a graph, because it will traverse an entire depth of paths and use these timestamps to understand if directional edges create components of the graph.

```python
DFS( G ):
		for( each vertex u element of G.V ):
				u.color = WHITE
				u.parent = NULL
		time = 0
		for( each vertex u element of G.V ):
				if(u.color == WHITE ):
						DFSVISIT(G, u)

DFSVISIT(G, u):
		time = time + 1
		u.d = time
		u.color = GRAY
		
		for( each v element of G.adjacent(u) ):
				if(v.color == WHITE ):
						v.parent = u
						DFSVISIT(G,v)

		u.color = BLACK
		time = time + 1
		u.f = time
```

→ this implementation allows DFS to recursively traverse connections of any node *u*, which are adjacent to *u* and called *v*.

→ this also manages to discover and explore nodes that are not initially connected to any first nodes, because it iterates through all nodes.

## Classifying

### Edge Classes & Strongly Connected Components

DFS allows for timestamping and comparing times between the discovery of nodes and their exploration. With the combination of directional edges, DFS can explore areas of graphs which are connected, and can tell which areas of the graph are *strongly connected* and which are *weakly connected.*

<aside>
⚙ The Components of any graph are the sub-graphs which are connected. Undirectional graphs are always strongly connected, which means that from any node *u*, you can reach any node *v*, as long as it is connected. Directional graphs change this rule, as edges may not allow traversing of the graph from any node *u* to any other node *v*. Certain components may be more strongly connected to others.

</aside>

To find these components, we must first classify edge types:

- Tree edge
    - any edge from *u* to *v* found by exploring *u* to *v*.
- Back edge
    - edge between nodes *u* and *v*, in which *u* is farther along the tree than *v. v* is an ancestor of *u.*
- Forward edge
    - any edge that is neither a tree or a back edge
    - it connects a previously discovered node to a later discovered node, that is an ancestor connects to a child.
- Cross edge
    - any edge that is neither a tree, forward, or back edge.
    - if the time to discover *u* is greater than the time to discover *v*, then it is a cross edge.

In order to have an algorithm discover strongly connected components, we must be able to *transpose* the graph.

<aside>
⚙ Transposing a digraph means to flip all directional edges. The transpose of a graph $G = G^T$.

</aside>

```python
stronglyconnected(G):
		DFS(G)
		G_t = transpose(G)
		DFS(G_t)
```

→ while counterintuitive, this algorithm allows us to examine the finishing times for the transposed graph DFS. After the first DFS, the initial finishing times are computed for all nodes in G. Then we perform the DFS on the transpose, and see that the first node to be explore is the last node from the first DFS.

This node will expose the first strongly connected component to us and see that the path taken in transposed DFS is the strongly connected component. After this, we remove the finishing times of those already-known components finishing times out of the list, and continue to explore the paths for the next highest finish time node.

## Minimum Spanning Tree

A minimum spanning tree is the tree constructed which contains *all nodes* with a minimum cost/weight. 

### Kruskal's

This algorithm finds edges that are *safe edges* which contribute to the MST, and do not create a *cycle* in the tree (which breaks the tree property). It does so by using the smallests weights from the available edges.

This algorithm uses some simple routines:

```python
make-set(x):
		x.parent = x
		x.rank = 0

link(x,y):
		if(x.rank > y.rank):
				y.parent = x
		else:
				x.parent = y
				if(x.rank == y.rank):
						y.rank = y.rank + 1

find-set(x):
		if(x != x.parent):
				x.parent = find-set(x.parent)
		return x.parent

union(x,y):
		link(find-set(x), find-set(y))
```

```python
Kruskal(G, w):
		#g = graph
		#w = weights
		A = {empty set}
		for( each vertex v element of G.V ):
				makeset( v )

		sort(edges of G.E in increasing order of weight)

		for( each edge(u,v) from sortedlist ):
				if( findset( u ) != findset( v ):
						A = A UNION (u,v)
						union(u,v)

		return A
```

### Prim's

This algorithm forms a *single tree*, growing from an arbitrary root *r*. Nodes not part of the tree, are placed in a *minimum priority queue* based on *v.key*, which is an *edge* with a minimum weight connecting *v* to a vertex *within* the tree.

The set A contains the finished MST once the minQ is empty.

```python
Prim(G,w,r):
		for( each element u of G.V ):
				u.key = inf
				u.parent = NULL

		r.key = 0
		Q = G.V #minQ
		
		while(Q != empty):
				u = extractmin(Q)
				for( each element v of G.adjacent(u) ):
						if( (v is element of Q) and (w(u,v) < v.key) ):
								v.parent = u
								v.key = w(u,v)
```

→ Prim's algorithm takes nodes with the smallest weighted edges and looks through its neighbors to understand if that neighbor is still not in the MST, and the the weight of taking the edge from u → v is smaller than v's key.

→ $O(|E| log(|V|))$

# Shortest Path

## Single Source

Uses BFS to construct and determine the *shortest paths*, but only works on unweighted graphs only. These algorithms determine all the shortest paths, from a single source *u* to all other nodes.

### Bellman-Ford

This algorithm can use negative weighted edges, with the constraint that there can be no loops of net-negative weight (meaning that it would always take the loop because it decreases the weight infinitely).

Routines:

```python
init-single-source(G, s):
		for( each element v of G.V ):
				v.distance = inf
				v.parent = NULL
		s.distance = 0

relax(u,v,w):
		if( v.distance > (u.distance + w(u,v)) ):
				v.distance = u.distance + w(u,v)
				v.parent = u
```

→ the assumptions here are that every node stores the distance from the single source to the node. Relaxing changes the distance of the node if there is an edge that causes a decrease in distance, which is the distance to reach node *u* plus the weight from u → v.

```python
bellmanford(G, w, s):
		init-single-source(G,s)
		
		for(i = 1 to (len(G.V) - 1) ):
				for( each edge (u,v) element of G.E ):
						relax( u, v, w )

		for( each edge (u,v) element of G.E ):
				if( v.distance > u.distance + w(u,v) ):
						return FALSE

		return TRUE
```

→ will return FALSE if there is a net negative weight cycle

→ otherwise, it returns true and the shortest path using the member's of a node (parent/child).

→ if a graph has |V| edges, and the shortest path has no cycles, then the shortest path can have a maximum of |V| - 1 edges.

→ the relax routine is called |V| - 1 times, for each edge.

### Dijkstra's

Works on the assumption that all weights are positive. It uses a minimum priority queue (minQ) to store all unexplored nodes, and a set S for explored nodes.

This algorithm uses the same routines as Bellman-Ford:

```python
init-single-source(G, s):
		for( each element v of G.V ):
				v.distance = inf
				v.parent = NULL
		s.distance = 0

relax(u,v,w):
		if( v.distance > (u.distance + w(u,v)) ):
				v.distance = u.distance + w(u,v)
				v.parent = u
```

```python
dijkstra(G, w, s):
		init-single-source(G,s)
		
		S = {empty set}
		Q = G.V #minQ

		while( Q != empty ):
				u = extract-min(Q)
				S = S UNION {u} #append u to s as it is explored
				for( each vertex v element of G.adjacent(u) ):
						relax(u, v, w)
```

## Single Destination

Is the opposite to single source, as we try to find the shortest paths from all nodes to a single node.

## Single Pair

Finds the shortest path between a given source and desination (single pair of nodes)

## All Pairs

Finds the shortest path from all pairs of vertices

### Floyd-Warshall

Uses matrices of $|V| \times |V|$ dimensions. Two matrices are constructed, one to hold the parent/predecessors of nodes, and the other to store distances and costs.

As the algorithm iterates, we create/edit new versions of these matrices to update information.

The parent matrix shows all the paths to get from one node to another, and through which node.

For each iteration, we consider all the paths from one node to another, through each node.

![https://i.gyazo.com/c2da39ed40ad41773e6cf297f708f7d2.png](https://i.gyazo.com/c2da39ed40ad41773e6cf297f708f7d2.png)

The first iteration considers all paths going through node 1. Then we examine the costs and paths of all other nodes going through 1. For example, node edges exist for 4 → 2, but there exists a path 4 → 1 → 2, with a total cost of 2+3 = 5.

There is also a path from 4 → 1 → 3, with a cost of 10, but there already exists a path 4 → 3 with cost -5, much lower. 

While updating this new cost in the cost matrix, we also update the parent matrix to match. Previously, no path existed from 4 → 2, but through node 1, cell [4][2] now contains a 1, since we go through 1.

# Backtracking

Is an approach to find *all* possible solutions. This is used to find all permutations in a sense, and is done through *space-state trees*. Backtracking is naturally done through DFS.

## Permutations

Given the problem of finding all permutations that 3 distinct cars can park into 3 distinct parking spots, how many possibilities are there? What if we were to constrain the variables, by disallow certain cars to park in certain spots?

A very simple way to do so is to examine all the branches that happen when we put any car in the first spot. the red and blue cars can park in the first spot, but the green car cannot. This *prunes* a subtree and we automatically satisfy the constraint. Next, we examine how the leftover cars can park in the leftover spots.

We can see that when we constrain a variable, we have only 4 possibilites:

<aside>
⚙ S1(R) + S2(G) + S3(B)
S1(R) + S2(B) + S3(G)
S1(B) + S2(G) + S3(R)
S1(B) + S2(R) + S3(G)

</aside>

## Hamiltonian Circuits

A hamiltonian circuit is a cycle that visits all nodes in a graph exactly once. A very simple way to do this is through DFS, by choosing any node to start and visiting all unvisited nodes, until we either cannot reach a directly, or all the edges from the last node are already visited. 

# Branch & Bound

Another approach to finding all possible solutions, while using BFS. The "bound" portion allows us to create *bounding conditions* in which we can prune subtrees.

## Subset-sum

Given a collection of numbers, find a subset that will equal a certain key value *d*. This problem is made easier by sorting all values first, then we can traverse this state-space using DFS.

We start this state-space problem using 0 as a root node, since there is an option to include no numbers. Every branch is binary, meaning that we have a choice of either including or excluding members of the set. The bounding condition here is that we backtrack when we include numbers that make the sum of values greater than the key. Another condition is that if we run out of elements, we cannot progress and we prune the subtree.

## Assignment

This algorithm uses a *best-fit* branch-and-bound, it is greedy and chooses the optimized branch to continue branching. An example of this is given a list of jobs, and people who can do those jobs, whose intersections mark the *cost* of each person doing those jobs, what is the optimized solution or configuration of people to jobs?

We can start this by creating a bounding equation of choosing the total lowest costs, regardless if the same job is done by two people. By altering this bounding equation from the top-down, and choosing different people with the lowest costs that also satisfy the rules, we can branch. Then we start choosing the next best person to do the job.

## Knapsack

As in the previous knapsack problem, we can calculate the ratio of profit:weight to make a better choice in items. The bounding equation is as such: $V+(C-w)(\frac{v_{i+1}}{w_{i+1}})$.

In the first iteration, a capacity of 10 means that the upper bound is 100 since there are no items, and the C - w = 10 is multiplied by the first item's value-weight ratio of 10.

Like in previous B&B techniques, we branch from the root node to either include item 1, or exclude it, and then calculate the bounding equation every node to score how good the branch is.

## Travelling Salesman

This is a classic problem in which a salesman must travel to all the cities, keeping the cost to a minimum.

In a case like this, we use a lower-bounding equation:

$$
S = min(a\rightarrow(b,c,d)) + min(a\rightarrow(b,c,d))
$$

→ this equation takes the two best (minimum) moves from a, to its connecting nodes b, c, or d. We take the ceiling of the sum, of every node's best moves and divide this by 2 to branch.