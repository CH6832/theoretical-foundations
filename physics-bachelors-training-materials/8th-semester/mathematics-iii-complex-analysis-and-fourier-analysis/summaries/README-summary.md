# Mathematics III: Complex Analysis and Fourier Analysis

## Course Description

This course delves into the advanced mathematical concepts of complex analysis and Fourier analysis. It aims to equip students with essential techniques for analyzing complex functions and understanding signal behavior. These tools are pivotal for tackling problems in various scientific and engineering disciplines.

## Key Topics

### Complex Analysis

#### Complex Functions

**Analytic Functions:**

- **Definition:**
  
  A function \( f(z) \), where \( z = x + iy \) is a complex variable, is analytic at a point \( z_0 \) if it has a complex derivative at \( z_0 \) and in some neighborhood around \( z_0 \). Formally, \( f(z) \) is analytic if:

  \[
  f'(z) = \lim_{h \to 0} \frac{f(z + h) - f(z)}{h}
  \]

  This limit must be independent of the direction from which \( h \) approaches zero.

- **Example:**

  The exponential function \( f(z) = e^z \) is analytic everywhere in the complex plane. Its derivative is \( e^z \), which is well-defined for all \( z \in \mathbb{C} \).

**Cauchy-Riemann Equations:**

- **Equations:**

  For a function \( f(z) = u(x, y) + iv(x, y) \), where \( u \) and \( v \) are real-valued functions of \( x \) and \( y \), the Cauchy-Riemann equations are:

  \[
  \frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}
  \]
  \[
  \frac{\partial u}{\partial y} = -\frac{\partial v}{\partial x}
  \]

  These equations ensure that \( f(z) \) is differentiable in the complex sense, which is stronger than just differentiability in the real sense.

- **Example:**

  For \( f(z) = z^2 \), where \( z = x + iy \):

  \[
  u(x, y) = x^2 - y^2
  \]
  \[
  v(x, y) = 2xy
  \]

  The Cauchy-Riemann equations hold since:

  \[
  \frac{\partial u}{\partial x} = 2x = \frac{\partial v}{\partial y}
  \]
  \[
  \frac{\partial u}{\partial y} = -2y = -\frac{\partial v}{\partial x}
  \]

#### Complex Integration

**Contour Integration:**

- **Integral Formula:**

  For a complex function \( f(z) \), the contour integral along a path \( \gamma \) is:

  \[
  \int_\gamma f(z) \, dz
  \]

  This integral is path-independent if \( f(z) \) is analytic within and on the contour \( \gamma \). If \( f(z) \) has no singularities inside \( \gamma \), the integral depends only on the endpoints of \( \gamma \).

- **Example:**

  For \( f(z) = \frac{1}{z - z_0} \) around a closed contour enclosing \( z_0 \):

  \[
  \oint_\gamma \frac{1}{z - z_0} \, dz = 2\pi i
  \]

  This result follows from the residue theorem.

**Residue Theorem:**

- **Theorem:**

  If \( f(z) \) is analytic inside and on a simple closed contour \( \gamma \) except for isolated singularities \( z_k \), then:

  \[
  \oint_\gamma f(z) \, dz = 2\pi i \sum \text{Res}(f, z_k)
  \]

  where \( \text{Res}(f, z_k) \) denotes the residue of \( f(z) \) at \( z_k \), which is the coefficient of \( \frac{1}{z - z_k} \) in the Laurent series expansion of \( f(z) \) around \( z_k \).

