# Chapter 2 → Systems of Linear Equations

Algorithms for solving systems of linear equations. This is made easier by representing systems of linear equations as *matrices*. Matrices are a main device used that can help us keep track of the intermittent steps of solving systems, and gives us access to different *matrix functions* that are easier ways to solve systems.

To start, we must define the components of a system of linear equations:

# 2.1 Terminologies and Definitions

<aside>
☁️ a *real* **linear equation** in *n* variables ($x_1,x_2,...,x_n$) with coefficients expressed as:

$a_1x_1+a_2x_2+...+a_nx_n = b$

in which all *a* are *coefficients*, and *b* is the *constant term*.

when **b** is equal to 0, then the linear equation is *homogenous*, otherwise, the lin. eq. is *nonhomogenous*.

</aside>

This format of equations also support the use of different letters per *n* variable, such as *x, y, and z*. Equations in which one of the variables is subjected to a function , ie. $sin(x)$, are not linear equations.

An ordered set/tuple of real numbers *solves* an equation if the *equality holds* when each variable is substituted by each respective number in that solution set.

<aside>
☁️ **Linear solution**

$a_1s_1+a_2s_2+...+a_ns_n = b$

</aside>

In which that vector composed of those that solution set is also a solution.

**Linear systems** are those in which a *finite set* of linear equations in *n* variables is present. Variables may be presented as "unknowns", and solutions of the system are those that solve each linear equation simultaneously. Linear systems are **consistent** if they have at least one solution (≥ 1), otherwise, they are **inconsistent**. The set of all solutions of a linear system of the solution set.

→ The set of solutions for an *inconsistent system* is then the *empty set*.

![https://i.gyazo.com/c480fe07c801cc09a69f9842afed47c8.png](https://i.gyazo.com/c480fe07c801cc09a69f9842afed47c8.png)

Consider this the general form of a system of linear equations. Since between each equation there are commonalities, such as the operations  + and =, and the variables themselves, we can remove them to acheive an *augmented matrix* that represents the linear system using its coefficients.

![https://i.gyazo.com/5cbf1abaa76f0041b1aa8e3759d2289a.png](https://i.gyazo.com/5cbf1abaa76f0041b1aa8e3759d2289a.png)

This forms the **coefficient matrix** of the linear system. We further break this down into the concept of the augmented matrix, by seperating the coefficients (*a*) from the constant terms (*b*). This creates the *coefficient matrix* and the *constant vector.* This can be abbreviated into the form:

$$
\begin{bmatrix}A\;|\;\overrightarrow{b}\end{bmatrix}
$$

These above examples of matrices are special cases of a typical matrix, which is defined as:

<aside>
☁️ **Matrix**

$(m\times n)$ matrix.

![https://i.gyazo.com/819327fe0f8abce26a2e215a593742f1.png](https://i.gyazo.com/819327fe0f8abce26a2e215a593742f1.png)

has *m * n* entries of real numbers, arranged in a rectangle. $(m\times n)$ is considered the size/shape of the matrix, which contains *m* rows (horizontally) and *n* columns (vertically)

</aside>

![https://i.gyazo.com/7776a1b4511c51ab2b96ab7949831104.png](https://i.gyazo.com/7776a1b4511c51ab2b96ab7949831104.png)

→ Each row can be considered its own *row vector*, and similarly a column has its *column vector*.

→ an $n \times n$ matrix is called a *square matrix* of order *n*.

There are THREE types of *elementary operations* used in solving a linear system:

1) Multiply equation through, by non-zero constant

2) Interchange TWO equations

3) Add a constant times one *equation* to another equation

Performing operations on linear systems do not change the *set of solutions*, because multiplying and dividing an equation by the same (non-zero) constant reverses their effects. Interchanging two equations TWICE brings the system back to the original shape. Adding and subtracting the *same constant* times one equation to another reverses the effect.

IE. all three operations are reversible, as long as we use non-zero constants. Likewise, if we apply each operation in the same order we did from the system, to the solution set, it then becomes the solution to the modified set.

Thus, we can define *equivalence* of two linear systems in the same variables, if they are *related by a finite sequence of elementary operations*.

<aside>
☁️ Equivalent Systems

Have the *same set* of solutions, ie. applying the same operations in the same order to both systems yields the same solution.

</aside>

Because we have the notation of the augmented matrix, we can use that notation with the three elementary operations to solve a linear system:

<aside>
☁️ 1) multiply row by non-zero constant

