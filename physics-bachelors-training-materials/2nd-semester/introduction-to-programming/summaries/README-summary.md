# Advanced MATLAB Programming

## Course Description

This course provides an in-depth exploration of MATLAB programming, covering both fundamental and advanced topics. It includes detailed explanations and examples of MATLAB's capabilities for data analysis, numerical methods, and algorithm development. By the end of the course, students will be proficient in using MATLAB for complex scientific and engineering problems.

## Key Topics

### Basics of MATLAB Programming

#### MATLAB Fundamentals

**Basic Operations:**

- **Syntax and Variables:**

  ```matlab
  a = 5;                   % Integer assignment
  b = 2.718;               % Floating-point assignment
  c = 'MATLAB';            % String assignment
  d = true;                % Logical assignment
  ```

  MATLAB uses a matrix-based language, where variables are primarily matrices.

- **Matrix Operations:**

  ```matlab
  A = [1 2; 3 4];          % Define a 2x2 matrix
  B = [5 6; 7 8];          % Define another 2x2 matrix
  C = A + B;               % Matrix addition
  D = A * B;               % Matrix multiplication
  E = A .* B;              % Element-wise multiplication
  ```

**Functions:**

- **Defining Functions:**

  ```matlab
  function result = multiply(x, y)
      result = x * y;
  end

  % Calling the function
  product = multiply(3, 4); % Returns 12
  ```

  Functions in MATLAB are defined in separate files or within scripts using the `function` keyword.

**Scripts and Functions:**

- **Scripts:**
  MATLAB scripts are files with a `.m` extension containing a sequence of MATLAB commands. They are executed in the base workspace.

  ```matlab
  % ExampleScript.m
  x = 1:10;
  y = x.^2;
  plot(x, y);
  title('Plot of y = x^2');
  ```

- **Functions:**
  Functions are files with a `.m` extension that can accept inputs and return outputs.

  ```matlab
  % ExampleFunction.m
  function [sum, diff] = calculate(x, y)
      sum = x + y;
      diff = x - y;
  end
  ```

### Advanced MATLAB Programming

#### Data Visualization

**Advanced Plotting:**

- **Multiple Plots and Subplots:**

  ```matlab
  x = linspace(0, 2*pi, 100);
  y1 = sin(x);
  y2 = cos(x);

  subplot(2,1,1);          % Create a 2x1 grid, first subplot
  plot(x, y1);
  title('Sine Function');

  subplot(2,1,2);          % Second subplot
  plot(x, y2);
  title('Cosine Function');
  ```

- **3D Plotting:**

  ```matlab
  [X, Y] = meshgrid(-5:0.1:5, -5:0.1:5);
  Z = sqrt(X.^2 + Y.^2);
  surf(X, Y, Z);            % 3D surface plot
  xlabel('X-axis');
  ylabel('Y-axis');
  zlabel('Z-axis');
  ```

- **Customized Graphics:**

  ```matlab
  x = 0:0.1:10;
  y = sin(x);
  plot(x, y, 'LineWidth', 2, 'Color', [0 0.5 0.5]);  % Customized line color and width
  grid on;
  legend('Sine Curve');
  ```

#### Numerical Methods

**Linear Algebra:**

- **Eigenvalues and Eigenvectors:**

  ```matlab
  A = [1 2; 3 4];
  [V, D] = eig(A);         % V contains eigenvectors, D contains eigenvalues
  ```

- **Matrix Factorizations:**

  ```matlab
  [L, U, P] = lu(A);       % LU decomposition with pivoting
  ```

**Optimization:**

- **Constrained Optimization:**

  ```matlab
  % Define the objective function
  objective = @(x) (x(1) - 2)^2 + (x(2) - 3)^2;

  % Define constraints
  constraints = @(x) [x(1) + x(2) - 2; -x(1) + x(2) - 1];

  % Initial guess
  x0 = [0, 0];

  % Solve
  [x_opt, fval] = fmincon(objective, x0, [], [], [], [], [], [], constraints);
  ```

**Differential Equations:**

- **Solving Ordinary Differential Equations (ODEs):**

  ```matlab
  % Define the differential equation
  ode = @(t, y) -2*y + t;

  % Initial condition
  y0 = 1;

  % Solve the ODE
  [t, y] = ode45(ode, [0, 5], y0);

  % Plot the solution
  plot(t, y);
  xlabel('Time');
  ylabel('y(t)');
  ```

- **Partial Differential Equations (PDEs):**

  Use `pdepe` for solving PDEs:

  ```matlab
  % Define PDE
  function [c, f, s] = pde_func(x, t, u, DuDx)
      c = 1;              % Coefficient for time derivative
      f = DuDx;           % Flux term
      s = 0;              % Source term
  end

  % Define boundary conditions
  function [pl, ql, pr, qr] = bc_func(xl, ul, xr, ur, t)
      pl = ul - 0;        % Left boundary condition
      ql = 1;            % Boundary condition coefficient
      pr = ur - 1;        % Right boundary condition
      qr = 0;            % Boundary condition coefficient
  end

  % Define initial conditions
  function u0 = ic_func(x)
      u0 = sin(pi*x);    % Initial condition
  end

  % Solve PDE
  m = 0;                % Symmetry parameter
  x = linspace(0, 1, 100);   % Spatial domain
  t = linspace(0, 1, 100);   % Time domain
  sol = pdepe(m, @pde_func, @ic_func, @bc_func, x, t);
  ```

