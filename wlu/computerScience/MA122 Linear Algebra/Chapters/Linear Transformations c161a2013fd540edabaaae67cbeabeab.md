# Linear Transformations

# 6.1 Matrix Transformations

Chapter 1 looked at the geometry of linear algebra, and how we can add, and scale vectors and shapes in $\R^n$. In this chapter, we apply this line of thinking to matrix multiplication and interpreting it as operating on matrices using linear geometries in spaces.

<aside>
💡 **Matrix Transformation**

Given that A is an $m\times n$ matrix, then the matrix transformation $T_A: \R^n \rarr \R^m$ is a function from $\R^n$ to $\R^m$, which is determined by a matrix multiplication *by A on the left*.

$$
T_A(x) = Ax
$$

Matrix A is the **standard matrix** of the function $T_A$. This is the general form, and when given a transformation of a matrix as a function $L: \R^n \rarr \R^m$, then the standard matrix here is $[L]$, where $[T_A] = A$.

When  $m = n$, then the function $T_A : \R^n \rarr \R^n$, and is called a **linear operator** on $\R^n$.

</aside>

For example, here are some transformations on the special matrices (zero and identity):

a) $A = 0_{m\times n}$ is the 0-function/transformation, where $0: \R^n \rarr \R^m$ with $0(u) = 0\in \R^m$

b) $A = I_n$ is the *identity function/transformation*, where $I_{\R^n} : \R^n \rarr \R^m$ where $I(u) = u$ 

Because we are *transforming* by a matrix A, we can also write the matrix transformation $T_A$ as a function using *standard coordinates* from the last chapter.

This is a bit hard to follow, so to say this more simply: the matrix transformation above describes the way we can transform ANY matrix using matrix multiplication. The matrix we are using to transform is $A$. Here's a more concrete example of what this means:

<aside>
💡 Example

Find the expression of the matrix transformation $T_A$ as a function, where $A = \begin{bmatrix}2&1&-1\\0&1&1\end{bmatrix}$.

Clearly, A is of size $2\times 3$ ($m\times n$), which means that using A to transform a matrix requires the matrix to be in $\R^3$, and it transforms to $\R^2$. So, if we take an arbitrary vector *x* in $\R^3$ to be $[x_1, x_1, x_3]^T$, then the expression of the matrix transformation looks like:

$$
T_A(x): Ax = \begin{bmatrix}2&1&-1\\0&1&1\end{bmatrix}\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}=\begin{bmatrix}2x_1+x_2-x_3\\x_2+x_3\end{bmatrix}
$$

So, any vector that is transformed by A takes on this form, so lets take some actual values of vectors:

$$
T_A(\begin{bmatrix}1\\1\\1\end{bmatrix}) = \begin{bmatrix}2(1)+(1)-(1)\\1+1\end{bmatrix}=\begin{bmatrix}2\\2\end{bmatrix}
$$

</aside>

This next Lemma is about clarifying the form of the standard matrix, based on the standard basis of any $\R^n$:

<aside>
💡 Given $L: \R^n \rarr \R^m$, and $\{e_1,e_2,...,e_n\}$ is the standard basis for $\R^n$, then the **standard matrix** for L is the $m \times n$ matrix:

$$
[L] = [L(e_1)\quad L(e_2)\quad ...\quad L(e_n)]
$$

</aside>

When asked to find the standard matrix of a function, what is basically being asked is to *extract* each *dimensions* parts from vector combination. Here's an example:

<aside>
💡 Given $L: \R^2 \rarr \R^3$:

$$
L(x)=\begin{bmatrix}3x_1-2x_2\\-x_2\\-x_1+x_2\end{bmatrix}
$$

Then to find the standard matrix of L, we need to compute $L(e_1)$ and $L(e_2)$, which is simply looking into each row and extracint the $x_i$ for the $e_i$ of the standard basis like so:

$$
L(e_1) = \begin{bmatrix}3x_1\\0\\-x_1\end{bmatrix}=\begin{bmatrix}3\\0\\-1\end{bmatrix}
$$

$$
L(e_2) = \begin{bmatrix}-2x_2\\-x_2\\x_2\end{bmatrix}=\begin{bmatrix}-2\\-1\\1\end{bmatrix}
$$

$$
[L] = \begin{bmatrix}3&-2\\0&-1\\-1&1\end{bmatrix}
$$

