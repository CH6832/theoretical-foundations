# Summary: Computational Methods for Scientists
## Introduction to MATLAB

### Overview
MATLAB (Matrix Laboratory) is a high-performance language for technical computing. It integrates computation, visualization, and programming in an easy-to-use environment. MATLAB is extensively used in academia and industry for its powerful capabilities in linear algebra, numerical analysis, and data visualization.

### Basic Operations

#### Matrix Addition and Subtraction
Matrix addition and subtraction in MATLAB are straightforward operations where corresponding elements are added or subtracted.

```matlab
A = [1, 2; 3, 4];
B = [5, 6; 7, 8];
C = A + B; % Matrix addition: C = [6, 8; 10, 12]
D = A - B; % Matrix subtraction: D = [-4, -4; -4, -4]
```

#### Matrix Multiplication
Matrix multiplication is done using the `*` operator. It follows the linear algebra rules where the number of columns in the first matrix must equal the number of rows in the second matrix.

```matlab
A = [1, 2; 3, 4];
B = [5, 6; 7, 8];
C = A * B; % Matrix multiplication: C = [19, 22; 43, 50]
```

#### Element-wise Operations
Element-wise operations are performed using `.*`, `./`, and `.^` operators. These operations apply to each corresponding element in the matrices.

```matlab
A = [1, 2; 3, 4];
B = [5, 6; 7, 8];
E = A .* B; % Element-wise multiplication: E = [5, 12; 21, 32]
F = A ./ B; % Element-wise division: F = [0.2, 0.3333; 0.4286, 0.5]
G = A .^ 2; % Element-wise squaring: G = [1, 4; 9, 16]
```

### Plotting

#### Basic 2D Plotting
2D plotting is essential for visualizing data. MATLAB's `plot` function is used for creating line plots.

```matlab
x = 0:0.01:2*pi; % Generate x values
y = sin(x); % Compute y values
plot(x, y); % Plot y = sin(x)
xlabel('x'); % Label x-axis
ylabel('sin(x)'); % Label y-axis
title('Plot of the Sine Function'); % Add title
```

#### Customizing Plots
MATLAB provides extensive options for customizing plots. You can change colors, line styles, and add annotations.

```matlab
x = linspace(0, 2*pi, 100);
y1 = sin(x);
y2 = cos(x);

plot(x, y1, 'r-', 'LineWidth', 2); % Plot sin(x) in red with a thicker line
hold on; % Retain current plot
plot(x, y2, 'b--', 'LineWidth', 2); % Plot cos(x) in blue with dashed lines
legend('sin(x)', 'cos(x)'); % Add legend
grid on; % Add grid lines
```

## Linear Algebra in MATLAB

### Matrix Operations

#### Matrix Inversion
Matrix inversion is used to solve systems of linear equations. The `inv` function computes the inverse of a matrix.

```matlab
A = [1, 2; 3, 4];
A_inv = inv(A); % Compute the inverse of A
% Verification: A * A_inv should be an identity matrix
identity_check = A * A_inv;
```

#### Determinant
The determinant of a matrix provides information about the matrix’s properties, such as invertibility.

```matlab
A = [1, 2; 3, 4];
det_A = det(A); % Compute the determinant of A
% For a 2x2 matrix, det(A) = a11*a22 - a12*a21
% det([1, 2; 3, 4]) = 1*4 - 2*3 = -2
```

#### Eigenvalues and Eigenvectors
Eigenvalues and eigenvectors are fundamental in various applications like stability analysis and vibration studies.

```matlab
A = [1, 2; 3, 4];
[V, D] = eig(A); % V contains eigenvectors, D is a diagonal matrix of eigenvalues
% Verify: A * V should be approximately equal to V * D
```

## Numerical Methods

### Root Finding

#### Bisection Method
The bisection method is a bracketing method that repeatedly narrows the interval containing the root.

```matlab
% Define the function
f = @(x) x^2 - 4;
% Define the interval [a, b]
a = 0;
b = 3;
% Find the root
root = fzero(f, [a, b]); % Find root in the interval [0, 3]
```

### Optimization

#### Constrained Optimization
Optimization problems with constraints can be solved using MATLAB’s `fmincon` function. Here’s an example of a quadratic objective function with linear constraints.

```matlab
% Define the objective function
objective = @(x) x(1)^2 + x(2)^2;
% Define the constraint function (x1 + x2 <= 1)
constraints = @(x) deal([], x(1) + x(2) - 1);
% Initial guess
x0 = [0, 0];
% Solve the optimization problem
[x, fval] = fmincon(objective, x0, [], [], [], [], [], [], constraints);
% x contains the optimal solution
```

