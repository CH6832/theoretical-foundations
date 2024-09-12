### **Exercises on Classification and Basic Concepts**

1. **Elliptic PDEs:**
   - **Problem:** Solve the elliptic PDE \(\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = 0\) in a square domain \(0 < x < 1\), \(0 < y < 1\) with boundary conditions \(u = 0\) on all boundaries.
   - **Objective:** Find the general solution using separation of variables.

2. **Parabolic PDEs:**
   - **Problem:** Solve the heat equation \(u_t = \alpha u_{xx}\) for \(0 < x < 1\) and \(t > 0\) with initial condition \(u(x, 0) = \sin(\pi x)\) and boundary conditions \(u(0, t) = u(1, t) = 0\).
   - **Objective:** Use separation of variables to find the solution.

3. **Hyperbolic PDEs:**
   - **Problem:** Solve the wave equation \(u_{tt} = c^2 u_{xx}\) in an infinite domain with initial conditions \(u(x, 0) = \sin(x)\) and \(u_t(x, 0) = 0\).
   - **Objective:** Use d'Alembert's formula to determine the solution.

4. **Order and Degree:**
   - **Problem:** Classify the PDE \(u_{tt} - 2u_{tx} + u_{xx} = 0\) in terms of order and degree.
   - **Objective:** Determine its classification and canonical form.

5. **Linear vs. Nonlinear:**
   - **Problem:** Determine whether the PDE \(u_t + u u_x = \nu u_{xx}\) is linear or nonlinear and solve it using the method of characteristics.
   - **Objective:** Analyze the nonlinearity and solve the PDE.

### **Exercises on First-Order PDEs**

6. **Method of Characteristics:**
   - **Problem:** Solve the first-order PDE \(u_x + 2u_y = 0\) using the method of characteristics.
   - **Objective:** Find the general solution and the characteristic curves.

7. **Linear First-Order PDEs:**
   - **Problem:** Solve the linear PDE \(u_x + 3u_y = e^x\) with initial condition \(u(x, 0) = 0\).
   - **Objective:** Use the method of characteristics to find the solution.

8. **Quasi-linear PDEs:**
   - **Problem:** For the quasi-linear PDE \(u_t + u u_x = \nu u_{xx}\), derive the characteristics and discuss how they help in solving the PDE.
   - **Objective:** Analyze the role of characteristics in solving the PDE.

### **Exercises on Second-Order PDEs**

9. **Canonical Forms:**
   - **Problem:** Convert the PDE \(u_{tt} - 4u_{xx} = 0\) into its canonical form using characteristic coordinates.
   - **Objective:** Find the new coordinates and the simplified form of the PDE.

10. **Classification of PDEs:**
    - **Problem:** Classify the PDE \(3u_{xx} + 2u_{xy} - u_{yy} = 0\) as elliptic, parabolic, or hyperbolic.
    - **Objective:** Determine the discriminant and classification.

11. **Laplace’s Equation:**
    - **Problem:** Solve Laplace’s equation \(\Delta u = 0\) in a circular disk of radius \(R\) with \(u = 0\) on the boundary.
    - **Objective:** Use separation of variables in polar coordinates to find the solution.

12. **Poisson's Equation:**
    - **Problem:** Solve Poisson’s equation \(\Delta u = -2\) in a square domain with \(u = 0\) on all boundaries.
    - **Objective:** Find the solution using Green’s functions.

### **Exercises on Elliptic PDEs**

13. **Boundary Value Problems:**
    - **Problem:** Solve the boundary value problem for \(\Delta u = -\pi^2 \sin(\pi x) \sin(\pi y)\) in a square domain with \(u = 0\) on the boundary.
    - **Objective:** Use separation of variables to solve the PDE.

14. **Green’s Functions:**
    - **Problem:** Find the Green’s function for the Laplace equation in a unit square domain.
    - **Objective:** Derive and use the Green’s function to solve a specific Poisson’s equation problem.

15. **Maximum Principle:**
    - **Problem:** Prove the strong maximum principle for the elliptic PDE \(\Delta u \geq 0\) in a bounded domain.
    - **Objective:** Use the principle to discuss the behavior of solutions.

### **Exercises on Parabolic PDEs**

16. **Heat Equation with Non-homogeneous Initial Condition:**
    - **Problem:** Solve \(u_t = \alpha u_{xx}\) with initial condition \(u(x, 0) = x(1-x)\) and boundary conditions \(u(0, t) = u(1, t) = 0\).
    - **Objective:** Use separation of variables to find the solution.

