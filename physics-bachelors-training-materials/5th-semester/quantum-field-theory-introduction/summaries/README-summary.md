# Quantum Field Theory - Introduction

## Course Description

This course introduces the fundamental concepts and techniques of Quantum Field Theory (QFT). It covers the theoretical framework of QFT, including the quantization of fields, interaction theories, and applications to particle physics. Emphasis is placed on both the theoretical foundations and practical applications of QFT.

## Key Topics

### **Basics of Quantum Field Theory**

- **Classical Field Theory:**

  - **Lagrangian and Hamiltonian Formalism:**

    - **Concept:**
      Classical fields, such as the electromagnetic field or scalar fields, are described using the Lagrangian density \( \mathcal{L} \), which depends on the fields and their derivatives. The field dynamics are obtained by applying the principle of least action.

    - **Mathematical Formulation:**
      The action \( S \) is given by:
      \[
      S = \int \mathcal{L} \, d^4x
      \]
      where \( \mathcal{L} \) is the Lagrangian density and \( d^4x \) is the integration over spacetime. The equations of motion are derived from:
      \[
      \frac{\delta S}{\delta \phi} = 0
      \]
      where \( \phi \) represents the field.

  - **Action Principle:**

    - **Concept:**
      The action principle states that the path taken by a field is the one that extremizes the action. For field theories, this results in the Euler-Lagrange equations applied to fields.

    - **Mathematical Formulation:**
      For a field \( \phi \), the Euler-Lagrange equation is:
      \[
      \frac{\partial \mathcal{L}}{\partial \phi} - \partial_\mu \left(\frac{\partial \mathcal{L}}{\partial (\partial_\mu \phi)}\right) = 0
      \]
      This equation governs the dynamics of the field.

- **Quantization of Fields:**

  - **Canonical Quantization:**

    - **Concept:**
      Canonical quantization involves promoting classical fields and their conjugate momenta to operators and imposing commutation relations.

    - **Mathematical Formulation:**
      For a scalar field \( \phi \), the quantization is achieved by:
      \[
      [\phi(\mathbf{x}, t), \pi(\mathbf{y}, t)] = i \hbar \delta^{(3)}(\mathbf{x} - \mathbf{y})
      \]
      where \( \pi \) is the conjugate momentum to \( \phi \), and \( \delta^{(3)} \) is the three-dimensional Dirac delta function.

  - **Path Integral Formulation:**

    - **Concept:**
      The path integral formulation expresses the transition amplitude as a sum over all possible field configurations weighted by the exponential of the action.

    - **Mathematical Formulation:**
      The path integral is:
      \[
      \langle \phi_f | \phi_i \rangle = \int \mathcal{D} \phi \, e^{i S[\phi]/\hbar}
      \]
      where \( \mathcal{D} \phi \) denotes integration over all field configurations, and \( S[\phi] \) is the action for a field configuration \( \phi \).

### **Quantum Electrodynamics (QED)**

- **Feynman Diagrams:**

  - **Diagrammatic Rules:**

    - **Concept:**
      Feynman diagrams provide a visual representation of particle interactions. Each diagram corresponds to a term in the perturbative expansion of the scattering amplitude.

    - **Mathematical Formulation:**
      The amplitude for a process is calculated by summing over all possible Feynman diagrams, where each diagram is assigned a mathematical expression based on the vertices, propagators, and external lines.

  - **Scattering Processes:**

    - **Concept:**
      Scattering amplitudes describe the probability of different outcomes from particle interactions.

    - **Mathematical Formulation:**
      For a simple \( e^+ e^- \to \mu^+ \mu^- \) process, the scattering amplitude \( \mathcal{M} \) can be computed using Feynman rules:
      \[
      \mathcal{M} \propto \frac{e^2}{(q^2 - m^2)^2}
      \]
      where \( e \) is the electric charge, \( q^2 \) is the momentum transfer, and \( m \) is the mass of the intermediate particle.

- **Renormalization:**

  - **Counterterms and Renormalization Procedure:**

    - **Concept:**
      Renormalization addresses infinities that arise in calculations by introducing counterterms that absorb these infinities, resulting in finite, physically meaningful predictions.

    - **Mathematical Formulation:**
      The renormalized charge \( e_r \) is related to the bare charge \( e_0 \) by:
      \[
      e_r = e_0 (1 + \delta e)
      \]
      where \( \delta e \) is the counterterm that absorbs the divergence.

  - **Physical Observables:**

    - **Concept:**
      After renormalization, physical quantities like scattering cross-sections and decay rates can be calculated and compared to experimental results.

    - **Mathematical Formulation:**
      For a physical observable \( O \), the renormalized value is given by:
      \[
      O_{\text{ren}} = O_{\text{bare}} + \text{(counterterms)}
      \]

### **Quantum Field Theory of Scalars and Spinors**

