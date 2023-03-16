# Eigenvalues, Eigenvectors, Diagonalization

Let's start off with understanding how we move on from transformations of a matrix. Given a transformation $T: \R^2 \rarr \R^2$, and that:

$$
T(v_1) = 2v_1, \quad T(v_2)=\frac{1}{2}v_2
$$

Where $v_1 = [1\quad 2], v_2 = [2,\quad -1]$. Then $\{v_1,v_2\}$ is a basis for $\R^2$ because they are lin. independent, and they are invertible.

# 7.1 Definitions and Properties of *Eigenvalues* and *Eigenvectors*

The scenario given by the textbook is extremely confusing and not intuitive in the slightest. It requires first knowing that we are using a *basis* that is not the coordinate plane. The scaling of non-coordinate basis vectors is not exactly the same as scaling coordinate vector bases. So, we need to find if there is a direction in $\R^n$ along which the multiplication of vectors by any $n \times n$ matrix coincides with scaling.

<aside>
💡 Eigenvalue and Eigenvector

Given A to be (n*n), a non-zero vector *v* is called an **eigenvector** of A, if $Av$ is a *scalar multiple* of *v*.

$$
Av = \lambda v
$$

The scalar $\lambda$ is the **eigenvalue** of A, while the vector *v* is the **eigenvector of A, corresponding to** $\lambda$**.**

</aside>

Here's an example to solidify the idea:

<aside>
💡 Verify that $v = [1,2]$ is an eigenvector of $A = \begin{bmatrix}3&0\\8&-1\end{bmatrix}$, with an eigenvalue of $\lambda = 3$.

$$
Av = \begin{bmatrix}3&0\\8&-1\end{bmatrix}\begin{bmatrix}1\\2\end{bmatrix}=\begin{bmatrix}3\\6\end{bmatrix} = 3v
$$

</aside>

If we think about this geometrically, we are *stretching/dilating* the vector *v* by a factor of 3. The equation $Av = \lambda v$ is a simultaneous equation for both *v* and the eigenvalue, so finding the eigens has two steps:

1) Find set of eigenvalues for A

2) Find set of eigenvectors for A that correspond to each eigenvalue.

Eigenvalues of A are NON-ZERO solutions to the equation $Av = \lambda v$. We can involve the identity matrix to spice up the equation like so:

$$
\lambda x =\lambda I_nx\\(\lambda I_n - A)x = 0
$$

This bottom equation is now in terms of the homogenous system, and only has a non-zero solution iff. $\det(\lambda I_n - A) = 0$. The determinant of the Eigenvalue Identity subtracted by the matrix A is 0. A little more simply said, the only solution to this homogenous system happens when $\lambda I_n$ is the same as A, because then the term $(\lambda I_n - A) = 0$, and thus a solution. 

Thus, this is one of the criteria for the eigenvalue:

<aside>
💡 a scalar is an eigenvalue of A if and only if $\det(\lambda I_n - A) = 0$.

</aside>

Let's take an example to find out the values of $\lambda$ that exist for a square matrix $A = \begin{bmatrix}3&0\\8&-1\end{bmatrix}$.

<aside>
💡 Example

$$
\det(\lambda I_n - A) = det(\begin{bmatrix}\lambda&0\\0&\lambda\end{bmatrix} - \begin{bmatrix}3&0\\8&-1\end{bmatrix}) = \det(\begin{bmatrix}\lambda - 3&0\\8&\lambda -1\end{bmatrix}) = (\lambda-3)(\lambda+1)=\lambda^2-2\lambda-3
$$

This means that the values of $\lambda$ for which the determinant equals 0, are then $\lambda_1 = 3, \lambda_2 = -1$

</aside>

This is applied more generally because this is normally the case, that the eigenvalue's criterion is in the form of a polynomial of degree $n$:

<aside>
💡 Theorem

Given A to be $n \times n$, then $\det(\lambda I_n - A)$  is a polynomial in $\lambda$ of degree *n*:

$$
\lambda^n + c_1\lambda^{n-1}+...+c_{n-1}\lambda+c_n
$$

</aside>

We know this is in the degree of *n*, because the highest power of $\lambda$ is the product of all the diagonal entries of $\lambda I_n - A$, and there are *n* diagonal entries.

This next lemma is an important concept about the determinant itself:

<aside>
💡 Lemma

