### **Smooth Manifolds**

1. **Find Local Coordinates:** Consider the 2-dimensional surface of a donut (a torus) embedded in \( \mathbb{R}^3 \). Show that it can be covered by two charts, and find local coordinates for each chart. Verify the smoothness of the transition maps.

2. **Differentiable Map between Manifolds:** Let \( f: \mathbb{R}^2 \to \mathbb{R}^3 \) be given by \( f(x, y) = (x, y, \sin(x^2 + y^2)) \). Prove that \( f \) is a differentiable map and determine its differential at the origin.

3. **Diffeomorphisms on the Sphere:** Show that the stereographic projection from \( S^2 \setminus \{ (0,0,1) \} \) to \( \mathbb{R}^2 \) is a diffeomorphism. Determine the inverse map explicitly.

4. **Check Smoothness:** Given the map \( g: \mathbb{R}^2 \to \mathbb{R}^3 \) defined by \( g(u, v) = (u, v, \exp(-u^2 - v^2)) \), prove that \( g \) is smooth and determine its Jacobian matrix.

### **Tangent Vectors and Tangent Spaces**

5. **Compute Tangent Vectors:** For the manifold \( M = \mathbb{R}^2 \) with coordinates \((x, y)\), find the tangent vectors at the point \( (1, 1) \) corresponding to the vector fields \( X = \frac{\partial}{\partial x} + \frac{\partial}{\partial y} \) and \( Y = \frac{\partial}{\partial x} - \frac{\partial}{\partial y} \).

6. **Vector Fields on a Torus:** On the torus \( T^2 \) given by \( \mathbb{R}^2 / \mathbb{Z}^2 \), define vector fields \( X \) and \( Y \) in local coordinates and compute their Lie bracket \( [X, Y] \).

7. **Pushforward Calculation:** For the map \( f: \mathbb{R}^2 \to \mathbb{R}^2 \) given by \( f(x, y) = (x^2, y^2) \), compute the pushforward of the vector \( (1, 0) \) at the point \( (1, 1) \).

8. **Pullback of Differential Forms:** Compute the pullback \( f^*(dx^1 \wedge dx^2) \) where \( f: \mathbb{R}^2 \to \mathbb{R}^2 \) is defined by \( f(x, y) = (e^x, \ln(y)) \).

### **Differential Forms and Integration**

9. **Compute Exterior Derivatives:** Find the exterior derivative of the 1-form \( \omega = x \, dy - y \, dx \) on \( \mathbb{R}^2 \).

10. **Apply Stokes' Theorem:** Let \( M \) be the unit disk in \( \mathbb{R}^2 \), and let \( \omega = x \, dy - y \, dx \). Compute the integral of \( d\omega \) over \( M \) and verify Stokes' theorem.

11. **Integration on Submanifolds:** For the 2-sphere \( S^2 \subset \mathbb{R}^3 \), compute the integral of the 2-form \( \omega = \sin(\theta) \, d\phi \) over the hemisphere parameterized by spherical coordinates \( (\theta, \phi) \) where \( 0 \leq \theta \leq \pi/2 \) and \( 0 \leq \phi < 2\pi \).

12. **Evaluate a 3-Form Integral:** Compute the integral of the 3-form \( \omega = x \, dy \wedge dz \) over the volume of the unit cube in \( \mathbb{R}^3 \).

### **Riemannian Geometry**

13. **Calculate Riemannian Metrics:** For the 2-dimensional surface of a sphere \( S^2 \) in \( \mathbb{R}^3 \) with metric induced from the Euclidean metric, compute the Riemannian metric tensor in spherical coordinates \( (\theta, \phi) \).

14. **Find Geodesics:** Determine the geodesics on the 2-dimensional surface of a cylinder. Use the fact that the cylinder can be parameterized by \( (u, v) \) where \( u \) is the angular coordinate and \( v \) is the height.

15. **Compute Christoffel Symbols:** Compute the Christoffel symbols for the Riemannian metric \( g = dx^2 + e^{2x} dy^2 \) on \( \mathbb{R}^2 \).

16. **Curvature Computation:** Calculate the Ricci curvature tensor for the 2-dimensional sphere \( S^2 \) with the standard round metric.

17. **Geodesic Completeness:** Show that \( \mathbb{R}^2 \) with the standard Euclidean metric is geodesically complete. 

### **Connections and Covariant Derivatives**

18. **Covariant Derivative Calculation:** Compute the covariant derivative of the vector field \( V = x \frac{\partial}{\partial x} + y \frac{\partial}{\partial y} \) on \( \mathbb{R}^2 \) using the standard Euclidean connection.

19. **Parallel Transport:** Show how parallel transport along a straight line in \( \mathbb{R}^3 \) affects a tangent vector at a given point.

20. **Affine Connection on the Torus:** Calculate the Christoffel symbols for the standard metric on the torus \( T^2 = \mathbb{R}^2 / \mathbb{Z}^2 \).

### **Advanced Topics in Differential Geometry**

21. **Lie Group and Lie Algebra:** For the Lie group \( \text{SO}(3) \), find the corresponding Lie algebra and compute the exponential map of an element in the Lie algebra.

22. **Kähler Manifolds:** Verify that the complex projective space \( \mathbb{CP}^n \) is a Kähler manifold. Compute the associated (1,1)-form and check that it is closed.

23. **Fiber Bundles:** Consider a trivial fiber bundle \( E = \mathbb{R}^2 \times \mathbb{R} \) with projection \( \pi: E \to \mathbb{R}^2 \). Define a connection and compute parallel transport of a vector field along a curve.

24. **Characteristic Classes:** Compute the Chern class of the complex line bundle over \( \mathbb{CP}^1 \) given by the standard complex line bundle.

25. **Morse Theory Application:** Analyze the critical points of the Morse function \( f: \mathbb{R}^2 \to \mathbb{R} \) given by \( f(x, y) = x^4 + y^4 - 4(x^2 + y^2) \) and determine the topological changes in the level sets.

26. **Homotopy and Manifolds:** For a smooth map \( f: S^2 \to \mathbb{R}^3 \) given by \( f(\theta, \phi) = (\sin\theta \cos\phi, \sin\theta \sin\phi, \cos\theta) \), show that it is a smooth embedding and describe its image.

27. **Riemannian Manifold Examples:** Describe the geodesics on a 2-dimensional surface of a sphere with radius \( R \) and compute the length of the shortest path between two antipodal points.

28. **Comparison of Metrics:** Compare the geodesics on the surface of a cylinder with radius \( R \) and a plane. Compute and compare the distances between two points on both surfaces.

29. **Complex Manifolds and Geometry:** For the complex manifold \( \mathbb{C}^n \) with the standard complex structure, compute the volume form and compare it with the real volume form obtained by considering \( \mathbb{C}^n \) as a real manifold.

30. **Integration of Differential Forms in Physics:** Compute the integral of the 4-form \( \omega = dx^1 \wedge dx^2 \wedge dx^3 \wedge dx^4 \) over a 4-dimensional hypercube in \( \mathbb{R}^4 \) and relate it to physical concepts such as volume.