### Advanced Data Analysis

**Data Handling:**

- **Importing and Exporting Data:**

  ```matlab
  data = readtable('data.csv');   % Import data from CSV file
  writetable(data, 'output.csv'); % Export data to CSV file
  ```

- **Handling Large Datasets:**

  Use MATLAB's `tall` arrays for handling large data that does not fit into memory:

  ```matlab
  t = tall(readtable('large_data.csv'));
  mean_value = mean(t.VarName);
  ```

**Statistical Analysis:**

- **Descriptive Statistics:**

  ```matlab
  data = randn(100,1);   % Generate random data
  mean_val = mean(data); % Mean
  std_dev = std(data);   % Standard deviation
  ```

- **Regression Analysis:**

  ```matlab
  X = [ones(length(x),1), x]; % Add intercept term
  [b, bint, r, rint, stats] = regress(y, X);
  ```

**Machine Learning:**

- **Classification:**

  ```matlab
  load fisheriris;
  X = meas(:,1:2);       % Select features
  Y = species;           % Target labels
  Mdl = fitcnb(X, Y);    % Train Naive Bayes classifier
  ```

- **Clustering:**

  ```matlab
  X = rand(100, 2);      % Generate random data
 [idx, C] = kmeans(X, 3); % Perform k-means clustering
  ```

### MATLAB Applications in Engineering and Science

**Signal Processing:**

- **Fourier Transform:**

  ```matlab
  t = 0:0.001:1;         % Time vector
  x = sin(2*pi*50*t) + sin(2*pi*120*t); % Signal
  Y = fft(x);            % Compute Fourier transform
  ```

- **Filtering:**

  ```matlab
  [b, a] = butter(5, 0.3); % Design a low-pass Butterworth filter
  filtered_signal = filtfilt(b, a, x); % Apply the filter
  ```

**Control Systems:**

- **System Analysis:**

  ```matlab
  sys = tf([1], [1, 2, 1]);  % Define a transfer function
  step(sys);                 % Plot step response
  ```

- **Design and Simulation:**

  ```matlab
  Kp = 1;                     % Proportional gain
  C = pid(Kp);                % Define a PID controller
  sys_cl = feedback(C*sys, 1); % Closed-loop system
  step(sys_cl

);               % Plot step response
  ```

**Image Processing:**

- **Basic Operations:**

  ```matlab
  img = imread('image.png'); % Read an image
  gray_img = rgb2gray(img);  % Convert to grayscale
  imshow(gray_img);         % Display the image
  ```

- **Filtering and Enhancement:**

  ```matlab
  filtered_img = imgaussfilt(gray_img, 2); % Apply Gaussian filter
  imshow(filtered_img);    % Display the filtered image
  ```

### Advanced MATLAB Programming Techniques

**Object-Oriented Programming (OOP):**

- **Defining Classes:**

  ```matlab
  classdef Circle
      properties
          Radius
      end
      methods
          function obj = Circle(radius)
              obj.Radius = radius;
          end
          function area = getArea(obj)
              area = pi * obj.Radius^2;
          end
      end
  end
  ```

- **Creating and Using Objects:**

  ```matlab
  myCircle = Circle(5);     % Create an instance of Circle
  area = myCircle.getArea(); % Get the area
  ```

**Parallel Computing:**

- **Using Parallel Pools:**

  ```matlab
  parpool('local', 4); % Start a parallel pool with 4 workers
  parfor i = 1:10
      disp(['Parallel loop iteration ', num2str(i)]);
  end
  ```

- **GPU Computing:**

  ```matlab
  A = gpuArray(rand(1000));  % Create a GPU array
  B = fft(A);                % Perform FFT on the GPU
  ```

**Custom Functions and Toolboxes:**

- **Creating Toolboxes:**

  Develop custom toolboxes by packaging functions and classes into `.mltbx` files. This facilitates sharing and reuse.

  ```matlab
  % Create a toolbox by organizing your functions and classes
  ```

- **Using Built-in Toolboxes:**

  MATLAB offers various toolboxes like Optimization, Statistics, and Neural Networks. For example, using the Optimization Toolbox:

  ```matlab
  % Solve an optimization problem using fminunc
  objective = @(x) (x(1) - 2)^2 + (x(2) - 3)^2;
  x0 = [0, 0];
  options = optimoptions('fminunc', 'Algorithm', 'quasi-newton');
  [x_opt, fval] = fminunc(objective, x0, options);
  ```