</aside>

Similar to have in normal functional algebra, if the *range* of the function $f(x)$ is also the *domain* of another function $g(x)$, then a new function can be **composed** using both f and g, called the composition of f with g: $g \circ f = (g\circ f)(x)=g(f(x))$. Matrix transformations can ALSO be composed, and is defined and denoted in the same way.

<aside>
💡 Matrix Transformation Composition

Given that A is $m \times k$, and B is $k \times n$ (they share the A's col and B's rows numbs), then the compositions of $T_A$ and $T_B$ is $T_{AB}$, and is given by the **matrix product $AB$**, such that $T_A \circ T_B = T_{AB}$.

Since $T_A: \R^k \rarr \R^m$ and $T_B: \R^n \rarr \R^k$, then $T_{AB}: \R^n \rarr \R^m$.

</aside>

This is basically the same as saying that we apply the transformation of A to B, then B to any $\R^n$ matrix. An important thing to know here is that composing $T_A$ with $T_B$ is NOT THE SAME as composing $T_B$ with $T_A$. Just like how $AB \ne BA$, the lack of commutativity.

Just like how matrix multiplication has its own properties, matrix transformations do as well when the transformation is defined by an $m \times n$ matrix:

<aside>
💡 The matrix transformation is a **linear transformation**

Given that A is an $m \times n$ matrix, and that $T_A: \R^n \rarr \R^m$, if $c \in \R$ and $u,v \in \R^n$ then:

a) $T_A(u+v) = T_A(u)+T_A(v)$

b) $T_A(cu) = cT_A(u)$

</aside>

Essentially, matrix transformations are just *mappings* of one vector into another, given a **function** that is defined by a matrix. In fact, the two properties of the matrix transformation determine whether or not a transformation is a matrix (or linear) transformation. Any function defined that has these two properties *must be a matrix* transformation, and thus, a linear transformation.

### [Khan Academy Video on Matrix Transformations](https://www.youtube.com/watch?v=4PCktDZJH8E&ab_channel=KhanAcademy)

Matrix transformations actually preserve the concept of the linear combination as well, because if $T_A : \R^n \rarr \R^m$, then the collection of vectors and a collection of coefficients of $\R$, then:

$$
T_A(a_1v_1+a_2v_2+...+a_kv_k) = a_1T_A(v_1)+a_2T_A(v_2)+...+a_kT_A(v_k)
$$

Matrix Transformations preserve subspaces (and their bases), if we include the subspace $V$ of $\R^n$, then the set $T_A(V)$ is a subspace of $\R^m$:

$$
T_A(V) = \{T_A(V): v \in V\}
$$

This being said, this basically means that we can *transform* subspaces using the transform function $T_A$. Clearly, if V is the trivial subspace $\{0_n\}$, then $T_A(V) = \{0_m\}$ (the trivial subspace of *n* transformed to *m*). If V is a non-trivial subspace, represented by its basis $\beta$, then any $v \in V$ is represented as a linear combination of vectors in this basis (as per the definition of a subspace), then its pretty clear that any vector in its transformed set, $T_A(V)$, is represented by a linear combination of the transformed set of vectors $T_A(v_1), T_A(v_2),...$

This transformed set of vectors forms the span of $T_A(V)$, which is now a subspace of $\R^m$.

If we think about what this means for linear systems and their solution sets, then the linear system $Ax = b$ can be a matrix transformation $T_A$, in which we are basically finding all the vectors *x* in $\R^n$, such that $T_A(x) = b$, which is the collection of vectors in $\R^n$, that are mapped to $b \in \R^m$ by $T_A$.

In terms of a homogenous system, $Ax = 0$, then the set of solutions to the homogenous system is a subspace of $\R^n$.

<aside>
💡 **Nullity & Null Space**

Given an $m \times n$ matrix A, its **null space** $N(A)$ is the *subspace of $\R^n$ consisting of the solutions to the linear system $Ax = 0$;* the homogenous system.

$$
N(A) = \{x \in \R^n:Ax = 0\}
$$

The dimension of a *null space* is the **nullity** of A, $nullity(A) = dim(N(A))$

</aside>

We can also take the null-space and nullity of a matrix transformation function, but in the case of $T_A$, we have that the nullspace of $T_A$ is:

$$
N(T_A) = \{x \in \R^n : T_A(x) = 0\}, \quad nullity(T_A) = dim(N(T_A))
$$

Which means that $N(A) = N(T_A)$, as well as its nullity.

<aside>
💡 **Rank of Matrix Transformation**

Given A to be $m \times n$, the range of $T_A$ is the subspace $\R^m$ such that $R(T_A) = \{T_A(x): x \in \R^n\}$. With the dimension of this range being considered as the *rank of $T_A$, $rank(T_A) = dim(R(T_A))$*

</aside>

<aside>
💡 **Theorem: Range of $T_A$**

The range $R(T_A)$ of the matrix transformation $T_A:\R^n\rarr \R^m$ is the column space of A ($col(A)$), thus, $dim(R(T_A)) = dim(col(A)) = rank(A)$

</aside>

Just like we have the the column space of A, we have the *row space of A* as well, which relates the null space and the column space.

<aside>
💡 **Row Space**

the **row space** $row(A)$ is the subspace of $\R^n$ spanned by the row vectors of A, $row(A) = Span(r_1,r_2,...,r_m)$

</aside>

This is important to know because the row space is *invariant* (unchanged) under any of the elementary row operations we have defined previously.

This is proven in the lemma that given a matrix A, its counterpart matrix B is obtained from A via elementary row operations. The rowspace remains the same between the two. Proving this requires knowing that any of the elementary row operations (switching, scaling, adding by a scaled row) maintain the fact that the row-space of A is not changed because none of the operations change the vectors fundamentally, because we *replace them* with new vectors. And, since each elem. operation is invertible/reversible, then the same assertion holds from B into A.

<aside>
💡 Lemma

Given A to be $m \times n$, and the matrix R is the RREF of A, then the non-zero vectors of R form the *basis* for $row(A)$, and that implies that the dimension of the row space is equal to the rank of A: $dim(row(A)) = rank(A)$

</aside>

<aside>
💡 Theorem

Let A to be an $m \times n$ matrix, and R is any REF of A, then the NON-ZERO vectors form a **basis** for $row(A)$, and this implies $dim(row(A)) = rank(A)$.

</aside>

The *dimension* of a basis is the number of vectors in it. Since a basis is the minimal set that spans a subspace, this dimension should be at most the dimension that it spans in $\R^n$ (n). The rank of a system/set of vectors determines its basis, which determines the dimension of both the row and column space.

Because row and column space are related, it's pretty intuitive that the *dimensions* are the same between them, because a row transposed is a column and vice versa:

<aside>
💡 $dim(row(A)) = dim(col(A^T))$

$dim(col(A)) = dim(row(A^T))$

</aside>

Thus it then follows that the rank of the matrix A is equal to its transpose.

For the homogenous linear system, the number of free variables is calculated by subtracting the total number of variables by the rank of the matrix A. The number of free variables is then the dimension of the null space of A, which is the nullity of A. 

