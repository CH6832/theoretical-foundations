### Complex Analysis

#### Analytic Functions

**1. Verifying Analyticity of Complex Functions**
- **Exercise:** Test whether the function \( f(z) = z^2 + e^z \) is analytic by using the Cauchy-Riemann equations. 
- **Real-world application:** Explore how the properties of analytic functions are used in fluid dynamics to model potential flow around objects.

**2. Mapping Properties of Analytic Functions**
- **Exercise:** Examine how the function \( f(z) = z^2 \) maps a square in the complex plane. Investigate how angles are preserved or distorted.
- **Real-world application:** Study the use of conformal mappings in electrostatics to solve boundary value problems for complex-shaped conductors.

**3. Conformal Mapping in Engineering**
- **Exercise:** Use the function \( f(z) = \frac{z - 1}{z + 1} \) to map the exterior of a circle to the interior of a unit disk.
- **Real-world application:** Apply conformal mappings to solve problems in aerodynamics, like airflow over an airfoil.

#### Complex Integration

**4. Contour Integration for Electric Fields**
- **Exercise:** Calculate the electric field around a charged wire using contour integration around the wire.
- **Real-world application:** Model the electromagnetic field in coaxial cables by integrating complex-valued functions.

**5. Application of Cauchy's Integral Theorem**
- **Exercise:** Prove Cauchy’s Integral Theorem by evaluating \( \oint_\gamma \frac{1}{z} dz \) around a closed contour.
- **Real-world application:** Use Cauchy’s Theorem to simplify calculations in complex impedance in electrical circuits.

**6. Cauchy's Integral Formula in Fluid Mechanics**
- **Exercise:** Apply Cauchy's Integral Formula to solve for the velocity potential in an ideal fluid.
- **Real-world application:** Understand how complex potentials are used to analyze 2D inviscid flow in fluid mechanics.

#### Residue Theorem

**7. Calculating Real Integrals with the Residue Theorem**
- **Exercise:** Use the Residue Theorem to compute the real integral \( \int_{-\infty}^{\infty} \frac{1}{x^2 + 1} dx \).
- **Real-world application:** Apply residue theory in evaluating integrals in quantum mechanics, particularly in path integrals.

**8. Evaluating Electrical Network Functions**
- **Exercise:** Use the Residue Theorem to analyze the transfer function of an RLC circuit.
- **Real-world application:** Utilize residue calculations to determine resonance frequencies in signal transmission systems.

**9. Residue Theorem in Stability Analysis**
- **Exercise:** Compute the residues of a transfer function to analyze the stability of control systems.
- **Real-world application:** Apply residue theory in feedback control systems to assess system stability through pole analysis.

#### Series and Laurent Series

**10. Laurent Series for Complex Functions**
- **Exercise:** Expand \( f(z) = \frac{1}{z(z-1)} \) in a Laurent series around \( z = 0 \).
- **Real-world application:** Use Laurent series expansions to model behavior near singularities in circuit analysis.

**11. Application of Power Series in Signal Processing**
- **Exercise:** Express \( f(z) = \frac{1}{1 - z} \) as a power series and find its region of convergence.
- **Real-world application:** Apply power series to analyze digital filter responses in signal processing.

**12. Laurent Series in Heat Conduction Problems**
- **Exercise:** Expand the heat conduction equation in a Laurent series to solve for temperature distribution in a ring.
- **Real-world application:** Use Laurent series to model steady-state heat flow in circular geometries.

### Fourier Analysis

#### Fourier Series

**13. Fourier Series in Sound Analysis**
- **Exercise:** Calculate the Fourier series of a square wave and analyze its harmonic content.
- **Real-world application:** Use Fourier series to decompose musical notes into their constituent frequencies, as done in sound synthesis and audio engineering.

**14. Fourier Series in Electrical Circuits**
- **Exercise:** Expand the voltage signal in a periodic circuit as a Fourier series to analyze harmonic distortion.
- **Real-world application:** Fourier series are used in power systems to assess signal integrity and mitigate harmonic distortion in AC power lines.

**15. Fourier Series in Heat Distribution**
- **Exercise:** Solve the heat equation on a circular domain using a Fourier series.
- **Real-world application:** Fourier series solutions are used in solving temperature distribution problems in heating and cooling systems in engineering.

