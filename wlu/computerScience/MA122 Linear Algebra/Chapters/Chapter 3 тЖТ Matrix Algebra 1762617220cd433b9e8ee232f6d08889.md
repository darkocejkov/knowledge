# Chapter 3 → Matrix Algebra

# 3.1 Definitions/Properties of Matrix Operations

## Real Matrix

An (m * n) REAL matrix $A_{m\times n}$ has (m*n) entries, in an (m*n) rectangle; similar to how it was seen in Chapter 2. The matrix is of size/shape (m*n). Another notation for understanding the matrix A of size m*n is $[a_{ij}]_{m\times n}$. This is understood as being the matrix A with size m*n, in which the entry in the *i'th row* and the *j'th* column is the (i,j) entry. Vectors in $\R^n$ can be either *rows,* in which their size is (1 * n), or *columns*, where the matrix is of size (n * 1). We can combine these to create m * n matrices, which have *m* rows and *n* columns. 

As such, we can construct a matrix by defining a *row* of column vectors, or a *column* or row vectors. The end result of these notations is a matrix that has m rows and n columns.

## Square Matrix

Matrices of size $n \times n$ are called *square* matrices of order *n*. This is because it has the same number of columns as rows, and is thus square. An interesting property about square matrices is that they have a **main diagonal**, which goes from $b_{1,1}$ to $b_{n,n}$; when the entries are of the form $b_{i,i}, i =1,2,...,n$.

## Zero Matrix

Matrices are called the *zero matrix* when every entry is a 0, there is a unique zero matrix for each size $m \times n$.

## Equal Matrices

Matrices A and B are equal iff:

<aside>
☁️ **A = B**

- A and B are of the samesize
- all entries are *respectively* equal (for any (i,j), A[i][j] = B[i][j])
</aside>

## Matrix Operations

### Matrix Addition and Subtraction

The SUM of matrices A and B is $A + B$, while the DIFFERENCE of the same matrices is $A - B$. The result is a matrix for which:

<aside>
☁️ $A+B$

$(A+B)_{i,j} = A_{i,j} + B_{i,j}$

- the addition of each respective entry
</aside>

<aside>
☁️ $A -B$

$(A-B)_{i,j} = A_{i,j} - B_{i,j}$

- the difference of each respective entry
</aside>

⭐ An important note is that we **CANNOT** add or subtract matrices of different sizes

- in order to realize this, what would happen to the extra entries? would we include them as-is, or exclude them, or just use 0s?
- thus, matrices of different sizes added or subtracted give an *undefined* result.

### Scalar Multiplication

<aside>
☁️ $(cA)_{i,j} = c(A)_{i,j}$

- that is, the scalar multiplication of A is obtained by multiplying every A entry by the scalar, c.
</aside>

→ this should look familiar, as the subtraction of two matrices   $A -B$ is the same as adding the negative, as in: $A + (-1)B$

## Properties of Operations

<aside>
☁️ Addition/Subtraction

- Commutative
    - $A + B = B + A$
- Associative
    - $(A+B) + C = A + (B+C)$
- 0 as Additive Identity
    - $A + 0 = A$
- Additive Inverse
    - $A + (-A) = 0$
</aside>

<aside>
☁️ Scalar Multiplication

- Associative
    - $(ab)C = a(bC)$
- 1 as Identity
    - $1A = A$
- Distributes over *matrix* addition
    - $a(B+C) = aB + aC$
- Distributes over *scalar* addition
    - $(a+b)C = aC + bC$
</aside>

## Matrix Transposition

This operation does not involve another matrix, or any algebraic operations.

<aside>
☁️ Transpose $A_{m,n} = A^T=A_{n,m}$

The transposition of A with size (m * n) is a matrix of size (n * m) (notice that the order of rows and columns is switched). The easiest way to describe a matrix transposition is that all rows become the columns, and all columns become rows.

