## Detailed Summary of *Classical Mechanics (Third Edition)*

### Authors
Herbert Goldstein, Charles P. Poole, John L. Safko

### Introduction
The third edition of *Classical Mechanics* provides a comprehensive exploration of classical mechanics, spanning from basic principles to advanced topics. This summary outlines key concepts, mathematical formulations, and explanations from each chapter.

### Chapter 1: Survey of the Elementary Principles
#### 1.1 Mechanics of a Particle
- **Basic Concepts**: The motion of a particle is described by position \( \mathbf{r}(t) \), velocity \( \mathbf{v}(t) \), and acceleration \( \mathbf{a}(t) \):
  
  $\mathbf{v}(t) = \frac{d\mathbf{r}(t)}{dt}$
  
  $\mathbf{a}(t) = \frac{d\mathbf{v}(t)}{dt}$
  Newton’s second law:
  
  $\mathbf{F} = m \mathbf{a}$

- **Conservation Laws**: In conservative systems, energy and momentum are conserved. Total energy \( E \):
  
  $E = T + V$
  where \( T \) is kinetic energy and \( V \) is potential energy.

#### 1.2 Mechanics of a System of Particles
- **Center of Mass**: 
  
  $\mathbf{R}_{cm} = \frac{1}{M} \sum_{i} m_i \mathbf{r}_i$
  where \( M = \sum_{i} m_i \) is the total mass.

- **Equations of Motion**: 
  
  $\mathbf{F}_i = m_i \mathbf{a}_i$

#### 1.3 Constraints
- **Types of Constraints**: Constraints restrict motion. Holonomic constraints are expressed as:
  
  $f(\mathbf{r}, t) = 0$
  Non-holonomic constraints involve differentials.

#### 1.4 D’Alembert’s Principle and Lagrange’s Equations
- **D’Alembert’s Principle**: 
  
  $\mathbf{F} - m \mathbf{a} = 0$

- **Lagrange’s Equations**: Derived from stationary action:
  
  $\frac{d}{dt} \left( \frac{\partial L}{\partial \dot{q}_i} \right) - \frac{\partial L}{\partial q_i} = 0$
  with \( L = T - V \) as the Lagrangian.

#### 1.5 Velocity-Dependent Potentials and the Dissipation Function
- **Dissipation Function**: 
  
  $F_d = \frac{1}{2} \sum_{i,j} \eta_{ij} \dot{q}_i \dot{q}_j$

- **Generalized Forces**: 
  
  $Q_i = -\frac{\partial V}{\partial q_i} + \frac{d}{dt} \left( \frac{\partial F_d}{\partial \dot{q}_i} \right)$

#### 1.6 Simple Applications of the Lagrangian Formulation
- **Example Problems**: Applied to systems like pendulums and harmonic oscillators.

### Chapter 2: Variational Principles and Lagrange’s Equations
#### 2.1 Hamilton’s Principle
- **Principle of Least Action**: 
  
  $S = \int_{t_1}^{t_2} L \, dt$

#### 2.2 Techniques of the Calculus of Variations
- **Euler-Lagrange Equation**: 
  
  $\frac{\partial L}{\partial q_i} - \frac{d}{dt} \left( \frac{\partial L}{\partial \dot{q}_i} \right) = 0$

#### 2.3 Derivation from Hamilton’s Principle
- **Variational Approach**: Derivation using calculus of variations.

#### 2.4 Extending Hamilton’s Principle to Systems with Constraints
- **Modified Action**: 
  
  $S = \int_{t_1}^{t_2} \left( L + \sum_{k} \lambda_k f_k \right) dt$

#### 2.5 Advantages of a Variational Principle Formulation
- **Flexibility and Generality**: Provides a general framework for deriving equations of motion.

#### 2.6 Conservation Theorems and Symmetry Properties
- **Noether’s Theorem**: Relates symmetries to conserved quantities.

#### 2.7 Energy Function and the Conservation of Energy
- **Conservation of Energy**: 
  
  $E = \frac{\partial L}{\partial \dot{q}_i} \dot{q}_i - L$

### Chapter 3: The Central Force Problem
#### 3.1 Reduction to the Equivalent One-Body Problem
- **Effective Potential**: 
  
  $V_{eff} = V(r) + \frac{L^2}{2 \mu r^2}$

#### 3.2 The Equations of Motion and First Integrals
- **Orbital Motion**: Radial and angular equations of motion.

#### 3.3 Equivalent One-Dimensional Problem, and Classification of Orbits
- **Orbit Classification**: Elliptical, parabolic, or hyperbolic trajectories.

#### 3.4 The Virial Theorem
- **Virial Relation**: 
  
  $2 \langle T \rangle = - \langle \mathbf{r} \cdot \mathbf{F} \rangle$

