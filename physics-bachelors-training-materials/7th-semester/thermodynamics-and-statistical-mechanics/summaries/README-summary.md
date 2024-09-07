# Thermodynamics and Statistical Mechanics

## Thermodynamics

### Laws of Thermodynamics

**1. Zeroth Law of Thermodynamics**

- **Statement:** If two systems, \( A \) and \( B \), are each in thermal equilibrium with a third system, \( C \), then \( A \) and \( B \) are in thermal equilibrium with each other.

  **Mathematical Representation:**
  
  \[
  A \text{ is in equilibrium with } C \text{ and } B \text{ is in equilibrium with } C \implies A \text{ is in equilibrium with } B
  \]

- **Explanation:** This law is fundamental for defining temperature. It implies that temperature is a property that is equal for systems in thermal equilibrium. The Zeroth Law allows us to use thermometers to measure temperature because they rely on the principle that systems in thermal equilibrium with each other have the same temperature.

**2. First Law of Thermodynamics**

- **Statement:** Energy can neither be created nor destroyed; it can only be transformed from one form to another. For a closed system, the change in internal energy is equal to the heat added to the system minus the work done by the system.

  **Mathematical Representation:**
  
  \[
  \Delta U = Q - W
  \]

  where:

  - **\( \Delta U \)** is the change in internal energy.
  - **\( Q \)** is the heat added to the system.
  - **\( W \)** is the work done by the system.

- **Explanation:** This law is a statement of energy conservation. It can be applied in various processes:

  - **Isothermal Process:** Temperature is constant (\( \Delta U = 0 \)). Therefore, \( Q = W \). This implies that all heat added to the system is converted into work.
  
  - **Adiabatic Process:** No heat exchange (\( Q = 0 \)). Thus, \( \Delta U = -W \). The internal energy change is entirely due to work done on or by the system.

**3. Second Law of Thermodynamics**

- **Statement:** The entropy of an isolated system never decreases; it either increases or remains constant. Entropy quantifies the amount of disorder or randomness in a system.

  **Mathematical Representation:**
  
  \[
  \Delta S \geq \frac{Q}{T}
  \]

  where:

  - **\( \Delta S \)** is the change in entropy.
  - **\( Q \)** is the heat added to the system.
  - **\( T \)** is the absolute temperature.

- **Explanation:** The second law introduces the concept of entropy, emphasizing that natural processes tend to move towards greater disorder. It also implies that it is impossible to convert all heat energy into work without any losses. The **Carnot cycle** is a theoretical construct that illustrates the maximum efficiency of heat engines, defined as:

  \[
  \eta = 1 - \frac{T_c}{T_h}
  \]

  where:

  - **\( T_h \)** is the temperature of the hot reservoir.
  - **\( T_c \)** is the temperature of the cold reservoir.

**4. Third Law of Thermodynamics**

- **Statement:** As the temperature of a system approaches absolute zero, the entropy approaches a constant minimum. For a perfect crystal, the entropy approaches zero.

  **Mathematical Representation:**
  
  \[
  \lim_{T \to 0} S = 0
  \]

- **Explanation:** This law implies that it is impossible to reach absolute zero in a finite number of steps. It provides a reference point for measuring entropy and explains why the entropy of a perfect crystal is zero at absolute zero.

### Thermodynamic Potentials

**1. Helmholtz Free Energy (\( F \))**

- **Definition:**

  \[
  F = U - TS
  \]

  where:

  - **\( U \)** is the internal energy.
  - **\( T \)** is the temperature.
  - **\( S \)** is the entropy.

- **Explanation:** Helmholtz free energy measures the work obtainable from a system at constant temperature and volume. It is particularly useful in systems where temperature is controlled. The Helmholtz free energy helps determine if a process will occur spontaneously. For example, at constant temperature, a process is spontaneous if \( \Delta F < 0 \).

**2. Gibbs Free Energy (\( G \))**

- **Definition:**

  \[
  G = H - TS
  \]

  where:

  - **\( H \)** is the enthalpy of the system.

  **Enthalpy (H) = U + PV**

- **Explanation:** Gibbs free energy determines the maximum reversible work at constant temperature and pressure. It is crucial for predicting equilibrium and phase transitions. The change in Gibbs free energy for a process is given by:

  \[
  \Delta G = \Delta H - T \Delta S
  \]

  For a reaction to be spontaneous at constant temperature and pressure, \( \Delta G < 0 \).

### Equations of State

**1. Ideal Gas Law**

- **Statement:**

  \[
  PV = nRT
  \]

  where:

  - **\( P \)** is the pressure.
  - **\( V \)** is the volume.
  - **\( n \)** is the number of moles.
  - **\( R \)** is the universal gas constant (\( 8.314 \, \text{J/mol·K} \)).
  - **\( T \)** is the temperature.

- **Explanation:** The ideal gas law describes the behavior of an ideal gas, where interactions between molecules are negligible. It assumes that gas molecules do not occupy any volume and do not interact with each other. Deviations from this behavior occur at high pressures and low temperatures.

**2. Van der Waals Equation**

- **Statement:**

  \[
  \left( P + \frac{a}{V^2} \right) (V - b) = nRT
  \]

  where:

  - **\( a \)** accounts for intermolecular forces.
  - **\( b \)** accounts for the finite size of molecules.

- **Explanation:** The Van der Waals equation corrects the ideal gas law to account for real gas effects. It introduces two parameters:

  - **\( a \):** Corrects for attractive forces between molecules.
  - **\( b \):** Corrects for the volume occupied by gas molecules.

