# Quantum Mechanics I

## Course Description

Quantum Mechanics I introduces the fundamental principles of quantum mechanics, focusing on the mathematical framework, dynamics of quantum systems, and their applications. This course covers the essential concepts and mathematical tools needed to understand the quantum behavior of particles and systems.

## Key Topics

### Mathematical Foundations

#### Wave Functions and Operators

**1. Schrödinger Equation:**

The Schrödinger Equation is the fundamental equation of quantum mechanics, describing how the quantum state of a system evolves over time.

- **Time-Dependent Schrödinger Equation (TDSE):**

  The TDSE is given by:

  \[
  i \hbar \frac{\partial \psi(\mathbf{r}, t)}{\partial t} = \hat{H} \psi(\mathbf{r}, t)
  \]

  - **\( i \)** is the imaginary unit.
  - **\( \hbar \)** (h-bar) is the reduced Planck constant, \( \hbar = \frac{h}{2\pi} \), where \( h \) is Planck's constant.
  - **\( \psi(\mathbf{r}, t) \)** is the wave function of the system, which contains all the information about the quantum state.
  - **\( \hat{H} \)** is the Hamiltonian operator, representing the total energy of the system.

  **Interpretation:**

  The TDSE states that the time rate of change of the wave function \( \psi \) is proportional to the action of the Hamiltonian on \( \psi \). The Hamiltonian typically includes the kinetic and potential energy of the system.

- **Time-Independent Schrödinger Equation (TISE):**

  For systems where the potential \( V(\mathbf{r}) \) does not change with time, the TDSE simplifies to:

  \[
  \hat{H} \psi(\mathbf{r}) = E \psi(\mathbf{r})
  \]

  - Here, **\( E \)** is the energy eigenvalue, representing the total energy of the quantum state.

  **Interpretation:**

  The TISE describes stationary states where the probability distribution of the particle does not change over time. The solutions \( \psi(\mathbf{r}) \) are known as eigenfunctions, and \( E \) are the corresponding eigenvalues.

**2. Operators and Observables:**

In quantum mechanics, physical quantities (observables) are represented by operators. When measuring an observable, the result is an eigenvalue of the corresponding operator.

- **Position Operator (\(\hat{\mathbf{r}}\)):**

  The position operator acts on the wave function as:

  \[
  \hat{\mathbf{r}} \psi(\mathbf{r}) = \mathbf{r} \psi(\mathbf{r})
  \]

  - **\( \mathbf{r} \)** is the position vector.
  
  **Interpretation:**

  The position operator returns the position vector when applied to the wave function, essentially giving the position of the particle.

- **Momentum Operator (\(\hat{\mathbf{p}}\)):**

  In the position representation, the momentum operator is:

  \[
  \hat{\mathbf{p}} = -i \hbar \nabla
  \]

  - **\( \nabla \)** (nabla) represents the gradient operator.

  **Interpretation:**

  The momentum operator involves differentiation with respect to position, reflecting how momentum changes with position in space. The factor of \(-i \hbar\) ensures the correct dimensional and quantum mechanical properties.

- **Hamiltonian Operator (\(\hat{H}\)):**

  The Hamiltonian for a non-relativistic particle is given by:

  \[
  \hat{H} = -\frac{\hbar^2}{2m} \nabla^2 + V(\mathbf{r})
  \]

  - **\( \frac{\hbar^2}{2m} \nabla^2 \)** is the kinetic energy term.
  - **\( V(\mathbf{r}) \)** is the potential energy function.

  **Interpretation:**

  The Hamiltonian operator combines kinetic and potential energy terms to describe the total energy of the system. The kinetic energy term involves the Laplacian operator \( \nabla^2 \), which measures the curvature of the wave function.

#### Hilbert Space and Linear Algebra

**1. Quantum States:**

Quantum states are vectors in Hilbert space, a complex vector space with an inner product.

