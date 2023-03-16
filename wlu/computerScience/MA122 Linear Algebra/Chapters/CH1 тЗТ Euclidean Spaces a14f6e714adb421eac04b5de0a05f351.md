# CH1 ⇒ Euclidean Spaces

A **Euclidean *n-space*** for any pos. int. n.

- Planes ⇒ 2-space
- Space ⇒ 3-space

# 1.1: Vectors

### 3Blue1Brown

[https://www.youtube.com/watch?v=fNk_zzaMoSs&ab_channel=3Blue1Brown](https://www.youtube.com/watch?v=fNk_zzaMoSs&ab_channel=3Blue1Brown)

⇒ $ℝ^2$ (Natural Number set Squared = Plane of All Natural Numbers)

- Consists of *all* ordered pairs of real numbers, a plane with a rectangular coordinate system.

![https://i.gyazo.com/c702cf08faf5965042ed1826b3589c40.png](https://i.gyazo.com/c702cf08faf5965042ed1826b3589c40.png)

**2 Ways to identify points in $ℝ^2$**

→ Direct Coordinates (Point), written as a **tuple**

→ P = (1,3); Q = (-2,2)

→ Vectors (Components)

→ $\overrightarrow{OP}=\begin{bmatrix}1&3\end{bmatrix}$ or $\overrightarrow{OP}=\begin{bmatrix}1\\3\end{bmatrix}$

→ Row vector vs. Column vector

Same with points in $ℝ^3$ ...

→ $(1, -1, 2)$ or $\begin{bmatrix}1\\-1\\2\end{bmatrix}$or $\begin{bmatrix}1&-1&2\end{bmatrix}$

$ℝ^n$ is a collection of vectors, with arithmetic operations defined by operations on its **components**

<aside>
📖 $ℝ^n$

is a *vector space* that consists of all vectors of the form:

$\overrightarrow{v} = \begin{bmatrix}v_1\\v_2\\...\\v_n\end{bmatrix}$, in which $v_1, v_2, ..., v_n \in ℝ$

</aside>

<aside>
📖 **Vector Addition**

$\overrightarrow{v} + \overrightarrow{w} = \begin{bmatrix} v_1 + w_1 \\ v_2 + w_2 \\...\\v_n+w_n \end{bmatrix}$

</aside>

<aside>
📖 **Scalar Product/Multiplication**

$b\overrightarrow{v}=\begin{bmatrix}bv_1\\bv_2\\...\\bv_n\end{bmatrix}$$(b \in \R)$

</aside>

⇒ Vectors are **proportional** or **parallel** to each other if one is obtained from the other via. scalar product

<aside>
📖 **Zero Vector**

— All components of a vector are **0** 

$**\overrightarrow{0} = \begin{bmatrix}0\\0\\..\\0\end{bmatrix}**$

</aside>

⇒ Two vectors $\overrightarrow{v}$ and $\overrightarrow{w}$ are equal *if and only if* for all i **= 1, 2, ..., n,** then $v_i = w_i$

![https://i.gyazo.com/023eb0671e324451e74823275135d543.png](https://i.gyazo.com/023eb0671e324451e74823275135d543.png)

$\R^1 = \R$ → Real Number line

![https://i.gyazo.com/81d0838ca6de79e1edd0ff980f8b6148.png](https://i.gyazo.com/81d0838ca6de79e1edd0ff980f8b6148.png)

$\R^2$ → Real Plane

$\R^3$ → Real Space

$\R^4$ → Real Space & Time ... onwards

The *zero vector* and the *scalar* number of *1* are special because of these *identities*:

<aside>
📖 $\overrightarrow{v}+\overrightarrow{0} = \overrightarrow{v}$

</aside>

<aside>
📖 $1\overrightarrow{v} = \overrightarrow{v}$

</aside>

Through these identities, we can say then that these operations on vectors is:

→ Addition is **commutative (*v**ariable order doesn't matter***)**

<aside>
📖 $\overrightarrow{v}+\overrightarrow{w} = \overrightarrow{w}+\overrightarrow{v}$

</aside>

→ Addition is **associative** *(parentheses order doesn't matter*)

<aside>
📖 $\overrightarrow{u}+(\overrightarrow{v}+\overrightarrow{w})=(\overrightarrow{u}+\overrightarrow{v})+\overrightarrow{w}$

</aside>

→ Scalar Products are **associative**

<aside>
📖 $(ab)\overrightarrow{v} = a(b\overrightarrow{v})$

</aside>

→ Scalar Products are **distributive** (*multiplcation distributes through brackets*)

<aside>
📖 $(a+b)\overrightarrow{v} = a\overrightarrow{v}+b\overrightarrow{v}$

$a(\overrightarrow{v}+\overrightarrow{w}) = a\overrightarrow{v} + a\overrightarrow{w}$

</aside>

Thus, through these identities it is given then, that

$\overrightarrow{v}+ (-1)\overrightarrow{v} = (1+(-1))\overrightarrow{v} = \overrightarrow{0}$

→ Adding a vector to its negation results in the *zero vector*, meaning that multiplying any vector by the negative scalar (-1) is a vectors *negation*.

So, if $\overrightarrow{v}+\overrightarrow{u} = \overrightarrow{0}$, then $-\overrightarrow{v}=\overrightarrow{u}$.

This is in our favor, because then we can derive a third operation, *subtraction* or *differences* between two different vectors.

<aside>
📖 **Vector Subtraction**

$\overrightarrow{w}-\overrightarrow{v} = \overrightarrow{w}+(-1)\overrightarrow{v}$

</aside>

A geometric vector $\overrightarrow{OP}$ has *initial point O* and *terminal* point P. We can also denote this vector using the *lowercase* $\overrightarrow{p}$. The difference $\overrightarrow{q} - \overrightarrow{p} = \overrightarrow{OQ}-\overrightarrow{OP} = \overrightarrow{OR}$

Vector addition and subtraction result in a vector, thus we define a new, resulting point $\overrightarrow{r}$ in the plane.  That is, it is a new point on the **same plane** of $\R^n$

> The vector $\overrightarrow{PQ}$ (starting at p, ending at q) is then parallel to the vector $\overrightarrow{r}$, which was the difference between points P and Q. This is the parallelogram rule, because $\overrightarrow{PQ}$ is parallel to $\overrightarrow{OR}$.
> 

![https://i.gyazo.com/71f660324a85c3e4ac3451ad056d577d.png](https://i.gyazo.com/71f660324a85c3e4ac3451ad056d577d.png)

Vectors $\overrightarrow{PQ}$ and $\overrightarrow{OR}$ are *equivalent* if they have:

1) same direction

2) form opposite sides of a parallelogram

3) $\overrightarrow{q}-\overrightarrow{p} = r$

$\overrightarrow{PQ}$ is a *directed line segment*.

An important thing to remember here is that $-\overrightarrow{OP}$ is opposite to $\overrightarrow{OP}$. This "Parallelogram Rule" is  saying that the sum and difference is creating two different parallelograms between the same two points. This is because the difference creates the negative vector $-\overrightarrow{OP}$.

Two directed line segments $\overrightarrow{PQ}$ and $\overrightarrow{RS}$ are equivalent iff. $\overrightarrow{q} - \overrightarrow{p} = \overrightarrow{t}$ and $\overrightarrow{s} - \overrightarrow{r} = t$, or abbreviated:

<aside>
📚 $\overrightarrow{q}-\overrightarrow{p} = \overrightarrow{s}-\overrightarrow{r}$

</aside>

# 1.2 Lines in $\R^2$

### Line Equations

⇒ RECALL: Lines in $\R^2$ can be in *standard form*, using X and Y variables:

<aside>
📚 $Ax + By + C = 0$ $(A,B,C \in \R)$

</aside>

Meaning that a line consists of **all the points** (r,s) for which this identify holds.

Lines can also be described by *parametric equations*:

<aside>
📚 $\begin{cases}x=at+c\\y=bt+d\end{cases}$

</aside>

Meaning that a line consists of all the points of the form $(at+c, bt+d)$ where *t* varies through all values in $\R$. **t** is the *parameter*. So, it is the case that with scalar multiplication and vector addition, we can translate this parametric equation to vector form

<aside>
📚 $\begin{bmatrix}x\\y\end{bmatrix} = \begin{bmatrix}a\\b\end{bmatrix}t + \begin{bmatrix}c\\d\end{bmatrix}$, where $\begin{bmatrix}a\\b\end{bmatrix}\ne\overrightarrow{0}$

</aside>

This is interpreted to mean that a line is *obtained by starting from a point* (c,d), and moving back and forth as described by the parameter *t*, along the direction of a fixed vector

![https://i.stack.imgur.com/LT6Tu.gif](https://i.stack.imgur.com/LT6Tu.gif)

<aside>
📚 Find the eq. in *standard form* of the line thru P, along the *direction* of $\overrightarrow{v}=\begin{bmatrix}2\\3\end{bmatrix}$

⇒ P = (-1, 1)

1) make vector form equation 

$\begin{bmatrix}x\\y\end{bmatrix}=\begin{bmatrix}2\\3\end{bmatrix}t+\begin{bmatrix}-1\\1\end{bmatrix}$

2) find equiv. parametric equations for x & y

$\begin{cases}x=2t-1\\y=3t+1\end{cases}$

3) eliminate $t$ via substitution or elimination

$3x-2y+5 = 0$

</aside>

<aside>
📚 $3x+2y+5 = 0$, find vector form

1) find two distinct points on this line, which will give us a *direction vector* on this line

$x =-1, y= -1= P (-1,-1)$

$x=1, y=-4=Q(1,-4)$

2) calculate direction vector of line seg. PQ

