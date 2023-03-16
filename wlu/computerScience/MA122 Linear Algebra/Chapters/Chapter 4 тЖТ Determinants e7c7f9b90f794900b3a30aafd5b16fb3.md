# Chapter 4 → Determinants

# 4.1 Determinants Defined

The determinant for the 2x2 matrix is defined as $det(A) = ad - bc$. This is similar to thinking about the *geometry* of the parallelogram that is formed by these two column vectors, as a matrix. In $\R^2$ it is also equivalent to the **area** of that paraellelogram. We can also think about the *row vectors* of this square matrix in terms of the area, if these row vectors were *linearly dependent* on the same direction, ie. they are parallel, then the area of this **singular** matrix will be zero (0) because they don't form a parallelogram in fact. So if the matrix A is singular, then we know that the determinant is also 0.

Scaling and adding to the area formed by that parallelogram is also in a way scaling the determinant, so those operations will carry through:

$$
det(\begin{bmatrix}a_1+a_2 &b_1+b_2\\c&d\end{bmatrix}) = det(\begin{bmatrix}a_1 &b_1\\c&d\end{bmatrix}) + det(\begin{bmatrix}a_2 &b_2\\c&d\end{bmatrix})
$$

And the same for *scaling* components of these determinants. 

We also know from the previous chapter that matrices of order 2 have their **inverse** expressed in terms of its determinant, as $A^{-1}=\frac{1}{det(A)}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$.

Defining the determinant is simple for orders of 2, but becomes complex for higher orders as there are many more combinations of terms of components of matrices. We use the recursive definition of higher order determinants:

<aside>
☁️ Determinants

Given A to be a 1x1 matrix, it's determinant is given by det(A) = det[a] = a. So if *k* is a (+int) and that the determinant of any (k*k) matrix is a $\R$, then the determinant of a (k+1)*(k+1) matrix is given by a recursive formula called the **cofactor expansion**, which is this:

For a square matrix A of order n = k+1, the (i,j)th submatrix is $\tilde{A}_{ij}$, in which the ith row and jth column are *deleted* from A. (In simple terms, this means that this submatrix is obtained by crossing out those rows and only considering the remaining components. The **determinant** of this SUBMATRIX is called the (i,j)-minor of A. We also define the (i,j)-cofactor denoted as $C_{ij}$(A), is $C_{ij}(A)=(-1)^{i+j}det(\tilde{A}_{ij})$.

This means that the cofactor is an *alternating sign* depending on the sum of (i + j) → positive if i+j = even, and negative when i+j is odd.

We can also split off the *cofactor expansion* to be along only rows or columns, such as:

- The cofactor expansion along the i-th row
    - $a_{i1}C_{i1}+a_{i2}C_{i2}+...+a_{in}C_{in}$
- Cofactor expansion along the j-th column
    - $a_{1j}C_{1j}+a_{2j}C_{2j}+...+a_{nj}C_{nj}$

and the DETERMINANT of A is the COFACTOR EXPANSION along the FIRST ROW:

- $det(A) :=a_{11}C_{11}+a_{12}C_{12}+..+a_{1n}C_{1n}$
</aside>

Based on the grid-matrix to the right, we can see the pattern of sums that result in the cofactors of components and their signs.

We can see in the example as well that the submatrices are defined as crossing out the rows that are used, leaving a submatrix of components. This is why in a 2x2 determinant, the components have different orders (a → d, d → a) and why B and C are negative, because their minors follow this pattern. This also combines nicely with the rest of the determinant equation for a 2x2, as ad - bc, because the det(A) originally involves the cofactors and minors of the FIRST ROW.

$$
det(A) = a_{11}C_{11}+a_{12}C_{12}\\det(A) = aC_{11}+bC_{12}=ad-bc
$$

Because the cofactors $C_{11}=d; C_{12}=-c$.

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled.png)

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%201.png)

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%202.png)

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%203.png)

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%204.png)

Let's expand this to a 3x3 matrix. We find the submatrices/minors of the matrix A by crossing out each row and column in that minor's original matrix. Because A is a 3x3 matrix, its minors are 2x2 matrices, and the *recursion* stops here, because we know what the determinant of a 2x2 matrix is without needing to recurse further.

