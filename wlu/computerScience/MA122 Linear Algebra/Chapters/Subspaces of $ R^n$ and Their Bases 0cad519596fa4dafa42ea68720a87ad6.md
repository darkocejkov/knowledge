# Subspaces of $\R^n$ and Their Bases

# 5.1 Subspaces of $\R^n$

<aside>
💡 the **real** n-space $\R^n$ consists of all vectors of the form $v = [v_1, v_2,v_3,..., v_n]$ and the *vector operations:*

> Such as the vector addition (sum) of two vectors, v and w: $v + w$
> 
> 
> The scalar product $bv$.
> 
</aside>

In set theory, this is what the n-space of $\R^n$ looks like:

$$
\R^n = \begin{cases}\begin{bmatrix}v_1\\v_2\\...\\v_n\end{bmatrix}: v_1, v_2, ..., v_n \in \R\end{cases}
$$

In these n-spaces, the two operations of the *sum* and the *scalar product* satisfy the properties we looked at previously, like:

SUM (vector addition)

- commutative $u + v = v + u$
- associative $(u + v) + w = u + (v+w)$
- 0 is the additive identity $u + 0 = u$
- additive inverse $u + (-u) = 0$

Scalar Product

- associative $(ab)u = a(bu)$
- 1 is the mult. identity $1u = u$
- distributes over vector addition $a(u + v) = au + av$
- distributes over scalar addition $(a+b)u = au + bu$

In $\R^n$, all of these properties remain true. They will also remain true in *subsets of $\R^n$,* because these subsets are *closed* under both vector addition and scalar mult. 

So what is a subset of $\R^n$? They are called **subspaces:**

<aside>
💡 Linear Subspace

a subspace V of $\R^n$ is a subset that satisfies the following conditions:

a) contains the ZERO vector ($\overrightarrow{0}$)

b) closed under vector addition, $v, w \in V, v+w \in V$

c) closed under scalar multipli. $w \in V$, then for any $a \in R, aw \in V$.

that is, "closed" means that the result of the function is in the same subspace as the input vectors.

d) V is non-empty (it has ≥ 1 vector)

</aside>

→ condition d) basically verifies that any subspace of $\R^n$ has at least 1 vector, and since it is closed under scalar. mult., then $0w = 0$, is implied to always be contained in the subspace.

<aside>
💡 Trivial Subspaces

the subspace $\{\overrightarrow{0}\}$ is called the **trivial subspace** of $\R^n$. Non-trivial subspaces are any that are not the trivial. A **proper subspace** of $\R^n$ is a subspace that is different from *both* the trivial subspace, and the "universe" $\R^n$.

</aside>

Because of the definition of a subspace, any subspace that is not the trivial subspace has $\infin$ vectors, because of the subspace being closed under vector sums and scalar mults., then there are infinitely many vectors that exist because the results of adding or scaling vectors is also in that subspace.

In order to find out whether or not a *subset* of $\R^n$ is actually a **subspace** of $\R^n$, we can look for the easiest case of a vector, the zero-vector.

For example, take this subset S:

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled.png)

Is it a subspace? 

→ it is only a subspace if the zero vector: $[0,0,0]$ is part of the solutions, and conforms to the relation $x_1 + x_2 + x_3 = 1$. So, 

$$
0 + 0 + 0 = 0 \ne 1
$$

→ so the zero vector is not part of the subset of vectors, so this subset is NOT a subspace.

However, to prove that a subset IS a subspace, we need to show that all three conditions (zero vector, closed addition, closed scalar) are true.

Zero Vector) $0 + 0 + 0 = 0 = 0 \checkmark$, W contains zero vector

Closed Sum) take two arbitrary vectors U and V, and add their arbitrary elements to create W.

$w_1+w_2+w_3 = (u_1+u_2+u_3)+(v_1+v_2+v_3) = 0+0=0$

Closed Scale)

$au_1+au_2+au_3 = a(u_1+u_2+u_3) = a*0 = 0$

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%201.png)

What we can see from these examples is that, generally:

<aside>
💡 a) the set of solutions of a *single, homogenous (equates to 0)* linear equation, which has coefficients in $\R$ is a subspace of $\R^n$

b) the set of solutions to the *non-homogenous* system of the same coefficients (n unknowns) is NOT a subspace of $\R^n$

</aside>

This is a pretty simple proof of b), because the system is non-homogenous, it can never have 0-vector as a solution, so it is not a subspace.

Proving a) is also straightforward. We have to show that all 3 conditions are true. Because it is homogenous, it has a trivial solution of the 0-vector, meaning that the zero vector is part of the subset of $\R^n$. By the definitions of vector sums and scales, it is also implied that these are true, because they remain closed no matter the size of *n*. 

→ for any equation in terms of the 0 vector, there is always the additive identity that can equate to the zero-vector. 

We can see that when we broaden it to deal with multiple subspaces, the *intersection* of the solutions is also a subspace of $\R^n$.

If we recall back to ch. 1.6, a plane $\pi$ in $\R^n$ through the origin consists of all vectors of the form: $x = su + tv$, where the vectors *u and v* are linearly independent. This plane is a subspace of $\R^n$