![https://i.gyazo.com/79e7d790f415e75360bda43c49e25ba3.png](https://i.gyazo.com/79e7d790f415e75360bda43c49e25ba3.png)

![https://i.gyazo.com/9db83010270daf1ed62d19d8aaf032e5.png](https://i.gyazo.com/9db83010270daf1ed62d19d8aaf032e5.png)

</aside>

⭐The Transposition of a *square* matrix can be seen as the *reflection* of the matrix about its main diagonal

Here are some properties of the matrix transposition:

<aside>
☁️ The following are all true:

- $(A^T)^T = A$
- given a row vector, its transposition is a column vector, and vice versa.
- $(A+B)^T = A^T + B^T$
- $(A-B)^T = A^T - B^T$
- $(aA)^T = aA^T$
- if C is a square matrix, then $C^T$ is of the same shape.
</aside>

In order to transpose any matrix, we can do so by picking one of two ways:

1) Isolate all row vectors, and turn them into column vectors

2) Isolate all column vectors, then turn them into row vectors

## Matrix Product

This operation is closely related to the dot-product of vectors. Rather than producing a single scalar number, it produces a third matrix. This operation is also specific to only matrices. It is a very useful operation for these matrices. The general idea is that given two vectors A and B, we compute the dot-product of each of A's rows to each of B's columns.

Let's simplify this idea, and use row and column vectors. Given $\overrightarrow{u}_{1,k}, \overrightarrow{v}_{k,1}$. The product of these two vectors is a $1 \times 1$ matrix. This is because we take the dot product of these vectors and it produces a single scalar. Because there is only 1 row in U and 1 column in V, then there is only 1 scalar present in the resulting vector. 

If we continue to expand this idea, we can see that if matrix A was $(m \times k)$, and B was $(k\times 1)$, then the resulting vector is then $(m\times 1)$. A shortcut to knowing the size of the resulting vectors is that we take the outer scalars in the sizes: $(m\times k)(k\times 1) = (m\times 1)$. This is contingent on both vectors being matched on the inner size. This means that for matrix products to work, the number of *columns* in any matrix A must equal the number of *rows* in matrix B. 