- $cR_j \rarr R_j$
    - (*j*th row)

2) interchange two rows

- $R_i \leftrightarrow R_j$
    - switch rows *i* and *j*

3) add constant times one row to another

- $cR_i + R_j \rarr R_j$
</aside>

As stated before, each of these operations is reversible, so if the letter $\rho$ denotes an elementary operation, then $\rho^{-1}$ denotes the reverse operation.

When solving a system of equations, we want to get the system in the most simple state, meaning that in each equation (row vector), we want to eliminate as many variables as possible, so that we  can obtain the value of a single variable and use back-substitution of that value to find the others, so that we can construct a solution set.

This method of solving linear systems is meant to bring the matrix in to the *reduced row echelon form* (RREF).

<aside>
☁️ Row Echelon Form (REF)

Matrices are in REF if they satisfy these properties:

1) Row is not entirely composed of ZEROes, the *first* NON-ZERO number is 1 (called the *leading* 1 of the row)

2) Any rows that are entirely ZEROs, are grouped at the bottom of the matrix

3) Any two successive rows that are NOT entirely ZEROs, the leading 1 in the lower row is farther to the right than the leading 1 of the upper row.

</aside>

This is similar, but distinct to the *reduced REF*, which states that:

<aside>
☁️ REDUCED REF

Each column that has a lead 1, has zeroes elsewhere IN THE SAME COLUMN.

</aside>