#### 3.5 Differential Equation for the Orbit, and Integrable Power-Law Potentials
- **Power-Law Potentials**: 
  
  $\frac{d^2 u}{d\theta^2} + u = \frac{1}{l^2} \frac{dV}{du}$

#### 3.6 Conditions for Closed Orbits (Bertrand’s Theorem)
- **Bertrand’s Theorem**: Closed orbits occur for inverse-square and harmonic potentials.

#### 3.7 The Kepler Problem: Inverse-Square Law of Force
- **Kepler’s Laws**: 
  
  $F = -\frac{G M m}{r^2}$

#### 3.8 Motion in Time in the Kepler Problem
- **Orbital Period**: 
  
  $T^2 = \frac{4 \pi^2 a^3}{G M (m + M)}$

#### 3.9 The Laplace–Runge–Lenz Vector
- **Laplace–Runge–Lenz Vector**: 
  
  $\mathbf{A} = \mathbf{p} \times \mathbf{L} - \mu \frac{\mathbf{r}}{r}$

#### 3.10 Scattering in a Central Force Field
- **Differential Cross-Section**: 
  
  $\frac{d\sigma}{d\Omega} = \frac{(Z_1 Z_2 e^2)^2}{16 \pi^2 \epsilon_0^2 E^2} \frac{1}{\sin^4(\theta/2)}$

#### 3.11 Transformation to Laboratory Coordinates
- **Laboratory Coordinates**: Simplifies scattering experiments.

#### 3.12 The Three-Body Problem
- **Restricted Three-Body Problem**: Analyzes a small body in the field of two larger bodies.

### Chapter 4: The Kinematics of Rigid Body Motion
#### 4.1 The Independent Coordinates of a Rigid Body
- **Configuration Space**: Described by three rotation angles.

#### 4.2 Orthogonal Transformations
- **Rotation Matrices**: 
  
  $\mathbf{R} \mathbf{R}^T = \mathbf{I}$

#### 4.3 Formal Properties of the Transformation Matrix
- **Orthogonality and Determinant**: Orthogonal matrices preserve angles and lengths.

#### 4.4 The Euler Angles
- **Definition and Usage**: Describe orientation using three rotations.

#### 4.5 The Cayley–Klein Parameters and Related Quantities
- **Rotations with Quaternions**: Alternative to Euler angles.

#### 4.6 Euler’s Theorem on the Motion of a Rigid Body
- **Euler’s Theorem**: Any rotation about a fixed point can be described by a single rotation about some axis.

#### 4.7 Finite Rotations
- **Composition of Rotations**: Successive infinitesimal rotations.

#### 4.8 Infinitesimal Rotations
- **Small Angle Approximations**: Describe small angular displacements.

#### 4.9 Rate of Change of a Vector
- **Rotational Rates**: 
  
  $\frac{d\mathbf{v}}{dt} = \mathbf{\Omega} \times \mathbf{v}$

#### 4.10 The Coriolis Effect
- **Coriolis Force**: 
  
 $

 \mathbf{F}_{cor} = -2 m (\mathbf{v} \times \mathbf{\Omega})$

#### 4.11 The General Problem of Rigid Body Motion
- **Equations of Motion**: 
  
  $\mathbf{I} \cdot \frac{d \mathbf{\omega}}{dt} + \mathbf{\omega} \times (\mathbf{I} \cdot \mathbf{\omega}) = \mathbf{T}$

#### 4.12 The Rotating Coordinate System
- **Pseudo-Forces**: Include Coriolis and centrifugal forces in rotating frames.

#### 4.13 Rigid Body Dynamics in a Central Force Field
- **Dynamics in Central Fields**: Application to celestial mechanics.

#### 4.14 Special Cases of Rigid Body Dynamics
- **Symmetrical Tops and Spheroids**: Simplified models for specific shapes.

### Chapter 5: The Dynamics of a Rigid Body
#### 5.1 The Rigid Body as a System of Particles
- **Distribution of Mass**: Center of mass and inertia tensor.

#### 5.2 The Inertia Tensor and Principal Axes
- **Inertia Tensor**: 
  
  $\mathbf{I} = \begin{pmatrix}
  I_x & 0 & 0 \\
  0 & I_y & 0 \\
  0 & 0 & I_z
  \end{pmatrix}$

#### 5.3 The Euler Equations of Motion
- **Euler’s Equations**: 
  
  $\frac{d \mathbf{L}}{dt} = \mathbf{T} + \mathbf{\Omega} \times \mathbf{L}$

#### 5.4 The Free Rigid Body
- **Rotation without External Forces**: Analysis of free rotation.

#### 5.5 The Problem of the Rigid Body with an Internal Degree of Freedom
- **Internal Modes**: Interaction of rotational and vibrational modes.