17. **Heat Equation with Periodic Boundary Conditions:**
    - **Problem:** Solve \(u_t = \alpha u_{xx}\) on \(0 < x < 2\pi\) with periodic boundary conditions \(u(0, t) = u(2\pi, t)\) and initial condition \(u(x, 0) = \sin(x)\).
    - **Objective:** Find the solution using Fourier series.

### **Exercises on Hyperbolic PDEs**

18. **Wave Equation with Non-homogeneous Boundary Conditions:**
    - **Problem:** Solve \(u_{tt} = c^2 u_{xx}\) for \(0 < x < L\) with boundary conditions \(u(0, t) = 0\) and \(u(L, t) = 0\), and initial conditions \(u(x, 0) = \sin\left(\frac{\pi x}{L}\right)\) and \(u_t(x, 0) = 0\).
    - **Objective:** Use separation of variables to find the solution.

19. **Wave Equation in an Infinite Domain:**
    - **Problem:** Solve \(u_{tt} = c^2 u_{xx}\) in \(-\infty < x < \infty\) with initial conditions \(u(x, 0) = e^{-|x|}\) and \(u_t(x, 0) = 0\).
    - **Objective:** Use d'Alembert’s solution to find the general solution.

### **Exercises on Fourier Series and Separation of Variables**

20. **Fourier Series Expansion:**
    - **Problem:** Compute the Fourier series for \(f(x) = x^2\) on the interval \([-L, L]\).
    - **Objective:** Find the coefficients and series representation.

21. **Separation of Variables in Cylindrical Coordinates:**
    - **Problem:** Solve the PDE \(u_{rr} + \frac{1}{r} u_r + \frac{1}{r^2} u_{\theta \theta} = 0\) in a cylindrical domain with \(u(r, \theta) = 0\) on the boundary.
    - **Objective:** Use separation of variables in cylindrical coordinates.

### **Exercises on Numerical Methods**

22. **Finite Difference Method for Heat Equation:**
    - **Problem:** Implement the finite difference method to approximate the solution of the heat equation \(u_t = \alpha u_{xx}\) with a grid spacing \(\Delta x\) and \(\Delta t\). Compare with the exact solution for a specific initial condition.
    - **Objective:** Analyze stability and accuracy of the numerical method.

23. **Finite Element Method for Poisson’s Equation:**
    - **Problem:** Apply the finite element method to solve Poisson’s equation \(\Delta u = -1\) in a unit square domain with \(u = 0\) on the boundary.
    - **Objective:** Construct and solve the finite element system.

### **Exercises on Advanced Topics**

24. **Nonlinear PDEs:**
    - **Problem:** Analyze the Burger’s equation \(u_t + u u_x = \nu u_{xx}\) for shock wave formation in a one-dimensional domain with a specific initial condition.
    - **Objective:** Discuss the formation of shock waves and solution techniques.

25. **Stochastic PDEs:**
    - **Problem:** Solve the stochastic PDE \(u_t = \alpha u_{xx} + \sigma u_x\) with given noise term \(\sigma\) and initial condition.
    - **Objective:** Use Ito calculus to find the solution and analyze its properties.

26. **Applications in Fluid Dynamics:**
    - **Problem:** Solve the Navier-Stokes equations for incompressible flow in a two-dimensional domain with specific boundary conditions.
    - **Objective:** Discuss numerical methods for solving the Navier-Stokes equations.

27. **Schrödinger’s Equation in Quantum Mechanics:**
    - **Problem:** Solve the time-dependent Schrödinger equation \(i \hbar \frac{\partial \psi}{\partial t} = -\frac{\hbar^2

}{2m} \Delta \psi\) for a particle in a one-dimensional box with specific initial conditions.
    - **Objective:** Use separation of variables to find the solution.

28. **Heat Transfer in Composite Materials:**
    - **Problem:** Solve the heat equation in a composite material with different thermal conductivities in different regions.
    - **Objective:** Use boundary conditions and continuity of flux to solve the problem.

29. **Wave Propagation in Complex Media:**
    - **Problem:** Analyze wave propagation described by a hyperbolic PDE in a medium with varying wave speeds.
    - **Objective:** Discuss how varying wave speeds affect the solution.

30. **Inverse Problems in PDEs:**
    - **Problem:** Given measurements of temperature on the boundary of a domain, reconstruct the initial temperature distribution using inverse methods.
    - **Objective:** Apply techniques from inverse problems to deduce the initial conditions.