Given A to be a square matrix of *n*. Then $\det(A)$ can be written as the sum of *distinct* terms, each being a signed product of *n* distinct entries in A. One of those terms will always be the product of all the entries on the *main diagonal* with the positive sign.

</aside>

This is proven by induction. We know that for an *n = 2*, the det(A) = ad - bc. the term *ad* here is a positive product of the main diagonal. When n > 2, we see that the cofactor expansion will always create a product of the diagonal entries in its first term, which keeps chaining as we recursively compute the determinant and minors of submatrices for which n ≥ 3.

This positive product of main diagonal entries is called a **signed elementary product**, which hints at its contribution in another way to defining the determinant of a square matrix. The other way uses the *factorial* of n in combination with attributing signs to the elements of the matrix.

<aside>
💡 Characteristic Polynomial & Equation

The **characteristic polynomial** of a square matrix A (order *n*) is the *degree n* polynomial:

$$
C_A(\lambda) = \det(\lambda I_n - A) = \lambda^n+c_1\lambda^{n-1}+...+c_n
$$

While the **characteristic equation of A** is the equation such that $C_A(\lambda) = 0$.

</aside>

One very important idea for this chapter is that **eigenvalues are roots for the characteristic equation**.

<aside>
💡 Let A be square of *n*, then a real number $\lambda$ is an eigenvalue of A, if and only if it is a *real root* of the characteristic poly. of A.

</aside>

Because the *triangular* (upper, lower, diagonal) matrices have special shortcuts to computing the determinant, then these matrices also have a very simple way to deduce their eigenvalues:

<aside>
💡 Given A be square of n, and it is triangular, then the eigenvalues of A are the *entries on the main diagonal* of A.

</aside>

This is because the determinant of the term $\lambda I_n - A$ means that only the main diagonal entries will be $\lambda - a_{ij}$, and the characteristic equation becomes 

$$
(\lambda - a_{11})(\lambda - a_{22})...(\lambda - a_{nn}) = 0
$$

So based on simple roots of a factored polynomial, the roots are $\lambda_i = a_{ii}$.

* Remember, this is true for only upper/lower triangular and diagonal matrices.

An interesting thing about the characteristic polynomial of A is that the determinant of A will appear in the last term:

<aside>
💡 Lemma

Given that $C_A(\lambda)$  is the characteristic polynomial of A, then

$$
c_n = C_A(0) = (-1)^n\det(A)
$$

</aside>

Because of this fact, we can relate the eigenvalue to invertibility, because eigenvalues are related to determinants of a square matrix.

<aside>
💡 The square matrix A is invertible if and only if $\lambda = 0$ is NOT an eigenvalue of A.

</aside>

This means that no eigenvector has an eigenvalue for which the matrix A is NOT invertible, because invertible matrices CANNOT have determinants of 0.

In the definition of the eigenvalues and characteristic equations, the stipulation is made that eigenvalues are **real** roots to the characteristic equation. So, because we deal with polynomials, which can have 3 different types of solutions, not all square matrices and their characteristic equations have real roots. If we remember back to the quadratic equation:

$$
x = \frac{-b \pm \sqrt{b_2-4ac}}{2a}
$$

The **discriminant** is the term that defines the number of roots (real or not): $b^2-4ac$.

1) Two distinct **REAL** roots if $b^2-4ac > 0$

2) Two REPEATED real roots if $b^2-4ac = 0$

3) No REAL roots if $b^2-4ac < 0$

Here's an example of a square matrix with no real roots (and thus, no eigenvalues):

$$
A = \begin{bmatrix}0&-1\\1&0\end{bmatrix}
\\
C_A(\lambda) = \det(\lambda I_2-A) = \begin{bmatrix}\lambda&1\\-1&\lambda\end{bmatrix} = \lambda^2 + 1
$$

Since $\lambda^2 + 1$ means that a = 1, b = 0, c = 1, then $b^2-4ac = 0 - 4 = -4$, and the matrix A has no real roots.

This matrix A is actually the standard matrix of the counter-clockwise rotation by $\pi/2$. Geometrically, this means that this rotation leaves *no direction unchanged*. By intuition then, the eigenvalues represent the scaling that happens to unchanged directions, because it only *scales* the direction, and does not change directions. Not all rotations leaves directions different, for example, rotations which use angles of $pi$ radians will leave directions unchanged.

These are the final steps of finding the *eigenvalues* of a square matrix A:

