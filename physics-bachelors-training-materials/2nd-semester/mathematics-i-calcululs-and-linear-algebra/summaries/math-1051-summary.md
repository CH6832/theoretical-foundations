# Summary of MATH3401 Lecture Notes with Explanations

## Table of Contents
1. [Complex Numbers](#complex-numbers)
   - [Notation](#notation)
   - [Polar Form](#polar-form)
   - [Euler's Formula](#eulers-formula)
2. [Vectors](#vectors)
   - [Revision](#revision)
   - [Vector Operations](#vector-operations)
   - [Applications](#applications)
3. [Matrices and Linear Transformations](#matrices-and-linear-transformations)
   - [2 x 2 Matrices](#2--2-matrices)
   - [Transformations of the Plane](#transformations-of-the-plane)
   - [Matrix Multiplication](#matrix-multiplication)
   - [Inverse of a Matrix](#inverse-of-a-matrix)
4. [Vector Spaces](#vector-spaces)
   - [Linear Combinations](#linear-combinations)
   - [Linear Independence](#linear-independence)
   - [Bases and Dimension](#bases-and-dimension)
   - [Subspaces](#subspaces)
5. [Inverses](#inverses)
   - [The Identity Matrix](#the-identity-matrix)
   - [Invertible Matrices](#invertible-matrices)
   - [Finding Inverses](#finding-inverses)
6. [Gaussian Elimination](#gaussian-elimination)
   - [Simultaneous Equations](#simultaneous-equations)
   - [Gaussian Elimination](#gaussian-elimination-1)
   - [Applications](#applications-1)
7. [Determinants](#determinants)
   - [Definition: Determinant](#definition-determinant)
   - [Properties of Determinants](#properties-of-determinants)
   - [Applications](#applications-2)
8. [Eigenvalues and Eigenvectors](#eigenvalues-and-eigenvectors)
   - [Eigenvalues](#eigenvalues)
   - [How to Find Eigenvalues](#how-to-find-eigenvalues)
   - [Applications](#applications-3)
9. [Limits and Continuity](#limits-and-continuity)
   - [Limits](#limits)
   - [Continuity](#continuity)
10. [Derivatives](#derivatives)
    - [Definition of the Derivative](#definition-of-the-derivative)
    - [Applications](#applications-4)
11. [Integration](#integration)
    - [The Fundamental Theorem of Calculus](#the-fundamental-theorem-of-calculus)
    - [Applications](#applications-5)
12. [Series](#series)
    - [Convergence of Series](#convergence-of-series)
    - [Types of Series](#types-of-series)

## Complex Numbers

### Notation
Complex numbers are of the form $( z = x + iy )$, where $( x )$ and $( y )$ are real numbers, and $( i )$ is the imaginary unit with the property $( i^2 = -1 )$. Here:
- **Real part**: $( \text{Re}(z) = x )$
- **Imaginary part**: $( \text{Im}(z) = y )$

#### Example:
For $( z = 3 + 4i )$, the real part is 3, and the imaginary part is 4.

### Polar Form
In polar form, a complex number $( z )$ is represented as:

$z = r(\cos \theta + i \sin \theta)$

where:
- $( r = |z| )$ is the modulus or magnitude, calculated as $( r = \sqrt{x^2 + y^2} )$.
- $( \theta )$ is the argument or angle, given by $( \theta = \arctan\left(\frac{y}{x}\right) )$ if $( x \neq 0 )$.

#### Example:
For $( z = 3 + 4i )$, the modulus $( r = \sqrt{3^2 + 4^2} = 5 )$ and the argument $( \theta = \arctan\left(\frac{4}{3}\right) )$.

### Euler's Formula
Euler's formula is:

$e^{i\theta} = \cos \theta + i \sin \theta$

This formula connects complex exponentials with trigonometric functions. In polar form:

$z = re^{i\theta}$

#### Example:
For $( \theta = \frac{\pi}{4} )$, $( e^{i\pi/4} = \cos \frac{\pi}{4} + i \sin \frac{\pi}{4} = \frac{\sqrt{2}}{2} + i \frac{\sqrt{2}}{2} )$.

## Vectors

### Revision
Vectors are quantities having both magnitude and direction. In $( \mathbb{R}^n )$, a vector $( \mathbf{v} )$ is represented as $( \mathbf{v} = (v_1, v_2, \dots, v_n) )$.

- **Magnitude (or norm)**: $( |\mathbf{v}| = \sqrt{v_1^2 + v_2^2 + \dots + v_n^2} )$

#### Example:
For $( \mathbf{v} = (3, 4) )$, $( |\mathbf{v}| = \sqrt{3^2 + 4^2} = 5 )$.

### Vector Operations
Vectors can be added and scaled:
- **Addition**: $( \mathbf{u} + \mathbf{v} = (u_1 + v_1, u_2 + v_2, \dots, u_n + v_n) )$
- **Scalar multiplication**: $( c\mathbf{v} = (cv_1, cv_2, \dots, cv_n) )$

#### Example:
If $( \mathbf{u} = (1, 2) )$ and $( \mathbf{v} = (3, 4) )$, then $( \mathbf{u} + \mathbf{v} = (4, 6) )$.

### Applications
Vectors are used in various applications such as physics (force, velocity) and computer graphics (image transformations).

## Matrices and Linear Transformations

### 2 × 2 Matrices
A $( 2 \times 2 )$ matrix is:
$A = \begin{pmatrix}
a & b \\
c & d
\end{pmatrix}$
It represents a linear transformation in a 2-dimensional plane.

#### Example:
For $( A = \begin{pmatrix}
2 & 1 \\
1 & 3
\end{pmatrix} )$, this matrix can scale and rotate vectors in 2D.

### Transformations of the Plane
The matrix $( A )$ transforms a vector $( \mathbf{v} )$ as follows:
$\mathbf{v}' = A\mathbf{v}$

#### Example:
If $( \mathbf{v} = \begin{pmatrix}
1 \\
2
\end{pmatrix} )$ and $( A = \begin{pmatrix}
2 & 0 \\
0 & 3
\end{pmatrix} )$, then $( \mathbf{v}' = \begin{pmatrix}
2 \\
6
\end{pmatrix} )$, which scales $( \mathbf{v} )$ by 2 and 3 in respective dimensions.

### Matrix Multiplication
Matrix multiplication is defined as:
$(AB)_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj}$
where $( A )$ is $( m \times n )$ and $( B )$ is $( n \times p )$.

#### Example:
For $( A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix} )$ and $( B = \begin{pmatrix}
2 & 0 \\
1 & 3
\end{pmatrix} )$:
$AB = \begin{pmatrix}
1 \cdot 2 + 2 \cdot 1 & 1 \cdot 0 + 2 \cdot 3 \\
3 \cdot 2 + 4 \cdot 1 & 3 \cdot 0 + 4 \cdot 3
\end{pmatrix} = \begin{pmatrix}
4 & 6 \\
10 & 12
\end{pmatrix}$

### Inverse of a Matrix
A matrix $( A )$ is invertible if there exists $( B )$ such that:
$AB = BA = I$
where $( I )$ is the identity matrix.

#### Finding Inverses
For a $( 2 \times 2 )$ matrix:
$A = \begin{pmatrix}
a & b \\
c & d
\end{pmatrix}$
the inverse is:
$A^{-1} = \frac{1}{ad - bc} \begin{pmatrix}
d & -b \\
-c & a
\end{pmatrix}$

#### Example:
For $( A = \begin{pmatrix}
4 & 3 \\
2 & 1
\end{pmatrix} )$:
$\text{det}(A) = (4 \cdot 1 - 3 \cdot 2) = -2$


$A^{-1} = \frac{1}{-2} \begin{pmatrix}
1 & -3 \\
-2 & 4
\end{pmatrix} = \begin{pmatrix}
-0.5 & 1.5 \\
1 & -2
\end{pmatrix}$

## Vector Spaces

### Linear Combinations
A vector $( \mathbf{v} )$ is a linear combination of vectors $( \mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k )$ if:
$\mathbf{v} = c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \dots + c_k\mathbf{v}_k$

#### Example:
In $( \mathbb{R}^2 )$, if $( \mathbf{v}_1 = \begin{pmatrix}
1 \\
0
\end{pmatrix} )$ and $( \mathbf{v}_2 = \begin{pmatrix}
0 \\
1
\end{pmatrix} )$, then $( \mathbf{v} = 2\mathbf{v}_1 + 3\mathbf{v}_2 )$ represents the vector $( \begin{pmatrix}
2 \\
3
\end{pmatrix} )$.

### Linear Independence
Vectors $( \mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k )$ are linearly independent if:
$c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \dots + c_k\mathbf{v}_k = \mathbf{0}$
implies $( c_1 = c_2 = \dots = c_k = 0 )$.

#### Example:
In $( \mathbb{R}^2 )$, the vectors $( \mathbf{v}_1 = \begin{pmatrix}
1 \\
0
\end{pmatrix} )$ and $( \mathbf{v}_2 = \begin{pmatrix}
0 \\
1
\end{pmatrix} )$ are linearly independent because no non-trivial combination gives the zero vector.

### Bases and Dimension
A basis of a vector space $( V )$ is a set of linearly independent vectors that span $( V )$. The dimension of $( V )$ is the number of vectors in any basis.

#### Example:
In $( \mathbb{R}^3 )$, a standard basis is $( \mathbf{e}_1 = \begin{pmatrix}
1 \\
0 \\
0
\end{pmatrix} )$, $( \mathbf{e}_2 = \begin{pmatrix}
0 \\
1 \\
0
\end{pmatrix} )$, and $( \mathbf{e}_3 = \begin{pmatrix}
0 \\
0 \\
1
\end{pmatrix} )$. The dimension is 3.

### Subspaces
A subspace is a set of vectors that forms a vector space under the same operations as the original space.

#### Example:
The set of all vectors of the form $( \begin{pmatrix}
x \\
0 \\
0
\end{pmatrix} )$ in $( \mathbb{R}^3 )$ forms a subspace of $( \mathbb{R}^3 )$, representing a line along the x-axis.

## Inverses

### The Identity Matrix
The identity matrix $( I )$ is:
$I = \begin{pmatrix}
1 & 0 & \dots & 0 \\
0 & 1 & \dots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & 1
\end{pmatrix}$
It acts as the multiplicative identity for matrices.

### Invertible Matrices
A matrix $( A )$ is invertible if there exists a matrix $( B )$ such that:
$AB = BA = I$
where $( I )$ is the identity matrix.

#### Example:
For $( A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix} )$, its inverse (if it exists) satisfies $( A A^{-1} = I )$.

### Finding Inverses
The inverse of a matrix can be computed using various methods such as:
- **Gauss-Jordan elimination**
- **Adjugate method**

## Gaussian Elimination

### Simultaneous Equations
A system of linear equations can be written as:
$A\mathbf{x} = \mathbf{b}$
where $( A )$ is the coefficient matrix, $( \mathbf{x} )$ is the vector of variables, and $( \mathbf{b} )$ is the constants vector.

#### Example:
For:
$\begin{cases}
x + y = 2 \\
2x - y = 1
\end{cases}$
the augmented matrix is:
$\left[\begin{array}{cc|c}
1 & 1 & 2 \\
2 & -1 & 1
\end{array}\right]$

### Gaussian Elimination
Gaussian elimination involves row operations to convert the augmented matrix to row echelon form (REF), from which solutions are found by back-substitution.

#### Example:
To solve:
$\begin{cases}
2x + 3y = 5 \\
4x - y = 7
\end{cases}$
the augmented matrix is:
$\left[\begin{array}{cc|c}
2 & 3 & 5 \\
4 & -1 & 7
\end{array}\right]$
Applying row operations:
$\left[\begin{array}{cc|c}
2 & 3 & 5 \\
0 & -7 & -3
\end{array}\right]$
leads to solutions by back-substitution.

### Applications
Gaussian elimination is used in various fields including engineering, economics, and computer science for solving systems of linear equations.

## Determinants

### Definition: Determinant
The determinant of a matrix provides a scalar value that can be computed using cofactor expansion. For a $( 2 \times 2 )$ matrix:

$\text{det}(A) = ad - bc$

#### Example:
For:

$A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}$

$\text{det}(A) = (1 \cdot 4 - 2 \cdot 3) = -2$

### Properties of Determinants
- **Product property**: $( \text{det}(AB) = \text{det}(A) \cdot \text{det}(B) )$
- **Invertibility**: A matrix is invertible if and only if its determinant is non-zero.
- **Transpose property**: $( \text{det}(A^T) = \text{det}(A) )$

### Applications
Determinants are used in solving linear systems, finding areas and volumes, and understanding matrix invertibility.

## Eigenvalues and Eigenvectors

### Eigenvalues
An eigenvalue $( \lambda )$ of a matrix $( A )$ satisfies:

$A\mathbf{v} = \lambda\mathbf{v}$

where $( \mathbf{v} )$ is the eigenvector associated with $( \lambda )$.

#### Example:
For $( A = \begin{pmatrix}
2 & 1 \\
1 & 2
\end{pmatrix} )$, solving $( \text{det}(A - \lambda I) = 0 )$ yields eigenvalues $( \lambda = 1 )$ and $( \lambda = 3 )$.

### How to Find Eigenvalues
Find eigenvalues by solving the characteristic polynomial:
$\text{det}(A - \lambda I) = 0$

#### Example:
For $( A = \begin{pmatrix}
4 & 1 \\
2 & 3
\end{pmatrix} )$:
$\text{det}(A - \lambda I) = \text{det}\begin{pmatrix}
4 - \lambda & 1 \\
2 & 3 - \lambda
\end{pmatrix} = (4 - \lambda)(3 - \lambda) - 2$
Solving $( \lambda^2 - 7\lambda + 10 = 0 )$ yields eigenvalues $( \lambda = 2 )$ and $( \lambda = 5 )$.

### Applications
Eigenvalues and eigenvectors are used in systems stability analysis, quantum mechanics, and principal component analysis (PCA) in statistics.

## Limits and Continuity

### Limits
The limit of a function $( f(x) )$ as $( x )$ approaches $( a )$ is:

$\lim_{x \to a} f(x) = L$

if $( f(x) )$ gets arbitrarily close to $( L )$ as $( x )$ gets close to $( a )$.

#### Example:
For $( f(x) = x^2 )$, $( \lim_{x \to 2} f(x) = 4 )$.

### Continuity
A function $( f(x) )$ is continuous at $( a )$ if:

$\lim_{x \to a} f(x) = f(a)$

This implies no discontinuities at $( a )$.

#### Example:
For $( f(x) = \sin x )$, $( \sin x )$ is continuous everywhere.

## Derivatives

### Definition of the Der

ivative
The derivative of $( f(x) )$ at $( x )$ is:

$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$

It represents the rate of change of $( f )$ with respect to $( x )$.

#### Example:
For $( f(x) = x^2 )$, $( f'(x) = 2x )$.

### Applications
Derivatives are used in optimization problems, motion analysis, and curve sketching.

## Integration

### The Fundamental Theorem of Calculus
The Fundamental Theorem states that:
1. If $( F )$ is an antiderivative of $( f )$, then:
   
   $\int_a^b f(x) \, dx = F(b) - F(a)$

2. If $( f )$ is continuous on $([a, b])$, then:
   
   $\frac{d}{dx} \left(\int_a^x f(t) \, dt\right) = f(x)$

#### Example:
For $( f(x) = x^2 )$, the integral is:

$\int_1^3 x^2 \, dx = \left[\frac{x^3}{3}\right]_1^3 = \frac{27}{3} - \frac{1}{3} = \frac{26}{3}$

### Applications
Integration is used in finding areas under curves, volumes of solids of revolution, and solving differential equations.

## Series

### Convergence of Series
A series $( \sum a_n )$ converges if the sequence of partial sums converges to a limit. 

#### Example:
The geometric series $( \sum_{n=0}^{\infty} r^n )$ converges to $( \frac{1}{1-r} )$ if $( |r| < 1 )$.

### Types of Series
- **Arithmetic Series**: Sum of terms in an arithmetic sequence.
- **Geometric Series**: Sum of terms in a geometric sequence.
- **Taylor Series**: Expands functions into infinite sums of their derivatives.

#### Example:
The Taylor series for $( e^x )$ is:

$e^x = \sum_{n=0}^{\infty} \frac{x^n}{n!}$
