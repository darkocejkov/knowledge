# Problem Walkthroughs & Breakdowns

- **Determinants**
    
    Given a matrix, the cofactor expansion is 
    
- **Subspaces and Basis**
    
    <aside>
    💡 Find the basis of the column space $col(A)$ from the column vectors of a matrix A:
    
    1) Reduce A to RREF/REF, to find the pivot columns
    
    *Not necessary to reduce in REF, because you can tell which columns are pivots from the REF, they are the same.
    
    2) Note down the pivot COLUMN indexes (1, 2, ... etc)
    
    3) in the original matrix A, take the original column values of each pivot column index (ie. take the i-th column from A, that is a vector in the basis)
    
    </aside>
    
    <aside>
    💡 Determine if a subset of $\R^n$ is a basis of $\R^n$.
    
    1) Does the subset have $n$ vectors? (dim(S))
    
    - if it does not, then it can not span $\R^n$, and is not a basis for it.
    
    2) If it does, do the *n* vectors form a linearly independent set?
    
    - Use row reduction to solve the *homogenous linear system.* If the rank does not equal the number of columns (n), then the set is linearly dependent.
    - In other words, if there is a free variable, then that means there is a non-trivial solution to the linear combination of the vectors equal to the zero-vector, and it is linearly **dependent**.
    </aside>
    
    <aside>
    💡 Given a subspace V of $\R^n$, in the form of a standard equation, show that a subset S of $\R^n$ is a basis:
    
    1) Do the vectors in the subset S also appear in the subspace V?
    
    - show this by using the standard equation condition (ex. $x_1 + x_2+x_4 = 0$) and test each of the vectors of S to appear in the subspace V.
        - if one of the vectors is not in the subspace, then it cannot form a basis for that subspace (because it must also be in the span of the subspace).
    
    2) Is the set S linearly independent? 
    
    - show this by doing row reduction (gauss-jordan) to find the RANK. If the rank(S) = # columns, then it is linearly independent, otherwise a set cannot form a basis if it not linearly independent.
    
    0) Convert the standard equation $x_1+x_2+x_4=0$ into a vector form. 
    
    - We can find a basis from the definition of the subspace using this vector form, and can verify that we need that many vectors in the set S to form a basis. We know the set we found linear independence on will be a basis of V because any vectors in V that are linearly independent, will form a basis for V.
    </aside>
    
    <aside>
    💡 Find the *dimension* of a subspace in $\R^n$
    
    * the Dimension of a subspace is equal to the number of vectors that is needed for it to be a basis, so it's the number of vectors in the basis of the subspace.
    
    Given a set of vectors that spans a subspace, we want to find the dimension of it, but we don't know if it is a basis or not, so we can easily just apply row reduction on the equivalent matrix of spanning vectors, and find the rank. Because the rank positions (leading 1's) tells us which columns/vectors of the spanning set are part of the basis, then the rank is the dimension.
    
    </aside>
    
    <aside>
    💡 Find the *ordered coordinates* of vectors in $\R^n$ with respect to an ordered basis for a subspace
    
    1) Created the augmented matrix $[A|w]$ where A is the vectors of the ordered basis, and *w* is the vector to "translate"
    
    2) Find the RREF of the matrix $[B|v]$, where B is in rank = dim(subspace), and the translated vector *w* is now *v*.
    
    $[w]_\beta = v$
    
    GOTCHA: When we translate this vector *w*, in the RREF, we only consider the values of *v* that are in non-zero rows (ie, rows that have pivots).
    
    LIFEHACK: this solution represents finding the linear combination of the vectors of the ordered basis to create that vector. Essentially, we are finding the combination of basis vectors that would create the vector we want. SO, if we have simple vectors and simple basis, then we can just visually inspect and determine the $[w]_\beta$, whose entries would be the coefficients of the linear combination.
    
    For example, if we have ordered basis vectors [1,0,0,1] and [0,1,1,0], then the ordered coordinate of [1,1,1,1] would be [**1,1**,0,0], because it equates to 1*[1,0,0,1] + 1*[0,1,1,0] + 0(3rd basis vector) + 0*(4th basis vector)
    
    </aside>
    
    <aside>
    💡 Find a vector's ordered coordinates when given the basis vectors and a set of respective coordinates for vectors within the subspace
    
    For example, given $[u]_\beta, [v]_\beta, [w]_\beta$, we can find a vector $[x]_\beta$ knowing the relationship it has with u, v, and w.
    
    - If $x = u-2v + 3w$ for example, then we know that addition is closed under the subspace and its vectors, so $[x]_\beta = [u]_\beta-2[v]_\beta+3[w]_\beta$, which is an easy calculation.
    </aside>
    
    <aside>
    💡 Determine if a set of vectors is an i) orthogonal basis and ii) an orthonormal basis
    
    First, for a set of vectors to be a *basis* in the first place, it must have *full rank* (rank = #columns) and the set must be linearly INDEPENDENT. Once those are verified, we know we have a *basis*. But is it orthogonal and orthonormal?
    
    i) for a basis to be **orthogonal**, each pair of vectors must be orthogonal (meaning that the dot-product between pairs is ZERO (0)). This is the easest way to test this, just dot each pair. If one pair is not orthogonal, then its not an orthogonal basis.
    
    ii) for a basis to be **orthonormal**, it must be orthogonal, so if it is not, its not orthonormal. the "normal" part means that every vector in the set must be a *unit vector*, meaning that its length/magnitude/norm must be ONE (1). 
    
    $||v|| = \sqrt{v_1^2+v_2^2+...+v_n^2} = 1$.
    
    </aside>
    