1) Find characteristic polynomial $C_A(\lambda) = \det(\lambda I_n - A)$

2) Solve characteristic equation $C_A(\lambda) = 0$

3) The real roots of the ch. eq. are then the real eigenvalues of A.

Now to move onto the *eigenspace*, which defines the space in which eigenvectors are.

<aside>
💡 **Eigenspace**

Given A to be $n \times n$, and $\lambda$ to be an eigenvalue of A, then the **eigenspace** $E_\lambda(A)$ of A corresponding to $\lambda$, consists of all solutions to the equation:

$$
(\lambda I_n - A)x = 0
$$

The $E_\lambda(A)$ is equivalent to $N(\lambda I_n - A)$, meaning that the null space of the matrix $\lambda I_n - A$ is the subspace of $\R^n$ that consists of the zero vector, and all eigenvenctors of A that correspond to the eigenvalue $\lambda$.

</aside>

What we learn from this is that there are $\infin$ eigenvectors of A that correspond to the same eigenvalue, so the eigenspace of A is a nontrivial subspace, which is defined by its basis of eigenvectors that correspond to $\lambda$.

In an example, we see that to find the eigenspaces, we obviously must first find the eigenvalues. Once we find the characteristic equations based on the eigenmatrix ($\lambda I_n - A$), we can substitute each eigenvalue to find the basis vectors FOR THAT SPECIFIC EIGENSPACE.

→ ie. if we find the matrix A has eigenvalues for $\lambda_1 = 2, \lambda_2 =-3$, then there are two eigenspaces, one for each eigenvalue. To find each eigenspace, we substitute the $\lambda$ in the matrix, and solve for the homogenous system made by $(\lambda I_n - A)[x_1\quad x_2]^T = 0$. This solving is done by finding the RREF. The basis vectors for the eigenspace are given by the vector generated by the general solution.

<aside>
💡 [3Blue1Brown video on Eigen-stuff](https://www.youtube.com/watch?v=PFDu9oVAE-g&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=14&ab_channel=3Blue1Brown)

Essentially, these *eigenvectors* are the vectors at which a transformation described by the matrix A do not change their *span*, but are only dilated or squished by a factor. They remain on the *same direction* as they were *before the transformation*, but are just scaled. This is why we are looking for $Av = \lambda v$, because transforming this eigenvector *v*, does nothing but scale it. Scaling it does not change its *span,* because it is along the same direction. And this eigenvalue that it is scaled by is specific to this eigenvector, and the space of which it spans as well.

This is also why the Null Space of the transformation is equivalent to the eigenspace it creates, because the null-space represents the dimension of space that gets reduced to *null* (the origin) as it transforms, and these eigenvectors do not get translated to other points in space, other than on their own span. These are the eigenvalues at which changing the basis vectors with these values, will cause the determinant to converge to 0.

3B1B also touches on the *eigenbasis* or the *eigenspace*. Essentially, the point of having an eigenbasis, is so that we can work with *diagonal matrices*, because they are very easy on computations; for example, taking the 100th power of a non-diagonal matrix is really difficult, because there is no formula like multiplying each entry by itself 100 times. This is opposite in diagonal matrices, in which the 100th power of the matrix is equivalent to taking the 100th power of each entry. Eigenspaces and bases are a way for us to *translate* transformations in such a way that the basis never changes its span, because it only stretches.

Not all transformation matrices can be diagonalized however, because some transformations leave no eigenvectors to form a basis. Take the rotation for example, every single span is changed, unless we rotate by certain $\theta$ for example, in-which the spans of some vectors don't change.

</aside>

Eigenvalues and Spaces work with operations on matrices as well:

<aside>
💡 Let A and B be squares of n, and that *v* is an eigenvector of BOTH A and B, with values $\lambda_A$ and $\lambda_B$, then:

a) *v* is an eigenvector of $A+B$, with eigenvalue $\lambda_A+\lambda_B$.

b) *v* is an eigenvector of $AB$, with eigenvalue $\lambda_A\lambda_B$.

c) *v* is an eigenvector of $cA$, with eigenvalue $c\lambda_A$.

</aside>

When we deal with operations on a single matrix A, the results of operations have stronger implications for the eigenvector, such as:

<aside>
💡 Matrix A is of order n, and $\lambda$ is an eigenvalue of A, with *v* being an eigenvector that corresponds to that eigenvalue:

a) for $k > 0$, $\lambda^k$ is an eigenvalue of $A^k$, and *v* is an eigenvector of that $A^k$ with the same eigenvalue

b) if A is invertible, then $\lambda^{-1}$ is an eigenvalue of $A^{-1}$, *v* is an eigenvector of that $A^{-1}$ with the same eigenvalue

</aside>

# 7.2 Diagonalizability

Given a square of n called A, which is a matrix that corresponds to scaling along directions of vectors in a basis, $\{v_1, v_2,...,v_n\}$. Then there are *n* real numbers (eigenvalues) $\lambda_1, \lambda_2, ..., \lambda_n$ such that:

$$
Av_1 = \lambda_1v_1\\Av_2 = \lambda_2v_2\\...
$$

Meaning that the basis is the *eigenvectors* of A, associated by eigenvalues $\lambda$. If we let P equal a matrix that is formed by this eigenbasis, then P is invertible (because it is a basis). So, we can transform the basis by the matrix A, which looks like: $AP = A[v_1\quad v_2 ...\quad v_n] = [Av_1\quad Av_2 ...] = [\lambda_1v_1\quad\lambda_2v_2...]$. All in all, this is what an example of that matrix would look like, it's a diagonal matrix, whose main diagonal entries are formed by the eigenvalues for each $v_i$.

Because P is invertible, because it's a matrix formed by a basis, we can multiply $AP = P[\lambda]$ by $P^{-1} \rarr P^{-1}AP = [\lambda]$. This is an example of cancellation using invertible matrices, and is a way for us to extract a diagonal matrix. Diagonal matrices are really important in many things, and we can define some more things about this process.

<aside>
💡 Similar Matrices

Given A and B to be square matrices, A is **similar** to B if there's an invertible matrix P of the same size, such that $P^{-1}AP = B$

</aside>

This is what we saw in the 3rd chapter about invertible matrices, how two matrices A and B may not be *equal*, but are *similar* because in essence, we are translating or changing bases using P and its inverse, to translate a matrix A into a different basis.

![Untitled](Eigenvalues,%20Eigenvectors,%20Diagonalization%202a38f62882ba4650843060706592e440/Untitled.png)

![Untitled](Eigenvalues,%20Eigenvectors,%20Diagonalization%202a38f62882ba4650843060706592e440/Untitled%201.png)

<aside>
💡 Diagonalizable Matrix

an n * n matrix A is **diagonalizable** if it is *similar* to a diagonal matrix, meaning that an invertible P can relate A to a diagonal matrix, $P^{-1}AP = D$. The matrix P diagonalizes A, and the the column vectors of P are an *ordered basis* that diagonalizes A.

</aside>

Similar to what's been brought up previously, we cannot diagonalize all matrices, there must be a basis of eigenvectors of A:

<aside>
💡 A matrix A of order n is diagonalizable if and ONLY if $\R^n$ has a *basis of eigenvectors* of A. This means that a basis must exist that spans $\R^n$ made entirely of A's eigenvectors.

</aside>

The 3B1B video touches on this exactly. This diagonalization is exactly what is meant by a change of basis. Intuitively, a matrix A can be interpreted as a *matrix transformation* that alters the basis vectors of the space. The transformation of these bases changes the span of vectors, unless they are eigenvectors of the transformation. So, the whole point of doing this dance of multiplying by the inverse of an eigenbasis, is to diagonalize the transformation in a change of basis, so that we can change the coordinate system to be in the perspective of only a *scaling of bases.*

In order to start understanding existence theorems, or the properties of matrices that do or don't make them diagonalizable, we need this:

<aside>
💡 Given A to be (n*n), and that $\lambda_1 , \lambda_2$ are distinct eigenvalues of A, with $v_1, v_2$ being their corresponding eigenvectors. If this is the case, then $v_1$ and $v_2$ are *linearly independent*.

In fact, given that all eigenvalues are distinct, and there exists respective eigenvectors of A, then the set of eigenvectors is linearly independent.

</aside>

This should make sense intuitively, because eigenvectors, are by definition, linearly independent because they are chosen because of their span. Any proportional vectors to an eigenvector are captured in its span, combined with the eigenvalue. Think of it as finding an eigenvectors finds the most minimal vector that spans that line. Sure, we can say the vector [100, 100] is an eigenvector, but the minimal vector [1,1] captures [100,100] in its span.