- **Residue Calculation:**

  For \( f(z) = \frac{1}{(z - z_0)^2} \), the residue at \( z_0 \) is 0 (since it's a pole of order 2, not 1). For \( f(z) = \frac{1}{z - z_0} \), the residue is 1.

#### Series and Laurent Series

**Power Series:**

- **Definition:**

  A complex function \( f(z) \) can be expressed as a power series around \( z_0 \):

  \[
  f(z) = \sum_{n=0}^{\infty} a_n (z - z_0)^n
  \]

  The radius of convergence \( R \) is:

  \[
  R = \frac{1}{\limsup_{n \to \infty} \sqrt[n]{|a_n|}}
  \]

- **Example:**

  The function \( f(z) = \frac{1}{1 - z} \) can be expanded into a power series:

  \[
  f(z) = \sum_{n=0}^{\infty} z^n
  \]

  for \( |z| < 1 \).

**Laurent Series:**

- **Definition:**

  For functions with singularities, the Laurent series expansion is:

  \[
  f(z) = \sum_{n=-\infty}^{\infty} a_n (z - z_0)^n
  \]

  This series includes terms with negative powers and allows representation of functions with poles.

- **Example:**

  For \( f(z) = \frac{1}{z(z-1)} \), the Laurent series around \( z = 0 \) is:

  \[
  \frac{1}{z(z-1)} = \frac{1}{z} \left(\frac{1}{1 - \frac{1}{z}}\right) = \frac{1}{z} \sum_{n=0}^{\infty} \frac{1}{z^n} = \sum_{n=-1}^{\infty} \frac{1}{z^n}
  \]

### Fourier Analysis

#### Fourier Series

**Expansion in Series:**

- **Fourier Series:**

  A periodic function \( f(x) \) with period \( T \) can be expanded as:

  \[
  f(x) = a_0 + \sum_{n=1}^{\infty} \left[ a_n \cos\left(\frac{2\pi n x}{T}\right) + b_n \sin\left(\frac{2\pi n x}{T}\right) \right]
  \]

  where \( a_n \) and \( b_n \) are Fourier coefficients:

  \[
  a_n = \frac{2}{T} \int_0^T f(x) \cos\left(\frac{2\pi n x}{T}\right) \, dx
  \]
  \[
  b_n = \frac{2}{T} \int_0^T f(x) \sin\left(\frac{2\pi n x}{T}\right) \, dx
  \]

- **Example:**

  For \( f(x) = x \) on the interval \([- \pi, \pi]\), the Fourier series is:

  \[
  f(x) = \frac{\pi^2 - x^2}{2} - \frac{2}{\pi} \sum_{n=1}^{\infty} \frac{(-1)^n}{n^2} \cos(nx)
  \]

**Convergence and Applications:**

- **Convergence:**

  The Fourier series converges to \( f(x) \) at points where \( f(x) \) is continuous. At points of discontinuity, the series converges to the average of the left-hand and right-hand limits of \( f(x) \).

- **Applications:**

  Used in solving partial differential equations (such as the heat equation) and analyzing periodic signals in engineering and physics.

#### Fourier Transforms

**Definition and Properties:**

- **Fourier Transform:**

  The Fourier transform \( \hat{f}(\omega) \) of a function \( f(x) \) is:

  \[
  \hat{f}(\omega) = \int_{-\infty}^{\infty} f(x) e^{-i \omega x} \, dx
  \]

  The inverse Fourier transform is:

  \[
  f(x) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \hat{f}(\omega) e^{i \omega x} \, d\omega
  \]

- **Properties:**

  - **Linearity:** 

    \[
    \mathcal{F}\{af(x) + bg(x)\} = a \hat{f}(\omega) + b \hat{g}(\omega)
    \]

  - **Duality:** 

    \[
    \mathcal{F}\{f(x)\}(\omega) \leftrightarrow \mathcal{F}\{\hat{f}(\omega)\}(-x)
    \]

  - **Convolution:** 

    \[
   

 \mathcal{F}\{f(x) * g(x)\} = \hat{f}(\omega) \cdot \hat{g}(\omega)
    \]

**Applications:**

- **Signal Processing:** Decomposing signals into their constituent frequencies, filtering noise, and designing signal processing algorithms.
- **Differential Equations:** Solving linear partial differential equations by transforming them into algebraic equations in the frequency domain.
- **Image Analysis:** Techniques for image compression, filtering, and reconstruction.

#### Discrete Fourier Transform (DFT)

**Definition:**

- **DFT:**

  For a discrete sequence \( \{x_n\} \) with \( N \) samples, the DFT is defined as:

  \[
  X_k = \sum_{n=0}^{N-1} x_n e^{-i \frac{2\pi k n}{N}}
  \]

  where \( X_k \) represents the frequency components of the sequence.

- **Example:**

  For a sequence \( x_n \) with \( N = 4 \) samples, the DFT provides 4 frequency components \( X_0, X_1, X_2, X_3 \).

**Fast Fourier Transform (FFT):**

- **FFT Algorithm:**

  The FFT is an efficient algorithm for computing the DFT. It reduces the computational complexity from \( O(N^2) \) to \( O(N \log N) \), making it suitable for large datasets. The most common FFT algorithm is the Cooley-Tukey algorithm, which recursively divides the DFT into smaller DFTs.

- **Applications:**

  - **Signal Processing:** Real-time processing and analysis of audio, video, and other signals.
  - **Data Analysis:** Efficiently handling large datasets for spectral analysis and filtering.
  - **Communication Systems:** Modulation, demodulation, and signal compression techniques.