- **Normalization:**

  The wave function \( \psi \) must be normalized:

  \[
  \int_{-\infty}^{\infty} |\psi(\mathbf{r})|^2 \, d\mathbf{r} = 1
  \]

  **Interpretation:**

  The integral of \( |\psi(\mathbf{r})|^2 \) over all space represents the total probability of finding the particle somewhere in space, which must be equal to 1.

**2. Eigenvalue Problems:**

Observables are represented by Hermitian operators, which have real eigenvalues and orthonormal eigenfunctions.

- **Eigenvalue Equation:**

  For an operator \( \hat{O} \), the eigenvalue equation is:

  \[
  \hat{O} \phi_n = \lambda_n \phi_n
  \]

  where \( \lambda_n \) are the eigenvalues, and \( \phi_n \) are the eigenfunctions.

  **Interpretation:**

  When measuring an observable represented by \( \hat{O} \), the possible outcomes are the eigenvalues \( \lambda_n \), and the corresponding states are described by the eigenfunctions \( \phi_n \).

### Quantum Dynamics

#### Time Evolution

**1. Unitary Evolution:**

Quantum state evolution is governed by unitary operators, ensuring probability conservation.

- **Time Evolution Operator:**

  \[
  \hat{U}(t) = e^{-\frac{i}{\hbar} \hat{H} t}
  \]

  **Interpretation:**

  The time evolution operator \( \hat{U}(t) \) describes how the quantum state evolves over time. The exponential operator arises from solving the TDSE in terms of time-independent solutions.

- **State Evolution:**

  The time-evolved state \( \psi(t) \) is given by:

  \[
  \psi(t) = \hat{U}(t) \psi(0)
  \]

  where \( \psi(0) \) is the initial state.

  **Interpretation:**

  The state \( \psi(t) \) represents the system's quantum state at time \( t \), evolving from the initial state \( \psi(0) \) according to the time evolution operator.

**2. Perturbation Theory:**

Perturbation theory is used to approximate solutions when a small disturbance is added to the system.