$\overrightarrow{PQ}=\overrightarrow{q}-\overrightarrow{p}=\begin{bmatrix}1\\-4\end{bmatrix}-\begin{bmatrix}-1\\-1\end{bmatrix}=\begin{bmatrix}2\\-3\end{bmatrix}$

3) Write in *vector form*

→ Direction vector PQ is the **slope** of the line

→ Any of the two points found are the **intercept** of the line

$\begin{bmatrix}x\\y\end{bmatrix}=\begin{bmatrix}2\\-3\end{bmatrix}t+\begin{bmatrix}-1\\-1\end{bmatrix}$

</aside>

This allows us to define a **line** in any $\R^n$, through a vector $\overrightarrow{p}$, with direction along a vector $\overrightarrow{v}$, which consists of all vectors of the form:

<aside>
📚 **Line**

$\overrightarrow{x} =t\overrightarrow{v}+\overrightarrow{p}$

⇒ $\overrightarrow{v}$ is along the direction of the line, and the direction lies on the line.

⇒ the point $\overrightarrow{p}$ is on the line

</aside>

### Line Intersections

Lines in the 2-plane may intersect, and when they do, they intersect at exactly 1 point, like P = (c,d). Given two lines that intersect at P:

$l_1 : A_1x+B_1y+C_1 = 0$

$l_2 : A_2x+B_2y+C_2 = 0$

(c,d) lies on both lines simultaneously, so

$\begin{cases}A_1c+B_1d+C_1 = 0\\A_2c+B_2d+C_2 = 0\end{cases}$

the ordered pair P = (c,d), or vector $\begin{bmatrix}c\\d\end{bmatrix}$solves the system of equations. Some systems may have no solutions, because the two lines are perfectly parallel (will never intersect). Otherwise, any two lines in a system that are not parallel, must intersect somewhere, so the system must have a solution.

Finding the solution requires solving the system of equations by finding a point for which they will both equal 0. This is often done through substitution or manipulation. If we find a contradiction, such as finding that eliminating all variables of a line results in something like $0 = 1$, then there is no solution because 0 can never equal 1.

Likewise, we can say that two lines are parallel if they never intersect. That is not to say that there are lines that are parallel if t8hey never intersect. Take for example two opposite sides of a cube, even if we take adjacent sides which are perpendicular, because they are opposite, they never intersect. They are still not parallel. This means that we can further define what it means to be parallel:

<aside>
📚 Parallel lines are ones that:

1) never intersect

2) are along the exact same direction

</aside>

This means that direction vectors of each parallel line must be *proportional* to one-another. 