![https://i.gyazo.com/eb6a77f9ae40a92843b657724ec5f534.png](https://i.gyazo.com/eb6a77f9ae40a92843b657724ec5f534.png)

Let's tackle an example to see this more practically and visually. Take these two vectors A and B. In order to compute their product - $AB$, we can see what the resulting matrix's size is. Since A is of size $2\times 3$, and B is of $3\times 4$, then the resulting vector is of size $2\times 4$. 

To determin the (i, j)th entry of the resulting matrix, we use the *i*th row of A, and the *jth* column of B. So, for example, if we wanted the (1, 4) entry of C, then we take the dot-product of $[1\;2\;4]\cdot[3\;1\;2]$, which is equal to $13$. This is done with all permutations of the number of rows of A and the number of columns of B.

- A1 * B1 = C[1,1]
- A1 * B2 = C[1,2]
- A1 * B3 = C[1,3]
- A1 * B4 = C[1,4]
- A2 * B1 = C[2,1]
- A2 * B2 = C[2,2]
- A2 * B3 = C[2,3]
- A2 * B4 = C[2,4]

![https://i.gyazo.com/527a11d491bbb5d314f7c6b33cc59d5d.png](https://i.gyazo.com/527a11d491bbb5d314f7c6b33cc59d5d.png)

Because we need the columns of the *first* matrix to match the *rows* of the second matrix, we can see that the product $BA$ is not defined, because they have a mismatch in this respect $(4 \ne 2)$.

We can also work through this by finding each column of the resulting product vector by seperating the columns of B. For example, if we are given two vectors A and B, and were asked to find the 4th or the 2nd column of the resulting product AB, then we just need to seperate the columns of B and compute the product on each of those columns, as if it were its own product.

Let me note that there is a difference between the scalar $a$ and the 1*1 matrix $[a]$, which has the scalar $a$ as its only entry. We can clearly see this because taking the product of a scalar $a$ is always defined, because we multiply every entry by that scalar. However, not all *products* involving $[a]$ may be defined, because this is a $1\times 1$ matrix, so the other vector must be either a row or column vector as in $\overrightarrow{row}\times[a]$ for example. For any vector, the product of the vector and this $1\times 1$ matrix is always defined, and $\overrightarrow{v}[a] = a\overrightarrow{v}$ is always true.

Through various examples we learn that the function of product on matrices is not always well-defined, meaning that for matrices A and B, the product $AB$ is defined while they match columns to rows, but $BA$  may not be.  Even when the $AB$ and $BA$ are defined, we can see that $AB \ne BA$
, even when A and B are square matrices (m = n).

We can also that the product of $A$ with its transposition $A^T$ is always well-defined, but the resulting matrices are not equal, whether or not they are of equal size.

### Cancellation Properties

Cancellation laws work differently for matrices. We can see that $A\times 0 = 0$ and $0 \times B = 0$ for matrices, given that the resulting zero matrix has the correct product size. However, these identities do not necessarily hold, because there are matrices A and B such that $AB = 0$, but A ≠ 0, and B ≠ 0. There are also matrices A, B and C such that A ≠ 0, and AB = AC, but B ≠ C.

This is because there is a certain property of matrices which will be visited later, and have cancellation laws. Matrices that can be cancelled in the typical way are *invertible.* 

Let's list out some matrix product properties:

<aside>
☁️ Matrix Product Properties → given that matrices A, B, and C are all in their appropriate sizes such that these are well-defined.

- Scalar Associative
    - $a(BC) = (aB)C = B(aC)$
- Associative
    - $A(BC) = (AB)C$
- Left Distribution
    - $A(B+C) = AB + AC$
- Right Distribution
    - $(B+C)A = BA + CA$
- Transpose Law
    - $(AB)^T = B^TA^T$
</aside>

# 3.2 Linear Systems Revisited

⭐ From this section forward, we consider vectors to be in their *column* format. so $\overrightarrow{v}$ is a column, while $\overrightarrow{v}^T$ is a row.

Remembering back to chapter 2, we want to involve the use of *matrix product* in the operations of Linear Systems. We can use the product of matrices to keep track of the *unknowns* explicitly; this is a form of **re-writing** the system, and not abbreviating it (because no information is lost).

<aside>
☁️ Linear Systems by Matrix Product

$$
A\overrightarrow{x} = \overrightarrow{b}
$$

→ Where $\overrightarrow{x}$ is a column containing the unknowns. 

</aside>

This equation results in the product of the *coefficient* matrix and the vector of all the unknowns involved. the result of this product gives back the explicit linear system, coefficients with their unknowns. This is because each row becomes the result of the dot product of the row itself and the vector of unkowns.

Let's also revisit the *solution set* idea from linear systems. A pattern emerges in relation to *non-homogenous* linear systems and *homogenous* ones; particularly that the solutions to a non-homo. system are offset by the solutions to the homogenous system. More clearly:

<aside>
☁️ Solutions of a Linear System

If $\overrightarrow{v}$ is a solution to the linear system $A\overrightarrow{x} = \overrightarrow{b}$ of *n* unknowns (non-homo.). Then $\overrightarrow{w}$ is a solution of the same system, IFF. $\overrightarrow{w} = \overrightarrow{u}+\overrightarrow{v}$, where $\overrightarrow{u}$ is a solution to the *homogenous* system variant: $A\overrightarrow{x} = \overrightarrow{0}$.

</aside>

In fact, using these theorems we can make these propositions:

Given $A\overrightarrow{x} = \overrightarrow{b}$ to be a *consistent* linear system, the following are true:

a) $A\overrightarrow{x} = \overrightarrow{0}$ has a unique solution, iff. $A\overrightarrow{x} = \overrightarrow{b}$ has a unique solution

b) $A\overrightarrow{x} = \overrightarrow{0}$ has *infinitely many* solutions, iff. $A\overrightarrow{x} = \overrightarrow{b}$ has infinitely many solutions

We use these to then build on the idea of rank:

<aside>
☁️ Rank Column Theorem

The matrix equation $AX =B$ has EXACTLY ONE solution if $rank([A|B]) = rank(A) = n$, where *n* is the # of columns of A (the coefficient matrix)

</aside>

What this means plainly is that there is only one solution, if the rank of the augmented matrix (coefficient matrix + constant vector) matches the rank of the coefficient matrix, which is equal to the number of columns that A has (the number of unknowns).

Let's take this to an example: given a 3x3 coefficient matrix, and a 3x2 unknown matrix (x), and a 3x2 constant matrix, find AX = B. 