![https://i.gyazo.com/d45d13f07d7f6b165ccd0d2d150a4419.png](https://i.gyazo.com/d45d13f07d7f6b165ccd0d2d150a4419.png)

![https://i.gyazo.com/12845530bf6487f76511193c5ef4573e.png](https://i.gyazo.com/12845530bf6487f76511193c5ef4573e.png)

→ Matrices  that are in RREF must be in REF, but not the other way round.

→ It can be the case where a matrix does not need to have ONLY 1's to be in RREF, the stipulation just means that in every column that has a leading 1 in a row, all other rows must have a 0 in that same column.

![https://i.gyazo.com/4ca52c65ad9522a9e5aa5c37ebeae796.png](https://i.gyazo.com/4ca52c65ad9522a9e5aa5c37ebeae796.png)

Where any * can be substituted for any Real number, this matrix is in REF

![https://i.gyazo.com/f506fdfc8cc1713a2a9fdfd05cdc5a5c.png](https://i.gyazo.com/f506fdfc8cc1713a2a9fdfd05cdc5a5c.png)

Where any * can be substituted for any Real number, this matrix is in RREF

Through an example, we can see that certain configurations of RREF yield a *unique* solution to the system, ie. there is only 1 solution. This is when every equation/row has only a single leading 1, which pairs to the constant, giving us 1 variable per equation, and thus 1 solution (the only solution).

We can use this idea to build onto the concept of the augmented matrix $\begin{bmatrix}A\;|\;\overrightarrow{b}\end{bmatrix}$. If A is a matrix of size $m \times n$ in REF, then its augmented matrix has variables corresponding to the leading 1s in A, they are called *leading variables*. Variables that are not *leading* are called *free variables*.

<aside>
☁️ R/REF and Consistency

We can tell a system is *inconsistent* if in REF/RREF one of the equations equations 0 to a $\R$, such as $0 = 2$.

</aside>

When solving a linear system, we can use *free variables* as *parameters*.

Take for example this system in RREF. Its last row equates to $0x+0y+0z=0$, meaning that we can ignore it. Thus, the remaining two equations equate to:

$$
\begin{cases}x+3z=2\\y-4z=1\end{cases}
$$

![https://i.gyazo.com/4da4dc605230c8025fc6c30bb3214dd8.png](https://i.gyazo.com/4da4dc605230c8025fc6c30bb3214dd8.png)

We can see (even in RREF form) that variables X and Y are the *leading variables*, and we can solve for each, in terms of the remaining *free variable*, Z.

$$
\begin{cases}x=2-3z\\y=1+4z\end{cases}
$$

Because Z is a free variable, we can parametrize it to generalize the system, which gives us a *vector equation* of a line:

![https://i.gyazo.com/620a8fe7f9dc2cdfcb728b4c8d65a7b2.png](https://i.gyazo.com/620a8fe7f9dc2cdfcb728b4c8d65a7b2.png)

→ Notice, that the solution to this system is not a *point/vector,* because we are considering the intersection between 3 planes (in standard form). This is one form of a solution of the intersection of 3 planes, because there are many ways that 3 planes can intersect the other two.

![https://i.gyazo.com/b35bc59708d93f7bc7a87b3f9e027ce5.png](https://i.gyazo.com/b35bc59708d93f7bc7a87b3f9e027ce5.png)

→ We can see that the solution previously is a *line*, meaning that all three planes meet at the same line.

<aside>
☁️ General Solution

To a linear system with *infinitely* many solutions, is a set of equations with parameters from which *all solutions* can be obtained, by assigning values to the parameters. For example, the previous solution has a general solution with ONE parameter.

</aside>

This leads us to further extrapolate on the situation of the solution set, and how it relates to a system with *n* unknowns:

<aside>
☁️ Solution Set of a Linear System (RREF)

For a linear system with *n* unknowns, whose *augmented matrix* is in RREF, EXACTLY ONE of the three must be TRUE:

1) linear system has NO solution if the augmented matrix has a *leading 1* in the constant column.

2) linear system has EXACTLY ONE solution if the augmented matrix has *n* leading 1s, and they are ALL in the coefficient matrix (R)

3) linear system has INFINITELY many solutions if the number of leading 1s in the augmented matrix is LESS THAN *N*, and they are all in coefficient matrix R

- this means that the number of free variables is also the number of parameters in the general solution, which is *n - #leading 1's*.
</aside>

![https://i.gyazo.com/c7a72d394c9b0c13fc044022d78198ef.png](https://i.gyazo.com/c7a72d394c9b0c13fc044022d78198ef.png)

![https://i.gyazo.com/0a7733c520fff9d58208e7b4fd14ee7e.png](https://i.gyazo.com/0a7733c520fff9d58208e7b4fd14ee7e.png)

![https://i.gyazo.com/7534d1905aace2a33cb170740faba53f.png](https://i.gyazo.com/7534d1905aace2a33cb170740faba53f.png)

# 2.2 Gaussian Elimination

To solve a linear system, we just need to convert it to an equivalent one, such that its augmented matrix is present in RREF. Here we can define what it means be to *row equivalent*:

<aside>
☁️ Row Equivalent Matrices

Two matrices (A, B) are *row equivalent* if B may be obtained from A, by a finite amount of elementary operations. If A if row equiv. to a matrix E, which is in REF, then E is the REF of A. If E is in RREF, then E is an RREF of A.

</aside>

Linear systems of *m* equations (rows) in *n* unknowns are equivalent iff. their augmented matrices are row equivalent, and if they are, they have the same set of solutions.

Here we learn an algorithm, called the **Gauss-Jordan Elimination Algorithm** that can be used to reduce *any* matrix to its RREF. Given this system, of 3 equations (m) in 5 unknowns (n).

![https://i.gyazo.com/14c7498ddf6f633297452c30fefbe28e.png](https://i.gyazo.com/14c7498ddf6f633297452c30fefbe28e.png)

<aside>
☁️ Gauss-Jordan Elimination

1) Locate the leftmost col. which *does not contain ONLY zeroes*

![https://i.gyazo.com/145ef1e12e5558f1c18bb8d6c6f3d607.png](https://i.gyazo.com/145ef1e12e5558f1c18bb8d6c6f3d607.png)

2) Interchange top row with another, to bring the *first non-zero entry* to the top:

![https://i.gyazo.com/67af8f0cc76ce9a2408151e7648e4b83.png](https://i.gyazo.com/67af8f0cc76ce9a2408151e7648e4b83.png)

3) Now we have a row which does *not* have a zero as its first entry as 0, call this integer *a*. Multiply the *first row* by $\frac{1}{a}$, which will give us a leading 1 in the first row. In this example, we divide by 1/2.

![https://i.gyazo.com/c275e1d1a15500424b2d6cb68ca0be49.png](https://i.gyazo.com/c275e1d1a15500424b2d6cb68ca0be49.png)

4) Now add multiples of the top row to the below rows such that the first column contains only that first leading 1 in it.

![https://i.gyazo.com/19525275ff5c2436948a50a1d3601ca5.png](https://i.gyazo.com/19525275ff5c2436948a50a1d3601ca5.png)

5) Repeat steps 1 to 4 (recursively downwards) through the rest of the matrix, column-by-column to arrive at that matrix's RREF.

The trick here is to ignore the first row every iteration, only considering the rows below the ones we complete. This essentially sub-divides the matrix into submatrices.

Once we have proceeded all the way downwards, and have no rows left in the submatrix, we have the matrix in REF. This previous part is called the *Gaussian Elimination*, and brings the matrix into REF. In order to bring this REF into RREF, we continue with the *Gauss-Jordan Elimination* in step 6.

![https://i.gyazo.com/5b5a9fd8b07d707f3da7eca65bbbb425.png](https://i.gyazo.com/5b5a9fd8b07d707f3da7eca65bbbb425.png)

6) Working from the *last leading 1 (bottom)* upwards, add multiples of each row containing a leading 1 to the rows above, to make each column contain only 1 non-zero integer, which is a leading 1.

This is done in order to eliminate all numbers above the leading 1's.

So if the last row (3rd) has two variables (as above, 6 and -7), then we add multiples of the last row to the 2nd, then the 1st row to eliminate those integers 6 and -7.

We then move upwards 1 row, to the 2nd row and multiply 5 times the 2nd row and add that to the first to eliminate that -5. This brings the matrix into RREF.

</aside>

We can use algorithms in general to create *constructive proofs* of existence theorems. This Gauss-Jordan algorithm thus is used to prove the existence of an RREF of any matrix, because this algorithm will work on any matrix.

- Pseudo-code for this Algorithm (NOT COMPLETE)
    
    ```python
    let m = input('m: ')
    let n = input('n: ')
    let mn = [] #2d array that holds arrays, each array being an equation
    for(int i = 0; i < m; i++){
    	print('M['+i+']')
    	let currentm = [] #a row is an equation
    	for(int j = 0; j < n; j++){
    			currentm[j] = input('N['+j+']: ') #get each coefficient/constant
    	}
    
    	mn.push(currentm) #add the gathered equation to the total array of equations
    }
    
    #gaussian elimination
    
    #gauss-jordan elimination
    ```
    

Here is a dumbed-down version of the WHOLE process:

1) considering all rows, choose the leftmost, first row (from the top) that does not have only 0's in its column

2) change that row with the first

3) multiply the inverse of that first digit through the entire row, this will give us a row with a leading 1 in the first column

4) multiply multiples of that first row to the rows below it, such that each digit in that first column become zero

5) rinse and repeat 1 - 4, such that we create a submatrix each time by ignoring the rows we've managed to already creating leading 1's within. do this until we have finished doing so on the last row, and there is no more submatrix to consider. this means that we have brought the original system/matrix into REF. This process eliminates all numbers BELOW each leading 1.

6) once the matrix is in REF, we continue using Gauss-Jordan to eliminate all 0's ABOVE each leading 1, which will efffectively put the matrix into RREF. To start, use the last (bottom) equation, considering the last leading 1. Multiply an integer times that row, and add to each row above it, such that that column with the leading 1 has 0's above it. Repeat this step by moving upwards, to the next leading 1, eliminating each column's digits that aren't leading 1s.

7) Once we have reached the first row, working from the bottom upwards in step 6), then the matrix is then in RREF.