→ this is proven by showing that all 3 conditions remain true for the equation of a plane. The zero vector is a part of the subset because for any vectors u and v, we can always use $s = t = 0$ and get the 0 vector in return. Vector addition is also closed, because adding two planes results in $w_1+w_2 = (a_1u+b_1v) + (a_2u+b_2v)=(a_1+a_2)u+(b_1+b_2)v$, which is part of the plane $\pi$, and $a_1+a_2 \in \R$. Similarly, scaling a plane by *s* results in the same idea, that $(sa)u + (sb)v$ is part of the plane $\pi$.

Think about lines now, aren't they also a subspace of $\R^n$? Yes, because the equation of a line conforms to the 3 conditions the same way that planes do.

Now, we can represent this geometrically. We can understand that lines and planes *through the origin* are subspaces of the Euclidean space $\R^n$, because their equations are *homogenous*. They satisfy all 3 conditions of a subspace of $\R^n$. Think of them like the *basis* of different spaces that can be represented within *n*. In $\R^2$, a line is a subspace, and a plane is as well. Any solutions to a *consistent, non-homogenous* systems are then **translations** of the subspace of the homogenous system, with the same coefficients.

This is like with *functions*, we have the typical functions of a line $y = mx+b$, and a parabola $ax^2+bx+c =y$. Any function goes through the origin, because it is a subspace of the of the *cartesian plane*. Functions can also be translated like vectors and planes.

This is exactly why solutions of a *homogenous* system and the corresponding *non-homogenous* systems are very similar, and are related by an **offset,** which is like the translation vector. We have a subspace that represents slices and lines of the Euclidean space, and then we translate it by some other vector(s) to capture a different subspace of the space, but with the same direction.

One way to think about the vectors captured in a subspace of $\R^n$ is that given a homogenous system, this equation is like the *entry criteria* of vectors in the space of $\R^n$ to enter the subspace. Vectors are only in the subspace if they fill the criteria. In the example below, the vectors included in the subset S are only included if their dot-product with the vector of [1,2,...,n] is ≥ 0. 

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%202.png)

To test whether this subset is a subspace, we test the 3 conditions:

1) zero-vector: 

$0 \cdot n = 0$. So, the zero vector is valid and passes the criteria, and is part of the subset.

2) Closed under addition: 

Given that any vector in the subset passes the criteria, we know that for vectors in S called v and w, $v\cdot n \ge0$ and $w\cdot n \ge 0$. So, $(v+w)\cdot n=v\cdot n+w\cdot n \ge 0$ because both v and w's dot product are AT LEAST, or greater than 0.

3) Closed under scale: 

the space-vector *n* is a valid vector to test in this system, so we can test if $n\cdot n \ge 0$. This is true, because $n\cdot n = ||n||^2 = 1 > 0$. However, due to the nature of dot-product, $(-n)\cdot n=-||n||^2 = -1 < 0$, so *n* is not a part of S, and thus this subspace is NOT closed under scalar product because $(-1)n$  is not a part of the subset. 

So, S is NOT a subspace of $\R^n$.

# 5.2 Linear Combinations & Linear Independence

In previous chapters, solving for a *homogenous* linear system resulted in **general solution** that are in the form of scalar parameters and vector additions of those scales. This form is also a very useful tool in represent subspaces of $\R^n$, and is called the **linear combination**

<aside>
💡 Linear Combination

given $v_1, v_2, ..., v_k$ to be a *collection* vectors in $\R^n$, with the collection being *S.* Thus, a vector $w \in \R^n$ is a linear combination of $v_1, v_2, ..., v_k$ if there exists scalars such that

$$
w = t_1v_1+t_2v_2+...+t_kv_k
$$

→ this is what we call a "representation of *w* as a *linear combination* of vectors in S" and the $\R$ numbers in the scalar parameters are called the **coefficients of the linear combination**

</aside>

→ a *collection* of vectors is different than a *set* of vectors. Namely, a **collection of vectors can contain copies of the same vector**, while *all vectors in a set must be distinct.*

The zero-vector can be represented through linear combinations, and is always a linear combination of ANY COLLECTION OF VECTORS in $\R^n$, and the coefficients are ALL 0; this is called the **trivial representation of 0**.

$$
0 = 0v_1 + 0v_2+...+0v_k
$$

Often the problem we seek to understand is that when we are given arbitrary vector *w*, and a collection S of vectors in the space, determining if *w* is actually a linear combination of the vectors in S.

We can also involve matrix products into this concept to simplify the equation of lin. combinations, given $t = \begin{bmatrix}t_1\\t_2,\\...\\t_k\end{bmatrix}$, $A = [v_1, v_2, ..., v_k]$, then the linear combination of the *k* vectors $v_1, v_2, ..., v_k$ with the coefficients $t_1, t_2, ..., t_k$ is:

$$
At = t_1v_1 + t_2v_2+...+t_nv_n
$$

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%203.png)

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%204.png)

![Linear combinations as scalars and sums](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%205.png)

Linear combinations as scalars and sums

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%206.png)

![Linear combination as matrix product](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%207.png)

Linear combination as matrix product

We can see that in the left col., we can intuitively combine the 4 vectors of V with the parameters of A and obtain the linear combination vector. In the right col. however, we have the same vectors represented as a matrix, multiplied with the vector in which each element corresponds to the row.

Linear combinations are actually related to the concept of subspaces, and here is why:

<aside>
💡 Lemma 5.2.5