Let's go to a more direct theorem:

<aside>
💡 Any $n \times n$ matrix A with $n$ distinct eigenvalues is diagonalizable.

</aside>

This is proven simply by understanding that a basis must have *n* vectors that make up the spanning set, and all *n* vectors must be linearly independent. It is then guaranteed that matrix A with *n* eigenvalues would have *n* eigenvectors that make up the full spanning set for $\R^n$.

Given a triangular matrix, or even a diagonal one, we can know just from the main diagonal entries whether it is diagonalizable or not, because its eigenvalues are the main diagonal entries themselves. IF the matrix has *n* distinct diagonal entries, then it is diagonalizable.

<aside>
💡 Factor Theorem (Lemma)

A real number *a* is a root of the real polynomial p(x) of degree *n*, if and only if (x - a) is a factor of p(x):

$$
p(x) = (x-a)q(x)
$$

where q(x) is a real poly. of degree (n-1). If $p(x) = (x-a)^rq(x)$, then *a* is a root of multiplicity.

</aside>

<aside>
💡 Thoerem, at most n distinct distinct real roots

Any real polynomial of degree *n* can have AT MOST *n* distinct real roots. Because of the fact that eigenvalues are the roots of the determinant of the polynomial of degree *n* ($C_a(\lambda)$), then A has AT MOST n distinct real eigenvalues.

</aside>

Using this theorem, in order to find whether or not a matrix is diagonalizable we need to compute the factors of its characteristic equation $C_A(\lambda) = 0$

If the matrix A has *n* distinct real roots (no repeats, etc.) then A is diagonalizable.

<aside>
💡 **Geometrical Multiplicity**

Given $\lambda$ to be an eigenvalue of an $n \times n$ matrix A. The **geometric multiplicity** $g_\lambda(A)$ of the eigenvalue, is the *dimension* of the corresponding eigenspace $E_\lambda(A)$:

$$
g_\lambda(A) = \dim(E_\lambda(A))
$$

</aside>

An important idea about the eigensets of a matrix is that it may have multiple eigenspaces, because it has multiple eigenvectors. An also important note to jot down is that the geometric multiplicity is equivalent to the null-space of this eigenspace. $\dim(N(E_\lambda(A)) =n - rank(E_\lambda(A)) = g_\lambda(A)$

<aside>
💡 Given that $\beta_i$ is a basis for the eigenspace $E_{\lambda_i}(A)$, then the union of all eigenbases is also a linearly independent set in $\R^n$:

$$
\beta = \beta_1 ∪ \beta_2 ∪ ... ∪\beta_r
$$

</aside>

This small factoid about the geometric multiplicity, that a super-basis can be formed by the union all of eigenbases brings us to the next point, that

<aside>
💡 Any n * n matrix A is *diagonalizable* if and only if the sum of the **geometric multiplicities** of its distinct eigenvalues equals *n*.

</aside>

Because the geo. multiplicity of a matrix depends on the eigenvalue, and we know that there are multiple bases formed by the multiple number of eigenvalues and eigenvectors, then because a matrix can have at most *n* distinct real eigenvalues, the sum of vectors within each eigenbasis should equal *n.*

In order to talk about the last criteria (and more detailed) of diagonalizability, we need to understand that any *real* polynomial $p(x)$ of degree *n*, can be factorized into a product of linear quadratic factors:

$$
p(x) = c(x-a_1)^{r_1}...(x-a_k)^{r_k}(x^2+b_1x+c_1)^{s_1}...(x^2+b_mx+c_m)^{s_m}
$$

Where $a_1, ..., a_k$ are the *distinct* real roots of p(x), with real coefficients, and any quadratic polynomial $x^2+b_jx +c_j$ has no real roots about it.

We know that $r_1+...+r_k+2s_1+...2s_m=n$.

<aside>
💡 Split over $\R$

Polynomials with coefficients in $\R$ **split over** the space $\R$ if it is a product of linear factors with coefficients in $\R$, meaning that **no quadratic factors are present**:

$$
p(x) = c(x-a_1)^{r_1}(x-a_2)^{r_2}...(x-a_k)^{r_k}
$$

</aside>

Essentially, the only factors we have present are linear factors in which each $a_i$ is a real root.

<aside>
💡 Algebraic Multiplicity

Given $\lambda$ to be an eigenvalue of an n*n matrix A, the **algebraic multiplicity** of $\lambda$, as $m_\lambda(A)$ is the *largest positive integer k* for which

$$
(x-\lambda)^k
$$

is a factor of the characteristic poly. $C_A(x)$  of A.

</aside>

Essentially, the highest degree of a root. Previously defined as a root of multiplicity, it is the root of multiplicity with the highest degree.

<aside>
💡 Given A to be a square matrix, with $\lambda$ being an eigenvalue of A. The *geometric multiplicity* of A is AT LEAST 1, and CANNOT EXCEED the algebraic multiplicity.

$$
1 \le g_\lambda(A) \le m_\lambda(A)
$$

</aside>

Thinking about this, the geo. multiplicity defines the number of vectors within the eigenbasis at that eigenvalue. If A has an eigenvalue, then it is true that it has at least 1 eigenvector associated with the value. This makes a lot of sense when you consider that a diagonalizable matrix should have at most *n* distinct eigenvalues, and that the sum of geo. multiplicies should sum of to the order of the matrix itself. 

<aside>
💡 Theorem

Given A being an n*n matrix, then A is *diagonalizable* if and only if the following are true:

a) the characteristic polynomial $C_A(A)$ *splits over $\R$*