The first step here is to seperate the unknown vector into $X = [\overrightarrow{x}\;\overrightarrow{y}]$, and the constants into: $B = [\overrightarrow{b_1}\;\overrightarrow{b_2}]$. This makes the work much easier, as we only then need to find:

$$
A\overrightarrow{x}=\overrightarrow{b_1}\\A\overrightarrow{y}=\overrightarrow{b_2}
$$

![https://i.gyazo.com/40b746ecb89d3acf1018dbfb94d592ff.png](https://i.gyazo.com/40b746ecb89d3acf1018dbfb94d592ff.png)

1) Take the entire [A|B] augmented matrix and use Gauss-Jordan to transform it into RREF.

2) Using the previous theorems, examine the number of solutions by the rank.

a) This particular example has a rank of 3, which is equal to the number of columns of A, so there is only 1 sol.

3) We can see that when the augmented, total matrix is in RREF, that $\overrightarrow{b_1}$ and $\overrightarrow{b_2}$ are in their solution states, so to find the solution to this, we simply put together the X and Y columns of B to find X.

Let's discuss the *identity matrix*:

<aside>
☁️ **Identity Matrix**

($I_n$), is a *square* matrix, of order *n*, with *1* on the main diagonal, and 0 elsewhere.

</aside>

This is an important concept when introduced to any other matrices with products:

<aside>
☁️ Let A be an $m \times n$ matrix, then:

$$
A = AI_n=I_mA
$$

</aside>

What this plainly means is that the product of any matrix A and the identify vector create identities of A. 

<aside>
☁️ Corollary 3.2.9

Let A be an $m \times n$ matrix. Then $A\overrightarrow{x} = \overrightarrow{0}$, for all $\overrightarrow{x} \in \R^n$, if and ONLY if A = 0

</aside>

<aside>
☁️ Corollary 3.2.10

Let C and D be $m\times n$ matrices. Then $C\overrightarrow{x} = D\overrightarrow{x}$, for every x in R^n, if and only if $C =D$.

</aside>

![https://i.gyazo.com/9ddd0851b2adbb850420357af227ec8c.png](https://i.gyazo.com/9ddd0851b2adbb850420357af227ec8c.png)

# 3.3 Invertible Matrices

In previous examples and theory, we know that two matrices of the same size cannot be fully multipled (such that $AB = BA$) unless they are square matrices (m = n). The set of square matrices of order *n* is closed under the matrix operations:

- A, B are square matrices of order *n*, then these are all square matrices of order *n* as well.
    - A+B
    - A-B
    - AB
    - BA
    - $A^T$
- The product of the zero matrix of order *n* (n * n), with any other square matrix, A, on either side, is the zero matrix.
- The product of the identity matrix $I_n$ with any matrix A, on either side, is A itself → $A = AI_n = I_nA$

Similar to traditional algebraic operations, we can further define what it means to have a *power* to an integer *k* finally. The *k-th* power of A is $A^k$, and is the product of *k* copies of A (assuming that k ≥ 0)

Remembering back to the properties of matrix products that are always true, these apply to this power concept as a result:

- multiplication is *not* commutative
- the zero matrix can be the product of non-zero matrices.

Let's also go ahead and define what it means for a matrix to be *invertible*:

<aside>
☁️ Invertible Matrices

Given $A$ be a square matrix of order *n*. A is **invertible** (**non-singular**) if there is a square matrix B of the same order of *n*, such that:

$$
AB = I_n\\BA=I_n
$$

</aside>

This means that A has an *inverse*, the inverse of A is B. If no matrix B exists here, then A is called a "singular" or "not invertible" matrix. Similar to *inverse functions,* A and B are considered inverse to *eachother*, meaning that B is an inverse of A, if and only if, A is an inverse of B.

→ As a note, we can see that the zero matrix is NOT invertible, because there is no square matrix B of any order of *n* such that $0B = 0 \ne I_n$, because the zero matrix will never equal the identity matrix via product.

<aside>
☁️ Unique Inversion

If an $n\times n$ matrix A is *invertible*, then its *inverse* is unique. Thus, if B and C are inverses of A, then B = C.

</aside>

Thus we can say that for any invertible matrix, it is "the inverse" rather than "an inverse". By notation, we can also indicate the inverse using typical inverse notation: $A^{-1}$.

This is such that we can notate that: $AA^{-1} = A^{-1}A = I_n$.

We can also notate the *k-th* power of an invertible matrix A, because: $A^{-k}=(A^{-1})^k = (A^{-1})(A^{-1})...$

<aside>
☁️ Invertible Theorem Properties

Let A be an invertible matrix, then:

a) $A^{-1}$ is also invertible, since $(A^{-1})^{-1} = A$