The way [this video](https://www.youtube.com/watch?v=uQhTuRlWMxw&t=5s&ab_channel=3Blue1Brown) explains it is very intuitive, as the free variables in this case are NOT linearly independent, and are part of the span of the basis vectors that are in the column and row spaces.

→ Essentially, the *rank* of a matrix equates to the dimension that the matrix transformation outputs things into, so if a 3x3 matrix has rank two, then its matrix transformations will be 2x2. This is because a matrix transformation stretches the space it is transforming to arrive at different vectors. "Full rank" vectors remain in the same space, while anything less than that will reduce the number of solutions to that transformation. Think of it like we are squishing space from 3D to 2D, then there are many less 3D vectors that will sit in the new *plane* that this matrix transforms, because a plane is a subspace of $\R^3$. 

→ the free variables are linearly dependent, and thus are in the span of the solution basis.

<aside>
💡 Rank Theorem

$$
nullity(A) + rank(A) = n
$$

</aside>

→ this is because N(A) is a subspace of $\R^n$, which has a nullity equal to the non-independent vectors that form the basis of the transformed space, it forms the set of vectors that are *nulled* (turned into the null vector because of the transformation), so adding the dimension of the null space to the dimension of the output matrices will equal the total dimension of the space.

→ for example, if we are transforming 3D $\R^3$ vectors into 2D $\R^2$, then the rank of any transformed A will equal 2, because we "lose" one dimension to the null-space, the *line* of vectors that are nulled that *cannot* be part of the solution of the transformation. So, 1 + 2 = 3, the dimension of $\R^3$.

We can also form the sum and scalar product of transformations themselves, as:

<aside>
💡 Sum of $L, M: \R^n \rarr \R^m$:

$$
(L+M)(v): L(v)+M(v)
$$

</aside>

<aside>
💡 Scalar Product of Transformation

$$
(aL)(v)  = aL(v)
$$

</aside>

<aside>
💡 Transformation identities

$$
T_A+T_B = T_{A+B}\\aT_A=T_{aA}
$$

</aside>

Because matrices can also be invertible (reversible in terms of transformations), then an inverse transformation is:

<aside>
💡 Inverse Transformation of A

Given A to be invertible, then $T_A: \R^n \rarr \R^n$ is invertible by $T_A^{-1}=T_{A^{-1}}$

</aside>

→ This is what an *inverse function* or *transformation* looks like. Because we can transform any matrix *x* by A using $Ax = b$, if A is invertible, then we can *rewind* the transformation that A performs when it transforms *x*.

# 6.2 Linear Operators on $\R^2$ and $\R^3$.

This portion of the chapter is focused on defining the different **types** of transformations within 2D planes and 3D space. Linear operations in any dimension always have these two properties (otherwise they are not linear operations): 1) they keep the origin *fixed* in space and 2) all lines are kept as lines, and all planes are planes, etc. (this is equivalent to saying that the distance and parallelism of the space stay the same between axes).

Linear transformations and operations then scale and shift the positions of the basis of a space, and in fact, are the only things we need to care about, because all other vectors can be calculated from the basis vectors (which determine the span of the subspace they belong to). The standard basis for example, spans the entirety of a space. Think of the standard basis as the axes of the space (x, y, z, ... etc). Any vector or plane in a space is then in respect to this original basis, the standard basis. When the standard basis is used, we can know exactly where vectors or planes span in the space the basis belongs to using a *linear combination* of the basis vectors.

→ this is exactly what the first chapter went on about, how adding two vectors yields a third vector, and is can be represented from the origin.

What about when we *transform* a space or plane? All the vectors in that space are now also transformed, and they are transformed by a finite amount. This is very simple when we know how *much the standard basis* has transformed, because any transformed vector in the transformed span can be rep. by a linear combination of the transformed basis vectors.

## Scalings

<aside>
💡 Standard Basis

$\R^2 : \{e_1, e_2\} =\begin{bmatrix}1&0\\0&1\end{bmatrix}$

$\R^3: \{e_1,e_2,e_3\} = \begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}$

</aside>

<aside>
💡 Scaling

the **scaling operator $\lambda$** scales the basis by a factor, and is a transformation that looks like: $[S]=\begin{bmatrix}\lambda_1 & 0\\0&\lambda_2\end{bmatrix},\quad S: \R^2\rarr \R^2$ 

</aside>

→ In essence, the axis $e_1$ is scaled by $\lambda_1$ and the $e_2$ axis is scaled by $\lambda_2$.

In this image, this is what a circle on the plane would look like when the *x-axis* is scaled by 2.5. The circle is stretched ONLY on the x-axis.

