### Exercises on Basic PDEs

1. **Elliptic PDE Exercise**: 
   Solve the Laplace equation \(\nabla^2 u = 0\) in a rectangular domain with boundary conditions \(u(x, 0) = 0\), \(u(x, L) = 0\), and \(u(0, y) = 0\), \(u(a, y) = 100\) for \(0 \leq x \leq a\) and \(0 \leq y \leq L\).

2. **Heat Equation Exercise**: 
   Solve the heat equation \(\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}\) with initial condition \(u(x, 0) = \sin(\pi x)\) and boundary conditions \(u(0, t) = u(1, t) = 0\).

3. **Wave Equation Exercise**: 
   Solve the wave equation \(\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}\) for a vibrating string of length \(L\) with initial conditions \(u(x, 0) = \sin\left(\frac{\pi x}{L}\right)\) and \(\frac{\partial u}{\partial t}(x, 0) = 0\).

4. **Elliptic PDE Canonical Form**: 
   Transform the elliptic PDE \(2 \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = 0\) into its canonical form.

5. **Parabolic PDE Canonical Form**: 
   Simplify the parabolic PDE \(\frac{\partial u}{\partial t} = \frac{1}{2} \frac{\partial^2 u}{\partial x^2} + x \frac{\partial u}{\partial x}\) to its canonical form.

6. **Hyperbolic PDE Canonical Form**: 
   Convert the hyperbolic PDE \(\frac{\partial^2 u}{\partial t^2} - 4 \frac{\partial^2 u}{\partial x^2} = 0\) to its canonical form.

### Exercises on Solution Techniques

7. **Separation of Variables (Heat Equation)**: 
   Solve the heat equation \(\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}\) on a rod of length \(L\) with boundary conditions \(u(0, t) = u(L, t) = 0\) and initial condition \(u(x, 0) = \sin\left(\frac{n\pi x}{L}\right)\), where \(n\) is a positive integer.

8. **Separation of Variables (Wave Equation)**: 
   Use the separation of variables method to solve the wave equation \(\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}\) with initial conditions \(u(x, 0) = x(L-x)\) and \(\frac{\partial u}{\partial t}(x, 0) = 0\).

9. **Method of Characteristics**: 
   Solve the first-order PDE \(\frac{\partial u}{\partial t} + \frac{\partial u}{\partial x} = 0\) with initial condition \(u(x, 0) = \sin(x)\) using the method of characteristics.

10. **Dirichlet Boundary Conditions**: 
    Solve the Laplace equation \(\nabla^2 u = 0\) in a circular domain of radius \(R\) with Dirichlet boundary conditions \(u(R, \theta) = 0\) for \(0 \leq \theta < 2\pi\).

11. **Neumann Boundary Conditions**: 
    Solve the heat equation \(\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}\) with Neumann boundary conditions \(\frac{\partial u}{\partial x}(0, t) = 0\) and \(\frac{\partial u}{\partial x}(L, t) = 0\), and initial condition \(u(x, 0) = x(L-x)\).

12. **Initial Value Problem**: 
    Solve the heat equation \(\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}\) on the interval \([0, L]\) with initial condition \(u(x, 0) = \sin\left(\frac{2\pi x}{L}\right)\) and boundary conditions \(u(0, t) = u(L, t) = 0\).

### Exercises on Special Functions and Fourier Analysis

13. **Fourier Series Expansion**: 
    Find the Fourier series expansion of the square wave function \(f(x) = \begin{cases} 
    1 & \text{for } -\frac{\pi}{2} < x < \frac{\pi}{2} \\
    -1 & \text{for } \frac{\pi}{2} < x < \frac{3\pi}{2} 
    \end{cases}\) with period \(2\pi\).

14. **Fourier Transform of a Gaussian Function**: 
    Compute the Fourier transform of the Gaussian function \(f(x) = e^{-x^2}\).

15. **Discrete Fourier Transform (DFT)**: 
    Compute the DFT of the discrete sequence \(x[n] = \{1, 2, 3, 4\}\).

16. **Inverse Fourier Transform**: 
    Find the inverse Fourier transform of \(\hat{f}(k) = \frac{1}{\sqrt{2\pi}} e^{-\frac{k^2}{2}}\).

17. **Fourier Series Coefficients**: 
    Compute the Fourier coefficients \(a_n\) and \(b_n\) for the function \(f(x) = x\) on the interval \([- \pi, \pi]\).

18. **Fourier Transform of a Rectangular Pulse**: 
    Calculate the Fourier transform of the rectangular pulse function \(f(x) = \begin{cases} 
    1 & \text{for } -\frac{T}{2} < x < \frac{T}{2} \\
    0 & \text{otherwise}
    \end{cases}\).

### Exercises on Numerical Methods

19. **Finite Difference Method (Heat Equation)**: 
    Use the finite difference method to approximate the solution of the heat equation \(\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}\) on a rod of length \(L\) with initial condition \(u(x, 0) = \sin\left(\frac{\pi x}{L}\right)\) and boundary conditions \(u(0, t) = u(L, t) = 0\).

20. **Finite Difference Method (Wave Equation)**: 
    Apply the finite difference method to solve the wave equation \(\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}\) with given initial conditions and boundary conditions.

21. **Finite Element Method (Heat Equation)**: 
    Use the finite element method to solve the heat equation on a 1D domain with boundary conditions \(u(0, t) = 0\) and \(u(L, t) = 100\) and initial condition \(u(x, 0) = 0\).

22. **Mesh Generation**: 
    Generate a mesh for a 2D domain using triangular elements and solve a simple PDE using this mesh.

23. **Finite Element Analysis (FEM) Example**: 
    For a given 2D problem, create a mesh, assemble the stiffness matrix, and solve the linear system of equations resulting from the finite element discretization.

24. **Stability Analysis (Heat Equation)**: 
    Perform stability analysis for the explicit finite difference method applied to the heat equation, including the CFL condition.

25. **Crank-Nicolson Method**: 
    Implement the Crank-Nicolson method for solving the heat equation and compare its accuracy with the explicit method.

### Advanced Applications and Mixed Exercises

26. **Thermal Conduction in a Cylinder**: 
    Solve the PDE for thermal conduction in a cylindrical domain with given initial and boundary conditions.

27. **Electrostatic Potential Calculation**: 
    Use the Laplace equation to calculate the electrostatic potential in a region with specified boundary conditions.

28. **Vibrating Membrane**: 
    Analyze the vibrations of a circular membrane using the wave equation and appropriate boundary conditions.

29. **Heat Distribution in a Complex Geometry**: 
    Solve the heat equation for a complex domain using numerical methods such as finite element analysis.

30. **Signal Processing with Fourier Transforms**: 
    Apply Fourier transforms to analyze and filter a signal with known frequency components.
