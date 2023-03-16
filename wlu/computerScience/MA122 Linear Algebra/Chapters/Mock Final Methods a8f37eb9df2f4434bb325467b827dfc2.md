# Mock Final Methods

1)  True or False

A) A set S containing four non-zero vectors from $\R^3$ must be linearly independent

FALSE. The maximal amount of vectors that spans $\R^3$ is 3. Since S has 4 > 3 vectors, it doesn't guarantee that the vectors are linearly independent.

B) A set S containing four non-zero vectors from $\R^3$ must span $\R^3$

FALSE. See above. 

C) If A is an (m x n) matrix, then the dimension of its *column space* is equal to the dimension of its rowspace

~~FALSE. Column space is equivalent to the dimension of rows, while Row Space is equivalent to columns. Since it has m ≠ n, then they cannot be equal.~~

**TRUE. This is because both the column and row-spaces of any matrix are both equal to the *rank* of the matrix.** If we think about it, this is because when we have a matrix A in RREF, then it's *leading 1's* or *pivots* are defined as the first entries in each row, where there are no other entries above or below a pivot. Because of this definition, the intuition here is that the pivots relate to the *maximal* number of linearly independent vectors formed by the *columns* of the matrix, and is we have a (3 x 4) matrix for example, we can have a maximum of rank 3, because it's 1 pivot per row.

The column space basis is the vectors from the original matrix, based on the *pivot columns*, whilst the row space basis is any non-zero row in the RREF(A). So, if A (3 x 4) has rank 3, that means that the 1 column/variable will be free, while the basis of the column space has 3 vectors (dim(col(A)) = 3), and because each row has a pivot, it is not empty, so dim(row(A)) = 3. 

The differences between the row-space and the column-space are the $\R^n$ that the vectors are in. Column space is in the subspace $\R^{\#rows}$ while Row Space is in the subspace of $\R^{\#columns}$

D) If matrix transformation L is represented by a (3 * 4) matrix A, then the range of L is comprised of vectors from $\R^4$

FALSE. The range of L must be in $\R^3$, since Ax requires a vector *x* to be in $\R^4$, and it transforms into $\R^3$.

E) If det(A) = 0 for a square matrix A, then nullity(A) > 0

TRUE. Since the determinant of A is 0, then it is NOT full rank, meaning that rank(A) ≠ n. Thus, nullity(A) + rank(A) = n means that nullity(A) > 0.

F) A (4 x 4) matrix is diagonalizable if it has four distinct eigenvalues.

TRUE. This rule is a "bypass" to the criteria of diagonalizability. If a matrix A has *n* distinct eigenvalues, then it is automatically diagonalizable. However, not all diagonalizable matrices have *n* distinct eigenvalues, so we cannot say that all diagonaliazable matrices have n eigenvalues.

G) All triangular matrices are diagonalizable.

FALSE. Despite triangular matrices having their eigenvalues as their main-diagonal entries, the fact that they are triangular does not guarantee that they will split over $\R$, or have *n* distinct eigenvalues, or the algebraic and geometric multiplicities.

H) If A is a square matrix with *two distinct* eigenvalues, then $A^4$ will also have two distinct eigenvalues.

TRUE. Because eigenvalues have the property that $\lambda^k$  is an eigenvalue of $A^k$, and since both eigenvalues are distinct, their k-th power will keep them distinct.