Given V to be a subspace of $\R^n$ and vectors $v_1, v_2, ..., v_k \in \R^n$. If $v_1, v_2, ..., v_k \in V$, then $v_1 + v_2 + ... + v_k \in V$

</aside>

This is true because of the fact that a subspace is closed, meaning that the sum of any two vectors in V also belongs in V. This leads into the next theorem:

<aside>
💡 Subspace contains linear combinations

Based on Lemma 5.2.5's conditions, any linear combination of vectors $v_1, v_2, ..., v_k \in \R^n$ also lies in $V$.

</aside>

This is proven because both scalars and vector sums are closed under the subspace, meaning that any $a_iv_i \in V$, and any $v_i + v_j \in V$, then any linear combination of $a_1v_1 + a_2v_2+...+a_kv_k \in V$.

This is also how we can obtain **subspaces of $\R^n$ through linear combinations:**

<aside>
💡 Linear Span

$v_1, v_2, ..., v_k \in \R^n$, with all vectors in a collection called *S*. The linear **span** of S, denoted by $Span(S)$ is the set consisting of *all linear combinations of the vectors in S*.

$$
Span(S) = Span(v_1, v_2, ..., v_k) = \{a_1v_1+a_2v_2+...+a_kv_k: a_1,a_2,...,a_k\in \R\}
$$

</aside>

What is obvious here is that any vector is a *linear combination of itself with a 1 coefficient*, so if a vector w is in the collection S, then $w \in Span(S)$.

To recap, a vector *w* is a linear combination of the vectors in S, and that the vector *w* is in the Span(S).

What this means is that basically:

<aside>
💡 Span is a Subspace

Given S to be a finite collection of vectors in $\R^n$, then the $Span(S)$ is a subspace of $\R^n$.

</aside>

When we want to find if a vector *w* is in the span of S, it equivalently means that we want to find out of *w* can be constructed from a linear combination of vectors within the collection S, and is essentially done by solving a linear system. In this broken down example, we can see that given these 5 vectors, each in $\R^4$, then we want to determine if *w* can be rep. as v1, v2, v3, v4 in a combination. 

The intuitive way to follow along is to represent this *system* in an augmented matrix, and find if there is a solution to the system. This is easily done through previous methods, via Gauss-Jordan elimination and finding the RREF. If we can find the RREF, then there is a solution, and *w* CAN be represented as a linear combination with the vectors of S.

A tricky part here is that there is a general solution, meaning that a free variable remains, so there are multiple combinations of coefficients that can give us the linear combination of *w* through vectors of S.

1.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%208.png)

3.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%209.png)

Final.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%2010.png)

2.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%2011.png)

4.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%2012.png)

By the previous intuition, we know that if a linear system has a solution, then it is *consistent*. So, applied here, the vector *w* is a linear combination iff. the linear system that represents the linear combination is **consistent**.

We can also use previous wisdom to understand that the linear combination is unique, based on if the zero vector has a representation in these vectors

<aside>
💡 The representation of *w* as a linear combination of $v_1, v_2, ..., v_k$ is UNIQUE if and ONLY if the zero vector has ONLY the trivial representation as a linear combination of $v_1, v_2, ..., v_k$.

</aside>

This is proven by adding the linear combinations of *w* and *0* together, as $w + 0 = w$, so we know that it is unique iff. this sum yields its own linear combination, which is the same as *w*'s combination.

Let us also revisit what it means to be **linearly dependent** or **independent:**

<aside>
💡 Vectors $v_1, v_2, ..., v_k\in \R^n$ are *linearly independent* if the equation $t_1v_1+t_2v_2+...+t_kv_k = 0$.

</aside>

This is because the only solution to this homogenous system should be the zero-vector, meaning that is the trivial solution ($t_1 = 0, t_2 = 0,..., t_k =0$) and that no two vectors $v_1, v_2, ..., v_k$ are related by their linearity. If the equation has AT LEAST one NONTRIVIAL solution, then the vectors are linearly dependent.

When all the vectors of a set/collection are linearly independent, then it is a *linearly independent* set/collection.

This makes it easy to understand sets/collections with their linear dependence:

<aside>
💡 If a collection S is of vectors in $\R^n$, then

a) if a vector appears more than once in S, then S is linearly dependent

b) is S is linearly independent, then S has no duplicates, meaning that S has distinct vectors, and S is a set, not a collection.

</aside>

<aside>
💡 Linear Independence and Rank

Given S to be a collection of $v_1, v_2, ..., v_k$, and A be the matrix whose columns are $A = [v_1, v_2, ..., v_k]$, then S is linearly INDEPENDENT if and ONLY if the rank of A is equal to the number of vectors/columns ie. $rank(A) = k$.

</aside>

<aside>
💡 Given Given S to be a collection of $v_1, v_2, ..., v_k$, if $k > n$, then S must be linearly dependent

→ what this means is that if the number of vectors outnumbers the number of unknowns/dimensions, then at least 1 vector must share a dimension with another (Pigeonhole Principle), and 2 of k vectors are dependent, so S must be linearly dependent.

</aside>

* rank(A) < k, then S is linearly dependent.

In order to prove that two vectors $u, v$ are linearly dependent is to show that at least one of the vectors is a scalar multiple of the other (proportional).

By way of solutions to $xu + yv = 0$