There are different types of scalings, such as a **non-isotropic scaling** because the scaling factors in different directions are not identical. In this image, the x-scaling factor is different than the y-scaling factor. When $\lambda > 1$, those scalings are called **dilations** (because they stretch towards $\infin$, while $\lambda < 1$ are called **contractions** because they stretch towards 0. Likewise, when all scaling factors along all directions are identical, the scalings are called **isotropic**.

![Untitled](Linear%20Transformations%20c161a2013fd540edabaaae67cbeabeab/Untitled.png)

An important note here is that scalings are all *invertible*, so we can rewind the changes of this 2.5 scaling back to 1.0, by dividing by 2.5

## Shears

The *shear* is done with a $k \in \R$, where k ≠ 0. We define the *shear along the standard basis direction $e_1$ as the factor k* in the matrix transformation $H: \R^2 \rarr \R^2$:

$$
[H_1] = \begin{bmatrix}1&k\\0&1\end{bmatrix}
$$

Essentially, what is done with a shear is that we are fixing one basis, and adding a component of that fixed basis into the other basis, giving it a second dimension. $e_1$ stays fixed here, while we give $e_2$ a *k* factor, that adds *k* amounts of $e_1$ into $e_2$. This shearing will basically change all squares in the plane to become parallelograms. This idea is the same along the direction of $e_2$.

$$
[H_2] = \begin{bmatrix}1&0\\k&1\end{bmatrix}
$$

We are basically adding a *k-scaled axis* to the other one.

## Orthogonal Projections

These projections were looked at in a totally different lens, because previously, an orthogonal projection was basically asking the question, how much of the vector *v* is in the direction of *w*? Here, we are re-phrasing it such that the vector *v* is transformed into *w.* so, we are looking for the vector such that $xv = w$. What vector *x* we could multiply with *v* to obtain the matrix *w*? This was calculated through looking at the dot-product between v and w, and the length of *w* as a shearing/scaling factor applied to all elements of w.

OR, transversely said, what the scaling/shearing factors are applied to *w*, that would result in *v*?

$$
proj_w(v) = Av
$$

Where the matrix A is the transforming matrix.

$$
[proj_w] = \frac{1}{||w||^2}\begin{bmatrix}w_1^2&w_1w_2\\w_1w_2&w_2^2\end{bmatrix} = \frac{1}{||w||^2}\begin{bmatrix}w_1\\w_2\end{bmatrix}[w_1\quad w_2] = \frac{1}{||w||^2}ww^T
$$

This equation above is called the *standard matrix of the orthogonal projection onto w,* and can be scaled to any $\R^n$, not just 2D. This is essentially the function or transformation that is applied to any matrix such that v is transformed into *w*.

We can see that in this standard matrix of projection, the product $ww^T$ exists, which means it is always symmetrical as a matrix.

We can also do this for any special vector or matrix, such as the x-axis or y-axis, and it uses the *standard bases*. In essence, any projections onto the axes or bases, basically remove all non-axis elements from those vectors. We could think of it as extracting the contribution of other axes in that vector.

This projection matrix can also apply to a projection onto a plane.

<aside>
💡 Given $\pi$ as a plane in $\R^3$ and it has normal vector $n = [n_1 \quad n_2 \quad n_3]^T$, then the orthogonal projection onto $\pi$  is a matrix transformation whose standard matrix is:

$$
[proj_\pi] = I_3 - [proj_n] = \begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix} - \frac{1}{||n||^2}nn^T
$$

</aside>

To visualize this a little better, think about a 3D vector having contributions from all three bases (x,y,z). To project this vector onto a plane, we have to know at least the normal direction of the plane. We can project this vector onto the normal, and like in the first chapter, subtract from the vector itself to find the portion of the vector that lies on the plane, and not normal to it.

The Identity Matrix is here so that we can subtract the scaling factors of the normal from the identity matrix to *remove* the contribution from the normal vector, and extract the portion of the vector that lies entirely in the plane itself.

We can apply this logic to a *coordinate plane* (xy, xz, yz, etc.) that is formed by the bases of the $\R^3$ space. When we project onto a coordinate plane, we are basically removing the entirety of the basis that is not involved in that coordinate plane. For example, when projecting any [x,y,z] vector onto the [x,y] plane, we are looking for the portion of this generic vector that is IN THE X-Y plane. Since the xy-plane's normal is the z-basis entirely, then we are creating a transformation matrix A that has its z-basis/contribution removed.

$$
[proj_{xy}]=\begin{bmatrix}1&0&0\\0&1&0\\0&0&0\end{bmatrix}
$$

$$
[proj_{xz}]=\begin{bmatrix}1&0&0\\0&0&0\\0&0&1\end{bmatrix}
$$

$$
[proj_{yz}]=\begin{bmatrix}0&0&0\\0&1&0\\0&0&1\end{bmatrix}
$$

So any vector that we want to project onto these coordinates planes loses their non-coordinate plane axis, as it is reduced to 0 in matrix multiplication. Let's stretch this idea further, and say that this coordinate plane itself will be transformed to become any other plane or vector that we project onto, and is entirely the same concept.

## Reflections

Similar to the normal idea of reflections, we need an axis to reflect about. This axis becomes a *mirror* to all other vectors, and reflections about this line are done to each vector. 

To do this, we need to know the line $l$ that goes *through the origin* and its normal vector $n$. 