## Advanced Topics

### Symbolic Mathematics
MATLAB’s Symbolic Math Toolbox enables algebraic computations, differentiation, and integration.

#### Symbolic Variables
Create and manipulate symbolic variables:

```matlab
syms x; % Define symbolic variable x
f = x^2 + 3*x + 2; % Define a symbolic function
diff_f = diff(f, x); % Compute the derivative: 2*x + 3
int_f = int(f, x); % Compute the integral: (x^3)/3 + (3*x^2)/2 + 2*x
```

#### Solving Symbolic Equations
Solve symbolic equations analytically:

```matlab
syms x;
eq = x^2 - 4; % Define the equation x^2 - 4 = 0
sol = solve(eq, x); % Solve the equation: sol = [-2, 2]
```

### Data Analysis and Statistics

#### Statistical Functions
MATLAB offers numerous statistical functions for analyzing data sets.

```matlab
data = randn(100, 1); % Generate a random data set with normal distribution
mean_data = mean(data); % Compute the mean
std_data = std(data); % Compute the standard deviation
median_data = median(data); % Compute the median
```

#### Curve Fitting
Use polynomial fitting to approximate data with a polynomial curve:

```matlab
x = linspace(0, 10, 100);
y = 3*x.^2 + 2*x + 1 + randn(1, 100); % Generate data with noise
fit_params = polyfit(x, y, 2); % Fit a 2nd degree polynomial
y_fit = polyval(fit_params, x); % Compute the fitted values
plot(x, y, 'o', x, y_fit, '-'); % Plot data and fitted curve
xlabel('x');
ylabel('y');
title('Curve Fitting with Polynomial');
```

### Advanced Plotting

#### 3D Plotting
MATLAB allows for advanced 3D visualizations, which are crucial for understanding complex data.

```matlab
[x, y] = meshgrid(-5:0.1:5, -5:0.1:5); % Generate grid points
z = sin(sqrt(x.^2 + y.^2)); % Compute z values
surf(x, y, z); % Create a 3D surface plot
xlabel('x');
ylabel('y');
zlabel('z');
title('3D Surface Plot of sin(sqrt(x^2 + y^2))');
```

#### Animation
Animations can be created to visualize changes in data over time.

```matlab
x = linspace(0, 2*pi, 100); % Generate x values
h = plot(nan, nan); % Create an empty plot
for k = 1:length(x)
    y = sin(x(k)); % Compute y values
    set(h, 'XData', x(1:k), 'YData', sin(x(1:k))); % Update plot
    drawnow; % Refresh plot window
end
```

### Advanced Numerical Methods

#### Ordinary Differential Equations (ODEs)
ODE solvers in MATLAB handle a range of ODE problems, from simple to complex.

```matlab
ode = @(t, y) -2*y + 1; % Define the ODE
[t, y] = ode45(ode, [0, 10], 0); % Solve the ODE
plot(t, y); % Plot the solution
xlabel('Time');
ylabel('y');
title('Solution of the ODE dy/dt = -2y + 1');
```

#### Partial Differential Equations (PDEs)
MATLAB's PDE toolbox

 is used for solving partial differential equations with boundary and initial conditions.

```matlab
model = createpde(); % Create a PDE model
geometryFromEdges(model, @LShapeG); % Define geometry
applyBoundaryCondition(model, 'edge', 1:4, 'u', 0); % Apply boundary conditions
thermalProperties(model, 'ThermalConductivity', 1); % Define properties
thermalBC(model, 'Edge', 1, 'Temperature', 100); % Set boundary condition
result = solve(model); % Solve the PDE
pdeplot(model, 'XYData', result.Temperature); % Plot the result
```

### Parallel Computing

#### Parallel For-Loops
Parallel computing can significantly speed up the execution of loops by distributing tasks across multiple workers.

```matlab
parfor i = 1:100
    result(i) = someFunction(i); % Execute function in parallel
end
```

#### GPU Computing
MATLAB supports GPU computing to accelerate computations by leveraging the power of GPUs.

```matlab
A = gpuArray(magic(1000)); % Transfer matrix to GPU
B = gpuArray(magic(1000));
C = A * B; % Perform matrix multiplication on GPU
% Transfer result back to CPU if needed
C_cpu = gather(C);
```

## Conclusion
MATLAB is a powerful tool for scientific computing, offering a wide range of functionalities from basic matrix operations to advanced numerical methods and data visualization. Mastering MATLAB’s advanced features can greatly enhance your capability to analyze complex data, solve intricate mathematical problems, and visualize results effectively. The examples provided here are just a starting point; MATLAB's extensive documentation and community resources can help you explore even further.