If u and v are dependent, then there is a solution that is non-trivial, so $u = -\frac{y}{x}v$, given that $x \ne 0$, so there is a non-trivial sol.

By way of knowing that one is proportional to another

If $u = cv$ for some *c*, then $u -cv = 0$, meaning that they are dependent, since the coefficient to *u* is 1.

<aside>
💡 Linear Dependence even with new vectors

If S is a *linearly dependent* collection of vectors $v_1, v_2, ..., v_k$, for any vector *w*, the collection of S with *w* is STILL dependent

</aside>

This is because $0 = a_1v_1 + a_2v_2 +...+a_kv_k$ has a non-trivial solution even if $0 = 0w + a_1v_1 + a_2v_2 +...+a_kv_k$.

<aside>
💡 Linear Independence even when removing vectors

If S is a collection of vectors and is *linearly independent*, for any $i \in \{1,2,...,k\}$, if any $v_i$ is removed from S, then the set is still linearly dependent.

</aside>

This is because the *linear independence* of a set/collection guarantees that no two vectors in the set are dependent/proportional. So, removing an element changes nothing of their lack-of-proportionality.

To prove this by rank, $rank([v_1, v_2, ...,v_k]) = k$ means that the collection of vectors is linearly independent, and no two vectors in the collection are proportional. So, since we remove an element, this stays consistent as $rank([v_1, v_2, ..., v_{i-1},v_{i+1}, ...,v_k]) = k-1$, since there is 1 less element.

Here's a recap of all of this information about linear in/dependence

- If some vectors in S are linearly dependent, then S is linearly dependent (even when adding new vectors, non-proportional to the others)
- If S is linearly indep., then any subset of S is also linearly indep.

What about the zero-vector?

<aside>
💡 If one of the vectors of S is $\overrightarrow{0}$, then $v_1, v_2, ..., v_k$ are linearly *dependent*.

</aside>

This is because we know that the set $S = \{0\}$ is linearly dependent, because the solution of this system must be the trivial solution in order to be linearly dep... we also know that the zero vector is linearly dependent to all vectors, so by default, this set will always be linearly dependent if it contains the zero vector.

The concept of linear combinations also fits very well into the linear dependence of a set of vectors.

<aside>
💡 Dependence and Linear Combinations

For any k ≥ 2, its vectors are linearly *dependent* of and ONLY if at least one of these vectors can be expressed as a linear combination of the other vectors.

</aside>

This is proven by understanding that if a set of vectors were linearly dependent, then the combination $t_1v_1 +t_2v_2+...+t_kv_k = 0$ has AT LEAST ONE NONTRIVIAL solution. Since the set is dependent, we assume there is a non-trivial solution, and that $t_1 \ne 0$ for example. 

$$
t_1v_1 = -t_2v_2-...-t_kv_k \\ v_1= (-t_2/t_1)v_2 -...
$$

Which directly means that the vector $v_1$ is a linear combination of all other vectors.

So, we know that the *span* of a subspace/set is the set of all linear combinations of that set, so if a vector *w* can be represented by a linear combination of the vectors of the set S, then it is in that set's span ($w \in span(S)$), and thus that means the vector *w* is linearly dependent to the vectors that make up the set S.

Because we know this, we can now say that adding a vector into a *linearly independent* set S will keep the set linearly independent if and only if that added vector is NOT in the span of S ($w \notin span(S)$).

→ This is because if the vector is not in the span, then it is not a linear combination of the vectors of S, and is then linearly independent from the vectors of S, so adding it to S will not make S linearly dependent.

# 5.3 Basis and Dimension

The last information that we covered showed that a span of a finite subset of $\R^n$ is a subspace of $\R^n$ itself, and that any subspace of $\R^n$ is a span to some finite subset of itself. We further define what it means to *span:*

<aside>
💡 Spanning Collection

If $V$ is a subspace of $\R^n$, and S is a collection of vectors in $\R^n$, S is a **spanning collection** (or *generating collection*) of $V$ if:

$$
V = Span(v_1,v_2,...,v_k)
$$

</aside>

To verbalize this, we say that the collection S **spans** or **generates** the subspace V. An important note here is that a subspace does NOT need to have a spanning collection.

Take this for example:

<aside>
💡 consider the three vectors in $\R^3$:

$$
e_1=\begin{bmatrix}1\\0\\0\end{bmatrix}, e_2 =\begin{bmatrix}0\\1\\0\end{bmatrix}, e_3 = \begin{bmatrix}0\\0\\1\end{bmatrix}
$$

Show that the span of this collection is $\R^3$, ie. $Span(e_1,e_2,e_3) = \R^3$.

</aside>

To show this, we need to algebraically and arbitrarily show that ANY vector in $R^3$ is in the subspace of Span(e1, e2, e3).

$$
v=\begin{bmatrix}v_1\\v_2\\v_3\end{bmatrix} = v_1\begin{bmatrix}1\\0\\0\end{bmatrix}+v_2\begin{bmatrix}0\\1\\0\end{bmatrix}+v_3\begin{bmatrix}0\\0\\1\end{bmatrix}=v_1e_1+v_2e_2+v_3e_3\in Span(e_1,e_2,e_3)
$$

This directly shows that any vector *v* can be represented as a linear combination of the three vectors in the set, and is part of the span of that set. Thus, these three vectors span the entirety of $\R^3$.