b) $A^k$ is invertible for each non-zero integer K, $(A^k)^{-1} = (A^{-1})^k = A^{-k}$

c) For each $a \in \R^n$, with a ≠ 0, $aA$ is also invertible, and $(aA)^{-1} = \frac{1}{a}(A^{-1})$

</aside>

→ We can see that for any k'th power of the inverse,  an even power results in the identity matrix, and an odd power results in the inverse itself.

In the various examples in the text, we can see that invertible matrices have *related entries*, and this is a relationship that we can define and test. We use this following theorem to find the inverse to any square matrix of order 2, as long as the determinant of the matrix is NOT zero.

<aside>
☁️ Determinants and Invertible Matrices

Let $A = \begin{bmatrix}a&b\\c&d\end{bmatrix}$ be a square matrix of order 2. Then A is invertible if and ONLY if $\det(A) \ne 0$. If the determinant of this matrix is not zero, then:

$$
A^{-1}=\frac{1}{\det(A)}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}
$$

</aside>

This is proven by direct computation. We see that the dot-products in each entry work out to non-zero values by $ad-bc$ in the main diagonal. Thus, we can see that this is the determinant of the matrix, and results in $(ad-bc)I_2 = \det(A)I_2$.

We can apply previous algorithms to also expand this idea to work for any order, not just $\R^2$. We involve the Gauss-Jordan algorithm to the Augmented matrix $[A|I_n]$ to bring it down to RREF. The algorithm will produce the inverse of A given that A is in fact, invertible.

<aside>
☁️ Algorithm of Inverse Finding

1) Apply Gauss-Jordan to $[A\;|\;I_n]$

2) Depending on the result of the RREF, we can see whether or not A is invertible since:

a) A is invertible if RREF has the form $[I_n \;|\;B]$, and that $B = A^{-1}$

b) A is *singular* otherwise

</aside>

This algorithm is proven by the fact that we are essentially solving the linear system of $AX = I_n$. When the RREF obtained from Gauss-Jordan has as the coefficient matrix A, the identity matrix, then we know that the constant vector in RREF is then the solution. Pulling into the mix the previous theorems about rank and number of solutions, we also see that the rank of the identity matrix is equal to the number of unknowns, or the order of each of the equations, meaning that there is only 1 solution to the system. Otherwise, there is no solution. And because of that, we know that if there is no solution, then there is no (square) matrix C such that $AC = I_n$, and thus A is not invertible (it is singular).

<aside>
☁️ Let A and B be square matrices of the same order *n*, then if $AB = I_n$, then $BA = I_n$

</aside>

→ This is proven because A and B are inverse to each other, so there is a solution to the linear system involving $[A|I_n]$, which transforms this into $[I_n|B]$. So, the same steps used transform $[I_n|A]$ into $[B|I_n]$. Applying this to the other system, $[B|I_n] \implies[I_n|A]$. This lemma is special because it shows that either condition $AB = I_n$  or $BA = I_n$ is ***sufficient*** to determine if the square matrix A is invertible, and if $B = A^{-1}$.

Invertible matrices make previous operations have similar, but different properties, for example:

<aside>
☁️ Let A be an invertible matrix of order *n*, then the following are true:

a) The linear system $Ax =b$ is consistent

b) The linear system $Ax = b$ has a *unique* solution.

</aside>

a) is proven because of the trivial solution that $x = A^{-1}b$  creates a solution, which is equal to b. Thus, because it has a solution, it is trivially consistent.

b) is proven through the use of the inverse of A. If we multiply the system by the inverse, we see that the arbitrary vector *x* has only 1 solution, which is equal to $A^{-1}b$.