Once we know the submatrices of the minors of the FIRST ROW (because the determinant only requires the first row of cofactors), we can find the cofactor expansion using the (i,j)th element and the (i,j)th minor, alternating the signs to suit the pattern of the checkerboards.

Let's involve the special matrices in the calculation of determinants. What happens when we attempt to find the determinant of a *lower triangular* matrix of order n? Well, because the first row has AT MOST, ONE non-zero element, then the cofactor expansion results in 0 * Cofactors in all but its first term, leaving the first cofactor of $a_{11}det(\tilde{A}_{11})$. Depending on the order of n, this will cause recursion downwards in order to find the lower determinants of matrices larger than order 2. Thus, the resulting equation after induction is:

$det(A) = a_{11}a_{22}...a_{nn}$, ie. the multiplication of the diagonal elements of A.

From this follows that the determinant of a diagonal matrix, is then also the same formula applied. Because it doesn't necessarily matter what the elements in the lower-triangle of the matrix are, just that the FIRST ROW of its elements result in 0 cofactors other than the first element of the diagonal.

So we can reason that the determinant of the identity matrix is always 1, and that $det(aI_{n}) = det(diag(a,a,...,a))=a^n$, meaning that the scalar of the identity matrix's determinant is that scalar to the power of the order of the identity matrix it multiplied.

<aside>
💡 SUMMARY

Determinant of 2x2: $det(A) = ad -bc$

Determinant of k*k, k > 2: det(A) = cofactor expansion of the first row = $a_{11}C_{11} + a_{12}C_{12}+...+a_{1k}C_{1k}$, where any cofactor $C_{ij}$'s SIGN (positive/negative) depends on the sum of i+j → $(-1)^{i+j}$, and whose value depends on the determinant of the submatrix of $\tilde{A}_{ij}$, where the i-th row and the j-th column are excluded from A to form the submatrix. This process is **recursive** in that it will recurse down the tree of determinants to find the lowest branch of known determinants, typically the 2x2 submatrices.

The Determinant of a LOWER TRIANGULAR matrix AND the DIAGONAL matrix are both the multiplicative chain of their diagonal elements, this is because the cofactor expansion only involves the FIRST element that is part of the main diagonal and the rest are NULLed by zero multiplicatives of elements.

</aside>

# 4.2 Properties of Determinants

<aside>
💡 Laplace (cofactor) Expansion Theorem

> Given that A is a SQUARE matrix of order N, then for any i = 1, 2, ..., n, the determinant of A can be computed along ANY row's cofactor expansion.
> 

This is an extremely useful theorem that is used to simplify the calculation of determinants for any square matrix, as we can choose an optimal row to simplify the computations

</aside>

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%205.png)

Take this matrix for example, a 4x4 matrix A. The second row has only ONE non-zero entry, making it the optimal row for choosing the cofactor expansion of, because the determinant of A is then $1 * det(\begin{bmatrix}1&1&2\\0&-2&0\\-1&1&1\end{bmatrix})$. This is because this is the (2nd row, 2nd column) cancelled submatrix, and all other cofactors are multiplied by the zeroes in the row. Further expansion shows us that in this 3x3 submatrix, there is an optimal row to choose, the 2nd, because there is only 1 non-zero entry (-2), so we can find the determinant of the 3x3 matrix by finding the cofactor expansion of the 2nd row, which is $-6$.

Thus, we can use the Laplacian theorem to justify other theorems, such as the fact that:

<aside>
💡 If any square matrix of order *n* has any row of only zeroes, then the determinant(A) = 0.

This is because the cofactor expansion of any row is equivalent to the cofactor expansion of any other row, so if there is a row of only zeroes, then we know that the minors multiply by the elements of the row, and yield 0. Which means that all other cofactor expansions will be the same.

</aside>