This leads us to define these special vectors, so:

<aside>
💡 For any n ≥ 1, the vectors $e_1, e_2, ..., e_n \in \R^n$ GENERATE $\R^n$

</aside>

Where each of these vectors is simply just zero-vector EXCEPT with the *i-th* position being a 1. This is like if each vector $e_i$ represented the i-th dimension/basis. So it is very simply illustrated for $\R^2 =Span(e_x,e_y)$, $\R^3 = Span(e_x,e_y,e_z)$.

When asked to describe a span, all is asked is to essentially represent the span as an equation (either vector or standard), because that describes best the span.

For example, take this set $S = \{[1,-1], [-2,2]\}$. The best way to describe $Span([1, -1], [-2, 2])$ is to make it into a vector equation, such that:

$$
Span(S) = [x,y] = a[1,-1] +b[-2,2] = (a-2b)[1,-1]
$$

So these vectors that make up S are linearly dependent (because $-2[1,-1] = [-2,2]$). In fact, this set S can span the same subspace of $\R^n$. This is because when the set is linearly dependent, those linearly dependent vectors represent the same line/direction/linearity, so adding vectors for which there are vectors in S that are proportional to the new one, it doesn't *increase* or *decrease* the span of the set.

<aside>
💡 Linearity in terms of functions
Span = Range

Set/Collection = Domain

Linear Combination = Function

→ The elements/vectors in a set define the *domain* of the function that is the linear combinations of the vectors in that set. The span of vectors that results, is then the *range* of the function, based on the domain.

</aside>

What about two different subspaces of $\R^n$?

<aside>
💡 Given that V and W are subspaces of $\R^n$, and that V is generated by $v_1, v_2, ..., v_k$, and W is generated by $w_1, w_2, ..., w_m$

a) W is a subset of V if and only if $w_1, w_2, ..., w_m \in V$

b) $V = W$ if and only if $w_1, w_2, ..., w_m \in V$ AND $v_1, v_2, ..., v_k \in W$ (the vectors that generate each set are in both sets)

</aside>

<aside>
💡 Corollary 5.3.7

If S is a set with $v_1, v_2, ..., v_k$, and *w* exists. Let the subspace V be generated by the Span of S.

$V = Span(w, v_1, v_2, ..., v_m)$

if and only if $w \in Span(S)$

</aside>

→ what this is basically saying is that if a subspace V is spanned by a set of vectors, then adding a vector that is in the span of S into the generating set will not change the Span of S. This was seen when vectors of the generating set were linearly dependent, because they are proportional, they represent the same piece of the dimension and don't change the span of the set. It's like adding 0, you can add however many zeroes you want, but it will never change the output. We know that this vector *w* will not change the Span of the set because it is in the span, meaning that it is linearly dependent to all other vectors of the generating set.

<aside>
💡 Theorem

Given S to be a collection of vectors $v_1, v_2, ..., v_k$, such that $V = Span(S)$ is a NONTRIVIAL subspace of $\R^n$.

Then V has a *linearly independent* spanning set that is a subset of S.

</aside>

This basically means that the subspace V has a spanning set that contains AT LEAST ONE non-zero vector. In the case that S is already linearly independent, then the theorem is proven already. However, is S is linearly dependent, then S has at least 2 vectors, one of which is non-zero. This means that of of the *k* vectors in the set of S can be represented by a linear combination of the other *k - 1* vectors. So, we can remove this linearly dependent (proportional) vector from the spanning set, without changing the span of the set. This removal is repeated for any remaining linearly dependent vectors of the spanning set, and voila, the span of S has not changed, but the spanning set is no longer linearly dependent.

→ In essence, a subspace that is non-trivial has a spanning set that is linearly independent "hidden" inside of its spanning set. 

This sets us up to define what a **basis** is.

<aside>
💡 Basis

Given a non-empty set $S = \{v_1, v_2, ..., v_k\}$, in the subspace $V \in \R^n$ is called a **basis** for the subspace if:

a) S is linearly independent

b) $V = Span(S) = Span(v_1, v_2, ..., v_k)$

</aside>

Essentially, the vectors $v_1, v_2, ..., v_k$ form a **basis** for $V$. This basis is the most minimal set that would describe the subspace V.

For example, we previously looked at how planes are a subspace of $\R^n$ if n ≥ 2. We know that by the definition of a plane, the vectors in $x = ru + tv$ are linearly independent. The set of these vectors $\{u,v\}$ forms a basis for the plane $\pi$ and the set spans the plane.

Recalling the vectors $e_1, e_2, ..., e_n$ being the simple vectors with only a 1 in the respective i-th entry. These vectors form the **standard basis** of the subspace they span, namely that they span the entirety of $\R^n$.

$$
e_1=\begin{bmatrix}1\\0\\0\end{bmatrix}, e_2 =\begin{bmatrix}0\\1\\0\end{bmatrix}, e_3 = \begin{bmatrix}0\\0\\1\end{bmatrix}
$$

<aside>
💡 Column Space

if a matrix A is of size $m\times n$, and is written as a set of its *column vectors* $A = [v_1, v_2, ..., v_n]$, then the **column space** $col(A)$ is the *subspace $\R^m$* generated by the column vectors of A.

$$
col(A) = Span(v_1, v_2, ..., v_n)
$$

</aside>

<aside>
💡 Basis for a column space

