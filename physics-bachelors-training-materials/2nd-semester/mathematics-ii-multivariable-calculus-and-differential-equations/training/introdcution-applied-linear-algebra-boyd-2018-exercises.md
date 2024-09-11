### **Vectors**

#### **1. Introduction to Vectors**
1. Represent the following list of numbers as a vector: 3, 5, -2, 8.
2. Given two vectors \(\mathbf{v} = \begin{bmatrix} 4 \\ 7 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 1 \\ -3 \end{bmatrix}\), calculate \(\mathbf{v} + \mathbf{w}\).
3. Compute the scalar multiplication of \(c = 3\) and \(\mathbf{v} = \begin{bmatrix} -2 \\ 5 \end{bmatrix}\).
4. If \(\mathbf{v} = \begin{bmatrix} 6 \\ -1 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 2 \\ 3 \end{bmatrix}\), calculate their inner product.
5. Explain why the inner product of two orthogonal vectors is zero.

#### **2. Vector Addition**
6. Prove that vector addition is commutative for vectors \(\mathbf{v} \in \mathbb{R}^n\) and \(\mathbf{w} \in \mathbb{R}^n\).
7. Demonstrate that vector addition is associative using specific vectors \(\mathbf{u} = \begin{bmatrix} 1 \\ 2 \end{bmatrix}\), \(\mathbf{v} = \begin{bmatrix} -3 \\ 4 \end{bmatrix}\), and \(\mathbf{w} = \begin{bmatrix} 0 \\ 5 \end{bmatrix}\).
8. Add the vectors \(\mathbf{v} = \begin{bmatrix} 3 \\ -2 \\ 5 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 1 \\ 0 \\ -3 \end{bmatrix}\).

#### **3. Scalar-Vector Multiplication**
9. Calculate the scalar-vector multiplication for \(c = -2\) and \(\mathbf{v} = \begin{bmatrix} 4 \\ 6 \\ -1 \end{bmatrix}\).
10. Show that scalar multiplication distributes over vector addition: \( c(\mathbf{v} + \mathbf{w}) = c\mathbf{v} + c\mathbf{w} \), for \(c = 2\), \(\mathbf{v} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}\), and \(\mathbf{w} = \begin{bmatrix} 1 \\ 2 \end{bmatrix}\).

#### **4. Inner Product**
11. Compute the inner product of the vectors \(\mathbf{v} = \begin{bmatrix} 2 \\ 3 \\ -1 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 5 \\ -4 \\ 6 \end{bmatrix}\).
12. Given the vectors \(\mathbf{v} = \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 2 \\ 3 \\ 0 \end{bmatrix}\), show how the inner product measures the angle between them.
13. If \(\mathbf{v} = \begin{bmatrix} 1 \\ 2 \\ 2 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 2 \\ 3 \\ 1 \end{bmatrix}\), compute the cosine of the angle between \(\mathbf{v}\) and \(\mathbf{w}\).

### **Linear Functions**

#### **5. Linear Functions**
14. Given \(f(\mathbf{x}) = 2x_1 - x_2 + 3\), calculate \(f(\mathbf{v})\) where \(\mathbf{v} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}\).
15. For \(f(\mathbf{x}) = x_1 - 2x_2 + 5x_3\), calculate \(f(\mathbf{v})\) where \(\mathbf{v} = \begin{bmatrix} 1 \\ 3 \\ -2 \end{bmatrix}\).
16. Explain why \(f(\mathbf{x}) = \mathbf{a}^\top \mathbf{x} + b\) is considered a linear function.

#### **6. Taylor Approximation**
17. Find the first-order Taylor approximation of \(f(\mathbf{x}) = x_1^2 + x_2^2\) around the point \(\mathbf{x}_0 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}\).
18. Compute the gradient \(\nabla f(\mathbf{x})\) for \(f(\mathbf{x}) = x_1^2 - 3x_2 + 4x_1x_2\) and evaluate it at \(\mathbf{x}_0 = \begin{bmatrix} 1 \\ 2 \end{bmatrix}\).

### **Norm and Distance**

#### **7. Norm**
19. Calculate the Euclidean norm of the vector \(\mathbf{v} = \begin{bmatrix} 3 \\ -4 \end{bmatrix}\).
20. Prove that \(\|\mathbf{v}\|_2 \geq 0\) for any vector \(\mathbf{v} \in \mathbb{R}^n\).
21. Given the vectors \(\mathbf{v} = \begin{bmatrix} 2 \\ 3 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\), calculate their Euclidean distance.

#### **8. Distance**
22. Compute the distance between the vectors \(\mathbf{v} = \begin{bmatrix} 1 \\ 4 \end{bmatrix}\) and \(\mathbf{w} = \begin{bmatrix} -2 \\ 0 \end{bmatrix}\).
23. Show that the Euclidean distance satisfies the triangle inequality.
24. If \(\mathbf{x}_1 = \begin{bmatrix} 3 \\ 5 \end{bmatrix}\), \(\mathbf{x}_2 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\), and \(\mathbf{x}_3 = \begin{bmatrix} 0 \\ 0 \end{bmatrix}\), verify that \(d(\mathbf{x}_1, \mathbf{x}_2) + d(\mathbf{x}_2, \mathbf{x}_3) \geq d(\mathbf{x}_1, \mathbf{x}_3)\).

### **Linear Independence**

#### **9. Linear Independence**
25. Determine if the vectors \(\mathbf{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\) and \(\mathbf{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}\) are linearly independent.
26. Show that if \(\mathbf{v}_1\), \(\mathbf{v}_2\), and \(\mathbf{v}_3\) are linearly dependent, one of the vectors can be expressed as a linear combination of the others.
27. Given \(\mathbf{v}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}\) and \(\mathbf{v}_2 = \begin{bmatrix} 2 \\ 2 \end{bmatrix}\), prove that \(\mathbf{v}_1\) and \(\mathbf{v}_2\) are linearly dependent.

#### **10. Basis and Orthonormal Vectors**
28. Show that the set of vectors \(\mathbf{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\) and \(\mathbf{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}\) forms an orthonormal basis for \(\mathbb{R}^2\).
29. Apply the Gram-Schmidt process to the set of vectors \(\mathbf{v}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}\) and \(\mathbf{v}_2 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\) to orthogonalize them.
30. Verify that a set of orthonormal vectors in \(\mathbb{R}^n\) remains orthonormal after scaling by a positive scalar.