![https://i.gyazo.com/10d600d4dc5368afc2159e25adf09520.png](https://i.gyazo.com/10d600d4dc5368afc2159e25adf09520.png)

<aside>
📚 **In/Dependence of two vectors**

Vectors $\overrightarrow{v}$ and $\overrightarrow{w}$ are **linearly dependent** if one of the vectors is *proportional* to the other. They are linearly independent if they are *not* dependent, one of them is *not* a *scalar multiple* of the other.

</aside>

Thus, two (non-zero) vectors are linearly depedent when they are *parallel* to each other. The zero vector $\overrightarrow{0}$ is linearly dependent to *any vector*.

<aside>
📚 This definition is a bit backwards. Think of this definition as meaning that linear dependence means that they are dependent on the same direction. This notion of independence means that they are not dependent on the same direction vector.

</aside>

<aside>
📚 The zero-vector is linearly dependent to all other vectors because the zero-vector can be proportional to all vectors if you multiply them by 0, resulting in a zero-vector.

</aside>

# 1.3 Length and Dot-Product

<aside>
☁️ RECALL: Distance between two points in $\R^2$

$d(A,B) = \sqrt{(b_1-a_1)^2+(b_2-a_2)^2}$

→ given by the pyth. theorem

</aside>

Thus, we can represent segment AB by $\overrightarrow{AB}=\begin{bmatrix}b_1-a_1\\b_2-a_2\end{bmatrix}$.

The **length** or **magnitude, or norm** of any vector $\overrightarrow{v}$ that starts at the origin O(0,0) and ends at V($v_1,v_2$):

<aside>
📚 $\overrightarrow{v} = \begin{bmatrix}v_1\\v_2\end{bmatrix}$, $||\overrightarrow{v}|| = \sqrt{v_1^2+v_2^2}$

</aside>

⇒ this applies to any $\R^n$ vector, we sum the squares of each vector component.

<aside>
📚 **Unit Vector**

a vector for which its magnitude equals 1.

</aside>

<aside>
📚 **Euclidean n-space**

$\R^n$ with the *norm* of vectors given by the square-root of the sum of squares of each vector component.

</aside>

> We know that the norm of $\overrightarrow{0} =0$, so for any vector that is not non-zero, its norm is greater than 0. The norm of a vector is 0 IF AND ONLY IF the vector is the zero-vector. A scalar multiple of a vector's norm is the same as multiplying the vector's norm by the scalar: $||a\overrightarrow{v}|| = |a| *||\overrightarrow{v}||$ ($|a|$ is the absolute value). If a vector $\overrightarrow{v}$ is not the zero-vector, then $\frac{1}{||\overrightarrow{v}||}\overrightarrow{v} = \begin{bmatrix}1\\1\\...\\1\end{bmatrix}$because the scalar product of a vector and its norm reciprocal always results in 1 for each component, whose square-root sum of squares is then 1.
> 

<aside>
☁️ **Direction / Normalization**

(of a non-zero vector) is the unit vector:

$\overrightarrow{v}\degree = \frac{1}{||\overrightarrow{v}||}\overrightarrow{v}$

</aside>

⇒ This describes the direction of any vector in its *unit-form*. Two vectors are in the same direction if $\overrightarrow{v}\degree = \overrightarrow{w}\degree$, and opposite in direction if $\overrightarrow{v}\degree = -\overrightarrow{w}\degree$.

⇒ For any non-zero vector, the scalar multiple of $a\overrightarrow{v}$ is in the same direction of $\overrightarrow{v}$ IF AND ONLY IF $a > 0$.

⇒ Only proportional (linearly dependent) non-zero vectors have same or opposite directions.

The norm/magnitude of vectors satisfy the *triangle inequality*, in which:

<aside>
☁️ **Triangle Inequality**

$||\overrightarrow{v}+\overrightarrow{w}||\leq||\overrightarrow{v}||+||\overrightarrow{w}||$

</aside>

![https://i.gyazo.com/585130ee889bdde32b5f7a3340f4a6ce.png](https://i.gyazo.com/585130ee889bdde32b5f7a3340f4a6ce.png)

<aside>
☁️ **Dot Product**

$\overrightarrow{v} = \begin{bmatrix}v_1\\v_2\\...\\v_n\end{bmatrix}$

$\overrightarrow{w} = \begin{bmatrix}w_1\\w_2\\...\\w_n\end{bmatrix}$

$\overrightarrow{v}\cdot\overrightarrow{w}=v_1w_1 + v_2w_2+...+v_nw_n$

...

$||\overrightarrow{v}||^2=v_1^2+v_2^2+...+v_n^2 = \overrightarrow{v}\cdot\overrightarrow{v}$

</aside>

⇒ Dot products are *commutative* (order does not matter): $\overrightarrow{v}\cdot\overrightarrow{w} = \overrightarrow{w}\cdot\overrightarrow{v}$

⇒ They are also *distributive* (distributes across addition)

⇒ It is also *associative* when multiplied by a scalar

<aside>
⭐ The dot-product of two vectors, *v* and *u,* represent how linearly dependent they are, or their angle. If two vectors are linearly dependent, then their dot-product is NOT zero. A zero dot-product represents that they are not linearly dependent whatsoever, the farthest away from linear dependence would mean that they are *orthogonal*, or perpendicular to each other. Anything less than orthogonal, and they start to move in a similar direction, either positively, or negatively.

</aside>

<aside>
☁️ The dot product results in ***scalar*** value. It is also associative when multiplied by a scalar because the multiplication is associative as well, that is, we can multiply the vector by a scalar *then* dot-product, OR we can perform the dot-product and then multiply by the scalar. The result is the same because either way, we're dealing with multiplication and that results in factors of the multiple being present in the dot-product.

</aside>

<aside>
☁️ **Well-defined expression**

A 'well-defined expression' is one that is unambigous, in which it's display does not allow for different algebraic interpretation. For example, those facebook math problems that involve multiplying, adding and subtraction but don't use any proper notation are ill defined, because there are many ways, even considering PEMDAS/BEDMAS, that you can multiply to achieve a different result.

</aside>

<aside>
☁️ **Cauchy-Schwarz Inequality**

$|\overrightarrow{v}\cdot\overrightarrow{w}|\leq||\overrightarrow{v}||\;||\overrightarrow{w}||$

this *lemma,* states that this equality holds IF AND ONLY IF $\overrightarrow{v}$ and $\overrightarrow{w}$ are **linearly dependent**.

</aside>

<aside>
☁️ Dot Product of Unit Vectors

$\overrightarrow{u}=\begin{bmatrix}\cos\alpha\\\sin\alpha\end{bmatrix}$ and $\overrightarrow{v}=\begin{bmatrix}\cos\beta\\\sin\beta\end{bmatrix}$

⇒ These are *unit vectors* because of the trigonometric identity:

$\cos^2\alpha+\sin^2\alpha=\cos^2\beta+\sin^2\beta=1$

⇒ Their dot product is thus

$\overrightarrow{u}\cdot\overrightarrow{v}=\cos\alpha\cos\beta+\sin\alpha\sin\beta=\cos(\beta-\alpha)$

⇒ $\beta - \alpha$ is exactly the angle formed by the vectors

</aside>

Angles between vectors ($\overrightarrow{u}$ and $\overrightarrow{v}$) is defined as $\widehat{(\overrightarrow{v},\overrightarrow{v})} = \cos^{-1}(\frac{u\cdot v}{||u||||v||}) \in[0, \pi]$

Two vectors are ***Orthogonal*** to each other if $\widehat{(\overrightarrow{v},\overrightarrow{v})} = \frac{\pi}{2}$.

<aside>
☁️ Vectors are orthogonal to each other if their angle in the plane is 90 degrees, they form a right-angle. Orthogonal vectors are denoted by:

$\overrightarrow{u}\perp\overrightarrow{v}$.

⇒ This is basically a notation that states that these vectors are *perpendicular* to each other, intersecting at a right-angle.

</aside>

Because we are using the $\cos^{-1}$, if we were to apply the inverse $\cos$ to the angle between vectors, we get back $\frac{u\cdot v}{||u||\;||v||}$ (the trigonometric ratio??), and can then apply other trig. functions to get all other trig. values of the angle. This term is the result of the dot-product of two unit vectors.

$$
\frac{\overrightarrow{u}\cdot\overrightarrow{v}}{||\overrightarrow{u}||\;||\overrightarrow{v}||} = (\frac{1}{||\overrightarrow{u}||}\overrightarrow{u})\cdot(\frac{1}{||\overrightarrow{v}||}\overrightarrow{v})
$$

<aside>
☁️ **Orthogonality**

$\overrightarrow{u}$ and $\overrightarrow{v}$ are orthogonal to each other IF AND ONLY IF $\overrightarrow{u}\cdot\overrightarrow{v}=0$

⇒ their dot product is 0

⇒ This is because (if we recall basic trigonometry...) that $\cos(\pi/2) = 0$. Then the dot product of these two vectors is 0, then the numerator becomes 0 and that means the equality is 0.

⇒ $\cos^{-1}(0) = \pi/2$

so ..., $\cos^{-1}(u\cdot v/||v||\;||u||)$ gives us the angle between two vectors, and when these vectors are perpendicular / orthogonal, the result is $\pi/2$.

</aside>

<aside>
☁️ **Pythagorean Theorem**

$\overrightarrow{v}$ and $\overrightarrow{w}$ are orthogonal vectors in any $\R^n$ then

$||\overrightarrow{u}+\overrightarrow{w}||^2 = ||\overrightarrow{u}||^2 +||\overrightarrow{w}||^2$

</aside>

This is proven by definition of dot-product operations:

$$
||\overrightarrow{u}+\overrightarrow{w}||^2 = (\overrightarrow{u}+\overrightarrow{w})\cdot(\overrightarrow{v}+\overrightarrow{w}) = \overrightarrow{v}\cdot\overrightarrow{v}+2\overrightarrow{v}\cdot\overrightarrow{w}+\overrightarrow{w}\cdot\overrightarrow{w} = ||\overrightarrow{u}||^2 +||\overrightarrow{w}||^2
$$

⇒ This is true when we apply the lemma of orthogonality when $\overrightarrow{v}\cdot\overrightarrow{w}=0$.

Applied in difference, we get the *law of cosines:*

<aside>
☁️ **Law of Cosines**

$||\overrightarrow{v} - \overrightarrow{w}||^2 = ||\overrightarrow{v}||^2 + ||\overrightarrow{u}||^2 - 2||\overrightarrow{v}||\cdot||\overrightarrow{w}||\cos(\widehat{\overrightarrow{v},\overrightarrow{w}})$

</aside>

![https://i.gyazo.com/9a831d8df7c8216dce4d8969373f73ff.png](https://i.gyazo.com/9a831d8df7c8216dce4d8969373f73ff.png)

Using orthogonality and dot-product, we can define the **point-normal** equation form of a line. It describes a *normal direction* and a *point on the line*. Vectors in a "Normal Direction" are "normal" or "perpendicular" or "orthogonal" to the line, and are called normal vectors of the line. 

$\overrightarrow{n}=\begin{bmatrix}A\\B\end{bmatrix}$ is a vector along the normal of an arbitrary line *l*, and passes through the point $P = (x_0, y_0)$, for any point $Q = (c,d)$ on *l*, then the line $\overrightarrow{PQ}\perp\overrightarrow{n}$.

<aside>
☁️ ie. Any segment on the line *l* is then orthogonal with the normal. The dot-product of the normal vector and any line segment is then 0.

</aside>

because $\overrightarrow{PQ}=\begin{bmatrix}c-x_0\\d-y_0\end{bmatrix}$, the point $(c,d)$ is only on the line *l*, if and only if $A(c-x_0) + B(d-y_0) = \overrightarrow{n}\cdot\overrightarrow{PQ}=0$

<aside>
☁️ ie. $A(c-x_0)$ , where A is a parameter that comes from the normal vector.

</aside>

This is the *point-normal form* of a line *l* with normal vector $\overrightarrow{n}$, through the point $(x_0, y_0)$. In general:

$A(x-x_0) +B(y-y_0) = 0$

<aside>
☁️ In order to convert this point normal to standard form we set:

$C = -Ax_0 - By_0$ as in $Ax + By + C = 0$

ex. find the equation in *standard form* in $\R^2$ thru the point (3, -7) and normal $\begin{bmatrix}6\\1\end{bmatrix}$.

⇒ $6(x-3) +(y+7) = 0$

⇒ $6x+y-11 = 0$

</aside>

# 1.4 Orthogonal Projection

Given a point *M* and line *l* in $\R^2$, the orthogonal projection of M onto *l* is a point Q on *l* such that the line segment from M to Q on the line, is perpendicular/orthogonal to the line. The length of MQ is the *distance* from point M to the line L. Since this line is orthogonal, it is the shortest distance from M to L. This is due to the geometric intuition that the shortest distance between two points is the straight line between those two points.

<aside>
☁️ $||\overrightarrow{MP}|| \geq ||\overrightarrow{MQ}||=d(M, l)$

</aside>

This is proven using the *pythagorean theorem*. For any point P on the line:

$$
\overrightarrow{MQ}+\overrightarrow{QP}=\overrightarrow{MP}
$$

$$
\overrightarrow{MQ}\perp\overrightarrow{QP} 
$$

MQ is orthogonal to QP, forming a right-angle triangle.

$$
||\overrightarrow{MP}||^2=||\overrightarrow{MQ}+\overrightarrow{QP}||^2=||\overrightarrow{MQ}||^2+||\overrightarrow{QP}||^2\geq||\overrightarrow{MQ}||^2
$$

Thus by definition: $||\overrightarrow{MP}||\geq||\overrightarrow{MQ}||$.

![https://i.gyazo.com/53555d84d21bece6d7db8f46eb9d7a3d.png](https://i.gyazo.com/53555d84d21bece6d7db8f46eb9d7a3d.png)

If we define the line by an equation in the form: $Ax+By+C=0$, then we can define the line's normal vector: $\overrightarrow{n}=\begin{bmatrix}A\\B\end{bmatrix}$, and can be used to find the segment $\overrightarrow{MQ}$, and can then determine Q because $\overrightarrow{OQ}=\overrightarrow{OM}+\overrightarrow{MQ}$.

<aside>
☁️ given $\overrightarrow{n}$ to be the normal vector of line *l*, we can find the line segment $\overrightarrow{MQ}$ such that $\overrightarrow{MQ}\perp\;l$ using a point P on the line:

$$
\overrightarrow{MQ}=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||^2}\overrightarrow{n}
$$

</aside>

 This is proven by the fact that $(\overrightarrow{MQ}, \overrightarrow{n})\perp\;l$:

 

$$
[1]=\overrightarrow{MQ}=\lambda\overrightarrow{n}
$$

$$
\overrightarrow{MP}=\overrightarrow{MQ}+\overrightarrow{QP}\;\;\;( n\cdot\overrightarrow{QP}=0)
$$

$$
\overrightarrow{n}\cdot\overrightarrow{MP}=\overrightarrow{n}\cdot(\overrightarrow{MQ}+\overrightarrow{QP})=\overrightarrow{n}\cdot\overrightarrow{MQ}=\overrightarrow{n}\cdot(\lambda\overrightarrow{n})=\lambda(\overrightarrow{n}\cdot\overrightarrow{n})=\lambda||\overrightarrow{n}||^2
$$

$$
[2] =\lambda=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||^2}
$$

$$
[1]\; and \;[2] = \overrightarrow{MQ}=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||^2}\overrightarrow{n}
$$

Thus we can understand orthogonal projection of $\overrightarrow{v}$ onto $\overrightarrow{w}$, given that they are vectors, and $\overrightarrow{w} \ne\overrightarrow{0}$. Another notation of the orthogonal projection of $\overrightarrow{v}$ onto $\overrightarrow{w}$ is the *component of* $\overrightarrow{v}$ along $\overrightarrow{w}$:

$$
proj_{\overrightarrow{w}}(\overrightarrow{v})=\frac{\overrightarrow{v}\cdot\overrightarrow{w}}{||\overrightarrow{w}||^2}\overrightarrow{w}

$$

> An interesting application of this projection is to the *mean value* of any *n* real numbers. The mean value can be interpreted to mean the projection of a vector consisting of components that are *n* real numbers, onto a vector $\overrightarrow{w}=\begin{bmatrix}1\\1\\1\\...\\1\end{bmatrix}$. The result of $proj_{\overrightarrow{w}}(\overrightarrow{x})$ is equal to the mean of components of *x,* such as*: $\frac{1}{n}(x_1+x_2+x_3+...+x_n)\overrightarrow{w}$.* We can also interpret this in terms of *linear regression*, because we are trying to find the projection of a result onto a line.
> 

The formula of the *projection of v onto w* can be rewritten to incorporate the unit vector of direction *w* as such:

$$
proj_{\overrightarrow{w}}(\overrightarrow{v})=(\overrightarrow{v}\cdot\frac{\overrightarrow{w}}{||\overrightarrow{w}||})\frac{\overrightarrow{w}}{||\overrightarrow{w}||}=(\overrightarrow{v}\cdot\overrightarrow{w}\degree)\overrightarrow{w}\degree
$$

The real number $\overrightarrow{v}\cdot\overrightarrow{w}\degree$ is called the *scalar component* of v, in the *direction of w*.

We can use this concept of projection to compute the distance between a point and a line given by an equation:

<aside>
☁️ **Distance between point and line ($\R^2$)**

Given M = (a,b), and *l* is a line in $\R^2$ given by: $Ax+By+C=0$, then the distance between the point and line is $d(M,l)$:

$$
d(M,l) = \frac{|Aa+Bb+C|}{\sqrt{A^2+B^2}}
$$

That is, the absolute value of the dot-product of the point and line coefficients, plus C, divided by the square root of squared sums of line coefficients.

</aside>

This is proven by the fact that the distance we are looking for is the *absolute value* of the scalar component in MP in the direction of the normal vector (because the distance shortest is the segment orthogonal to the line, from the point M). This allows us to see that the distance between point Q and line *l* is the same as the magnitude of the vector $\overrightarrow{MQ}$. Through algebra, we can see that $\overrightarrow{MQ}=||\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||^2}\overrightarrow{n}||=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||}$, as the bottom $||\overrightarrow{n}||^2$ is partially cancelled out by the multiplicative magnitude of *n*. 