Given S to be a collection of $v_1, v_2, ..., v_k$ in $\R^n$ with AT LEAST ONE non-zero vector, then $A_{n\times k}$ is the $n \times k$ matrix formed by the vectors in S as column vectors. $A = [v_1, v_2, ..., v_k]$.

The following are true:

a) pivot COLUMNS of A are *linearly independent*

b) non-pivot columns of A are *linearly dependent*

In essence, the pivot columns form the basis for the column space of A.

</aside>

This is basically proven by taking an arbitrary matrix A and putting it into REF, of which we will find the columns which are pivots (recall: pivot columns are any columns which CONTAIN A LEADING 1). Once we know which columns (vectors) have a leading 1, we can take those columns from A directly and put them into their own matrix A'. Because we know that A is only composed of columns which have pivot entries, we know the rank of this matrix is equivalent to the number of columns $rank(A') = r$. Because of the rank being equal to the number of columns (vectors), then we know this collection of A' is linearly *independent*. 

* Note : we don't need to put it into RREF because we can tell the pivot columns earlier by going into REF.

We can now outline an algorithm to find the basis for any subspace.

<aside>
💡 Algorithm: Finding the Basis of a Subspace

1) Create the matrix $A_{n\times k}$ by using the vectors of the spanning set $v_1, v_2, ..., v_k$ as its columns.

$$
A_{n\times k} = [v_1, v_2, ..., v_k]
$$

2) Put A into REF by using Gaussian Elimination, this matrix in REF is called $R$.

3) Using the pivot column positions in $R$, take the columns that correspond to those positions from A, and this forms the basis for the generation set of the subspace $V$.

</aside>

* Please note here that the outcome of vectors depends on the order of the generating set. 

In the recent discoveries, we can see that the vectors in the basis sets for a subspace can be different, but we are going to look at why there must be the same *number* of vectors. We need to look at how the ranks of matrices with the same columns differ based on the arrangement of the columns:

<aside>
💡 Given A to be an $m\times n$ matrix, and B is obtained from A by re-arranging the columns. Then, $rank(B) \leq rank(A)$.

</aside>

This is because re-arranging the columns can result in a different number of rows containing only zeroes, but not always. For example, B could have 1 row with only rows, and A can have 0. If we do this a second time, and re-arrange B's columns into a matrix C, then C also has $n - r$ zero rows, the same as B. So, the rank(C) ≤ r, and $rank(B) = rank(C) \le r= rank(A)$.

Let's solidify this into saying that:

<aside>
💡 Given A to be $m\times n$, and B is A with re-arranged columns, then the $rank(B) = rank(A)$

</aside>

This is confusingly proven by applying the previous lemma twice. If B is made from A, then we can re-arrange B to be A again, meaning that these both apply at the same time:

$$
rank(A) \le rank(B) , rank(B) \le rank(A)\therefore rank(A) = rank(B)
$$

This is all to prepare for the main result, that the bases of a subspace must all have the same size:

<aside>
💡 Same Size Bases

given that $\alpha = \{v_1,...,v_k\}, \beta=\{u_1,...,u_m\}$ are bases for the subspace V, then $k = m$

</aside>

Basically, the number of vectors in the independent sets $\alpha,\beta$ are the same.

This is proven because if the matrix A is composed of $\alpha$, and B is composed of $\beta$, and they are both linearly independent because they are bases, then the $rank(A) = n$ and the $rank(B) = m$ by previous theorems. In essence, there is an RREF that comes from A, in which there are no non-zero rows between any of the pivot columns, which means that all the columns form the basis of the subspace it spans. This linear system is then consistent, we can see that the matrix [A | u] can be reduced to [R | w] by the same sequence of row operations.

We can also take the augmented matrix [A | B] and reduce it to RREF using the same sequence of row operations, in which the outcome is [R | W], and also follows the same pattern of having *k* non-zero rows, and whose leading 1's are all in R.

So, since $rank([A|B]) = k$ and $rank([B|A]) = m$ is true because [A|B] and [B|A] are equivalent by rearranging columns, so $k = m$.

<aside>
💡 Dimension

let $\beta$ be *any basis* for a subspace V. The number of vectors in $\beta$ is called the **dimension** of V, denoted $\dim(V)$.

</aside>

Here are dimensions of the 3 biggest concepts:

<aside>
💡 $\dim(\R^n) = n$

→ because the standard basis {e1, e2, ..., en} has *n* vectors.

$\dim(line)= 1$

$\dim(plane)= 2$

</aside>

It then follows from the column space of a matrix A that:

<aside>
💡 Given A to be a matrix, with $col(A)$ being its column space, then its dimension is equal to the rank of the column space.

$$
\dim(col(A)) = rank(A)
$$

</aside>

Let's generalize the concept of the subspace, because any subspace in $\R^n$ has a basis.

<aside>
💡 Given V to be a nontrivial subspace of $\R^n$, and S is a lin. indep. subset of the vectors in V. V then has a basis that contains S as a subset. Basically, in a subspace, any linearly independent subset S can be *enlarged* to a basis of V.

</aside>

This Lemma is proven by the cases of S spanning the subspace of V. If S spans V, then it does not need to be enlarged, because it is the basis of V. However, if S does not span V, then there are vectors in the subspace of V that are not in the span of S, so it is largely independent from the other vectors of S, and adding this vector *w* to S only enlarges the span of S to approach V. If it is not a basis already, we can keep adding vectors from the subspace into the set of S which are not spanned by S to reach the basis of V.