Knowing these theorems can help us solve linear systems if we know, or are able to find, that the coefficient matrix is invertible. If it is invertible, then there is a solution because it is consistent, and there is only 1 solution, $A^{-1}b$.

<aside>
☁️ Property of Cancellation

Let A be an invertible matrix of order *n:*

a) For $(n\times k)$ matrices B and C, if $AB = AC$ then $B = C$

b) For $(m\times n)$ matrices B and C, if $BA = CA$ then $B = C$

</aside>

These properties, in essence, allow us to "cancel" A from the equality, and thus allow us to state the equal relationship between two arbitrary matrices B and C. (a) is called the *left* cancellation, because A appears on the LEFT of each matrix multiplication, it is specific to B and C being matched on *n* rows. (b) is the *right* cancellation, for the same reasons of (a), except it appears on the right, and matches B and C on *n* columns.

These properties are proven by the fact that A is invertible, and has an inverse $A^{-1}$, which we use to cancel out A as so (making sure to multiply $A^{-1}$ on the left for *left cancellation*, and *right* for *right cancellation*)

$$
A^{-1}(AB) = A^{-1}(AC)\\(A^{-1}A)B = (A^{-1}A)C\\I_nB=I_nC\\I_nB=B\\I_nC=C\\\therefore B=C
$$

⭐ HOWEVER, if B and C are square matrices also of order *n*, and $AB = CA$, then there is no way to cancel A because it appears on different sides. We can apply A's inverse to this in the same direction on both sides, but emerge with $B = A^{-1}CA$ or $C = ABA^{-1}$, so here we see that B and C are not the same, but they are *similar*.

<aside>
☁️ Matrix Product Invertability

Let A and B be square matrices of order *n*. $AB$ is invertible, if and only if, A and B are BOTH invertible → $(AB)^{-1}=B^{-1}A^{-1}$.

If this is true, then $AB$ is invertible, and $B^{-1}A^{-1}$ is its inverse.

</aside>

From this we can specify whether or not a matrix product is invertable based on the invertability of its components:

<aside>
☁️ Invertible Matrix Products

If all (square) matrices involved in a matrix multiplication are *invertible*, then the product is also invertible.

The inverse of this product is the product of inverses in reverse order $(A_1A_2...A_m)^{-1}=(A_m^{-1}...A_2^{-1}A_{1}^{-1})$

</aside>

What about the *transposition* of an invertible matrix?

<aside>
☁️ Transposition Invertability

Let A be a square matrix, then A is invertible, if and only if, $A^T$ is also invertible.

$$
(A^T)^{-1}=(A^{-1})^T
$$

</aside>

Let's summarize the equativalence conditions for *invertible matrices* that are square:

<aside>
☁️ Square Matrix equivalencies, given that A is a square matrix of order *n*, these are ALL equivalent:

a) A is invertible

b) For every vector *b* of order n, the linear system $Ax = b$ has a unique solution

c) There is a vector b such that the linear system $Ax = b$ has a unique solution

d) $rank(A) = n$

e) RREF of A is $I_n$

f) For every vector b, the linear system $Ax = b$ is consistent

g) The linear (homogenous) system $Ax = 0$ has only 1 solution, the trivial solution.

</aside>

Operations on square matrices (of the same size) have similar rules to the math of numbers, except that they are still not commutative.

The *polynomial of matrices* is an example where scalar variables have the same rules:

<aside>
☁️ Polynomial of Matrices

Let A be a square matrix of order *n*, for the polynomial $f(x)$, we can apply the corresponding matrix A into this polynomial in substitute for the variable *x*. One caveat here is that $A^0 = I_n$ as the equivalent to $x^0 = 1$.

→ Here, even the standard rules for powers applies as:

a) $A^rA^s = A^{r+s} = A^sA^r$

b) $(A^r)^s = A^{rs}=(A^s)^r$

Calculating the result for $f(A)$ is the same as you would in a polynomial, except now we are using a square matrix that satisfies all the rules (except commutativity), and is closed under all these rules, so we arrive at a resulting square matrix of the same order as the result.

→ When the matrices we use as input to the function have the *roots of the polynomial equation* in their main diagonal (regardless of order), the result will always be the zero-matrix.

→ Because powers of a square matrix (the same matrix) commute, then for any polynomials $f(x), g(x)\implies f(A)g(A) = g(A)f(A)$

