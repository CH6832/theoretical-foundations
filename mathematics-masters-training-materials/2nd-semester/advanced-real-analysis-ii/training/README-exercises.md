### **1. Measure Theory**

1. **Sigma-Algebras and Measures**: Prove that any countable subset of \( \mathbb{R} \) is a measurable set with respect to the Lebesgue measure. Discuss the implications for the measure of the set.

2. **Lebesgue Measure and Countable Additivity**: Show that the Lebesgue measure on \( \mathbb{R} \) is countably additive by proving it for disjoint intervals.

3. **Outer Measures and Carathéodory’s Extension Theorem**: Using Carathéodory’s extension theorem, construct the Lebesgue measure starting from the outer measure defined on intervals.

4. **Measurable Functions and Egorov’s Theorem**: Given a sequence of measurable functions \( f_n \) on \( [0,1] \) that converges almost everywhere to a function \( f \), prove that for any \( \epsilon > 0 \), there exists a measurable set \( E \) with \( \mu(E) < \epsilon \) where \( f_n \) converges uniformly to \( f \) on \( [0,1] \setminus E \).

5. **Lusin’s Theorem**: Prove that if \( f \) is a measurable function on \( [0,1] \) and \( \epsilon > 0 \), then there exists a compact subset \( K \subset [0,1] \) such that \( f \) is continuous on \( K \) and \( \mu([0,1] \setminus K) < \epsilon \).

6. **Application of Outer Measures**: Consider the set of all rational numbers in \( [0,1] \). Prove that this set has Lebesgue measure zero.

7. **Product Measures**: Let \( \mu \) and \( \nu \) be the Lebesgue measures on \( [0,1] \). Show that \( \mu \times \nu \) is the Lebesgue measure on \( [0,1] \times [0,1] \) by evaluating the measure of a rectangle.

8. **Integration with Respect to a Measure**: Compute the Lebesgue integral of the function \( f(x) = x \) over the interval \( [0,1] \) and compare it to the Riemann integral.

9. **Monotone Convergence Theorem**: Prove the monotone convergence theorem by considering an increasing sequence of non-negative functions \( f_n(x) = \frac{x}{n} \) on \( [0,1] \).

10. **Fatou’s Lemma**: Prove Fatou’s Lemma for a sequence of non-negative measurable functions \( f_n \) on \( [0,1] \) and use it to show that \( \int_{[0,1]} \liminf_{n \to \infty} f_n \, d\mu \leq \liminf_{n \to \infty} \int_{[0,1]} f_n \, d\mu \).

### **2. Lp Spaces**

11. **Lp Space Computations**: Calculate \( \| f \|_p \) for the function \( f(x) = x^2 \) on \( [0,1] \) where \( p = 2 \) and compare it with \( \| f \|_1 \) and \( \| f \|_\infty \).

12. **Hölder’s Inequality**: Verify Hölder’s inequality for the functions \( f(x) = x \) and \( g(x) = x^2 \) on \( [0,1] \) with \( p = 2 \) and \( q = 2 \).

13. **Minkowski’s Inequality**: Prove Minkowski’s inequality for \( L^p \) spaces using the example of \( f(x) = x \) and \( g(x) = x^2 \) on \( [0,1] \).

14. **Completeness of Lp Spaces**: Show that \( L^2([0,1]) \) is a complete space by demonstrating that every Cauchy sequence in \( L^2([0,1]) \) converges to a limit in \( L^2([0,1]) \).

15. **Dual Space of Lp**: Determine the dual space of \( L^1([0,1]) \) and show that it is isometrically isomorphic to \( L^\infty([0,1]) \).

### **3. Radon-Nikodym Theorem**

16. **Radon-Nikodym Derivative**: Given two measures \( \mu \) and \( \nu \) on \( [0,1] \) where \( \nu \) is absolutely continuous with respect to \( \mu \), compute the Radon-Nikodym derivative \( \frac{d\nu}{d\mu} \) for \( \nu(A) = \int_A \chi_{[0,1/2]} \, d\mu \).

17. **Conditional Expectation**: Compute the conditional expectation of \( X \) given a sigma-algebra \( \mathcal{G} \) for \( X \) being a random variable and \( \mathcal{G} \) a sub-sigma-algebra of \( \mathcal{F} \).

18. **Application in Probability**: Apply the Radon-Nikodym theorem to compute the probability density function of a random variable given a probability measure and its absolutely continuous counterpart.

19. **Radon-Nikodym and Integration**: Show that if \( \nu \ll \mu \) and \( f = \frac{d\nu}{d\mu} \), then \( \nu(A) = \int_A f \, d\mu \) for any measurable set \( A \).

20. **Absolute Continuity**: Prove that if \( \nu \) is absolutely continuous with respect to \( \mu \), then for any measurable set \( A \) with \( \mu(A) = 0 \), \( \nu(A) = 0 \).

### **4. Fubini’s Theorem**

21. **Iterated Integrals**: Use Fubini’s theorem to compute the double integral of \( f(x,y) = e^{-(x^2+y^2)} \) over \( [0,1] \times [0,1] \).

22. **Product Measures in Practice**: Show how to evaluate the integral of \( f(x,y) = x^2 y \) over \( [0,1] \times [0,1] \) by applying Fubini’s theorem.

23. **Fubini’s Theorem and Convergence**: Prove Fubini’s theorem by demonstrating that the integral \( \int_{[0,1] \times [0,1]} f(x,y) \, d\mu(x) \, d\nu(y) \) equals \( \int_0^1 \left( \int_0^1 f(x,y) \, d\nu(y) \right) d\mu(x) \) for an integrable function \( f \).

24. **Application to Probability**: Apply Fubini’s theorem to compute the expected value of a bivariate random variable \( (X, Y) \) with joint density \( f_{X,Y}(x,y) = x y \) over the unit square.

### **5. Functional Analysis**

25. **Normed Spaces**: Prove that every normed space is a vector space with a norm satisfying the properties of positivity, scalability, and the triangle inequality.

26. **Banach Space Properties**: Show that \( \ell^p \) spaces are Banach spaces for \( 1 \leq p < \infty \) and provide an example of a Banach space that is not reflexive.

27. **Hahn-Banach Theorem**: Apply the Hahn-Banach theorem to extend a linear functional defined on a subspace of a normed space to the entire space.

28. **Bounded Linear Operators**: Prove that the space of bounded linear operators on a finite-dimensional normed vector space is isomorphic to the space of matrices.

29. **Open Mapping Theorem**: Use the open mapping theorem to show that any surjective continuous linear operator from a Banach space to a normed space is an open map.

30. **Uniform Boundedness Principle**: Prove the uniform boundedness principle and apply it to a sequence of bounded linear operators on a Banach space.