<aside>
☁️ **Distance between point and line (alt.)**

$$
d(M, l) = ||\overrightarrow{MQ}|| = \frac{|\overrightarrow{MP}\cdot\overrightarrow{n}|}{||\overrightarrow{n}||}
$$

</aside>

If $\overrightarrow{n}=\begin{bmatrix}A\\B\end{bmatrix}$, and $\overrightarrow{MP}=\begin{bmatrix}x_0-a\\y_0-b\end{bmatrix}$ (because P is a point on the line with coords. P(x, y), and MP = p - m), then ||MQ|| = $\frac{|A(x_0-a)+B(y_0-b)|}{\sqrt{A^2+B^2}}$, and this gives us an equation that expresses the distance in terms of *coefficients* in its equation in standard form, considering the line and the point.

<aside>
☁️ Find the distance from point M(-1,2) to the line *l* given by 3x+4y=2

3x+4y=2 → 3x+4y-2=0, where A = 3, B = 4, C = -2.

d(M,l) = $\frac{|3\times(-1)+4\times2-2|}{\sqrt{3^2+4^2}}=\frac{3}{5}$.

</aside>

Given the previous definition of orthogonal vectors, we can build on our definition to understand the relationship between more than two vectors and orthogonality.

<aside>
☁️ $\overrightarrow{v}, \overrightarrow{w}\in\R^n, \overrightarrow{w}\ne\overrightarrow{0}$