</aside>

We can also define the squared sum and difference of matrices:

<aside>
☁️ Squared Sum

$(A+B)^2 = A^2+AB+BA+B^2$ 

because AB and BA are not always the same, if they are: $= A^2 +2AB + B^2$

</aside>

<aside>
☁️ Difference of Squares

$a^2-b^2 = (a-b)(a+b) =(A-B)(A+B) = A^2-BA+AB-B^2$

again, unless AB = BA, we cannot simply further.

</aside>

# 3.4 Special Square Matrices

We can see some patterns in operations of matrices when we use matrices of special forms, like patterns in their entries with respect to the diagonal. Here are some of the special matrices to look out for:

<aside>
☁️ Given A as a square matrix of order *n:*

a) A is **symmetric** if $A^T = A$

![https://i.gyazo.com/09cf89e5be8cd12d88a88b10aea8a5a4.png](https://i.gyazo.com/09cf89e5be8cd12d88a88b10aea8a5a4.png)

b) A is **upper triangle** if *all entries below diagonal* are 0

![https://i.gyazo.com/6367edbbb622a5fb4e53fa1b91eac9ae.png](https://i.gyazo.com/6367edbbb622a5fb4e53fa1b91eac9ae.png)

c) A is **lower triangle** if *all entries above diagonal* are 0

![https://i.gyazo.com/45a6b2cb174d60c2cc63076074a37015.png](https://i.gyazo.com/45a6b2cb174d60c2cc63076074a37015.png)

d) A is **diagonal** if *all entries not on main diagonal* are 0 (it is both upper and lower triangle)

</aside>

These matrices aren't just interesting visually, they also maintain special properties in relation to matrix operations:

<aside>
☁️ Let A and B be square matrices of order n, the following are true:

a) Matrix Addition (A+B), subtraction (A-B), scalar multiplication (cA or cB) maintain the special patterns. For example, if A and B are both symmetric or upper/lower/diagonal triangles, then adding, subbing, or scaling them will preserve their form

b) Transposition preserves *symmetry* and *diagonality*, but *switches* triangularity (A is lower → $A^T$ is upper, vice versa).

c) Matrix Multiplication preserves *diagonality* and *triangularity.* If A and B are both the same triangularity, then AB is the same triangularity.

d) Powers and Inverse preserve ALL special forms. If A is symmetric, then taking $A^k$, all positive powers of this will also maintain the special form. Even if A is invertible, taking the *negative* powers will maintain the forms.

</aside>

<aside>
☁️ Let A have triangularity (either upper or lower), of order *n*. If A is invertible, then the following are true:

a) All entries on main diagonal are NON ZERO

b) The inverse of A, $A^{-1}$ is ALSO the same triangularity

</aside>

<aside>
☁️ The product of two symmetric matrices is symmetric IF AND ONLY IF they *commute*:

$(AB)^T = B^TA^T=BA$

</aside>

# 3.5 Elementary Matrices

This section is meant to further refine the operation of solving linear systems using matrix multiplication instead of row-based operations. We start by observing this operation:

![https://i.gyazo.com/0ff86f2c90f4d2d52303f91656e954ca.png](https://i.gyazo.com/0ff86f2c90f4d2d52303f91656e954ca.png)

When multiplying the matrix A (2x3) by diagonal vectors of size 2x2 and 3x3, we can see that it restricts the order that we multiple A by these matrices.  We takefrom this observation the pattern that:

<aside>
☁️ Multiplying from the LEFT affects the ROWS

</aside>

<aside>
☁️ Multiplying from the RIGHT affects the COLUMNS

</aside>

In which multiplying A by a diagonal on the LEFT makes the entries of the diagonal ROW-WISE, while multiplying the diagonal on the right of A makes the entries of the diagonal in the product COLUMN-WISE. So, in order to squeeze this idea into Gaussian Elimination, we would rather substitute row operations for diagonal matrix multiplications, and thus multiply the coefficient matrix by the diagonal to the left, so it affects the whole row.

Just like how we used elementary operations ****with scalars, we can do these same operations with the corresponding elementary matrices:

<aside>
☁️ Elementary Matrices

are square matrices of order *n*, that are obtained from the *identity matrix* $I_n$ by applying the elementary (row) operations a single time:

a) $cR_j \rarr R_i$