- **First-Order Perturbation:**

  For a Hamiltonian \( \hat{H} = \hat{H}_0 + \lambda \hat{H}' \):

  \[
  E_n^{(1)} = \langle \psi_n^{(0)} | \hat{H}' | \psi_n^{(0)} \rangle
  \]

  where \( \lambda \) is a small parameter, \( \hat{H}_0 \) is the unperturbed Hamiltonian, and \( \hat{H}' \) is the perturbation.

  **Interpretation:**

  The first-order correction to the energy \( E_n^{(1)} \) is the expectation value of the perturbation \( \hat{H}' \) in the unperturbed state \( \psi_n^{(0)} \). This provides an approximation to the energy levels when the perturbation is small.

#### Quantum Mechanics of Particles

**1. Single-Particle Systems:**

- **Free Particle:**

  For a free particle (no potential \( V(\mathbf{r}) \)):

  \[
  \psi(\mathbf{r}) = A e^{i \mathbf{k} \cdot \mathbf{r}}
  \]

  - **\( A \)** is a normalization constant.
  - **\( \mathbf{k} \)** is the wave vector, related to momentum \( \mathbf{p} = \hbar \mathbf{k} \).

  **Interpretation:**

  The wave function describes a free particle as a plane wave, where \( \mathbf{k} \) determines the wavelength and momentum.

- **Harmonic Oscillator:**

  For a particle in a potential \( V(x) = \frac{1}{2} m \omega^2 x^2 \):

  \[
  \hat{H} = -\frac{\hbar^2}{2m} \frac{d^2}{dx^2} + \frac{1}{2} m \omega^2 x^2
  \]

  The eigenfunctions are given by Hermite polynomials \( H_n(x) \):

  \[
  \psi_n(x) = \frac{1}{\sqrt{2^n n!}} \left( \frac{m \omega}{\pi \hbar} \right)^{1/4} e^{-\frac{m \omega x^2}{2 \hbar}} H_n \left( \sqrt{\frac{m \omega}{\hbar}} x \right)
  \]

  **Interpretation:**

  The harmonic oscillator's solutions involve Hermite polynomials, reflecting the quantized energy

 levels of the system.

- **Potential Wells:**

  For a particle in an infinite potential well of width \( L \):

  \[
  E_n = \frac{n^2 \pi^2 \hbar^2}{2mL^2}
  \]

  and

  \[
  \psi_n(x) = \sqrt{\frac{2}{L}} \sin\left(\frac{n \pi x}{L}\right)
  \]

  **Interpretation:**

  The energy levels are quantized, and the wave functions are standing waves confined within the well.

**2. Angular Momentum:**

- **Orbital Angular Momentum (\(\hat{L}\)):**

  The orbital angular momentum operator in spherical coordinates is:

  \[
  \hat{L}^2 = -\hbar^2 \left( \frac{1}{\sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial}{\partial \theta} \right) + \frac{1}{\sin^2 \theta} \frac{\partial^2}{\partial \phi^2} \right)
  \]

  - **\( \theta \)** and **\( \phi \)** are spherical angles.

  **Interpretation:**

  This operator measures the angular momentum of a particle in spherical coordinates. The eigenvalues are \( \hbar^2 l(l+1) \), where \( l \) is the angular momentum quantum number.

- **Spin Angular Momentum:**

  For spin-\(\frac{1}{2}\) particles, the spin operators are represented by Pauli matrices \( \sigma_x, \sigma_y, \sigma_z \). The eigenvalues of the spin operators are \( \pm \frac{\hbar}{2} \).

  **Interpretation:**

  Spin angular momentum represents intrinsic angular momentum not related to spatial motion. The Pauli matrices describe the spin components in quantum mechanics.

### Quantum Mechanics in Various Systems

#### Potential Wells and Barriers

**1. Quantum Tunneling:**

Quantum tunneling is the phenomenon where particles pass through potential barriers that they cannot classically surmount.

- **Transmission Coefficient:**

  For a particle encountering a potential barrier of height \( V_0 \) and width \( a \), the transmission coefficient \( T \) is approximately:

  \[
  T \approx e^{-2 \kappa a}
  \]

  where:

  \[
  \kappa = \sqrt{\frac{2m (V_0 - E)}{\hbar^2}}
  \]

  **Interpretation:**

  The transmission coefficient describes the probability of a particle tunneling through a barrier. The exponent \( -2 \kappa a \) indicates the exponential decay of the wave function within the barrier.

**2. Bound States:**

Bound states are quantum states where particles are confined to a region and have discrete energy levels.

- **Example of Infinite Potential Well:**

  The energy levels for a particle in a one-dimensional infinite potential well are:

  \[
  E_n = \frac{n^2 \pi^2 \hbar^2}{2mL^2}
  \]

  and the corresponding wave functions are:

  \[
  \psi_n(x) = \sqrt{\frac{2}{L}} \sin\left(\frac{n \pi x}{L}\right)
  \]

  **Interpretation:**

  The discrete energy levels arise due to boundary conditions that confine the particle within the well. The wave functions represent standing waves with nodes at the boundaries.

#### Multi-Particle Systems

**1. Identical Particles:**

- **Fermions and Bosons:**

  - **Fermions:** Follow the Pauli exclusion principle, which states that no two identical fermions can occupy the same quantum state. Their wave functions are antisymmetric under particle exchange.

  - **Bosons:** Can occupy the same state, and their wave functions are symmetric under particle exchange.

  **Interpretation:**

  The nature of particles (fermions or bosons) affects how they statistically distribute among available quantum states.

**2. Quantum Statistics:**

- **Bose-Einstein Statistics:**

  Applies to bosons and describes phenomena such as Bose-Einstein condensates, where particles occupy the same ground state.

- **Fermi-Dirac Statistics:**

  Applies to fermions and describes the distribution of particles in energy states, leading to the Fermi level in metals and semiconductors.

  **Interpretation:**

  Bose-Einstein and Fermi-Dirac statistics explain how particles behave at low temperatures and how they distribute themselves among quantum states.