Let the vector $\overrightarrow{p}$ satisfy the following conditions:

1) $\overrightarrow{p},\overrightarrow{w}$ are *parallel* vectors

2) $(\overrightarrow{v}-\overrightarrow{p})$ and $\overrightarrow{w}$ are *orthogonal* vectors. 

</aside>

This leads us to define the *component* of v that is orthogonal to w, and it is the vector defined by:

<aside>
☁️ **Component Orthogonal to a vector**

$$
perp_{\overrightarrow{w}}(\overrightarrow{v})=\overrightarrow{v} - proj_{\overrightarrow{w}}(\overrightarrow{v}) = \overrightarrow{v}-\frac{\overrightarrow{v}\cdot\overrightarrow{w}}{||\overrightarrow{w}||^2}\overrightarrow{w}
$$

</aside>

<aside>
☁️ $\overrightarrow{v}=\begin{bmatrix}2\\4\\1\end{bmatrix}, \overrightarrow{w}=\begin{bmatrix}1\\1\\2\end{bmatrix}$. Find the component of V orthogonal to W.

</aside>

This is very simply thought of as the remaining right-angle portion of the triangle. The projection of a point V onto W is the place where, on the vector W, is the shortest distance between point V and vector W. The component that is orthogonal to this projection, completes the [parallelogram by that rule.](https://www.desmos.com/calculator/kghqzkxrfj)

For example, lets take M = (-1,2) and a line $3x+4y=2$. Find the point Q on the line such that the distance = $||\overrightarrow{MQ}||$.

1) Choose point P on the line and compute the orthogonal projection of PM onto normal.