Actually, there can be at most *n* linearly independent vectors in $\R^n$, so the basis has at most *n* vectors.

Most importantly, once we add in the last vector that forms the basis of V, we have a set $S_t$ such that:

$$
S_t = \{v_1, v_2, ...v_r, w_1,w_2, ...,w_t\}
$$

and this set $S_t$ is a basis for V which contains the original set S as a subset.

<aside>
💡 Dimension of the Trivial Subspace

$$
dim(\{0\}) = 0
$$

</aside>

This is abstracted, but is simple since the *empty set* is a basis for this subspace. And since the empty set has no vectors, ie. 0, then the dimension of the trivial subspace is 0.

<aside>
💡 Existence of Basis

a) Every subspace of $\R^n$ has a *basis*

b) if V is a subspace of $\R^n$, then the $\dim(V)\le n$. 

</aside>

Any subspace has a basis because it is composed of a vector that generates it. With no basis, there is no subspace. Even if we are looking at the trivial subspace, it also has a basis, the empty set. Otherwise, it contains a set of vectors such that the spanning set S is linearly dependent, and there can be AT MOST *n* vectors that form that basis.

Let's recall vectors and orthogonality. For two vectors to be orthogonal, their dot-product is 0. Geometrically, they are at a $\pi/2$ angle to each other.

<aside>
💡 Orthogonal Basis

Given a set S of at least two vectors, S is an **orthogonal set** if each *pair* of distinct vectors in S are orthogonal to each other.

ie. the dot-product of every pair of vectors is 0. If this set S spans a subspace V, then the basis of V is an orthogonal basis.

</aside>

We can use the handy nature of orthogonality to also prove that orthogonal vectors are linearly independent.

<aside>
💡 Orthogonal set of linearly independent (nonzero) vectors

If S is an orthogonal set of NONZERO vectors, then S is linearly independent.

</aside>

→ The non-zero comes into play here because all vectors are lin. dep. with the zero-vector.,

This is proven through showing that the coefficients of the linear combination must all be zero, because the dot-product between orthogonal vectors is 0. However, this doesn't mean that the dot-product of a vector to itself is 0, unless the vector is the zero vector. So, the coefficients between every pair of orthogonal vectors is 0, so there is no other solution other than the trivial solution, so the set is lin. independent.

This implies that any orth. set of vectors will form an orthogonal basis of its span.

Let's spice it up and include the *invertible matrices* into this concept:

<aside>
💡 Let $v_1, v_2, ..., v_n$ be vectors that form the basis for $\R^n$. They only form the basis if and only if the matrix $A = [v_1, v_2, ..., v_n]$ is invertible

</aside>

→ The matrix A is square because there are *n* vectors in *n* unknowns. The vectors form the basis only if they are linearly independent, so the matrix A has a rank of *n*. So the matrix A is invertible, because the rank equals the number of columns.

We can determine if a set of vectors is a basis by two ways:

<aside>
💡 1) Using row operations into REF to determine rank. If rank = n, then it forms a basis for $\R^n$

2) Using determinants, calculate the determine of A through cofactor expansion. Recalling back to chapter 4, a matrix is invertible if it is square, and its determinant is non-zero. If $det(A) \ne 0$, then it forms a basis for $\R^n$.

</aside>

We have seen that the set of solutions to a (homogenous) linear system in *n* unknowns is a subspace of $\R^n$, so we can say that there is a subspace V in which the subspace is the set of solutions to the system. This is illustrated by using the basis vectors of a subspace to find the linear system (homogenous) whose solution set is equivalent to the subspace V.

→ We use the basis vectors in augmented matrix form and find the RREF. We are then looking for any whole-zero rows, which would denote a homogenous linear system that has a solution set that is the entirety of the subspace V.

* this is essentially like finding a vector that is orthogonal to all vectors in the subspace V.

THOUGHTS ABOUT LINEAR COMBINATIONS AND SPANS

<aside>
💡 Thinking about these concepts, they can be applied to a number of things. However, think about a function of working. Each person in a team forms the set of vectors of a subspace, with the subspace being the scope of work that can be accomplished. In this analogy, imagine each person and their skills is static, they are not learning anything new.

When you have a single person working on a project, they can only do what they know how to do, a line. However, when we add a second person, it doesn't mean the scope of work (span of work) will change, it depends on what they know. If the team members are dependent on the same knowledge, then nothing new is done, and the span of work stays the same. However, adding someone new with new knowledge will increase the span of work through the linear combination of the knowledge of the independent members.

</aside>

# 5.4 Coordinates with respect to Ordered Bases

A basis for a subspace V is minimal as a spanning set, meaning that no smaller set will completely span V, and if it does, then the smaller set is the actual basis. In fact, this is not the case per the definition of a base of V, because bases must all have the same size.

Bases are also maximal as a linearly independent subset of V, so any other vectors within V are linear combinations of the vectors, and any larger set is no longer linearly independent, disqualifying them as bases.

The linear combination that represents the basis for subspace V is unique.

However, a previous example covered that depending on the arrangement of columns, we might arrive to a different basis. This is why we establish an order to writing the basis of a subspace, and require the new concept of **coordinates**, with respect to an *ordered basis*

