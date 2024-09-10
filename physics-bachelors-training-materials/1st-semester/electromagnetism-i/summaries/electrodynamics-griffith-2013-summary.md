### Vector Calculus

#### Gradient of a Scalar Field

**Formula:**

$\nabla f = \left( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \right)$

**Explanation:**

- The gradient \(\nabla f\) of a scalar function \(f\) represents the direction and rate of the fastest increase of \(f\).
- Each component \(\frac{\partial f}{\partial x}\), \(\frac{\partial f}{\partial y}\), and \(\frac{\partial f}{\partial z}\) is the partial derivative of \(f\) with respect to \(x\), \(y\), and \(z\), respectively.
- In physical terms, if \(f\) represents elevation, the gradient points in the direction of the steepest ascent and its magnitude indicates how steep the slope is.

#### Divergence of a Vector Field

**Formula:**

$\nabla \cdot \mathbf{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}$

**Explanation:**

- Divergence \(\nabla \cdot \mathbf{F}\) measures how much a vector field \(\mathbf{F}\) spreads out from a point.
- For a vector field \(\mathbf{F} = (F_x, F_y, F_z)\), the divergence is the sum of the partial derivatives of its components.
- Positive divergence indicates a source (field lines diverge), while negative divergence indicates a sink (field lines converge).

#### Curl of a Vector Field

**Formula:**

$\nabla \times \mathbf{F} = \left| \begin{array}{ccc}
\hat{i} & \hat{j} & \hat{k} \\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\
F_x & F_y & F_z
\end{array} \right|$

**Explanation:**

- The curl \(\nabla \times \mathbf{F}\) measures the rotation or circulation of the vector field \(\mathbf{F}\) around a point.
- It is computed as the determinant of the matrix with unit vectors \(\hat{i}\), \(\hat{j}\), and \(\hat{k}\) in the top row, partial derivatives in the second row, and components of \(\mathbf{F}\) in the third row.
- The result is a vector that points in the direction of the axis of rotation with a magnitude proportional to the amount of rotation.

#### Gradient of a Product

**Formula:**

$\nabla(fg) = f \nabla g + g \nabla f$

**Explanation:**

- When you have the product of two scalar functions \(f\) and \(g\), the gradient of this product is given by this formula.
- It combines the gradients of \(f\) and \(g\), scaled by the other function, indicating how changes in both functions affect the product.

#### Divergence of a Product

**Formula:**

$\nabla \cdot (f \mathbf{F}) = f (\nabla \cdot \mathbf{F}) + \mathbf{F} \cdot (\nabla f)$

**Explanation:**

- For a scalar function \(f\) and a vector field \(\mathbf{F}\), the divergence of their product is a combination of \(f\) times the divergence of \(\mathbf{F}\) plus \(\mathbf{F}\) dotted with the gradient of \(f\).
- This formula helps in calculating how the quantity described by \(f \mathbf{F}\) changes over space.

#### Curl of a Product

**Formula:**

$\nabla \times (f \mathbf{F}) = (\nabla f) \times \mathbf{F} + f (\nabla \times \mathbf{F})$

**Explanation:**

- This formula calculates the curl of the product of a scalar function \(f\) and a vector field \(\mathbf{F}\).
- It consists of two terms: \((\nabla f) \times \mathbf{F}\), which is the curl of \(f\) scaled by \(\mathbf{F}\), and \(f (\nabla \times \mathbf{F})\), which is \(f\) scaled by the curl of \(\mathbf{F}\).

### Integral Calculus

#### Line Integrals

**Formula:**

$\int_C \mathbf{F} \cdot d\mathbf{r}$

**Explanation:**

- The line integral of a vector field \(\mathbf{F}\) along a curve \(C\) measures the total effect of \(\mathbf{F}\) along \(C\).
- \(d\mathbf{r}\) is a differential element along \(C\). The dot product \(\mathbf{F} \cdot d\mathbf{r}\) projects the field \(\mathbf{F}\) onto the direction of \(d\mathbf{r}\), summing up along the path \(C\).

#### Surface Integrals

**Formula:**

$\int_S \mathbf{F} \cdot d\mathbf{A}$

**Explanation:**

- The surface integral of \(\mathbf{F}\) over a surface \(S\) measures the total flux of \(\mathbf{F}\) through \(S\).
- \(d\mathbf{A}\) is a differential area element on \(S\) with direction normal to the surface. The dot product \(\mathbf{F} \cdot d\mathbf{A}\) measures the component of \(\mathbf{F}\) passing through \(S\).

