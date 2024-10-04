# Table of Contents

- [Preface](#preface)
- [Part 1: Vectors](#part-1-vectors)
  - [Chapter 1: Vectors](#chapter-1-vectors)
  - [Chapter 2: Linear Functions](#chapter-2-linear-functions)
  - [Chapter 3: Norm and Distance](#chapter-3-norm-and-distance)
  - [Chapter 4: Clustering](#chapter-4-clustering)
  - [Chapter 5: Linear Independence](#chapter-5-linear-independence)
- [Part 2: Matrices](#part-2-matrices)
  - [Chapter 1: Matrices](#chapter-1-matrices)
  - [Chapter 2: Matrix Examples](#chapter-2-matrix-examples)
  - [Chapter 3: Linear Equations](#chapter-3-linear-equations)
  - [Chapter 4: Linear Dynamical Systems](#chapter-4-linear-dynamical-systems)
  - [Chapter 5: Matrix Multiplication](#chapter-5-matrix-multiplication)
  - [Chapter 6: Matrix Inverses](#chapter-6-matrix-inverses)
- [Part 3: Least Squares](#part-3-least-squares)
  - [Chapter 1: Least Squares](#chapter-1-least-squares)
  - [Chapter 2: Least Squares Data Fitting](#chapter-2-least-squares-data-fitting)
  - [Chapter 3: Least Squares Classification](#chapter-3-least-squares-classification)
  - [Chapter 4: Multi-Objective Least Squares](#chapter-4-multi-objective-least-squares)
  - [Chapter 5: Constrained Least Squares](#chapter-5-constrained-least-squares)
  - [Chapter 6: Constrained Least Squares Applications](#chapter-6-constrained-least-squares-applications)
  - [Chapter 7: Statistical Estimation](#chapter-7-statistical-estimation)
  - [Chapter 8: Convex Optimization](#chapter-8-convex-optimization)
- [Appendix](#appendix)
  - [Mathematical Notations](#mathematical-notations)
  - [References](#references)

## Preface

*The preface provides an overview of the book, its objectives, and its target audience. It also explains the structure of the content and how to best utilize the book.*

Linear algebra is a fundamental tool in mathematics, engineering, data science, and machine learning. This book aims to present the core concepts of vectors, matrices, and least squares in a clear and practical manner. The target audience includes undergraduate students, professionals looking to refresh their knowledge, and individuals interested in machine learning and optimization techniques.

## Part 1: Vectors

### Chapter 1: Vectors

#### Introduction to Vectors

Vectors represent quantities that have both magnitude and direction. In physics, vectors are used to represent forces, velocities, and other directional quantities. In machine learning, vectors are often used to represent features of data points.

#### Vector Addition

Vectors can also be represented geometrically. The sum of two vectors $(\mathbf{v} + \mathbf{w})$ can be visualized as placing the tail of vector $\mathbf{w}$ at the head of vector $\mathbf{v}$.

#### Scalar-Vector Multiplication

Scaling a vector by a positive scalar $c$ increases its magnitude, while scaling by a negative scalar $c$ flips its direction.

#### Inner Product

The inner product can be used to find the angle $\theta$ between two vectors:
$\mathbf{v} \cdot \mathbf{w} = \|\mathbf{v}\| \|\mathbf{w}\| \cos(\theta)$
When $\mathbf{v} \cdot \mathbf{w} = 0$, the vectors are orthogonal (perpendicular).

#### Vector Projections

The projection of a vector $\mathbf{v}$ onto another vector $\mathbf{w}$ is given by:
$\text{proj}_{\mathbf{w}}(\mathbf{v}) = \frac{\mathbf{v} \cdot \mathbf{w}}{\mathbf{w} \cdot \mathbf{w}} \mathbf{w}$
This is useful in applications like least squares fitting, where we project data points onto a line or plane.

### Chapter 2: Linear Functions

#### Linear Functions

Linear functions map vectors to scalars or other vectors. These functions are called "linear" because they satisfy the properties of additivity and homogeneity: $f(\mathbf{x} + \mathbf{y}) = f(\mathbf{x}) + f(\mathbf{y})$ and $f(c \mathbf{x}) = c f(\mathbf{x})$.

#### Affine Functions

Affine functions are an extension of linear functions, including a bias term:
$f(\mathbf{x}) = \mathbf{a}^\top \mathbf{x} + b$
These are common in linear regression and machine learning models.

#### Exercises

1. Show that the function $f(\mathbf{x}) = 3x_1 + 4x_2 + 2$ is affine but not linear.

### Chapter 3: Norm and Distance

#### Norm

Other common norms include the $1$-norm (Manhattan distance) and infinity norm:
$\|\mathbf{x}\|_1 = \sum_{i=1}^{n} |x_i|
\quad \text{and} \quad
\|\mathbf{x}\|_\infty = \max_i |x_i|$
Each norm has specific use cases, like the $1$-norm for sparse representations.

#### Distance

The Euclidean distance is widely used in clustering, classification, and nearest neighbor algorithms. However, in high-dimensional spaces, alternative metrics like cosine similarity may be more effective.

#### Exercises

1. Compute the $1$-norm, $2$-norm, and $\infty$-norm for the vector $\mathbf{v} = \begin{bmatrix} 3 \\ -4 \\ 1 \end{bmatrix}$.

### Chapter 4: Clustering

#### Clustering

Clustering involves grouping data points into subsets (clusters) where points in the same group are more similar to each other than to those in other groups.

#### A Clustering Objective

Common clustering objective functions include minimizing within-cluster variance and maximizing between-cluster separation. These objectives are used in algorithms like k-means and hierarchical clustering.

#### The k-means Algorithm

K-means is a popular algorithm that partitions data into $k$ clusters by minimizing the within-cluster sum of squares:
$\sum_{i=1}^{k} \sum_{\mathbf{x} \in C_i} \|\mathbf{x} - \mathbf{c}_i\|_2^2$
where $C_i$ is the set of points in cluster $i$ and $\mathbf{c}_i$ is the centroid of cluster $i$.

#### Exercises

1. Implement the k-means algorithm on a small dataset and visualize the clusters.

### Chapter 5: Linear Independence

#### Linear Dependence and Independence

Vectors $\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_k$ are linearly dependent if there exist scalars $c_1, c_2, \dots, c_k$ (not all zero) such that:
$c_1 \mathbf{v}_1 + c_2 \mathbf{v}_2 + \dots + c_k \mathbf{v}_k = 0$
Otherwise, they are linearly independent.

#### Basis and Dimension

A basis for a vector space is a set of linearly independent vectors that span the space. The number of vectors in the basis is the dimension of the space.

## Part 2: Matrices

### Chapter 1: Matrices

#### Matrix Operations

Matrix addition and scalar multiplication are defined element-wise. Matrix multiplication is defined as:
$(\mathbf{A} \mathbf{B})_{ij} = \sum_{k} A_{ik} B_{kj}$
Matrix multiplication is not commutative, i.e., $\mathbf{A} \mathbf{B} \neq \mathbf{B} \mathbf{A}$ in general.

#### Matrix Transpose

The transpose of a matrix $\mathbf{A}$, denoted $\mathbf{A}^\top$, is obtained by flipping it over its diagonal. That is, $(\mathbf{A}^\top)_{ij} = \mathbf{A}_{ji}$.

### Chapter 2: Matrix Examples

#### Symmetric Matrix

A matrix $\mathbf{A}$ is symmetric if $\mathbf{A} = \mathbf{A}^\top$. Symmetric matrices have real eigenvalues and orthogonal eigenvectors.

### Chapter 3: Linear Equations

#### Gaussian Elimination

Gaussian elimination is a method for solving systems of linear equations by transforming the coefficient matrix into an upper triangular form.

### Chapter 4: Linear Dynamical Systems

#### State-Space Representation

A linear dynamical system can be represented as:
$\mathbf{x}_{k+1} = \mathbf{A} \mathbf{x}_k + \mathbf{B} \mathbf{u}_k$
where $\mathbf{x}_k$ is the state vector, $\mathbf{u}_k$ is the input, and $\mathbf{A}$ and $\mathbf{B}$ are system matrices.

### Chapter 5: Matrix Multiplication

#### Strassen's Algorithm

Matrix multiplication can be performed more efficiently than the standard $O(n^3)$ algorithm using methods like Strassen’s algorithm, which has a complexity of approximately $O(n^{2.81})$.

### Chapter 6: Matrix Inverses

#### Invertibility

A matrix $\mathbf{A}$ is invertible if there exists a matrix $\mathbf{A}^{-1}$ such that $\mathbf{A} \mathbf{A}^{-1} = \mathbf{I}$. Not all matrices are invertible.

## Part 3: Least Squares

### Chapter 1: Least Squares

#### Introduction

The least squares method minimizes the sum of squared differences between observed and predicted values. It is widely used for fitting models to data.

### Chapter 2: Least Squares Data Fitting

#### Ridge Regression

Ridge regression adds a regularization term to the least squares problem:
$\min_\mathbf{w} \|\mathbf{y} - \mathbf{X} \mathbf{w}\|_2^2 + \lambda \|\mathbf{w}\|_2^2$
This helps prevent overfitting by penalizing large weights.
