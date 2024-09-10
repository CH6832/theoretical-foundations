# Experimental Physics III

## Course Description

This course offers an in-depth practical experience in advanced experimental techniques in quantum mechanics, condensed matter physics, and nuclear physics. Students will perform experiments, analyze data, and interpret results to understand key physical concepts and phenomena.

## Key Topics

### **Quantum Mechanics Experiments**

#### **Interference and Diffraction**

- **Double-Slit Experiment:**

  - **Concept:**
    The double-slit experiment demonstrates wave-particle duality and the principle of superposition. When coherent light or particles pass through two slits, they create an interference pattern on a screen, showing characteristics of both waves and particles.

  - **Mathematical Explanation:**
    The intensity \( I \) of the interference pattern at a point on the screen is given by:
    \[
    I = I_0 \left[1 + \cos\left(\frac{2\pi d \sin \theta}{\lambda}\right)\right]
    \]
    where \( I_0 \) is the maximum intensity, \( d \) is the distance between the slits, \( \theta \) is the angle of observation, and \( \lambda \) is the wavelength of the light.

  - **Experimental Setup:**
    A coherent light source (e.g., a laser) illuminates two slits separated by a distance \( d \). The resulting pattern on a screen is analyzed to determine the wavelength of the light and to confirm wave-particle duality.

  - **Data Analysis:**
    Students measure the fringe spacing and use the above formula to calculate the wavelength of the light. The consistency of the pattern with theoretical predictions verifies the principles of quantum mechanics.

- **Single-Photon Interference:**

  - **Concept:**
    Single-photon experiments further explore quantum behavior, showing that even individual photons create an interference pattern, suggesting wave-like properties at the quantum level.

  - **Mathematical Explanation:**
    The probability density function for detecting photons at a particular position is:
    \[
    P(x) \propto \left| \psi(x) \right|^2
    \]
    where \( \psi(x) \) is the wavefunction of the photon.

  - **Experimental Setup:**
    A source emits photons one at a time through a double-slit apparatus. Over time, the buildup of an interference pattern on a detector screen illustrates the wave nature of photons.

  - **Data Analysis:**
    Students use the probability distribution function to analyze the interference pattern and discuss the implications for quantum mechanics and the concept of wavefunction collapse.

#### **Quantum Entanglement**

- **Bell's Theorem Tests:**

  - **Concept:**
    Bell's theorem experiments test the predictions of quantum mechanics against local hidden variable theories. They assess whether correlations between entangled particles violate Bell’s inequalities.

  - **Mathematical Explanation:**
    Bell's inequality for two entangled particles is often expressed as:
    \[
    S = \left\langle A_1B_1 \right\rangle + \left\langle A_1B_2 \right\rangle + \left\langle A_2B_1 \right\rangle - \left\langle A_2B_2 \right\rangle \leq 2
    \]
    where \( \left\langle A_iB_j \right\rangle \) are expectation values of measurement outcomes.

  - **Experimental Setup:**
    Entangled photons are sent to two detectors located far apart. Their polarization states are measured, and the correlation between them is analyzed to test Bell’s inequality.

  - **Data Analysis:**
    Students compare experimental results with theoretical predictions. A violation of Bell's inequality supports quantum mechanics and challenges classical notions of locality and realism.

- **Quantum Cryptography:**

  - **Concept:**
    Quantum cryptography uses the principles of quantum mechanics to create secure communication channels that are theoretically immune to eavesdropping.

  - **Mathematical Explanation:**
    The security of the quantum key distribution protocol, such as BB84, can be analyzed using the concept of quantum entropy:
    \[
    S(\rho) = - \text{Tr}(\rho \log \rho)
    \]
    where \( \rho \) is the density matrix of the quantum system.

  - **Experimental Setup:**
    A quantum key distribution system is set up using entangled photon pairs or weak coherent pulses. Key distribution and security are tested against potential eavesdropping.

  - **Data Analysis:**
    Students analyze the security of the key against various attack models, including quantum eavesdropping strategies. They use entropy measures to assess the robustness of the cryptographic protocol.

### **Condensed Matter Experiments**

#### **Crystal Structure and Properties**

- **X-ray Diffraction:**

  - **Concept:**
    X-ray diffraction (XRD) allows for the analysis of crystal structures by measuring the angles and intensities of diffracted X-rays.

  - **Mathematical Explanation:**
    Bragg's law relates the diffraction angle \( \theta \) to the lattice spacing \( d \) and the wavelength \( \lambda \):
    \[
    n\lambda = 2d \sin \theta
    \]
    where \( n \) is an integer representing the order of diffraction.

  - **Experimental Setup:**
    A crystal sample is placed in an X-ray beam, and the diffracted rays are measured with a detector. The resulting diffraction pattern is analyzed to determine the crystal lattice parameters.

  - **Data Analysis:**
    Students use Bragg's law to calculate the lattice spacing and identify the crystal structure. They also use the intensity data to refine structural models of the crystal.