$$
refl_n(v) = v-2proj_n(v)
$$

This reflection uses the projection of any vector onto that line's normal to find the reflection of that line across/about the line.

Because this method uses the projection idea, we can also create a *standard matrix* for the reflection. Hre is what it looks like for $\R^2$, given a line through the origin and a normal vector $n = [n_1 \quad n_2]$:

$$
[refl_n]=\begin{bmatrix}1&0\\0&1\end{bmatrix} - \frac{2}{||n||^2}\begin{bmatrix}n_1\\n_2\end{bmatrix}[n_1 \quad n_2] = -\frac{1}{n_1^2+n_2^2}\begin{bmatrix}n_1^2-n_2^2&2n_1n_2\\2n_1n_2 &-n_1^2+n_2^2\end{bmatrix}
$$

This is meant as a general formula for any line with a normal, but we can also apply this to the coordinate axes such as x and y. The simplest way to describe them is to just *change the sign of the other coordinate*. If we are reflecting over the x-axis, then the y-axis flips signs, and vice-versa.

From these visualizations, its pretty intuitive that to find the reflection, we basically find it's longest distance away from the plane using the normal of the plane, and then subtract 2 times that distance from the vector's matrix to find the distance it would be on the other side. Subtract 1 of those distances, and the vector is *on the plane*, and subtract another, and that vector is reflected on the opposite side of that plane.

![Untitled](Linear%20Transformations%20c161a2013fd540edabaaae67cbeabeab/Untitled%201.png)

![Untitled](Linear%20Transformations%20c161a2013fd540edabaaae67cbeabeab/Untitled%202.png)

The *standard matrices* for these linear operators are basically finding the matrix that we use to multiply any matrix to apply that operation on it. They use the *identity matrix* to account for each basis and its 1-to-1 contribution to any matrix. Essentially, we are applying the transformation to the basis vectors, and then can use that *standard matrix* in terms of matrix multiplication to apply each transformation to any vector or plane or matrix.

## Rotations

Are transformations in which we move points along *arcs of circles* at centered at the **origin**. They are called *rotation operators*. The rotation operator through the angle $\theta$ is the matrix transformation $R_\theta: \R^2 \rarr \R^2$ has the standard matrix:

$$
[R_\theta] = \begin{bmatrix}\cos\theta &-\sin\theta\\\sin\theta&cos\theta\end{bmatrix}
$$

This standard matrix will rotate **counter-clockwise** by $\theta$ radians.

![Untitled](Linear%20Transformations%20c161a2013fd540edabaaae67cbeabeab/Untitled%203.png)

Here are some basic properties of the rotation:

<aside>
💡 Rotational Properies

a) $R_0 = I_\R$

b) $R_s \circ R_t = R_t \circ R_s = R_{s+t}$

c) $R_\theta^{-1} = R_{-\theta}$

</aside>

a) Namely, rotating by 0 radians will yield the standard identity matrix as a basis.

b) Rotating by *s* and then *t* is the same as rotating by *t* and then *s*, and the same as rotating by *s+t*

c) The inverse rotation is rotating by the negative variant of the degree

- this is because a positive rotation is *counter*clockwise, while a negative rotates *clockwise*.

We can also rotate *about an axis* for example. This doesn't mean much in $\R^2$, because we need an extra dimension above the object we are rotating for it to make a difference.

In $\R^3$, rotating *about an axis* keeps that axis fixed, while changing the other two axes. For example, if $e_1 = i, \quad e_2 = j, \quad e_3 = k$, then rotating about the z-axis would mean keeping k ($e_3$) fixed like so:

$$
R_{k,\theta}(e_3) = e_3\\R_{k,\theta}(e_1) = \begin{bmatrix}\cos\theta\\\sin\theta\\0\end{bmatrix}\\R_{k,\theta}(e_2) = \begin{bmatrix}-\sin\theta\\\cos\theta\\0\end{bmatrix}
$$

$$
[R_{k,\theta}] = \begin{bmatrix}\cos\theta  &-\sin\theta&0\\\sin\theta&\cos\theta&0\\0&0&1\end{bmatrix}
$$

This is the standard matrix of rotating about the positive z-axis by an angle $\theta$; because projecting $e_3$ onto the coordinate plane xy-plane is 0, and projecting $e_1, e_2$ onto xy-plane is themselves.