<aside>
💡 Coordinates

Given that V is a subspace of $\R^n$, an **ordered basis $\beta = \{v_1,v_2,...,v_k\}$ for v** imposes the particular order among the *vectors* in the given basis. The coordinates of a vector *w* in V with respect to the ordered basis $\beta$ are the *k* real numbers presented in the UNIQUE k-tuple $(c_1, c_2,...,c_k)$ such that

$$
w = c_1v_1 + c_2v_2+...+c_kv_k
$$

Where the vector $c = [c_1, c_2,...,c_k]$, or written as $[w]_\beta$ is the *coordinate vector* of w, with respect to the ordered basis $\beta$.

</aside>

This is, in a way, similar to translating the coordinates from the origin and instead using the "origin" of the basis.

This is true because if we examine the *standard basis* for any $\R^n$, then we can see that the coordinates of a vector *w* in this space, with respect to the basis $\alpha = \{e_1,e_2,...,e_n\}$ are the normal **standard coordinates** from the true origin. And thus, the coordinate vector $[w]_\alpha$ coincides with *w* itself.

This is a very important concept in a lot of different applications, and helps to translate the differences between fields-of-view. Choosing a basis and the coordinates with respect to that basis are like choosing a different point of view, and some problems are better suited to better POVs.

![Untitled](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%2013.png)

Thus, we can see that if V is a subspace, and it has an ordered basis $\beta$, then it is idiosyncratically a function that we are applying to any vector *v* to put it into the subspace V, with its coordinate vector $[v]_\beta$. This preserves the vector addition and scalar product operations:

$$
[v+w]_\beta = [v]_\beta+[w]_\beta\\\;[av]_\beta = a[v]_\beta
$$

The function of *transforming* *v* into $[v]_\beta$ is a class of *linear transformation*, which is what Chapter 6 is all about.

<aside>
💡 **Orthonormal Basis**

An *orthonormal set* is based on a set S that is *orthogonal* AND only contains *unit vectors*. An ordered basis for a subspace is orthonormal if it uses an orthonormal set.

</aside>

An example of this would be the **standard basis** set of any $\R^n$, because for $\beta_0=\{e_1,e_2,...,e_n\}$, all vectors are orthogonal to each other, and for each vector, $||e_i|| = 1$ trivially (because they each only have 1 entry, a single 1, so $\sqrt{1}=1$)

In the figure, we can see that each entry of the $\R^2$ vector is in it's unit form, and that they are orthogonal because [a b].[b -a] = 0.

![General form of orthonormal set in R^2](Subspaces%20of%20$%20R%5En$%20and%20Their%20Bases%200cad519596fa4dafa42ea68720a87ad6/Untitled%2014.png)

General form of orthonormal set in R^2

Computing the coordinates of a vector with respect to the orthonormal basis are quite easy to calculate:

<aside>
💡 Given that $\beta$ is an orthonormal basis for the subspace V, then the coordinates of a vector *w* in the subspace with respect to $\beta$ are computed by the dot-product between $w\cdot v_i$

$$
w = (w\cdot v_1)v_1 +(w\cdot v_2)v_2+...+(w\cdot v_k)v_k
$$

</aside>

Because we know now that the standard basis is an orthonormal basis for any $\R^n$, we can also translate other concepts such as orthogonal projections.

<aside>
💡 RECALL: Orthogonal Projection

$$
proj_wv = \frac{v\cdot w}{||w||^2}w
$$

if *w* is a unit vector, then:

$$
proj_wv = (v\cdot w)w
$$

</aside>

so, we can see that when the vector we are projecting *v* onto is a unit vector (like the orthonormal basis vectors), that each coordinate of the orthonormal basis is a projection of that vector onto the basis. This is simplest to imagine with orthonormal bases, which are unit vectors, but the concept still applies even when $\beta$ is not a -normal basis, and only orthogonal. This is why we can generalize the meaning of an orthogonal project to be onto a subspace.

<aside>
💡 Orthogonal Projection to subspace

given that V is a subspace of dimension k ≥ 1. A vector *u* is orthogonal to V, if *u* is orthogonal to ALL everys in V. An orthogonal projection of a vector *w* ONTO V, is $proj_Vw \in V$, such that $w-proj_Vw$ is *orthogonal to V*.

</aside>

<aside>
💡 Projection using orthonormal basis for V

Given that $\beta$ is an *orthonormal basis for V*, which is a subspace. And *w* exists, then the projection of *w* onto the subspace V is simple:

$$
proj_V(w) = (w\cdot v_1)v_1+(w\cdot v_2)v_2 +...+(w\cdot v_k)v_k
$$

ie. the translation of the vector V to be in coordinate with respect to the basis $\beta$.

</aside>

Proving this requires understanding that the result of the projection of *w* onto V is a vector in itself that is in the span of the subspace, labelled *p*. Then, we know that $w - p$ is then orthogonal to V, and thus to all vectors in $\beta$. In fact, because of this knowledge:

$$
0 = (w-p)\cdot v_i = (w\cdot v_i)-(p \cdot v_i)\\p\cdot v_i = w\cdot v_i
$$

Thus, for all $i = 1,2,...,k$, the projection dot the basis equals the vector dot the basis. This means that translation is done by the basis itself.