Onto a more complex involvement of the determinant, if a square (n*n) matrix A is expressed as a COLUMN vector composed of its ROW vectors, then we can further break this down to express a SINGLE ROW as a scalar sum of two vectors, u and v → $w_k = ru_k + v_k$. Where *k* is a fixed row, and the row $w$ is that fixed row expressed as that scalar sum of u and v; this means that (u and v) are both row vectors, and then the determinant of A is equivalent to the added determinants of these two rows U and V.

$$
det(A) = det(rU) + det(V) = r*det(U)+det(V)
$$

The determinant can be visualized to explain the *area* of the parallelogram or the VOLUME of the (3D) parallelepiped. This is why the area of a parallelogram in $\R^2$ is equal to the determinant of the 2x2 matrix formed by both 2D vectors. In the previous equation involving fixing a *row* of the matrix and expressing it as a scalar sum, relates to fixing an axis of the parallelogram and varying the other dimensions. The determinant calculates this changing area.

<aside>
💡 If A is a square matrix where its order ≥ 2, and it has two IDENTICAL rows, then det(A) = 0.

This is proven with Induction. The base case is that in $\R^2$, identical rows look like: $\begin{bmatrix}a&b\\a&b\end{bmatrix}$, $det(A) = ab - ba = 0$. So, by the base case, we can assume that for any k ≥ 2, the det. of any k * k matrix with identical rows is 0. To inductively prove this, we set $n = k + 1$, and consider that matrix of n * n A to have two identical rows. To show this, we do the cofactor expansion along a row that is NOT one of the identical rows. We see that as we find the MINORS of this grand-matrix A, the submatrices will NOT have the rows that we just cancelled out (ie. the NON-identical ones), so they WILL CONTAIN the identical rows. We know from the base case, that the determinant of this will equal 0, so the cofactors along the non-identical row will equal zero as they all contain the identical row, and that implies that det(A) = 0.

*Editor's note : the *identical* rows and columns also applies to *proportional* rows and columns. This is because geometrically, they are in the same direction/plane, and do not form a parallelogram. In terms of linear systems, either row can be used to entirely eliminate the identical/proportional row, creating a zero-row, and thus algebraically, the determinant is 0 → because this matrix is then singular, because it is not a result of elementary matrix products.

</aside>

This factoid is further carried into the proposition:

<aside>
💡 $a_{i1}C_{k1}+a_{i2}C_{k2}+...+a_{in}C_{kn} =0$

</aside>

Given that this applies to a square matrix A where n ≥ 2, and $i, k \in [1,2,...,n]; i \ne k$.

This means that the cofactor is considered along two different *rows* (as i and k are the row-variables), and it takes the *i-th* row's element at the *k-th* row's minor. This is proven by the fact that we replace the k-th row with the i-th row of A to get a matrix B, which means that the cofactor expansion is along the k-th row of B, which has identical rows, and thus implies that the det(B) is 0.

This proposition is also called the Kronecker Delta:

<aside>
💡 $a_{i1}C_{k1}+a_{i2}C_{k2}+...+a_{in}C_{kn} = \delta _{ik}det(A)$

$$
\delta _{ik} = \begin{cases}0, i\neq k\\1, i=k\end{cases}
$$

</aside>

The identity matrix $I_n$ is the matrix with entries given by $(I_n)_{ij} = \delta _{ij}$. 

Here is a summary theorem that explains the properties of the determinant under the **elementary operations**:

<aside>
💡 Determinants under Elementary Operations

a) if $A_1$ is obtained from A by multiplying a row by *r*, then $det(A_1) = rdet(A)$

b) if $A_2$ is obtained from A by *switching two rows*, then $det(A_2) = -det(A)$

c) if $A_3$ is obtained from A by *adding some multiple of one row to another*, then $det(A_3) = det(A)$

</aside>

These rules can be applied to simplify higher-order square matrices to help simplify the computation of the determinant. For example, we can put certain matrices into *lower triangular* by using the rule of *c*), and the determinant stays the same, but is easier to calculate because to find the determinant of a lower triangle matrix is just multiplying the diagonal (main) elements.

Elementary MATRICES do not have zero determinants, they have very simple determinants in fact.