The normal vector is $\overrightarrow{n}=\begin{bmatrix}3\\4\end{bmatrix}$, given the equation of the line from the coefficients. This is because the line is technically equal to $y = \frac{1}{2}-\frac{3}{4}x$. The vector [3,4] is orthogonal to this because the slope of vector [3,4] is from point [0,0] to [3,4] which is:

$$
\frac{\Delta\;Y}{\Delta\;X}=\frac{4-0}{3-0} = \frac{4}{3}
$$

Which is the *negative reciprocal* of the equation's slope. To obtain a point P on the line, we can simply set X = 0, and obtain Y = 1/2. Point P is now (0, 1/2), and is on the line.

The vector PM is thus:

$PM = OM - OP = m - p = [-1,2]-[0,1/2] = [-1,3/2]$.

We project this vector PM onto the vector *n* using the projection formula above, and obtain:

$proj_n(PM)=\frac{3}{25}\begin{bmatrix}3\\4\end{bmatrix}$

![https://i.gyazo.com/c916db573b3dce0f03e9f457fe254266.png](https://i.gyazo.com/c916db573b3dce0f03e9f457fe254266.png)

Here we project the seqment PQ onto the normal because we know that the distance we want to this point Q from M is based on the orthogonal, shortest distance. Once we find the projection component of this vector PM onto the normal, we can then subtraction the vector M from the projection. We subtract the vector M because OM = OP + PM. To find the point Q, we know based off the parallelogram rule, that OQ = PQ + OP, and since PQ is equivalent to the subtraction of PM and the projection of PM onto N, then that is a route to find OQ, our objective.

<aside>
☁️ However, if the *direction vector* of the line is known, then we can compute PQ through the Projection of PM onto that direction instead, to find the point Q directly by OQ = OP + PQ.

*in this case above, we don't have the direction vector and have the normal vector instead. this means that instead of computing PQ directly by the direction vector, we calculate the opposite component of M orthogonal to the line first, then use that to solve for PQ.*

</aside>

![https://i.gyazo.com/214e7e77ec8a5c44bb67a2df3f99bcf6.png](https://i.gyazo.com/214e7e77ec8a5c44bb67a2df3f99bcf6.png)

### [Example Video](https://www.youtube.com/watch?v=fqbwErsP8Xw&ab_channel=KimberlyBrehm)

![perpwv.png](CH1%20%E2%87%92%20Euclidean%20Spaces%20a14f6e714adb421eac04b5de0a05f351/perpwv.png)

<aside>
☁️ $\overrightarrow{v}, \overrightarrow{w}\in\R^n, \overrightarrow{w}\neq\overrightarrow{0}$, then:

1) If a vector $\overrightarrow{u}$ is non-zero, and $\overrightarrow{u}$ and $\overrightarrow{w}$ are linearly dependent, then

$$
proj_{\overrightarrow{u}}\overrightarrow{v} = proj_{\overrightarrow{w}}\overrightarrow{v}
$$

⇒ this is true even if *u* is in the opposite direction to *w*.

2) if $\overrightarrow{w}$ is a unit vector $(||\overrightarrow{w}|| = 1)$, then

$$
proj_{\overrightarrow{w}}\overrightarrow{v} = (\overrightarrow{v}\cdot\overrightarrow{w})\overrightarrow{w}
$$

⇒ this can be interpreted to be the essential geometry that underlies the dot-product operation. the dot-product with a unit vector outputs the scalar component of the orthogonal projection onto that unit vector.

</aside>

---

# 1.5 Area in $\R^2$ and $2\times2$ Determinants

Given two vectors V and W, suppose the parallelogram ABCD is formed by the vectors and their addition. The area of a parallelogram is computed by the product of the base and height.

$$
area(ABCD) = ||\overrightarrow{v}||\;||\overrightarrow{HD}|| = ||\overrightarrow{v}||\times||\overrightarrow{w}||\sin\widehat{(\overrightarrow{v},\overrightarrow{w})}
$$

This identity gives us this resulting equation:

$$
area(ABCD) =\sqrt{||\overrightarrow{v}||^2||\overrightarrow{w}||^2-(\overrightarrow{v}\cdot\overrightarrow{w})^2}
$$

This holds for any $\R^n$, but when we only consider $\R^2$, we can see (via Cauchy-Schwarz ineq.) that the term within the square root turns into:

$$
area(ABCD)=\sqrt{(v_1w_2-v_2w_1)^2}=|v_1w_2-v_2w_1|
$$