One note about notation is that we can multiply an integer times one row, and add it to another, replacing the 2nd equation with that new one. We cannot do this when we are multiplying *both equations*, only when we multiply one. This is because it is not an elementary operation when done multiplying both equations by a scalar, so we must seperate the multiplication of the second into its own step. If two steps are independent, that is they don't involve the same rows, we can do them at the same time.

Here are some facts about Matrices and their Row Echelon Forms:

<aside>
☁️ Row Echelon Forms

Given A, be a matrix, then these are all true:

a) A has a *unique* RREF

b) A may have ≥ one REF

c) All REFs of A have the *same number of non-zero rows* (if any). Leading 1's of those rows are *always* in the same position.

</aside>

<aside>
☁️ Pivot Columns

A is an $m \times n$ matrix. The positions of leading 1's in any of its REF are called the *pivot positions* of A. Columns containing a pivot position are called *pivot columns*.

</aside>

<aside>
☁️ Rank

A is an $m \times n$ matrix. The *Rank* of A → rank(A) = # of leading 1's in A's RREF.

</aside>

We have a lemma that states that:

<aside>
☁️ Rank Lemma

A is $m \times n$, then $rank(A) \leq min(m,n)$.

</aside>

This is trivially proven through the fact that there cannot be more leading 1's in the RREF than the number of rows or columns of A. Another interesting lemma is that:

<aside>
☁️ Equal Ranks

Row equivalent Matrices have the *same rank*.

</aside>

This is because elements that are row equivalent are obtainable through elementary operations from one into another, so we know that row equivalent matrices have the same RREF, which implies they have the same rank.

We have some theorems that comapre the rank of a matrix to the number of unknowns, and some patterns emerge with how many solutions systems possess given rank and unknowns:

<aside>
☁️ Rank vs. #Unknowns

Given a linear system in *n* unknowns, the augmented matrix $\begin{bmatrix}A\;|\;\overrightarrow{b}\end{bmatrix}$ must have exactly ONE statement that agrees:

a) No solution, if $rank(A|b) > rank(A)$

b) 1 Solution, if $rank(A|b) = rank(A) = n$

c) $\infin$  Solutions, if $rank(A|b) = rank(A) < n$

- this means that the number of *parameters* in the general solution is $n - rank(A)$

The linear system is *consistent* iff. $rank(A|b) = rank(A)$

</aside>

In order to find out how many solutions a system has, we can find the REF of any matrix and use this theorem to determine *how many* solutions it can have. This is similar to the *discriminant* of the quadratic formula, which can tell how many intersections a parabola has with a line (2, 1, or no $\R$ solutions).

There are also some patterns that deal with the rank and the number of rows, since we know that the number of rows is the same as the number of equations in the system.

<aside>
☁️ Rank vs. #Rows (Equations)

A is a matrix of $m \times n$.

a) If rank(A) = m, then for any constant vector, the system with the augmented matrix (A|b) is consistent

b) if rank(A) < m, then both are true:

i) there is constant vector *c* such that the linear system with augmented matrix (A|c) *is* consistent

ii) there is constant vector *d* such that the linear system with augmented matrix (A|d) *is not* consistent

... ie. there are vectors that can make the system either consistent or inconsistent

</aside>

Just like how typical linear equations can be homogenous, then a homogenous linear system requires that the constant vector of that matrix be the 0 vector. Because an obvious solution to the system is then the zero-vector for each row, meaning that it requires *n* zeros.

→ this is because when all equations in the system equate to zero, the *trivial* solution is then the easiest solution, which is just substituting all variables/unknowns to be 0. 

Solutions that are not the zero-vector are called *nontrivial* solutions.

In fact, because of knowing this idea that homogenous linear systems exist, we can use the theorem:

<aside>
☁️ Homogenous Linear Systems

with *n* unknown, have *n - r* free variables, if the coefficient matrix (A) has rank equal to *r*. It has a unique solution iff. rank(A) = *n.*

</aside>

It then follows that:

<aside>
☁️ Homogenous Linear systems with *m* equations, each in *n* unknowns, has non-trivial solutions if $m < n$.

</aside>

→ This is because the system will have a free variable, which introduces non-trivial solutions.

<aside>
⭐ Let's bring back to the concept of linear systems, transformations. The rank of a linear system corresponds to its *output dimension*, ie. if A matrix is *full rank*, this means that whatever it tranforms, stays in the same dimension. You can't *add* a dimension by a matrix-product tranformation, you can only stay the same, or reduce the dimension.

Row reduction is a way of reducing the *contribution* of other equations in the same axis. In the problem space, we would a row that has an easy division by some constant, to achieve the smallest unit in that direction or axis, to 1. Then, because we know this has a contribution, reducing other rows, in this axis, would mean that we are eliminating the contribution of the other spaces, finding a *basis* to this linear system, finding the solution that satisfies all spaces, or finding the single space (point, line, plane, cube, etc.) that would be created by the intersection of these system spaces. 

</aside>