- **Scalar Fields:**

  - **Klein-Gordon Field:**

    - **Concept:**
      The Klein-Gordon equation describes the behavior of scalar particles, which are spin-0 particles.

    - **Mathematical Formulation:**
      The Klein-Gordon equation is:
      \[
      (\partial^\mu \partial_\mu + m^2) \phi = 0
      \]
      where \( m \) is the mass of the scalar field \( \phi \).

  - **Interaction Terms:**

    - **Concept:**
      Interaction terms describe how fields interact with each other. In perturbation theory, interactions are represented as vertices in Feynman diagrams.

    - **Mathematical Formulation:**
      For a scalar field theory with a \( \lambda \phi^4 \) interaction, the interaction term in the Lagrangian is:
      \[
      \mathcal{L}_{\text{int}} = -\frac{\lambda}{4!} \phi^4
      \]

- **Spinor Fields:**

  - **Dirac Equation:**

    - **Concept:**
      The Dirac equation describes spin-½ particles and incorporates both quantum mechanics and special relativity.

    - **Mathematical Formulation:**
      The Dirac equation is:
      \[
      (i \gamma^\mu \partial_\mu - m) \psi = 0
      \]
      where \( \gamma^\mu \) are the gamma matrices and \( \psi \) is the Dirac spinor.

  - **Majorana and Weyl Spinors:**

    - **Concept:**
      Majorana spinors are particles that are their own antiparticles, while Weyl spinors describe particles with definite chirality.

    - **Mathematical Formulation:**
      For Majorana spinors, the condition is:
      \[
      \psi = \psi^c
      \]
      where \( \psi^c \) is the charge-conjugated spinor. Weyl spinors satisfy chiral projections.

### **Gauge Theories and Symmetries**

- **Gauge Invariance:**

  - **Local Symmetry:**

    - **Concept:**
      Gauge invariance involves local symmetries and corresponds to interactions between fields. It ensures that physical laws are invariant under local transformations.

    - **Mathematical Formulation:**
      For an Abelian gauge theory, the gauge transformation is:
      \[
      A_\mu \to A_\mu + \frac{1}{e} \partial_\mu \alpha
      \]
      where \( \alpha \) is the gauge function and \( A_\mu \) is the gauge field.

  - **Yang-Mills Theory:**

    - **Concept:**
      Yang-Mills theory extends gauge invariance to non-Abelian gauge fields, resulting in complex interaction dynamics.

    - **Mathematical Formulation:**
      The Yang-Mills field strength tensor is:
      \[
      F_{\mu\nu}^a = \partial_\mu A_\nu^a - \partial_\nu A_\mu^a + g f^{abc} A_\mu^b A_\nu^c
      \]
      where \( f^{abc} \) are the structure constants of the gauge group.

- **Spontaneous Symmetry Breaking:**

  - **Higgs Mechanism:**

    - **Concept:**
      Spontaneous symmetry breaking occurs when the vacuum state does not exhibit the symmetry of the Lagrangian, leading to mass generation for gauge bosons.

    - **Mathematical Formulation:**
      The Higgs field \( \phi \) acquires a vacuum expectation value \( \langle \phi \rangle = v \), breaking the symmetry and giving mass to gauge bosons:
      \[
      \math

cal{L}_{\text{Higgs}} = |D_\mu \phi|^2 - \mu^2 |\phi|^2 + \lambda |\phi|^4
      \]

### **Advanced Topics**

- **Effective Field Theories:**

  - **Low-Energy Descriptions:**

    - **Concept:**
      Effective field theories provide descriptions of physical systems at low energies, capturing the relevant degrees of freedom without requiring a full high-energy theory.

    - **Mathematical Formulation:**
      The effective Lagrangian can be expressed as:
      \[
      \mathcal{L}_{\text{eff}} = \mathcal{L}_{\text{free}} + \mathcal{L}_{\text{int}}
      \]
      where \( \mathcal{L}_{\text{free}} \) is the free theory and \( \mathcal{L}_{\text{int}} \) includes interaction terms relevant at low energies.

  - **Renormalization Group:**

    - **Concept:**
      The renormalization group studies how physical parameters change with energy scales, providing insight into the behavior of systems at different scales.

    - **Mathematical Formulation:**
      The renormalization group equation is:
      \[
      \frac{d g(\mu)}{d \ln \mu} = \beta(g(\mu))
      \]
      where \( g(\mu) \) is a coupling constant and \( \beta(g) \) is the beta function.

- **Quantum Gravity:**

  - **Introduction to Quantum Gravity:**

    - **Concept:**
      Quantum gravity aims to describe the gravitational force within the framework of quantum mechanics, addressing the unification of general relativity and quantum theory.

    - **Mathematical Formulation:**
      Quantum gravity theories, such as loop quantum gravity or string theory, seek to develop a quantum description of spacetime geometry and dynamics.