**16. Fourier Series in Vibrations**
- **Exercise:** Use the Fourier series to analyze the displacement of a vibrating string.
- **Real-world application:** Apply Fourier series to model the resonance frequencies of guitar strings or in designing mechanical systems like suspension bridges.

#### Fourier Transforms

**17. Fourier Transform in Image Processing**
- **Exercise:** Compute the Fourier transform of a 2D image to filter noise and enhance edges.
- **Real-world application:** Use the Fourier transform in algorithms for image compression (e.g., JPEG) and reconstruction in MRI scans.

**18. Fourier Transform in Communication Systems**
- **Exercise:** Analyze the frequency spectrum of an AM modulated signal using the Fourier transform.
- **Real-world application:** Fourier transforms are essential in communication systems for signal modulation and demodulation, including radio transmission.

**19. Application of Fourier Transform in Optics**
- **Exercise:** Apply the Fourier transform to model light diffraction through a single slit.
- **Real-world application:** Use Fourier transforms in optics to design lenses and other optical systems through the analysis of wavefronts and diffraction patterns.

**20. Fourier Transform in Quantum Mechanics**
- **Exercise:** Compute the Fourier transform of the wave function in position space to obtain the momentum space representation.
- **Real-world application:** Use Fourier transforms to solve the Schrödinger equation for particle wave functions in quantum mechanics.

#### Fast Fourier Transform (FFT)

**21. FFT for Real-time Signal Processing**
- **Exercise:** Implement the FFT algorithm to filter noise from a real-time audio signal.
- **Real-world application:** FFT is widely used in noise reduction for audio processing, such as in hearing aids or voice recognition systems.

**22. FFT in Spectrum Analysis**
- **Exercise:** Apply the FFT to a sampled signal from a power grid and detect harmonic distortions.
- **Real-world application:** FFT is crucial in real-time power grid monitoring to detect and mitigate power quality issues.

**23. FFT in Medical Imaging**
- **Exercise:** Use FFT to process MRI signals and reconstruct a 3D image from the frequency domain.
- **Real-world application:** FFT algorithms are integral in reconstructing images in medical imaging technologies like MRI and CT scans.

**24. FFT in Wireless Communication**
- **Exercise:** Analyze the frequency components of a transmitted wireless signal using FFT.
- **Real-world application:** FFT is used in OFDM (Orthogonal Frequency Division Multiplexing), a key technique in modern communication systems like LTE and Wi-Fi.

### Applications in Physics and Engineering

**25. Fourier Analysis in Heat Diffusion**
- **Exercise:** Use the Fourier transform to solve the heat diffusion equation in an infinite domain.
- **Real-world application:** Analyze temperature distribution in industrial furnaces using Fourier transform techniques to optimize heating.

**26. Fourier Analysis in Wave Equations**
- **Exercise:** Solve the 1D wave equation using Fourier series to analyze a vibrating string with fixed boundaries.
- **Real-world application:** Use Fourier analysis in acoustic engineering to study sound wave propagation in rooms and concert halls.

**27. Fourier Transform in Earthquake Analysis**
- **Exercise:** Apply the Fourier transform to seismic data to identify dominant frequencies and predict earthquake behavior.
- **Real-world application:** Fourier transforms are used in geophysics to analyze seismic waves for earthquake detection and prediction.

**28. Complex Analysis in Fluid Flow**
- **Exercise:** Use complex potentials to solve for the flow around a cylinder in a fluid using \( f(z) = \frac{1}{z} \).
- **Real-world application:** Complex analysis is used to model inviscid flow patterns around objects like aircraft wings in aerodynamics.

**29. Fourier Transform in Digital Filters**
- **Exercise:** Design a digital low-pass filter using the Fourier transform to remove high-frequency noise from a signal.
- **Real-world application:** Fourier transform techniques are fundamental in the design of digital filters used in audio and video signal processing.

**30. Complex Analysis in Electromagnetics**
- **Exercise:** Apply complex analysis to solve Maxwell's equations for electromagnetic wave propagation in a waveguide.
- **Real-world application:** Use complex function theory to model and analyze the behavior of electromagnetic waves in waveguides, important in telecommunication systems like fiber optics.