1) if $E_1$ is obtained by multiplying one row of $I_n$ by a non-zero *r*, then:

$det(E_1) = rdet(I_n) = r(\neq 0)$

2) if $E_2$ is obtained by switching two rows of $I_n$, then:

$det(E_2) = -det(I_n) = -1$

3) if $E_3$ is obtained by adding scalar multiple of one row of $I_n$ to another, then:

$det(E_3) = det(I_n) = 1$

Recall to the fact that we can carry out the elementary operations on a matrix A through multiplication of the corresponding elementary matrix E (of the same size). If this condition is true, then it is also true that:

<aside>
💡 $det(EA) = det(E)det(A)$

</aside>

<aside>
💡 Determinant of an invertible matrix

given A to be a *square matrix of order N*, then A is invertible *if and only if* $det(A) \ne 0$.

</aside>

This is proven by the fact that all invertible matrices are a composition of elementary matrix multiplications, so since every elementary matrix has a determinant that is not 0, then there is no way for the matrix multiplication to equal 0. That means that if the matrix A is invertible, then it has a determinant because it has a non-zero matrix multiplication, but also that A is invertible if it has a non-zero determinant. Thus, if A has a zero determinant, then it is not invertible.

Transposed matrices have equivalent rules and theorems about the determinant, but apply to columns rather than rows.

<aside>
💡 Determinant of the Transpose

for a square matrix A, $det(A) = det(A^T)$

</aside>

→ this is proven with two cases, that A is singular, or A is invertible.

if A is singular, then it is not invertible, and has a zero determinant, and thus the determinant of the transpose is also 0.

if A is invertible, then we use the above fact that it is a product of elementary matrices, and that the transpose is equivalent to the reverse product of transposed elementary matrices. So, those multiplicative determinants apply and the determinant remains the same, because the determinant is scalar and associative, so $det(A) = det(E_1) *...*det(E_k) = det(E_k^T)*...*det(E_1^T)=det(A^T)$ 

Because the determinant applies to COLUMNS as it does to ROWS, then we adapt the properties to fit:

a) determinants can be computed using cofactor expansion along ANY ROW or COLUMN

b) if A has a zero ROW or COLUMN, then det(A) = 0

c) if A has ≥ 2 proportional (equal) ROWS or COLUMN, then det(A) = 0

d) if A is UPPER or LOWER triangular, then the determinant is the product of main diagonal entries

Using the previous theorems and axioms, we can finally understand why this is also true:

<aside>
💡 Determinant of the Product (of two distinct Matrices)

$$
det(AB) = det(A)det(B)
$$

</aside>

Similar to how we proved that the determinant of the transpose of the same as the original matrix, we use cases here. The first case is that:

A is singular → 

Thus, AB is also singular (because AB can only be invertible if both A and B are invertible), so since AB is singular, then det(AB) = 0, because of the previous few theorems. And since A is singular det(A) = 0. This is trivial, because $0 = 0det(B) = 0$.

A is invertible →

Then A is a product of Elementary Matrices $A = E_1E_2...E_k$, and thus $AB = E_1E_2...E_kB$.

Because of the last lemma, we know that $det(EA) = det(E)det(A)$; which applies repeatedly to this case in which AB is composes of elementary matrices and B. thus, $det(AB) = det(E_1)det(E_2)...det(E_k)det(B) = det(E_1E_2...E_k)det(B) = det(A)det(B)$.

As a small note, the determinant **bypasses** the rule of *noncommutativity* of the matrix product, meaning that $det(AB) = det(A)det(B)=det(B)det(A)=det(BA)$.

<aside>
💡 Determinant of a scalar multiple of A

$$
det(kA)=k^ndet(A)
$$

</aside>

This is proven very simply by the fact that $det(kA)=det(kI_nA) = det(kI_n)det(A)=k^ndet(A)$.

<aside>
💡 Determinant of the inverse of A

given A to be invertible (ie. det(A) ≠ 0), then $det(A^{-1})=\frac{1}{det(A)}$.

</aside>