- **Linear Transformations, Row Spaces, and Null Spaces**
    
    <aside>
    💡 Find the basis for $row(A)$, Find the basis for col(A)
    
    Given a matrix A, the row-space of A is the subspace that is spanned by the rows of A, and if we use elementary row-operations on a matrix A, to obtain B, the row spaces of A and B are THE SAME. Meaning, that all we need to do to find a basis for any matrices' row(A), we row reduce into RREF, and use the NON-ZERO rows and vectors of the basis.
    
    The column space, is however related to the pivot columns (the index-values of the pivot columns related to the original array), so we just take the index of columns that have pivot elements (leading 1's), and take the column's entries from the original array A, which forms the basis of the column space of A.
    
    The rank of A is identical to the number of leading 1's in the RREF(A), which $rank(A) = \dim(row(A)) = \dim(col(A))$
    
    Find a basis for row(A) that consists of *some* row vectors of A. 
    
    → This means that we want to express the basis of row(A) using the row vectors of A, exactly how it is is done with the column space col(A). This means that we would want to find the *column space* of the transpose of A, $A^T$; then using the indexes of the pivot columns, take those columns from $A^T$ and that would use rows from A to form the basis of row(A).
    
    → HOWEVER, instead of performing RREF on the tranpose of A, we can just take the non-zero rows as row-indexes from the original array A to find the basis.
    
    </aside>
    
    <aside>
    💡 Find the basis of the null-space $N(A)$.
    
    Given the matrix A, find the null-space by:
    
    1) find RREF(A)
    
    2) the null-space is the general solution to the HOMOGENOUS linear system of the RREF(A), so we equate all non-zero rows to 0, and find the relation between each $x_i$, setting free variables as parameters. The resulting general vector solution is the basis for the basis of the nullspace of A (N(A)).
    
    The nullity is the number of vectors in the basis for N(A). We can verify this by knowing that $nullity(A) +rank(A) = n$.
    
    </aside>
    
    <aside>
    ⭐ Determine whether a vector is part of a space of the linear system
    
    Given a linear system as a matrix, we might need to evaluate whether a vector is part of the *column space, row space,* or*, null space*.
    
    Col(A) → Find the RREF of the augmented matrix, including the vector we want to test. If the system maintains a consistent solution, then it exists in the column space of the matrix.
    
    Null(A) → Find $Ax$, and if $Ax = 0$, then the matrix exists in the null space.
    
    → If A has no null space (ie. the only vector in the null-space is the *zero vector*), then it is invertible.
    
    </aside>
    
    <aside>
    ⭐ Determine the *n* of the $\R^n$ of a subspace of a matrix
    
    Null(A) is a subspace of $\R^n$, where *n* is the number of *columns*
    
    Col(A) is a subspace of $\R^n$, where *n* is the number of *rows*
    
    Row(A) is a subspace of $\R^n$, where *n* is the number of *columns*
    
    </aside>
    
    <aside>
    💡 Show that a function L that is defined by $L(x,y,z) = (x-3y, y-2x, x+y+x, -5z)$ is a matrix transformation.
    
    In order to determine if this function is a matrix transformation, we need to find its **standard matrix**, which is essentially like pulling out each component of x,y, and z in the vector on the RHS of the function. To do this, look at each entry, and extract the [x] matrix, [y] matrix, and [z] matrix which take entries from the RHS if they contribute to that entry. Once we have the vectors, we can put them into a matrix called the **standard matrix,** represented as $[L]$. 
    
    To show that this function is a matrix transformation, we need to show that when we multiply (on the left) the standard matrix by the input vector specificed by $L(x,y,z)$, that we get back the vector with entries on the RHS of the function.
    
    **ALTERNATIVELY**, if we need to show that some transformation is a **matrix** transformation or a **linear** transformation, we need to show that it follows these two rules:
    
    1) closed under addition
    
    $T_A(u+v)=T_A(u)+T_A(v)$
    
    2) closed under scalar multiple
    
    $T_A(cu) = cT_A(u)$
    
    The way to do this, is to take two vectors $u,v \in \R^n$, show that the addition of each of their transformations is equal to the transformation of their sum. Same thing with the scalar multiple.
    
    </aside>
    
    <aside>
    💡 Find the standard matrix of linear operators
    
    Linear operators are transformations which are entirely linear, meaning they do not change the dimension of the space, such as going from $\R^3 \rarr \R^2$, do operate entirely such that $\R^n \rarr \R^n$.
    
    These are the types of linear operators:
    
    - Scale
        
        ![Untitled](Problem%20Walkthroughs%20&%20Breakdowns%20a245e840d97943dc8650ca696be62cbc/Untitled.png)
        
        - Dilate = stretch, value ≥ 1
        - Compress/Contraction = squish, 0 < value < 1
        
        $$
        \begin{bmatrix}\lambda_i&0\\0&\lambda_j\end{bmatrix}
        $$
        
        - Scalings for which $\lambda_k$ is the same for all, then it is called an *isotropic* scaling. Otherwise, it is non-isotropic.
    - Shear
        
        ![Untitled](Problem%20Walkthroughs%20&%20Breakdowns%20a245e840d97943dc8650ca696be62cbc/Untitled%201.png)
        
        - Fix one vector in place, scaling the other
        
        $$
        [H_x]=\begin{bmatrix}1&\lambda_i\\0&1\end{bmatrix}, [H_y]=\begin{bmatrix}1&0\\\lambda_i&1\end{bmatrix}
        $$
        
        Where $H_x$ represents a shear in the *x-direction* or the $e_1$ basis, while $H_y$ is a shear in the y-direction, or $e_2$ basis.
        
    - Orthogonal Projection
        - It is the projection of one vector onto another, such that the projection is in the same direction as the subspace we are projecting onto.
        
        $$
        [proj_w] = \frac{1}{||w||^2}\begin{bmatrix}w_1\\w_2\end{bmatrix}\begin{bmatrix}w_1&w_2\end{bmatrix}
        $$
        
        - The vector *w* is the vector we want to PROJECT ONTO. This is also not limited to $\R^2$.
        - The projection onto a plane uses the previous result:
        
        $$
        [proj_\pi] = I_3 - [proj_n]
        $$
        
        → where $proj_n$ is the standard matrix of projection onto the NORMAL of the plane $\pi$.
        
    - Reflection
        
        ![Untitled](Problem%20Walkthroughs%20&%20Breakdowns%20a245e840d97943dc8650ca696be62cbc/Untitled%202.png)
        
        - Is a unique type of projection, we project onto the normal of the line we want to reflect over, because that's the distance from the point to the line, and subtract 2 times that to reflect to the other side of the line.
        
        $$
        [refl_n] = \begin{bmatrix}1&0\\0&1\end{bmatrix}-\frac{2}{||n||^2}\begin{bmatrix}n_1\\n_2\end{bmatrix}\begin{bmatrix}n_1&n_2\end{bmatrix}
        $$
        
    - Rotation
        - Given an angle $\theta$, we want to rotate every vector by that angle.
        - This standard matrix rotates COUNTERCLOCKWISE, so a positive angle means we are rotating counterclockwise, while a negative angle rotates CLOCKWISE.
        
        $$
        [R_\theta] = \begin{bmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{bmatrix}
        $$
        
        → rotating *about an axis* or *line* means that we fix that position in the standard matrix
        
    </aside>
    
    <aside>
    💡 Applying Matrix/Linear Transformations
    
    Given a transformation's STANDARD MATRIX, we can compute the transformation of any vector with it using *matrix product*. If $[T_A]$ represents any transformation's standard matrix, then for any vector *v* in the appropriate dimension of the transformation:
    
    $$
    [T_A]v
    $$
    
    → we multiply the transformation matrix on the LEFT of the vector/matrix.
    
    If we are to apply *multiple* transformations to a vector, it's easiest to find the standard matrix of the COMPOSITION of the transformation. This means that we want to apply the transformations to *each other* using matrix product. For example, if we are to apply FIRST $T_A$, THEN $T_B$, then $T_C$ to any vector *v*, we could do it both ways:
    
    1) $T_C(T_B(T_A(v)))$
    
    2) $T_{CBA}(v)$
    
    Because we are applying first the transformation A to *v*, then B, then C. OR, we can calculate the matrix $CBA$ first, then apply that conglomerate transformation
    
    </aside>
    