#### Volume Integrals

**Formula:**

$\int_V \rho \, dV$

**Explanation:**

- The volume integral of a scalar function \(\rho\) over a volume \(V\) calculates the total quantity of \(\rho\) within \(V\).
- \(dV\) is a differential volume element. This integral sums up \(\rho\) across the entire volume \(V\).

### Fundamental Theorems

#### Divergence Theorem

**Formula:**

$\int_V (\nabla \cdot \mathbf{F}) \, dV = \int_S \mathbf{F} \cdot d\mathbf{A}$

**Explanation:**

- The divergence theorem relates the volume integral of the divergence of a vector field \(\mathbf{F}\) to the surface integral of \(\mathbf{F}\) over the boundary surface \(S\) of volume \(V\).
- It essentially says that the total "outflow" of \(\mathbf{F}\) from \(V\) is equal to the flux of \(\mathbf{F}\) through the boundary \(S\).

#### Stokes' Theorem

**Formula:**

$\int_S (\nabla \times \mathbf{F}) \cdot d\mathbf{A} = \int_C \mathbf{F} \cdot d\mathbf{r}$

**Explanation:**

- Stokes' theorem relates the surface integral of the curl of \(\mathbf{F}\) over a surface \(S\) to the line integral of \(\mathbf{F}\) around the boundary curve \(C\) of \(S\).
- It connects the rotational aspects of a vector field on \(S\) to the circulation around its boundary \(C\).

### Electrostatics

#### Electric Field

**Formula:**

$\mathbf{E} = \frac{\mathbf{F}}{q}$

**Explanation:**

- The electric field \(\mathbf{E}\) represents the force per unit charge at a point in space.
- It describes how a test charge \(q\) would experience a force \(\mathbf{F}\) due to the presence of other charges.

#### Gauss's Law

**Formula:**

$\nabla \cdot \mathbf{E} = \frac{\rho}{\epsilon_0}$

**Explanation:**

- Gauss's law relates the divergence of the electric field \(\mathbf{E}\) to the charge density \(\rho\).
- It implies that the total electric flux out of a closed surface is proportional to the charge enclosed within that surface.

#### Electric Potential

**Formula:**

$V = -\int_\infty^r \mathbf{E} \cdot d\mathbf{r}$

**Explanation:**

- The electric potential \(V\) at a point is the work done to bring a unit positive charge from infinity to that point.
- It is related to the electric field by the negative line integral of \(\mathbf{E}\).

### Magnetostatics

#### Magnetic Field

**Formula:**

$\mathbf{F} = q (\mathbf{v} \times \mathbf{B})$

**Explanation:**

- The magnetic field \(\mathbf{B}\) exerts a force \(\mathbf{F}\) on a charged particle with charge \(q\) moving with velocity \(\mathbf{v}\).
- The force is perpendicular to both the velocity and the magnetic field, described by the cross product \(\mathbf{v} \times \mathbf{B}\).

#### Gauss's Law for Magnetism

**Formula:**

\

[
\nabla \cdot \mathbf{B} = 0$

**Explanation:**

- Gauss's law for magnetism states that there are no magnetic monopoles; hence the divergence of the magnetic field \(\mathbf{B}\) is zero.
- This implies that magnetic field lines are always closed loops or extend to infinity.

#### Ampère's Law

**Formula:**

$\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$

**Explanation:**

- Ampère's law relates the curl of the magnetic field \(\mathbf{B}\) to the current density \(\mathbf{J}\).
- It indicates how the magnetic field is generated by electric currents.

#### Maxwell's Equations

**Maxwell's Equations in Vacuum:**

1. **Gauss's Law for Electricity:**

$\nabla \cdot \mathbf{E} = \frac{\rho}{\epsilon_0}$

2. **Gauss's Law for Magnetism:**

$\nabla \cdot \mathbf{B} = 0$

3. **Faraday's Law of Induction:**

$\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$

4. **Ampère's Law with Maxwell's Addition:**

$\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$

**Explanation:**

- Maxwell's equations unify electromagnetism and describe how electric and magnetic fields propagate and interact.
- **Gauss's Law for Electricity** shows how electric charges create electric fields.
- **Gauss's Law for Magnetism** indicates that magnetic field lines are continuous with no beginning or end.
- **Faraday's Law** describes how changing magnetic fields produce electric fields.
- **Ampère's Law with Maxwell's Addition** combines the effects of currents and changing electric fields in producing magnetic fields.