Multiply a row by a non-zero constant

b) $R_i \leftrightarrow R_j$

Interchange two rows

c) $cR_j +R_i=R_i$

Add a constant times one row, to another (replacing it)

</aside>

This way, we're applying the operations to the identity matrix, and multiplying the system by that matrix to *propogate* those changes in second step. Here are some examples of row operations to elementary matrices:

→ 3x3 matrices, $-3R_2 \rarr R_2$ (multiplying the second row by -3)

$$
\begin{bmatrix}1&0&0\\0&-3&0\\0&0&1\end{bmatrix}
$$

→ 4x4 matrices, $R_2 \leftrightarrow R_4$ (swapping the second and fourth rows)

$$
\begin{bmatrix}1&0&0&0\\0&0&0&1\\0&0&1&0\\0&1&0&0\end{bmatrix}
$$

⭐ To examine this further, we are changing the 2nd row to the 4th, so in the 2nd diagonal entry we move that down to the forth row, and the fourth diagonal entry is moved to the 2nd row

→ 3x3, $3R_3 + R_1 \rarr R_1$ (multiplying the third row by 3 and adding it to the first row)

$$
\begin{bmatrix}1&0&3\\0&1&0\\0&0&1\end{bmatrix}
$$

⭐ Here, we put 3 in the first row and third column.

The idea here is that to multiply a row/equation, we input the scalar into a diagonal corresponding to the COLUMN.  To move a row in the system, we move the scalar of 1 to a different row in that same row's corresponding column. If we want to add one row to another, we indicate that by putting the COLUMN of the row that we want to add, into the ROW of the row to add it to.

Because we saw earlier that we want to affect the *rows* of the system rather than the columns, we want to multiply the elementary matrices we create to the LEFT of the coefficient matrix:

<aside>
☁️ Let A and B be $m \times n$ matrices, if B is obtained from A by applying an elementary row operation for a single time, then:

$$
B = EA
$$

Where E is an $m\times m$ matrix, and is the only elementary matrix that corresponds to that elementary row operation

</aside>

We can use the augmented matrix's constant matrix to keep track of the elementary row operations as in $[A|I_n]$, where $I_n$ is its own elementary matrix that is modified every step. 

<aside>
☁️ The invertability of the elementary matrix

Given that E is an elementary matrix, it is then invertable, and the inverse is also an elementary matrix (of the same type, a/b/c).

</aside>

This is identical to saying that every elementary row operation is *reversible*, each elementary matrix that we apply is *invertible*, meaning that if we were to apply the *inverse* of the elementary row operation, it *undoes* the operation, reversing the effect.

<aside>
☁️ Matrix as a result of chained elementary operations

Given A and B being $m\times n$ matrices, and that B is obtained from A by a sequence of elementary row operations applied to the elementary matrices $E_1,E_2,...E_k$, all of order *m*. Then the matrix $B = E_kE_{k-1}...E_2E_1A$

</aside>

This being said is pretty obvious, because to obtain A, we multiply each resulting product of $E_iA$ for all necessary elementary matrices to obtain B. Because we are always multiplying the elementary matrix to the left of A, then it chains to the left, and B is the result after all operations.

<aside>
☁️ RREF invertability

Given A is an $m\times n$ matrix, and that R is A's RREF, then $R = CA$, in which C is a product of elementary matrices of order *m*, and is invertible.

</aside>

This is seen from section 3.3, since every elementary matrix is invertible, then its product is also invertible. Thus, since C is that product of chained elementary matrices of the same order, then it is invertible.

We can further break down what it means to be invertible, by knowing this fact that the product of invertible matrices is also invertible:

<aside>
☁️ Given any square matrix A of order *n*, it is invertible if and only if it is a product of elementary matrices.

</aside>

This means that any invertible matrix is, in essence, constructed from the chained multiplication of elementary matrices, and in way, can be factored backwards. We know this because if A is invertible, then its RREF is $I_n$, the identity matrix. That means that to arrive at the RREF, we must apply elementary matrices and operations to revert this matrix A back to its original state, RREF.