- **Polynomials, Eigenvectors, Eigenvalues**
    
    [https://www.emathhelp.net/en/calculators/linear-algebra/](https://www.emathhelp.net/en/calculators/linear-algebra/)
    
    → [Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/eigenvalue-and-eigenvector-calculator/) This calculator takes in a matrix, and will find all eigenvalues as well as the eigenspaces (WITH STEPS).
    
    <aside>
    💡 Find Eigenvalues of Matrix
    
    Given a square matrix, we need to find the *characteristic polynomial* and *equation* of that matrix, with respect to the $\lambda I_n$.
    
    So, the first step is to subtract A from $\lambda I_n$, and then find the determinant of it: $det(\lambda I_n - A)$. This is really simple for a 2x2 matrix, but for any *n* > 2, we need to use cofactor expansion. Choose the easiest row, which would have the least cofactors involved in it. For example, if a row was [1,0,0] then the determinant of a matrix with this row would equal $1*C_{i1}$, in which the cofactor is the DETERMINANT of the submatrix without row *i* or column 1.
    
    Once we have the characteristic polynomial in terms of the variable $\lambda$, then we need to find the *roots* of this polynomial.
    
    → To find the roots, we use different methods depending on the values of the coefficients and the degree of the polynomial. For example, a polynomial with degree 2 would look like: $a\lambda^2+b\lambda+c$, so we can either factor such that $(\lambda+d)(\lambda+e)$, and then each root would be a solution to the equations $(\lambda+d)=0$ and $(\lambda + e) = 0$. If we have a quadratic that does not factor easily, we can use the quadratic equation. If we have a cubic polynomial, we can long-divide to find the first factor, and then we have $(\lambda+f)(\lambda^2+\lambda+g)$, and then we can find the factors of the quadratic easier.
    
    The ROOTS to this polynomial are the values of the Eigenvalues of the initial matrix A.
    
    HOWEVER, if we have a matrix A that is *triangular* in any way (upper, lower, diagonal), then we don't need to find the polynomial, because the determinant comes from the entries of the main diagonal, so the roots of triangular matrices are $(\lambda-a)(\lambda-b)(\lambda-c)$ for example, with $a,b,c$ being the main diagonal entries, so the roots are the entries of the main diagonal themselves.
    
    </aside>
    
    <aside>
    💡 Find the Eigenspace(s) of a matrix
    
    Given any square matrix, if we are trying to find the eigenspaces of that matrix, we first need to know what its *eigenvalues* are. This is because eigenspaces are *specific to each eigenvalue*, meaning if there are *m* eigenvalues, then there are *m* eigenspaces. 
    
    The way to find each eigenspace $E_\lambda$, we substitute each $\lambda$ value into the matrix $\lambda I_n - A$. Then, we want to solve the linear system $(\lambda I_n - A)x= 0$. To do this, we just reduce the matrix $\lambda I_n - A$ into RREF, and find the *general solution.* This general solution will for a basis for the null-space of the transformation, and is the same as the eigenspace for the eigenvalue. We do this for each eigen value.
    
    </aside>
    
    <aside>
    ⭐ Find if a matrix A is diagonalizable, and find its diagonal matrix
    
    We need to use Eigenvalues and Eigenvectors here. To verify whether a matrix A is diagonalizable, there are some *criteria* A needs to fulfill, in terms of its characteristic polynomial.
    
    Does the $C_A(\lambda)$ *split over $\R$?* This means that there are no factors of lambda > 1 for which we cannot reduce. For example, $\lambda^2 + 1$.
    
    1) Calculate characteristic polynomial, with eigenvalue factors.
    
    a) Save each eigenvalue's *algebraic multiplicity* ex. $(\lambda - a)^c(\lambda +b)^d$. This means that for eigen value (a), we have multiplicity *c*, and vice versa.
    
    2) Find each eigen-value's *eigenspace.* Take note of each eigenspace's *dimension (number of vectors*).
    
    </aside>