### Statistical Mechanics

#### Microcanonical, Canonical, and Grand Canonical Ensembles

**1. Microcanonical Ensemble**

- **Definition:** Represents an isolated system with fixed energy \( E \), volume \( V \), and number of particles \( N \).

  **Entropy (S):**

  \[
  S = k_B \ln \Omega
  \]

  where:

  - **\( \Omega \)** is the number of accessible microstates.
  - **\( k_B \)** is Boltzmann's constant.

- **Explanation:** In the microcanonical ensemble, the system is completely isolated, and energy is conserved. The entropy is related to the number of microstates corresponding to a particular macrostate. For large systems, entropy is extensive and proportional to the logarithm of the number of microstates.

**2. Canonical Ensemble**

- **Definition:** Represents a system in thermal equilibrium with a heat bath at constant temperature \( T \), with fixed volume \( V \) and number of particles \( N \).

  **Partition Function (Z):**

  \[
  Z = \sum_i e^{-\beta E_i}
  \]

  where:

  - **\( \beta = \frac{1}{k_B T} \)**
  - **\( E_i \)** are the energy levels.

  **Free Energy (F):**

  \[
  F = -k_B T \ln Z
  \]

- **Explanation:** The canonical ensemble allows the system to exchange energy with the surroundings but not particles. The partition function sums over all possible states of the system, weighted by their Boltzmann factor. Free energy determines the equilibrium state, where the probability distribution of states is given by:

  \[
  P_i = \frac{e^{-\beta E_i}}{Z}
  \]

**3. Grand Canonical Ensemble**

- **Definition:** Represents a system in equilibrium with a reservoir that can exchange both energy and particles, with fixed temperature \( T \), volume \( V \), and chemical potential \( \mu \).

  **Grand Partition Function (Ξ):**

  \[
  \Xi = \sum_{N} \sum_{i} e^{-\beta (E_i - \mu N)}
  \]

  where:

  - **\( \mu \)** is the chemical potential.
  - **\( N \)** is the number of particles.

  **Grand Free Energy (G):**

  \[
  G = -k_B T \ln \Xi
  \]

- **Explanation:** The grand canonical ensemble is useful for systems where the number of particles can vary, such as in chemical reactions or open systems. The grand partition function sums over all possible states and particle numbers, weighted by their energy and chemical potential.

#### Statistical Distributions

**1. Maxwell-Boltzmann Distribution**

- **Definition:** Describes the distribution of speeds in an ideal gas.

  \[
  f(v) = \left( \frac{m}{2 \pi k_B T} \right)^{3/2} 4 \pi v^2 e^{

-\frac{mv^2}{2k_B T}}
  \]

  where:

  - **\( v \)** is the speed of a particle.
  - **\( m \)** is the mass of a particle.

- **Explanation:** This distribution applies to classical particles and assumes that particles are distinguishable and non-interacting. It is derived from the Boltzmann distribution and provides insights into the kinetic theory of gases.

**2. Fermi-Dirac Distribution**

- **Definition:** Describes the distribution of particles in a system of non-interacting fermions (e.g., electrons) at thermal equilibrium.

  \[
  f(E) = \frac{1}{e^{(E - \mu)/k_B T} + 1}
  \]

  where:

  - **\( E \)** is the energy of a state.
  - **\( \mu \)** is the chemical potential.

- **Explanation:** Fermi-Dirac statistics apply to fermions, which obey the Pauli exclusion principle (no two fermions can occupy the same quantum state). This distribution explains phenomena such as electron degeneracy pressure in white dwarfs and the behavior of electrons in metals.

**3. Bose-Einstein Distribution**

- **Definition:** Describes the distribution of particles in a system of non-interacting bosons (e.g., photons) at thermal equilibrium.

  \[
  f(E) = \frac{1}{e^{(E - \mu)/k_B T} - 1}
  \]

  where:

  - **\( E \)** is the energy of a state.
  - **\( \mu \)** is the chemical potential (usually \( \mu = 0 \) for photons).

- **Explanation:** Bose-Einstein statistics apply to bosons, which do not obey the Pauli exclusion principle. This distribution accounts for phenomena like Bose-Einstein condensation, where particles occupy the lowest energy state at low temperatures.

### Applications and Models

**1. Ising Model**

- **Description:** A lattice model used to study phase transitions, specifically ferromagnetism. Each site on the lattice has a spin that can be up or down.

  - **Hamiltonian (H):**

    \[
    H = -J \sum_{\langle i,j \rangle} S_i S_j - h \sum_i S_i
    \]

    where:

    - **\( J \)** is the interaction strength between neighboring spins.
    - **\( h \)** is an external magnetic field.
    - **\( \langle i,j \rangle \)** denotes summation over nearest-neighbor pairs.

- **Explanation:** The Ising model helps understand how interactions between neighboring spins lead to collective phenomena such as magnetization. It is a simplified model but provides insights into more complex phase transitions.

**2. Ideal Gas and Classical Models**

- **Description:** Classical statistical mechanics is used to derive macroscopic properties of gases based on the microscopic behavior of particles.

  - **Ideal Gas Law:**

    \[
    PV = nRT
    \]

  - **Applications:** This law applies to ideal gases, where the particles do not interact and occupy no volume. Deviations from this ideal behavior are studied using more complex models like the Van der Waals equation.

- **Explanation:** Classical models assume ideal conditions and use statistical methods to predict properties like pressure, volume, and temperature. They provide a basis for understanding more complex systems and real gases.