This is proven by $1 = det(I_n)=det(AA^{-1})=det(A)det(A^{-1})$. Because the determinant of the Identity matrix is always 1 (because 1*1*...*1 = 1), the identity matrix is always the result of the product of a matrix and its inverse. Thus, if we multiply the determinant of a matrix by some other number, and it must equal 1, then we multiply by the reciprocal.

Unfortunately, there is no closed formula dealing with adding or subtracting matrices within the determinant, so $det(A+B) \neq det(A)+det(B)$.

# 4.3 Adjoint Matrix + Cramer's Rule

> In the previous chapters, we looked at and studied the Gauss-Jordan algorithm, which is a series of steps we take, and the output of that algorithm is a matrix which tells us the *inverse* of the original matrix, or if the matrix is singular through contradiction.
In this chapter however, we saw that we can determine if a matrix is *singular* or *invertible* entirely based on whether the **determinant** of the matrix is 0 or non-0. This will help us construct a closed formula for finding the inverse if it exists, based entirely on the elements of the matrix itself.
> 

<aside>
💡 Adjoint Matrix

given A to be a SQUARE matrix of order N (n ≥ 2), then the *matrix of cofactors* of A is the matrix $C(A)$ whose (i,j)-entry is the (i,j)-cofactor of A. The **Adjoint Matrix of A** is the transpose of its cofactor matrix.

</aside>

![Cofactor Matrix of A](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%206.png)

Cofactor Matrix of A

![Adjoint Matrix of A](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%207.png)

Adjoint Matrix of A

<aside>
💡 As a reminder, the *cofactor* (i, j) is based on the submatrix of A (called the minor), in which we ignore the (i, j) row/column, and include the remaining elements. This is a (n-1 * n-1) submatrix of A. the cofactor itself is the computed determinant of the minor of the same (i,j).

$$
C_{ij}=(-1)^{i+j}det(\tilde{A}_{ij})
$$

</aside>

We need to also remember the theorem involving the **Kronecker Delta:**

<aside>
💡 Given A to be a square n*n matrix (n ≥ 2), then for any indices $1 \le i, j\le n$,

$$
a_{i1}C_{j1}+a_{i2}C_{j2}+...+a_{in}C_{jn} = \delta_{ij} det(A)\\\delta_{ij}=\begin{cases}1, i=j\\0, i\ne j\end{cases}
$$

</aside>

We can now help to prove the closed computation of the determinant of an invertible matrix:

<aside>
💡 A is invertible, square of n, n ≥ 2, then det(A) ≠ 0 AND

$$
A^{-1}=\frac{1}{det(A)}adj(A)
$$

</aside>

Which is exactly what we saw when we were finding the inverse of a 2x2 matrix. Because the 2x2 matrix's minors are 1x1 submatrices, the 2x2 matrix is the easiest to compute WITHOUT cofactors, because it is only $det(A) = ad-bc$. Finally, the gotcha in computing the 2x2 matrix inverse using this determinant is that we did not multiply by the matrix A itself, but rather one in which $\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$. This was implicitly the adjoint matrix of A, because the cofactor of [a] was [d], and the cofactor of [b] was [-b], and vice versa.

To mathematically prove this theorem, we compute $A*adj(A)$. 

Multiplying each row of A by adj(A), we can see that we land with:

$$
a_{11}C_{11}+a_{12}C_{12}+...+a_{1n}C_{1n}
$$

Which is equivalent to the *kronecker delta* relation defined previously. Because each of the elements in the (n*n) resulting matrix are one of these, we can see that the **kronecker delta's** value start to affect the determinant, as the delta is 1 when (i = j), and 0 otherwise. So, the only times i = j is on the main diagonal, so the product of A and its adjoint matrix starts to turn into the diagonal matrix of the determinant of A, which in turn is basically multiplying the Identity Matrix of N by the determinant of A.

And because we *know* that the matrix A is invertible, and its determinant cannot equal 0, then:

$$
A(\frac{1}{det(A)}adj(A))=I_n
$$

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%208.png)

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%209.png)

In this way, then the term $\frac{1}{det(A)}adj(A)$ multiplies with A to equal $I_n$, which by definition, makes the inverse of A equal to $A^{-1}=\frac{1}{det(A)}adj(A)$.