b) for any eigenvalue of A, the geometric multiplicity and algebraic multiplity coincide st. $m_\lambda(A) = g_\lambda(A)$ for ALL eigenvalues of A.

</aside>

This being said, there are no factors of A's polynomial that have no real roots ($x^2 + 1$ for example), and the number of eigenvectors in each eigenbasis matches to that root (eigenvalue's) multiplicity in the characteristic polynomial.

Criteria of Diagonalizability:

1) is *similar* to a diagonal matrix ($P^{-1}AP = D$), meaning that matrix A is similar to a diagonal matrix D.

2) has *n* DISTINCT eigenvalues

3) with each eigenbasis spanning $\R^n$

4) has *n* distinct roots

5) the sum of geometric multiplicities across all eigenspaces sums up to the order of A (*n*)

<aside>
💡 Symmetrical Matrices are always diagonalizable

</aside>

# 7.3 Diagonalization

Algorithm for *diagonalizing* a matrix A that is square. Part of this process is testing whether or not it is diagonalizable in certain parts, to know when to continue, since not all matrices are able to be diag'd.

<aside>
💡 Diagonalization:

1) Find Eigenvalues of A:

a) Find char. polynomial $C_A(\lambda)$

b) Does $C_A(\lambda)$ split over $\R$? If it does not, STOP.

c) Label distinct roots of $C_A(\lambda)$ as distinct eigenve values of A, and record each $\lambda$'s degrees (algebraic multiplicity)

2) Find EigenSpaces of A:

a) For each distinct eigenvalue $\lambda_j$ of A, solve the homo. system $(\lambda_jI - A)x = 0$ to find the *basis* for the corresponding eigenspace $E_{\lambda_j}(A)$

b) If the geometric multiplicity (number of vectors in $E_{\lambda_j}$) is LESS THAN the algebraic mult., STOP. OTHERWISE, if ALL geometric multiplicities coincide with their respective eigenvalues, we can diagonalize.

3) Write the diagonalizing matrix, and the corresponding diagonalization of A:

a) Construct square matrix P which is formed by *all basis vectors* of eigenspaces $E_{\lambda_j}$ for all eigenvalues of A. P is then invertible and a basis. Repetition is allowed for eigenvalues of > 1 multiplicity.

b) Construct (n*n) diagonal matrix D by writing eigenvalues on the main diagonal, in the order of eigenspaces respective to the columns of P.

</aside>

The invertible matrix P diagonalizes A, since $P^{-1}AP = D$.

Diagonalizing matrices are not unique, since the matrix still continues to be diagonal with different arrangements of P's columns.

An important property about diagonal matrices, is that they are very simple to compute powers of A on, because we have this fact:

<aside>
💡 Let A be an n*n diagonalizable matrix, and P be its diagonalizing matrix, so $P^{-1}AP = D$ is a diagonal matrix. For any *positive* integer *k*,

$$
A^k = PD^kP^{-1}
$$

</aside>

This also holds for all k which are non-zero, if A is invertible.

The important thing here is that when we want the *k-th* power of A, we simply apply that power to all entries of the diagonal matrix D.

$textbook\; over\quad\blacksquare$