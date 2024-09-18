### **1. Turing Machines, Computability, and Complexity Classes (P, NP, PSPACE, EXP)**

1. **(Theoretical)** Design a Turing machine to decide the language \( L = \{0^n 1^n | n \geq 0\} \). Write its transition table and prove that the machine halts for all inputs.
2. **(Theoretical)** Prove that the halting problem is undecidable by reducing it from the diagonalization argument.
3. **(Theoretical)** Show that the class EXP is a proper subset of EXPSPACE by proving that EXPSPACE-complete problems cannot be solved in exponential time.
4. **(Implementation)** Write a program to simulate a basic deterministic Turing machine and use it to recognize a context-free language like \( L = \{ a^n b^n | n \geq 1\} \).
5. **(Theoretical)** Use the Time Hierarchy Theorem to prove that \( P \neq EXP \).
6. **(Theoretical)** Show that every regular language is decidable by constructing a Turing machine that recognizes any given regular expression.
7. **(Theoretical)** Prove that PSPACE is closed under complement using Savitch’s Theorem.
8. **(Theoretical)** Show that the class NP is contained in EXPTIME by proving that an NP problem can be solved using brute force in exponential time.
9. **(Theoretical)** Prove that the set of all Turing machines that halt on the empty string is not recursively enumerable.
10. **(Implementation)** Simulate a Universal Turing Machine for a simple language and analyze its time and space complexity.

---

### **2. Reductions and NP-Completeness**

11. **(Theoretical)** Prove that the SAT problem is NP-complete by reducing an arbitrary NP problem to SAT using the Cook-Levin Theorem.
12. **(Theoretical)** Reduce the Vertex Cover problem to the Independent Set problem, proving that Independent Set is NP-complete.
13. **(Implementation)** Implement a reduction from 3-SAT to the Hamiltonian Cycle problem to prove NP-completeness of the Hamiltonian Cycle.
14. **(Theoretical)** Prove that if there exists a polynomial-time algorithm for an NP-complete problem, then P = NP.
15. **(Theoretical)** Prove that the Traveling Salesman Problem (TSP) in the decision form is NP-complete by reducing it from the Hamiltonian Cycle problem.
16. **(Implementation)** Implement the reduction from 3-SAT to the Subset-Sum problem and demonstrate it on small instances of 3-SAT formulas.
17. **(Theoretical)** Show that the Partition problem is NP-complete by reducing Subset-Sum to Partition.
18. **(Theoretical)** Prove that CLIQUE is NP-complete by reducing 3-SAT to CLIQUE.
19. **(Implementation)** Implement a polynomial-time verifier for the Hamiltonian Cycle problem and demonstrate how it verifies certificates for specific instances.
20. **(Theoretical)** Show that the NP-complete problems are closed under polynomial-time many-one reductions.

---

### **3. Randomized Complexity Classes (RP, BPP, etc.)**

21. **(Theoretical)** Prove that every language in RP can be solved by a probabilistic Turing machine that has a non-zero chance of producing incorrect results only for “yes” instances.
22. **(Implementation)** Implement a randomized algorithm for the primality testing problem and show that it runs in polynomial time with a bounded error.
23. **(Theoretical)** Prove that BPP is closed under intersection, i.e., if two languages are in BPP, then their intersection is also in BPP.
24. **(Theoretical)** Prove that \( P \subseteq BPP \) by constructing a deterministic simulation of a probabilistic algorithm with error probability \( \frac{1}{2} \).
25. **(Implementation)** Implement the Miller-Rabin primality test and analyze its error probability. Test it on large integers.
26. **(Theoretical)** Show that any language in RP is also in NP.
27. **(Theoretical)** Prove that ZPP (zero-error probabilistic polynomial time) is the intersection of RP and co-RP.
28. **(Theoretical)** Show that every language in P is also in BPP by demonstrating that deterministic algorithms can be simulated by probabilistic algorithms with zero error.
29. **(Implementation)** Implement a Las Vegas algorithm for randomized quicksort and compare its performance to the deterministic version.
30. **(Theoretical)** Show that if NP = RP, then all NP-complete problems are solvable in randomized polynomial time.

---

### **4. Quantum Complexity (BQP, QMA)**

31. **(Theoretical)** Prove that BQP (Bounded-error Quantum Polynomial Time) is contained in PSPACE by demonstrating that a quantum computation can be simulated using polynomial space.
32. **(Implementation)** Implement Grover’s algorithm in a quantum computing framework (e.g., Qiskit) and demonstrate it on a small search problem.
33. **(Theoretical)** Show that if BQP = P, then factoring large integers can be done in polynomial time (implication for RSA cryptography).
34. **(Theoretical)** Prove that \( NP \subseteq QMA \) by constructing a quantum verifier that checks an NP problem using a quantum witness.
35. **(Theoretical)** Demonstrate that QMA problems are verifiable in polynomial time with a quantum proof by constructing a circuit that verifies a QMA instance.
36. **(Theoretical)** Show that BQP is not known to be contained in NP by analyzing the limitations of classical verifiers for quantum computations.
37. **(Implementation)** Simulate a quantum circuit for Shor’s algorithm for factoring integers and demonstrate it for small composite numbers.
38. **(Theoretical)** Prove that quantum entanglement provides an exponential advantage for some communication complexity problems (e.g., the quantum fingerprinting problem).
39. **(Implementation)** Implement a basic quantum teleportation protocol using a quantum computing framework and explain its relevance to quantum communication.
40. **(Theoretical)** Show that the Deutsch-Jozsa algorithm solves a problem in polynomial time that requires exponential time classically, and prove its correctness.

---

### **5. P vs NP and Modern Conjectures**

41. **(Theoretical)** Prove that if P = NP, then every problem in NP can be solved in polynomial time, and explain its consequences for cryptography.
42. **(Theoretical)** Use the PCP Theorem to show that approximating the maximum clique size within a factor of \( n^\epsilon \) for any \( \epsilon > 0 \) is NP-hard.
43. **(Implementation)** Implement a brute-force solution to the 3-SAT problem and experimentally evaluate how its running time scales with the size of the input.
44. **(Theoretical)** Prove that if there is a polynomial-time algorithm for solving TSP exactly, then P = NP.
45. **(Theoretical)** Explain the consequences of the statement "P ≠ NP" for the complexity of solving optimization problems exactly versus approximately.
46. **(Theoretical)** Analyze the implications of Ladner’s Theorem, which states that if P ≠ NP, then there are problems in NP that are neither in P nor NP-complete.
47. **(Implementation)** Implement an approximation algorithm for the Traveling Salesman Problem and compare its performance to an exact algorithm on small instances.
48. **(Theoretical)** Show that natural proofs, as defined by Razborov and Rudich, cannot be used to prove P ≠ NP unless strong cryptographic assumptions are violated.
49. **(Theoretical)** Analyze how interactive proofs (IP = PSPACE) affect the boundary between NP and PSPACE in light of the P vs NP question.
50. **(Theoretical)** Prove that co-NP is not known to be contained in P, and discuss the significance of this in relation to the P vs NP problem.

---

These 50 exercises provide comprehensive coverage of the topics in **Computation Theory and Complexity** and are designed to engage students in both theoretical proofs and practical implementations at an advanced level.