#### 5.6 The Rigid Body with a Fixed Point
- **Rotation About a Fixed Point**: Analysis of specific cases like gyroscopic motion.

#### 5.7 The Rigid Body with a Rotating Axis
- **Spinning Tops and Gyroscopes**: Dynamics of rotating bodies.

#### 5.8 Precession and Nutation
- **Precession**: Slow rotation of the axis of a spinning body.

#### 5.9 The Atmosphere and the Earth
- **Earth’s Rotation**: Application to atmospheric dynamics.

#### 5.10 Torsional Oscillations and Normal Modes
- **Oscillatory Motion**: Analysis of vibrational modes.

#### 5.11 The Euler-Poincaré Equations
- **Euler-Poincaré Formulation**: Generalized equations for rigid body motion.

### Chapter 6: The Theory of Small Oscillations
#### 6.1 Linear Approximation to Small Oscillations
- **Small Oscillations**: Linearized analysis of stability.

#### 6.2 The Normal Coordinates
- **Normal Modes**: 
  
  $\mathbf{q}(t) = \mathbf{Q} \mathbf{q}_0 \sin(\omega t)$

#### 6.3 The Eigenvalue Problem
- **Matrix Formulation**: 
  
  $\mathbf{M} \ddot{\mathbf{q}} + \mathbf{K} \mathbf{q} = 0$

#### 6.4 The Principle of Least Action in Small Oscillations
- **Action Principle**: Applied to small oscillations.

#### 6.5 Forced Oscillations and Resonance
- **Forced Systems**: Analysis of driven oscillations.

#### 6.6 Coupled Oscillations
- **Interaction of Oscillators**: Solution for multiple coupled systems.

#### 6.7 Nonlinear Oscillations
- **Nonlinear Effects**: Analysis of nonlinear systems.

### Chapter 7: Canonical Transformations and Hamiltonian Mechanics
#### 7.1 Canonical Transformations
- **Generating Functions**: 
  
  $\frac{\partial F}{\partial q_i} = p_i$

#### 7.2 The Hamilton-Jacobi Theory
- **Hamilton-Jacobi Equation**: 
  
  $H \left( q_i, \frac{\partial S}{\partial q_i}, t \right) + \frac{\partial S}{\partial t} = 0$

#### 7.3 Action-Angle Variables
- **Action-Angle Coordinates**: 
  
  $J_i = \frac{1}{2 \pi} \oint p_i dq_i$

#### 7.4 Hamiltonian Mechanics
- **Hamilton’s Equations**: 
  
  $\dot{q}_i = \frac{\partial H}{\partial p_i}$
  
  $\dot{p}_i = - \frac{\partial H}{\partial q_i}$

#### 7.5 The Hamiltonian of a System of Particles
- **Generalized Coordinates**: Extends to multiple particles.

#### 7.6 The Canonical Quantization
- **Quantum Mechanics**: Introduction to canonical quantization.

### Chapter 8: The Theory of Small Oscillations
#### 8.1 The Small Oscillation Theory
- **Small Oscillations**: Linear stability analysis.

#### 8.2 Coupled Oscillators
- **Coupled Systems**: Interaction and normal modes.

#### 8.3 The Eigenvalue Problem
- **Normal Modes**: Solution using matrix methods.

#### 8.4 Nonlinear Oscillations
- **Nonlinear Effects**: Analysis of nonlinear systems.

### Chapter 9: Relativistic Mechanics
#### 9.1 The Special Theory of Relativity
- **Postulates**: Constancy of the speed of light and relativity of simultaneity.

#### 9.2 Lorentz Transformations
- **Transformations**: 
  
  $x' = \gamma (x - vt)$
  
  $t' = \gamma (t - \frac{vx}{c^2})$

#### 9.3 Relativistic Dynamics
- **Relativistic Energy and Momentum**: 
  
  $E^2 = (pc)^2 + (mc^2)^2$

#### 9.4 Applications to Classical Mechanics
- **Relativistic Corrections**: Impact on classical mechanics.

#### 9.5 The Four-Dimensional Formulation
- **Four-Vectors**: Space-time coordinates.

#### 9.6 Relativistic Kinematics and Dynamics
- **General Formulations**: Application to various problems.

#### 9.7 The Principle of Equivalence
- **General Relativity**: Extension to curved space-time.

### Chapter 10: Non-Inertial Reference Frames
#### 10.1 Accelerated Frames
- **Pseudo-Forces**: Forces observed in non-inertial frames.

#### 10.2 The Coriolis Effect
- **Coriolis Force**: Application to rotating frames.

#### 10.3 The Eulerian and Lagrangian Descriptions
- **Fluid Dynamics**: Differences between Eulerian and Lagrangian descriptions.

#### 10.4 The Equations of Motion in Non-Inertial Frames
- **General Equations**: Extension to non-inertial frames.