When we apply this to *linear systems*, we can see that as if A was invertible, then $Ax = b$ has the trivial sol. of $x = A^{-1}b$. Using the new inverse formula, we can see that:

$$
x = \frac{1}{det(A)}adj(A)b
$$

This is exactly what **Cramer's Rule** is.

<aside>
💡 Cramer's Rule

given the linear system $Ax = b$, where A is a square matrix of n, and that $det(A) \ne 0$, then the system has a unique solution that is given by:

$$
x_1 = \frac{det(A_1)}{det(A)},\;x_2 = \frac{det(A_2)}{det(A)},\;x_n = \frac{det(A_n)}{det(A)}
$$

Where the matrix $A_j$ is obtained by *replacing the **j-th** column of A, by the column vector $\overrightarrow{b}$.*

</aside>

For n = 1, the proof is trivial since the equation $ax = b$ has the unique sol. $x = \frac{b}{a}$ if a ≠ 0.

For n ≥ 2, we know that A is invertible since det(A) ≠ 0, and that the sol. to $Ax = b$ is then $x = A^{-1}b$. To prove that $A_j$ is the matrix A in which the column *j* is replaced by *b*, we compute that $\frac{1}{det(A)}adj(A)b$ concludes in $x_j = \frac{b_1C_{1j}+b_{2}C_{2j}+...} {det(A)}$. If we start from the other end, and replace the j-th column in A with b, we can see that $det(A_j) = b_{1}C_{1j}+b_2C_{2j}+...+b_nC_{nj}$ which is the *numerator in $x_j$.* So, to simplify the computation, we can compute $x_j$ by using $det(A_j)$ and $det(A)$.

# 4.4 $\R^3$ Cross Product

We can further define the cross product of two vectors in $\R^3$ using the determinant. This is to illustrate the *growth in volume* of the 3D parallelepiped formed by the two vectors. Two vectors, both in $\R^3$ cannot have their determinant computed however, because putting both vectors into a single matrix results in a (3 * 2) matrix, which we cannot compute the determinant because it is not square (and thus is not invertible).

HOWEVER, we can turn this 3*2 matrix into a (3*3) just by adding 3 special $\R^3$ vectors:

$$
i = \begin{bmatrix}1\\0\\0\end{bmatrix},j=\begin{bmatrix}0\\1\\0\end{bmatrix}, k=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

<aside>
💡 Cross product as the *determinant*

given $v = \begin{bmatrix}v_1\\v_2\\v_3\end{bmatrix} and \;w=\begin{bmatrix}w_1\\w_2\\w_3\end{bmatrix}$, then the vector $v\times w$ can be expressed as:

$$
v\times w = det\begin{bmatrix}i&j&k\\v_1&v_2&v_3\\w_1&w_2&w_3\end{bmatrix} = (transposed)\;\begin{bmatrix}i&v_1&w_1\\j&v_2&w_2\\k&v_3&w_3\end{bmatrix}
$$

</aside>

This definition of the cross product still holds the properties of the cross product, namely that:

Anti-commutative: $v\times w = -(w\times v)$

Bilinear: $(u + v)\times w = (u\times w) + (v\times w)$

Right-hand Rule: $i\times j = k,\;j\times k = i,\;k \times i = j$

This definition is also proven by taking the *cofactor expansion* along the FIRST row (in which it is just the **basis vectors**, i, j, and k).

$$
i*det\begin{bmatrix}v_2&v_3\\w_2&w_3\end{bmatrix}-j*det\begin{bmatrix}v_1&v_3\\w_1&w_3\end{bmatrix} + k*det\begin{bmatrix}v_2&v_2\\w_1&w_2\end{bmatrix}=
\begin{bmatrix}v_2w_3 - v_3w_2\\v_3w_1-v_1w_3\\v_1w_2-v_2w_1\end{bmatrix}=v\times w
$$

In chapter 1, we figured out that the cross-product of two vectors, v and w, results in a third vector that is **orthogonal** to BOTH vectors v and w. This is why we cannot do cross-products in any other dimension than $\R^3$.