![https://i.gyazo.com/5833b607c64d3da6bc09f53b0fe3368e.png](https://i.gyazo.com/5833b607c64d3da6bc09f53b0fe3368e.png)

<aside>
☁️ $\overrightarrow{v}=\begin{bmatrix}-\frac{1}{3}\\1\end{bmatrix}, \overrightarrow{w}=\begin{bmatrix}3\\1\end{bmatrix}$. Find Parallelogram defined by OPRQ.

Following the formula for $\R^2$, we can see that the area of OPRQ is = $|-\frac{10}{3}| = \frac{10}{3}$. 

An interesting turn to this equation is that vectors V and W are orthogonal, as their dot-product is equal to 0. This means that the angle between V and W is $\frac{\pi}{2}$, and thus it is rather the area of the **square** that they form. Thus, when we deal with the area that two vectors and their sum form, and those vectors are orthogonal, we can alternatively use the formula for the area of a square, which is: $width\times\;length=||\overrightarrow{v}||\times||\overrightarrow{w}||$.

</aside>

The term $v_1w_2-v_2w_1$ tends to show up in more than just this. This term is called the *determinant* of a square matrix. In order to understand what this means, we need to understand a matrix:

<aside>
☁️ **Determinants**

Given a square array - $A = \begin{bmatrix}a&b\\c&d\end{bmatrix}$ of FOUR real numbers, is a 2-by-2 square matrix. 

Its determinant, called $\det(A)$ is a *real number* given by the formula:

$$
\det(A)=\det\begin{bmatrix}a&b\\c&d\end{bmatrix}=ad - bc
$$

</aside>

The shorthand notation of the determinant is also:

$$
\begin{vmatrix}a&b\\c&d\end{vmatrix}
$$

![https://i.gyazo.com/ec5bbcb2f842468fd9c4e4efd5b94fa6.png](https://i.gyazo.com/ec5bbcb2f842468fd9c4e4efd5b94fa6.png)

We can see that the area in $\R^2$ is then the absolute value of the determinants of the square matrix of two vectors.

This idea of the area of the parallelogram breaks down when we consider the case that the two vectors V and W are linearly *dependent* (ie. they are parallel), because the parallelogram is "squished" into line, it has no area, so its area must be 0. 

What if we wanted to find the area of a triangle? We know that the area is a triangle is half of a parallelograms, because a parallelogram can be constructed by two, mirrored triangles.  Take this picture for instance.

![https://i.gyazo.com/ff317a391fec499de4efbbe0fb414e16.png](https://i.gyazo.com/ff317a391fec499de4efbbe0fb414e16.png)

---

# 1.6 Planes in $\R^3$

The best way to describe planes mathematically and numerically is through their *point-normal form,* which describes a point Q = (a,b,c) on the plane, perpendicular to a non-zero vector N, through a point P(x,y,z).

<aside>
☁️ **Point-Normal Form of a Plane**

Rather than using Q, let's use the arbitrary point $X = (x,y,z)$, so the equation of the plane *through* P and *perpendicular* to $\overrightarrow{n}$ is:

$$
\overrightarrow{n}\cdot\overrightarrow{PX}=\overrightarrow{n}\cdot(\overrightarrow{X}-\overrightarrow{p})=A(x-x_0)+B(y-y_0)+C(z-z_0)=0
$$

</aside>

![https://i.gyazo.com/0ddcbaf96e910b3e0efc91aca8707f8b.png](https://i.gyazo.com/0ddcbaf96e910b3e0efc91aca8707f8b.png)

<aside>
☁️ **Standard Form of a Plane**

When $D = -Ax_0-By_0-Cz_0$, then that is the standard form of the plane:

$$
Ax+By+Cz+D=0; (A\&B\&C\neq0)
$$

</aside>

ex. Find the eq. of the plane through the point P(2,2,0), perpendicular to n = [1,3,4].

<aside>
☁️ In point-normal form, this equation is given by:

$(x-2)+3(y-2)+4(z-0)=0 \iff x+3y+4z-8=0$

</aside>

There are multiple equations that can define this single plane, because if we were to multiply algebriacally by a non-zero $\R$, then that is the same plane.

Let's think about the orthogonal projects of points onto planes. Let M = (a,b,c) be a point in $\R^3$, and $\pi$ be a plane. The orthogonal projection of M onto $\pi$, is the point Q on $\pi$, such that $\overrightarrow{MQ}\perp\pi$.

The distance from $\overrightarrow{MQ}$ to $\pi$ is $||\overrightarrow{MQ}||$.

Just like with $\R^2$, given a point P on $\pi$, the length of MP cannot be smaller than MQ:

$$
||\overrightarrow{MP}||\geq||\overrightarrow{MQ}||
$$

(for all P on $\pi$).

![https://i.gyazo.com/03b31c0164b63d5d234a90ec91032914.png](https://i.gyazo.com/03b31c0164b63d5d234a90ec91032914.png)

![Projection of point M onto plane, orthogonal to the plane](https://i.gyazo.com/cbab419ffc6841607d5c348907c2d29f.png)

Projection of point M onto plane, orthogonal to the plane

If *n* is a normal vector of this plane, then MQ is then the *orthogonal projection* of MP onto the normal *n*, in the direction of *n*.

$$
\overrightarrow{MQ}=proj_{n}(\overrightarrow{MP})=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||^2}\overrightarrow{n}
$$

And the distance from M to the plane $\pi$ is the same as the formula for $\R^2$: $d(M, \pi)=||\overrightarrow{MQ}||=\frac{\overrightarrow{MP}\cdot\overrightarrow{n}}{||\overrightarrow{n}||}$.

If the plane is in *standard form*, then we can describe the distance using: $d(M,\pi) = \frac{|Aa+Bb+Cc+D|}{\sqrt{A^2+B^2+C^2}}$.

<aside>
☁️ ex. point M = (2,2,2) on the plane $\pi$, with eq. $2x+3y+4z=6 \iff 2x+3x+4z-6=0$

a) Distance from M to $\pi$

$$
d(M,\pi)=\frac{|2*2+3*2+4*2-6|}{\sqrt{4+9+16}}=\frac{12}{\sqrt{29}}
$$

b) Point Q on plane, with shortest distance

- start with a point P on the plane, apply the *projection* of P onto the normal to find the distance between Q and M (||MQ||), and then find Q by OQ = OM + MQ.

We get point P by setting $x=0,y=0 \implies\;P(0,0,3/2)$.

- The normal vector *n* is obtained from the coefficients of the standard-form equation ⇒ [2,3,4]

$$
MQ = proj_n(MP)=\frac{MP\cdot n}{||n||^2}=-\frac{12}{29}\begin{bmatrix}2\\3\\4\end{bmatrix}
$$

To find the point Q, we "triangulate" or find the other side of the triangle through the expression: $OQ = OM + MQ$, if we know OM and MQ, we add them to find the remaining part of the parallelogram/triangle.

$$
OQ= OM + MQ = [2,2,2]-\frac{12}{29}[2,3,4]=\frac{1}{29}[34,22,10]
$$

</aside>

Rather than looking for the orthogonal projection of a *point* onto a plane, we can look for the projection of a *vector* onto a plane.

<aside>
☁️ **Projection onto a Plane**

$\overrightarrow{n}, \overrightarrow{v}\in\R^3$, $\pi$ is a plane with normal $\overrightarrow{n}$. The *orthogonal projection of V onto plane $\pi$* is:

$$
proj_\pi(v)=v-proj_n(v)=v-\frac{v\cdot n}{||n||^2}n
$$

This projection of V onto the plane $\pi$ is exactly the component of V that is *orthogonal* to the normal vector *n*. 

$$
proj_\pi(v)=perp_n(v)
$$

</aside>

The projection of V onto the plane is the *component of V in $\pi$.* This component is on the plane.

Because a plane has two directions, it is a 2D plane, equations in this vector form require *two* parameters:

$$
\begin{bmatrix}x\\y\\z\end{bmatrix}=sv+tw+p
$$

*s* and *t* are the parameters here.

![https://i.gyazo.com/582abab109652cc9e3237328f6ad5695.png](https://i.gyazo.com/582abab109652cc9e3237328f6ad5695.png)

Notationally, $p = OP$ defines a *fixed point* P on the plane. $v, w$ are fixed *vectors*, that represent moving in TWO directions, a way to move around the plane. If V and W are linearly dependent, then the equation only defines a line in $\R^3$.

For example, take V = [-1,3,1] and W = [3,-9,-3]. We can see that W = -3V, so: $sv+tw+p \implies(s-3t)v+p$, which is the form of a line, which is $\lambda v+p$.

<aside>
☁️ Plane in $\R^n$, in Vector Form

A plane in any $\R^n$, where n > 2, consists of all vectors of the form:

$$
x=sv+tw+p
$$

- P is a fixed vector
- V and W are fixed, AND *linearly independent*
- s,t are *arbitrary* parameters.
</aside>

If we compare the *point-normal form* and the *vector form* equations for a plane, the only way to have them hold together is if $n\cdot v=n\cdot w= 0$. What this essentially means is that the normal vector must be orthogonal to the two vectors that make the plane.

<aside>
☁️ Given the plane in standard form: $x-2y+3z = 6 \implies x-2y+3z-6=0$

a) point-normal

- fix two of the three variables, (x,y), (y,z), or (x,z) and solve for the last to determine a point on the plane.
- ie. $x_0 =1, y_0=-1 \iff z_0=1$, P = (1,-1,1)
- Use the coefficients of the standard form to know the *normal vector n* = [1,-2,3].
- use the normal vector *n* and the point P:
    - $(x-1)-2(y+1)+3(z-1)=0$

b) vector form

- find TWO linearly independent vectors, that are both orthogonal to the normal vector.
    - P = (1,-1,1)
    - Q = (0,0,2)
    - R = (6,0,0)
        - these are all points on the plane
- PQ = q - p = first vector = [-1,1,1]
- PR = r - p = second vector = [5,1,-1]
    - PQ and PR are linearly independent
- use the two vectors and a point to form the vector form:

$$
x = s\begin{bmatrix}-1\\1\\1\end{bmatrix}+t\begin{bmatrix}5\\1\\-1\end{bmatrix}+\begin{bmatrix}1\\-1\\1\end{bmatrix}
$$

</aside>

![https://i.gyazo.com/0419001a53cbd45c62a8ee5290b448c4.png](https://i.gyazo.com/0419001a53cbd45c62a8ee5290b448c4.png)

![https://i.gyazo.com/4f7abe2bdaf39bcbe4690d11827ee9f8.png](https://i.gyazo.com/4f7abe2bdaf39bcbe4690d11827ee9f8.png)

When two planes (which are distinct, and do not coincide) intersect, their intersection forms a line. Take for instance these two planes:

$$
\begin{cases}x+2y-4z=3\\3x-y+2z=4\end{cases}
$$

This is a system of equations, similar to how it was done in $\R^2$. We find their solution by eliminating variables.

- subtract 3 times the FIRST equation from the SECOND.
    - $\begin{cases}x+2y-4z=3\\-7y+14z=-5\end{cases}$
- divide the SECOND by -7
    - $\begin{cases}x+2y-4z=3\\y-2z=5/7\end{cases}$
- subtract 2 times the SECOND equation from the FIRST
    - $\begin{cases}x=11/7\\y-2z=5/7\end{cases}$
- Since both systems now are independent with their variables (they share no variables between systems), we rewrite the SECOND equation such that it is in parametric form:
    - This is done by setting Z = t

$$
\begin{cases}x=11/7\\z=2t+5/7\\z=t\end{cases}=\begin{bmatrix}x\\y\\z\end{bmatrix}=t\begin{bmatrix}0\\2\\1\end{bmatrix}+\begin{bmatrix}11/7\\5/7\\0\end{bmatrix}
$$

→ This is the equation of the line that represents the intersection of both planes.

<aside>
☁️ **Plane Parallelism**

Two planes are *parallel* if they do not intersect at any point. Similar to how *lines* in $\R^3$ may not intersect, but are linearly independent, this is true for planes in higher dimensions.

We can tell if two planes *don't intersect* because their system of equations will result in a contradictory outcome.

</aside>

In the previous examples of non/intersecting planes, we can tell that they intersect through their normal vectors as well. Logically, if planes intersect, their normals are not linearly dependent.

Let's cover the idea of *cross-product*, which will be covered later, because it useful for solving problems in $\R^3$. This is because the cross-product works ONLY with $\R^3$ vectors.

$$
\overrightarrow{v}=\begin{bmatrix}v_1\\v_2\\v_3\end{bmatrix}, \overrightarrow{w}=\begin{bmatrix}w_1\\w_2\\w_3\end{bmatrix}
$$

$$
v\times w=\begin{bmatrix}v_2w_3-v_3w_2\\v_3w_1-v_1w_3\\v_1w_2-v_2w_1\end{bmatrix}
$$

Each component of the cross-product above, is a *determinant* in itself, of a 2 by 2 matrix. This cross-product is *anti-commutative*, meaning that $\overrightarrow{v}\times\overrightarrow{w}=-\overrightarrow{w}\times\overrightarrow{v}$.

Property that we observe with this fact that the cross-product is anti-commutative, is that:

<aside>
☁️ $\overrightarrow{v}\in\R^3$

$\overrightarrow{v}\times\overrightarrow{v}=\overrightarrow{0}$

</aside>

An interesting technique to understanding the result of a cross-product is done through the *right-hand rule*. 

$$
i = \begin{bmatrix}1\\0\\0\end{bmatrix}, j=\begin{bmatrix}0\\1\\0\end{bmatrix}, k=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

1) $i \times j = k$

2) $j\times k=i$

3) $k \times i = j$

![https://i.gyazo.com/e278b9148709e4d64824777fdb741b85.png](https://i.gyazo.com/e278b9148709e4d64824777fdb741b85.png)

This helps us understand that the resulting vector of a cross-product is then *orthogonal* to both *V and W*. 

<aside>
☁️ **Given the standard form of *a plane*, find the standard form**

This kind of problem utilizes the cross-product to determine a normal vector, that we indeed know for fact that this normal is orthogonal to both vectors V and W that comprise the equation of the plane.

</aside>

Similarly, if we are given three points in $\R^3$ and are meant to find the equation in standard form of the plane through these three points, we must compute the cross-product of the two vectors:

$$
PQ = q-r, PR = r-p, \overrightarrow{n}=PQ\times PR
$$

If we are asked to find the vector along the direction of a line that is defined by the intersection of two planes, then the vector must be *orthogonal to the normal direction of each of the two planes*. What this means is that the vector is in *both* of the planes, because it is orthogonal to the normals of both planes at once. Given standard forms of equations, we can find both of their normals through their coefficients and use the cross-product of those normal directions to find the vector in the *direction of the line, orthogonal to both normals*.