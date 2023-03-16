# Loops & Recurrence Relations

Similar to how we can analyze runtime by understanding explicity how loops progress, we can do so with recurrance relations.

Instead of analyzing loops and iterative commands, recurrence relations are used to analyze *recursive functions*.

---

# Relations

The following formats of relations relate to how the recursion call deals with the input. For example, decreasing functions will always take away from *n* when recursing, the difference between types is the way calls are made (in loop, two in a row, etc.)

Dividing relations divide the input that is sent to the recursion call.

## Decreasing

### Linear

```python
function(n) #T(n)
		print(n) #C
		function(n-1) #T(n-1)
```

$T(n) = T(n-1) + C$

→ T(n) = 1, when n = 0 (base case)

→ T(n) = T(n-1) + C, when n > 0

...

T(n) = [T(n-3) + C) + 2C]

T(n) = (T(n-k)) + kC

→ stops when n = k

T(n) = T(n-n) + nC

T(n) = 1 + n

→ **O(n)**

### Quadratic

```python
function(n)
		if( n > 0 )
				for(i = 0 -> n) 
						function(n - 1) #n
```

$T(n) = T(n-1) + n$

→ T(n) = 1, when n = 0

→ T(n) = T(n-1) + n, when n > 0

...

T(n-1) = T(n-2) + (n-1)

T(n) = (T(n-2) + (n-1)) + n

...

T(n) = T(n-k) + (n-(k-1)) + ... + (n-2) + (n-1) + n

→ stops when n = k

T(n) = T(n-n) + (n-n+1) + ... + (n-1) + n

T(n) = T(0) + 1 + 2 + 3 ... + n

→ the sum of a continuous series = $(n(n+1))/2$

→ $n(n+1) = n^2 + n$

→ the largest degree is $n^2$

→ O($n^2$)

### Logarithmic

```python
function(n)
		if(n > 0)
				for(i = 0; i < n; i = i*2) #logn
						function(n-1) #t(n-1)
```

$T(n) = T(n-1) + logn$

...

T(n) = T(n-3) + log(n-2) + log(n-1) + log(n)

→ stops when n = k

T(n) = T(0) + log(1) + log(2) + log(3) + ... + log(n)

→ T(n) = T(0) + log($n!$)

→ T(n) = 1 + log(n!)

We cannot express this relation as a definite function right now, but we can express it in terms of its *class*. 

log(n!) ≤ log(n) + log(n) + ... + log(n)

→ sum of log(n) = log($n^n$) = $nlogn$

log(n!) ≤ sum of log(n)

→ the sum of log(n) is an *upper bound*, so we can say that:

→ log(n!) ≤ nlogn

→ O(nlogn)

### Exponential

```python
function(n) #T(n)
		if(n > 0)
				function(n-1) #T(n-1)
				function(n-1) #T(n-1)
```

$T(n) = 2T(n-1) + 1$

...

T(n) = 2T(n-1) + 1

T(n) = 2(2T(n-2)+1)+1

→ T(n) = $2^2$T(n-2) + 2 + 1

...

T(n) = $2^k$T(n-k) + $2^(k-1)$ + ... + $2^2$ + 2 + 1

→ stops when n = k

→ the *geometric progression* a + ar + a$r^2$ + ... a$r^k$ = a($r^k$$^+$$^1$ - 1)/(r-1)

T(n) = $2^n$(T(0)) + (2$^k$$^+$$^1$ - 1)

T(n) = 2$^n$ + 2$^n$-1

T(n) = 2$^n$$^+$$^1$ - 1

→ the largest degree is $2^n$, thus

→ O($2^n$)

## Dividing

One thing of note is that the *constant* term is given in Big O notation

```python
function(n)
		if(n > 0)
				function(n/2)
				
```

$T(n) = 2T(n/2) + O(n)$

...

T(n/2) = 2T(n/($2^2$)) + n

T(n) = $2^2$(2T(n/($2^3$)) + n/($2^2$) + 2n

...

T(n) = $2^k$T(n/($2^k$) + 2n

→ stops when n/($2^k$) = 1, so when n = $2^k$, thus k = logn

T(n) = $2^k$T(1) + (n)logn

→ thus, this relation is bounded to nlogn

## Trees

We can construct *trees* to represent the branching of the recursion, mostly used with *[dividing](Loops%20&%20Recurrence%20Relations%20f47d8de94e5b4dada17948e63de11c2e.md)* relations.

For example, when we divide the input on recursion by *2*, then each branch has (n/2) halves. 

If we sum the *steps taken* in this tree, breadth-wise, then we will always sum to *n* steps.

→ n = n, n/2 + n/2 = n, ...

The height of this tree (depth) is also *log n*, because we divide input by 2 every step.

→ thus, the runtime of dividing relations of $T(n) = 2T(n/2) + O(n)$ is nlogn

<aside>
💡 This requires understanding of the fact that 2T(n/2) = T(n/2) + T(n/2). Each recursion is a branch, so if we branch twice for every node, both nodes will have an even amount of n.

</aside>

→ this changes when dealing with: $T(n) = T(n/3) + T(2n/3) + O(n)$, because one branch gets 1/3, while the other gets 2/3 of the input.

# Master's Theorem

A quick and accurate algorithm to solve a recurrence relation's runtime.

<aside>
💡 $T(n) = aT(n/b) + f(n)$

</aside>

Relations must be in this form, where $f(n) = O(n^k log^pn)$.

Variables of importance:

- a
- b
- k

Given any relation in this form, we follow the *general* steps:

- if( $f(n) = O(n^{logb(a) - e})$ )
    - T(n) = $\theta(n^{logb(a)}$)
- if( $f(n) = \theta(n^{logb(a)})$ )
    - T(n) = $\theta(n^{logb(a)}*lg(n))$
- if( $f(n) = \Omega(n^{lob(a) + e}) and(af(n/b)  <= cf(n))$ )
    - T(n) = $\Omega(f(n))$
    

Given a *dividing relation* of the following form:

<aside>
💡 T(n) = aT(n/b) + f(n)
f(n) = O($n^k$$log^pn$
a ≥ 1, b > 1

</aside>

Follow these steps:

- if( $a > b^k$ )
    - T(n) = $O(n^{log_b(a)})$
- if( $a = b^k$ )
    - if( p = -1 )
        - T(n) = $O(n^{log_b(a)}*log(log(n)) )$
    - if( p > -1 )
        - T(n) = $O(n^{log_b(a)} *log^{p+1}(n) )$
    - if( p < -1 )
        - T(n) = $O(n^{log_b(a)})$
- if( $a < b^k$ )
    - if( p ≥ 0 )
        - T(n) = $O(n^k *log^p(n))$
    - if( p < 0 )
        - T(n) = O($n^k$)

Given a *decreasing relation* of the following form:

<aside>
💡 T(n) = aT(n - b) + f(n)
f(n) = O($n^k$), k ≥ 0
a > 0, and b > 0

</aside>

Follow these steps:

- if( a > 1 )
    - T(n) = O($f(n) * a^{n/b}$)
- if( a = 1 )
    - T(n) = $O(n*f(n))$
- if( a < 1 )
    - T(n) = $O(f(n))$