In fact, the **norm** (length/magnitude) of the cross-product is also important, and is represented in this identity:

<aside>
💡 **Lagrange's Identity**

For $v, w \in \R^3$

$$
||v\times w||^2=||v||^2||w||^2-(v\cdot w)^2
$$

</aside>

This is proven by computation directly, from both sides (meeting in the middle).

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%2010.png)

This theorem is applied to create the theorem of area of a parallelogram (in $\R^3$).

<aside>
💡 let $\angle ABCD$ be a parallelogram in $\R^3$, then

the area of $\angle ABCD = ||AB\times AD||$

</aside>

This seems very intuitive now, because the area of the parallelogram in $\R^2$ was the determinant.

We can see now that the formula for calculating area of a parallelogram in n > 2 involves the Lagrange Identity:

$$
area(ABCD) = ||v||\;||w||\sin\widehat{(v,w)}\\=\sqrt{||v||^2||w||^2-(v\cdot w)^2}=||v\times w||
$$

A Parallelepiped is a 3D Form that is made of 6 parallelograms, each parallelogram represents a single face of the -piped. At any single vertex of a -piped, there are THREE edges converging at A, which we can represent by *u, w, v*.

A formula emerges from the previous theorems about the *volume (3D)* of the -piped.

<aside>
💡 Area of a parallelepiped

Given that u, w, and v are in $\R^3$, then the volume of the -piped formed by these 3 vectors is:

$$
|u\cdot (v\times w)| = |det\begin{bmatrix}u_1&v_1&w_1\\u_2&v_2&w_2\\u_3&v_3&w_3\end{bmatrix}|
$$

→ we can also from this formula, determine if the 3 vectors are on the *same plane* if the area equals 0. This means that no -piped is formed by these 3 vectors.

</aside>

This is proven because the volume of this -piped is calculated geometrically by the product of the length of |HE| = h, and the base formed by (v x w). The length of height (h) is the orth. projection of u onto the area formed by v and w:

$$
h = ||proj_{v\times w}(u)|| = \frac{|u\cdot (v\times w)|}{||v\times w||}
$$

This means that the geo. computation of the volume is $||v\times w|| \times h = |u\cdot(v \times w)|$; because the lower fraction is cancelled by the multiplication (because they are the same).

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%2011.png)

This term "$u \cdot (v\times w)$" is then equivalent to the *determinant of the parallelepiped* by definition, but here is the theorem and proof:

<aside>
💡 Geometrical volume related to the determinant of a parallelepid

$$
u \cdot (v\times w) = det\begin{bmatrix}u_1&u_2&u_3\\v_1&v_2&v_3\\w_1&w_2&w_3\end{bmatrix} = det(transposed)
$$

→ in this case, the (transposed) matrix is just the matrix formed by the three $\R^3$ vectors of the -piped, transposed.

</aside>

This is proven through computation and using the basis vectors *i, j and k.*

![Untitled](Chapter%204%20%E2%86%92%20Determinants%20e7c7f9b90f794900b3a30aafd5b16fb3/Untitled%2012.png)

And this is also how we can prove that the cross product of $v \times w$ is ORTHOGONAL to both v and w:

$$
v\cdot (v\times w) = det\begin{bmatrix}v_1&v_1&w_1\\v_2&v_2&w_2\\v_3&v_3&w_3\end{bmatrix}=0
$$

→ Because the determinant of a matrix with proportional rows/columns is 0, because it is singular.

Since $v \times w$ is ALSO a vector in $\R^3$, then what about $u \times (v \times w)$ or other bilinear combinations of the cross products of the three vectors?

<aside>
💡 Given $u, v, w \in \R^3$, then

a) $u \times (v \times w) = (u\cdot w)v - (u\cdot v)w$

b) **Jacobi Identity**: $u\times (v \times w) + v \times (w \times u) + w\times (u\times v) = 0$

</aside>

The Jacobi Identity follows from the first point, and all the terms of combinations of cross-products negate each other, it also works because dot-products are commutative.