- **Electrical Resistivity:**

  - **Concept:**
    Electrical resistivity is a measure of a material's resistance to electric current. It provides insights into the material's electronic properties and conductivity.

  - **Mathematical Explanation:**
    Resistivity \( \rho \) is related to resistance \( R \) and dimensions of the material:
    \[
    R = \rho \frac{L}{A}
    \]
    where \( L \) is the length of the sample and \( A \) is its cross-sectional area.

  - **Experimental Setup:**
    A sample material is placed in a circuit, and its resistance is measured as a function of temperature. The resistivity is calculated from these measurements.

  - **Data Analysis:**
    Students analyze the temperature dependence of resistivity, fitting the data to models such as the Drude model for metals or the Arrhenius equation for semiconductors.

#### **Magnetism and Superconductivity**

- **Magnetic Susceptibility:**

  - **Concept:**
    Magnetic susceptibility measures how a material responds to an external magnetic field, providing insights into its magnetic properties.

  - **Mathematical Explanation:**
    The susceptibility \( \chi \) is related to the magnetization \( M \) and the applied magnetic field \( H \):
    \[
    M = \chi H
    \]

  - **Experimental Setup:**
    A sample is placed in a magnetic field, and its magnetization is measured using a SQUID magnetometer or similar instrument.

  - **Data Analysis:**
    Students use the susceptibility data to identify the magnetic phase (paramagnetic, diamagnetic, or ferromagnetic) and determine parameters such as the Curie temperature for ferromagnetic materials.

- **Superconductivity:**

  - **Concept:**
    Superconductivity is the phenomenon where a material exhibits zero electrical resistance below a critical temperature and expels magnetic fields (Meissner effect).

  - **Mathematical Explanation:**
    The resistance \( R \) of a superconducting material drops to zero below its critical temperature \( T_c \). The critical magnetic field \( H_c \) is given by:
    \[
    H_c = \frac{\Phi_0}{2 \pi \xi^2}
    \]
    where \( \Phi_0 \) is the magnetic flux quantum and \( \xi \) is the coherence length.

  - **Experimental Setup:**
    A superconducting material is cooled below its \( T_c \) using liquid nitrogen. The resistance is measured, and the Meissner effect is observed by applying a magnetic field.

  - **Data Analysis:**
    Students analyze the transition temperature and critical magnetic field, discussing the implications for superconducting applications.

### **Nuclear Physics Experiments**

#### **Radioactive Decay**

- **Alpha, Beta, and Gamma Decay:**

  - **Concept:**
    Radioactive decay involves the transformation of an unstable nucleus into a more stable one, emitting alpha particles, beta particles, or gamma rays.

  - **Mathematical Explanation:**
    The decay rate \( \lambda \) (decay constant) is related to the half-life \( T_{1/2} \) by:
    \[
    \lambda = \frac{\ln 2}{T_{1/2}}
    \]

  - **Experimental Setup:**
    Detectors are used to measure the rate and type of radiation emitted by radioactive sources. The half-life and energy spectra of the emitted radiation are analyzed.

  - **Data Analysis:**
    Students calculate the decay constants and half-lives from the measured decay rates, analyzing the types of decay processes and their implications for nuclear stability.

- **Half-Life Determination:**

  - **Concept:**
    The half-life of a radioactive substance is the time it takes for half of its nuclei to decay.

  - **Mathematical Explanation:**
    The number of remaining nuclei \( N(t) \) at time \(

 t \) is given by:
    \[
    N(t) = N_0 e^{-\lambda t}
    \]
    where \( N_0 \) is the initial number of nuclei and \( \lambda \) is the decay constant.

  - **Experimental Setup:**
    The decay of a radioactive sample is monitored over time using a Geiger counter or similar detector.

  - **Data Analysis:**
    Students plot the number of counts versus time, fit the data to an exponential decay model, and extract the half-life of the sample.

#### **Particle Detection**

- **Geiger-Müller Counters:**

  - **Concept:**
    Geiger-Müller counters detect ionizing radiation by measuring the number of particles passing through a tube filled with gas.

  - **Mathematical Explanation:**
    The count rate \( R \) is related to the activity \( A \) of the radioactive source by:
    \[
    R = A \cdot \text{Efficiency}
    \]

  - **Experimental Setup:**
    A GM counter is used to measure radiation from a source. The count rate is recorded and analyzed for different source activities and distances.

  - **Data Analysis:**
    Students calculate the activity of the source and discuss the detector's efficiency and the implications for radiation safety.

- **Scintillation Detectors:**

  - **Concept:**
    Scintillation detectors measure ionizing radiation by detecting light emitted from a scintillation material when it interacts with radiation.

  - **Mathematical Explanation:**
    The light output \( L \) is proportional to the energy \( E \) of the incoming radiation:
    \[
    L = \text{Efficiency} \cdot E
    \]

  - **Experimental Setup:**
    Scintillation detectors are used to measure the energy and intensity of radiation. The emitted light is converted to an electrical signal by a photomultiplier tube.

  - **Data Analysis:**
    Students analyze the energy spectra and identify different types of radiation, discussing the applications of scintillation detectors in various fields.
