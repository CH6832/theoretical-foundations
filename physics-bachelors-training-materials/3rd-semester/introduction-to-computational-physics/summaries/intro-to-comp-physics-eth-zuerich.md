## **Enhanced LaTeX Lecture Notes in Markdown**

**Note:** To convert this Markdown content to LaTeX, you can use a Markdown to LaTeX converter or manually translate it using the LaTeX syntax.

### **Part I: Stochastic Processes**

#### **Random Numbers**

* **Definition:** Sequences of numbers lacking predictable patterns.
* **Congruential RNG (Multiplicative):**
  * Formula: $X_{n+1} = (a \cdot X_n + c) \mod m$
  * Parameters: $a$, $c$, $m$, $X_0$
* **Lagged Fibonacci RNG (Additive):**
  * Formula: $X_n = (X_{n-j} \circ X_{n-k}) \mod m$
  * Parameters: $j$, $k$, $\circ$
* **Quality of RNG:** Period, uniformity, independence.
* **Non-Uniform Distributions:** Inverse transform, Box-Muller, acceptance-rejection methods.

#### **Percolation**

* **Sol-Gel Transition:** Transition from liquid-like to solid-like state.
* **Percolation Model:** Lattice with occupied sites, percolation occurs when a cluster spans the lattice.
* **Fractals**
  * **Self-Similarity:** Parts are similar to the whole.
  * **Fractal Dimension:** Measures complexity.
  * **Box Counting Method:** Counts boxes covering the fractal.
  * **Sandbox Method:** Counts points within a radius.
  * **Correlation-Function Method:** Measures correlation of points.
  * **Correlation Length:** Size of clusters.
  * **Finite Size Effects:** Deviations due to finite size.
  * **Fractal Dimension in Percolation:** Relates mass and size of clusters.
  * **Examples:** Mandelbrot set, Sierpinski triangle, Koch snowflake.

#### **Cellular Automata**

* **Discrete models:** Grid of cells with states evolving based on neighbor states.

### **Part II: Monte Carlo Methods**

* **Random sampling for numerical results.**
* **Applications:** Statistical physics, financial modeling, risk analysis.
* **Computation of Integrals:**
  * Formula: $I \approx \frac{1}{N} \sum_{i=1}^N f(x_i)$
* **Higher Dimensional Integrals:** Efficient for high-dimensional problems.
* **Canonical Monte Carlo:** Simulations in the canonical ensemble.
* **Ising Model:** Model of ferromagnetism.
* **Interfaces:** Boundaries between different phases.

### **Part III: Solving Systems of Equations Numerically**

#### **Solving Equations**

* **One-Dimensional Case:**
  * Bisection method: Iteratively bisects interval.
  * Newton-Raphson method: Iterative approximation using derivative.
* **Multi-Dimensional Case:**
  * Newton's method: Extends to multiple dimensions using Jacobian matrix.

#### **Linear Systems of Equations**

* **Gaussian Elimination:** Reduces to upper triangular form.
* **LU Decomposition:** Decomposes matrix into lower and upper triangular factors.
* **Iterative Methods:** Jacobi, Gauss-Seidel.

#### **Eigenvalues and Eigenvectors**

* **Definition:** $A\mathbf{v} = \lambda\mathbf{v}$
* **Power Method:** Iteratively finds largest eigenvalue and eigenvector.

#### **Ordinary Differential Equations (ODEs)**

* **Initial Value Problems (IVPs):**
  * Euler's method: Simple approximation.
  * Runge-Kutta methods: Higher-order approximations.
* **Boundary Value Problems (BVPs):**
  * Shooting method: Converts BVP to IVP.
  * Finite difference method: Discretizes domain and solves system of equations.

#### **Partial Differential Equations (PDEs)**

* **Classification:** Elliptic, parabolic, hyperbolic.
* **Numerical Methods:** Finite difference, finite element, finite volume.

#### **Optimization Problems**

* **Unconstrained Optimization:**
  * Gradient descent: Moves in direction of negative gradient.
  * Newton's method: Uses second-order Taylor expansion.
* **Constrained Optimization:**
  * Lagrange multipliers: Introduces new variables for constraints.
  * KKT conditions: Necessary conditions for optimality.

#### **Fourier Transforms**

* **Fourier Series:** Represents periodic functions as sum of sines and cosines.
* **Fourier Transform:** Generalizes Fourier series to non-periodic functions.
* **Properties:** Linearity, scaling, shift, convolution.
* **Applications:** Signal processing, quantum mechanics, image processing.

#### **Numerical Integration**

* **Basic Concepts:** Trapezoidal rule, Simpson's rule.
* **Adaptive Quadrature:** Romberg integration, Gaussian quadrature.

#### **Advanced Topics**

* **Finite Element Method (FEM):** Discretizes domain into elements.
* **Spectral Methods:** Use global basis functions.
* **Monte Carlo Methods:** Importance sampling, quasi-Monte Carlo.
* **Multigrid Methods:** Efficient for large, sparse systems.
* **Adaptive Methods:** Adjust discretization or solution process.
* **Parallel Computing:** Domain decomposition, message passing.
* **Emerging Trends:** Machine learning, exascale computing, quantum computing.

**Note:** To convert this Markdown content to LaTeX, you can use a Markdown to LaTeX converter or manually translate it using the LaTeX syntax.
