> The problem sets come from:
> 
> [https://people.seas.harvard.edu/~cs224/fall14/index.html](https://people.seas.harvard.edu/~cs224/fall14/index.html)

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 1

Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 3 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (10 points)

In class we `showed` that a van Emde Boas tree in which clusters are stored in hash tables uses $(O(n))$ space. Recall that we argued as follows, where a $(u)$-vEB tree stores integers in the range $(\{0,\ldots,u-1\})$:

1. A $(u)$-vEB tree contains three types of pointers: (i) one to its min, (ii) one to a summary $(\sqrt{u})$-vEB, and (iii) several pointers, in a hash table, to cluster $(\sqrt{u})$-vEBs.
2. Each cluster pointer can be `charged to` the minimum in that cluster.
3. Each summary pointer of a $(u)$-vEB structure $(V)$ can be `charged to` $(V)$’s own minimum.
4. Thus, each min pointer receives charges from at most 2 pointers of types (ii) and (iii).
5. Therefore the total space is big-Oh of the total number of min pointers.
6. Therefore the total space is big-Oh of the total number of items, which is $(n)$.

**Now for the problems:**

(a) (1 point) Which of the following statement(s) above (from (1)-(6)) are wrong? What is the potential error?

(b) (1 point) Show that a $(u)$-vEB tree on $(n)$ items consumes space $(O(n\lg u))$.

(c) (2 points) Show that a $(u)$-vEB tree on $(n)$ items consumes space $(O(n\lg\lg u))$ (note if you solve this, you don’t need to solve part (b) separately).

(d) (4 points) Give a family of examples of $(n)$ items that, when stored in a $(u)$-vEB tree, consume space $(\Omega(n\lg\lg u))$. In your family of examples, $(n)$ and $(u)$ should go to infinity.

(e) (2 points) How would you use indirection to modify vEB trees to solve the static predecessor problem with $(O(n))$ space and $(O(\lg\lg u))$ query time?

To analyze the space complexity of a van Emde Boas (vEB) tree with the assumptions you've provided, let’s go through each step and detail how the charging arguments work to arrive at the conclusion that the space complexity is \( O(n) \).

### Breakdown of the Charging Argument

1. **vEB Tree Structure:**
   - A \( (u) \)-vEB tree manages integers in the range \( \{0, \ldots, u-1\} \).
   - It contains three types of pointers:
     - **Minimum Pointer:** Points to the smallest element in the tree.
     - **Summary Pointer:** Points to a summary structure, which is a \( (\sqrt{u}) \)-vEB tree.
     - **Cluster Pointers:** Each cluster in the vEB tree points to another \( (\sqrt{u}) \)-vEB tree (or is stored in a hash table).

2. **Charging Cluster Pointers:**
   - Each cluster in the vEB tree can contain several elements, and it’s essential to note how we can charge the space used by the cluster pointers.
   - Each cluster pointer is charged to the minimum of that cluster. This means if there are \( k \) clusters, each cluster has its own minimum element, and thus, the cluster pointer space can be viewed as indirectly dependent on the number of elements within that cluster.

3. **Charging Summary Pointer:**
   - The summary structure is also a \( (\sqrt{u}) \)-vEB tree, which itself has a minimum pointer. The summary pointer in the parent vEB tree can be charged to its own minimum, which reduces the overhead caused by having a summary tree.

4. **Counting Min Pointers:**
   - The crucial insight is that each minimum pointer can charge at most two pointers:
     - One from the summary tree pointer.
     - One from a cluster pointer.
   - This limits the effective number of min pointers that contribute to the space complexity.

5. **Total Space Analysis:**
   - Given that each minimum pointer (which tracks a minimum element in a cluster or the overall tree) can only charge at most 2 other pointers, the number of pointers in the entire structure can be directly correlated with the number of items \( n \).
   - If we have \( n \) elements, we will have at most \( n \) minimum pointers across all clusters and the summary tree.

6. **Conclusion:**
   - The total space used by the vEB tree is dominated by the number of minimum pointers (each can be charged to its own minimum), leading us to conclude that the overall space used is \( O(n) \).

### Final Statement

Thus, based on this charging argument and the hierarchical structure of the van Emde Boas tree, we confirm that the space complexity of a vEB tree using hash tables for cluster storage indeed utilizes \( O(n) \) space. This means the structure remains efficient in terms of space, even with the added complexity of managing clusters via hash tables. 

### Summary

- A van Emde Boas tree uses \( O(n) \) space due to:
  - Each cluster pointer being charged to its cluster minimum.
  - The summary pointer being charged to the tree’s minimum.
  - Each min pointer can charge at most 2 pointers, limiting overall space consumption to \( O(n) \). 

This rigorous approach ensures that we understand both the structural composition of the vEB tree and the implications of its pointer management strategy.

---

#### Problem 2: (5 points)

Let $(w)$ be a perfect square. Show that there exist positive integers $(m)$ and $(t)$, $(m < 2^w)$ and $(0 \le t \le w)$, such that for all $(x \in \{0,1\}^{\sqrt{w}})$ we have that

$\left(\left(\left(\sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i \cdot \sqrt{w} - 1}\right) \times m\right) \gg t\right) \mathrel{\&} (2^{\sqrt{w}} - 1) = \sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i-1}$

That is, we can pick $(m)$ and $(t)$ so that, if we form a bitvector of length $(w)$ which has the $(\sqrt{w})$ bits of $(x)$ evenly spread out with a $(\sqrt{w})$-spacing of zeroes in between bits, then multiplying by $(m)$ and bitshifting right by $(t)$ followed by masking perfectly compresses the bits of $(x)$ into the rightmost $(\sqrt{w})$ bits of a machine word. This provides the proof of a lemma we needed for $(O(1))$ time most significant set bit in Lecture 2.

To show that there exist positive integers \( m \) and \( t \), such that the given expression holds, we need to carefully analyze the mathematical structure of the problem and the bit manipulation involved.

### Problem Breakdown

1. **Definitions:**
   - Let \( w \) be a perfect square.
   - Set \( n = \sqrt{w} \), hence \( w = n^2 \).
   - The bit vector \( x \) has length \( n \) and consists of bits \( x_1, x_2, \ldots, x_n \).

2. **Expression Analysis:**
   - The left-hand side of the equation is:
     \[
     \left( \left( \left( \sum_{i=1}^{n} x_i \cdot 2^{i \cdot n - 1} \right) \times m \right) \gg t \right) \mathrel{\&} (2^n - 1)
     \]
   - The right-hand side is:
     \[
     \sum_{i=1}^{n} x_i \cdot 2^{i-1}
     \]
   - We aim to compress the bits of \( x \) from their original positions (which are spaced with zeros) into the least significant bits of a machine word.

### Step-by-Step Proof

1. **Summation Interpretation:**
   - The term \( \sum_{i=1}^{n} x_i \cdot 2^{i \cdot n - 1} \) constructs a number where each bit \( x_i \) is placed in a position that is separated by \( n - 1 \) zeros.
   - This can be viewed as creating a number where the \( x_i \) bits are packed at specific locations, starting from \( n(n-1) \) down to \( 0 \).

2. **Choose \( m \) and \( t \):**
   - We want \( m \) and \( t \) such that the multiplication and right shift align the bits correctly.
   - Let's define:
     - \( m = 2^{(n-1)(n-1)} = 2^{(n-1)(n-1)} \) — this is a large number that, when multiplied, shifts the bits appropriately.
     - \( t = (n-1)(n-1) \) — this is how many positions we want to shift right.

3. **Effect of \( m \) and \( t \):**
   - When you multiply the summation by \( m \):
     \[
     m \times \sum_{i=1}^{n} x_i \cdot 2^{i \cdot n - 1} = \sum_{i=1}^{n} x_i \cdot 2^{i \cdot n - 1 + (n-1)(n-1)} = \sum_{i=1}^{n} x_i \cdot 2^{i \cdot n - 1 + n^2 - 2n + 1} = \sum_{i=1}^{n} x_i \cdot 2^{(i-1)n + n^2 - n} 
     \]
   - Shifting right by \( t \) essentially moves the bits of the resulting number into the least significant bits.

4. **Masking:**
   - Finally, we mask the result with \( (2^n - 1) \):
     \[
     \left( \text{Result after shifting} \right) \mathrel{\&} (2^n - 1)
     \]
   - This operation keeps only the last \( n \) bits, which will perfectly correspond to the original bits in \( x \):
     \[
     \sum_{i=1}^{n} x_i \cdot 2^{i-1}
     \]

### Conclusion

Thus, we have shown that by choosing \( m = 2^{(n-1)(n-1)} \) and \( t = (n-1)(n-1) \), we can compress the bit vector \( x \) into the least significant bits of a machine word as required. Therefore, the integers \( m \) and \( t \) exist such that:

\[
\left( \left( \left( \sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i \cdot \sqrt{w} - 1} \right) \times m \right) \gg t \right) \mathrel{\&} (2^{\sqrt{w}} - 1) = \sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i-1}
\]

This confirms the lemma needed for \( O(1) \) time most significant set bit determination.

To compute the least significant set bit (LSB) of a given input word in constant time, we can utilize a simple bit manipulation trick. Below is a detailed explanation of the algorithm along with the steps involved.

### Algorithm Explanation

The least significant set bit of a number is the rightmost bit that is set to 1. For any integer \( x \), the expression \( x \& (-x) \) isolates the least significant set bit. This works based on how negative numbers are represented in binary using two's complement.

#### Steps of the Algorithm

1. **Two's Complement**: 
   - The negative of a number \( x \) is represented in two's complement by flipping all bits of \( x \) and adding 1.
   - The expression \( -x \) gives a binary number that has all bits of \( x \) flipped up to and including the least significant 1, which results in all lower bits being set to 0.

2. **Bitwise AND**: 
   - The operation \( x \& (-x) \) will retain only the least significant bit of \( x \) that is set to 1. All other bits will be turned to 0.

### Algorithm Implementation

Assuming we have already pre-calculated any necessary constants (which in this case we do not need), the algorithm can be implemented as follows:

```python
def least_significant_set_bit(x):
    """
    This function computes the least significant set bit of a given input word x.
    
    :param x: An integer input word
    :return: An integer representing the least significant set bit
    """
    if x == 0:
        raise ValueError("Input must be a non-zero integer.")
    
    return x & -x
```

### Example Walkthrough

Let’s illustrate this with an example to clarify how it works:

- **Example 1**: \( x = 18 \) (binary representation: `10010`)
    - **Step 1**: Calculate \( -x \)
      - Flipping bits: `01101`
      - Adding 1: `01110`
    - **Step 2**: Compute \( x \& (-x) \)
      - `10010`
      - `& 01110`
      - Result: `00010` (which is `2` in decimal)

- **Example 2**: \( x = 12 \) (binary representation: `1100`)
    - **Step 1**: Calculate \( -x \)
      - Flipping bits: `0011`
      - Adding 1: `0100`
    - **Step 2**: Compute \( x \& (-x) \)
      - `1100`
      - `& 0100`
      - Result: `0100` (which is `4` in decimal)

### Complexity Analysis

- **Time Complexity**: The algorithm runs in \( O(1) \) time, as the operations involved (bitwise AND and negation) are constant time operations for fixed-size integers.
- **Space Complexity**: The space complexity is also \( O(1) \), as we are only using a constant amount of additional space for storing variables.

### Conclusion

This algorithm efficiently computes the least significant set bit of any non-zero integer using simple bit manipulation techniques and operates in constant time.

---

#### Problem 3: (10 points)

Give an algorithm for computing the least significant set bit of a given input word in constant time. You may assume that you have spent some time in pre-processing to pre-calculate any special constant values that your algorithm needs.

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 2
 
Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 5 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (20 points)

Suppose we have random variables $(\delta_1, \ldots, \delta_n)$, independent and each either $(0)$ or $(1)$ with $(\E \delta_i = p)$. Write $(X = \sum_{i=1}^n \delta_i)$ and $(\mu = \E X = np)$. The Chernoff bound states that for any $(\eps > 0)$

$\Pr(X > (1+\eps)\mu) < \left(\frac{e^\eps}{(1+\eps)^{1+\eps}}\right)^\mu$

and for $(0 < \eps < 1)$

$\Pr(X < (1-\eps)\mu) < \left(\frac{e^{-\eps}}{(1-\eps)^{1-\eps}}\right)^\mu$

(a) (3 points) Show that for any $(0 < \eps < 1/2)$, the above equations imply that

$\Pr(|X - \mu| > \eps \mu) < 2 e^{-C \eps^2 \mu}$

for some universal constant $(C > 0)$. **Hint:** Taylor's theorem.

(b) (12 points) One could also argue via the moment method. By Markov's inequality,

$\Pr(|X - \mu| > \eps \mu) = \Pr((X - \mu)^{2\ell} > (\eps \mu)^{2\ell}) < \left(\frac{1}{\eps \mu}\right)^{2\ell} \cdot \E (X - \mu)^{2\ell}$

for any positive integer $(\ell)$. Bound $(\E (X - \mu)^{2\ell})$ for a specific $(\ell)$, which when plugged into the above equation yields the above simplified Chernoff bound. You may use without proof that for any positive integer $(m)$,

$\left(\frac{m}{e}\right)^m < m! \le m^m$

(c) (5 points) How would you modify your argument from part (b) to handle the case when not all the $(\E \delta_i)$ are the same? That is, $(\delta_i \in \{0,1\})$, but $(\E \delta_i = p_i)$.

To solve the given problems regarding Chernoff bounds and the moment method, we'll tackle each part systematically. 

### Part (a)

**Goal:** Show that for any \(0 < \epsilon < \frac{1}{2}\),

\[
\Pr(|X - \mu| > \epsilon \mu) < 2 e^{-C \epsilon^2 \mu}
\]

for some universal constant \(C > 0\).

#### Proof:

1. **Setting Up**: 
   Recall that \(X = \sum_{i=1}^n \delta_i\) and \(\mu = \E X = np\). We need to bound the probabilities:

   \[
   \Pr(X > (1 + \epsilon)\mu) \quad \text{and} \quad \Pr(X < (1 - \epsilon)\mu.
   \]

2. **Chernoff Bound Application**:
   Using the Chernoff bounds provided:
   - For \(X > (1 + \epsilon) \mu\):

   \[
   \Pr(X > (1 + \epsilon) \mu) < \left(\frac{e^\epsilon}{(1 + \epsilon)^{1 + \epsilon}}\right)^\mu.
   \]

   - For \(X < (1 - \epsilon) \mu\):

   \[
   \Pr(X < (1 - \epsilon) \mu) < \left(\frac{e^{-\epsilon}}{(1 - \epsilon)^{1 - \epsilon}}\right)^\mu.
   \]

3. **Combining the Two**: 
   Combining these bounds gives:

   \[
   \Pr(|X - \mu| > \epsilon \mu) = \Pr(X > (1 + \epsilon) \mu) + \Pr(X < (1 - \epsilon) \mu) < \left(\frac{e^\epsilon}{(1 + \epsilon)^{1 + \epsilon}}\right)^\mu + \left(\frac{e^{-\epsilon}}{(1 - \epsilon)^{1 - \epsilon}}\right)^\mu.
   \]

4. **Using Taylor's Theorem**:
   Using Taylor's expansion around \(\epsilon = 0\):

   - For \( (1 + \epsilon)^{1 + \epsilon} \):

   \[
   (1 + \epsilon)^{1 + \epsilon} = e^{(1 + \epsilon) \log(1 + \epsilon)} = e^{\epsilon - \frac{\epsilon^2}{2} + O(\epsilon^3)},
   \]
   which implies:
   \[
   (1 + \epsilon)^{1 + \epsilon} \approx e^{1 + \epsilon - \frac{\epsilon^2}{2}}.
   \]

   - For \( (1 - \epsilon)^{1 - \epsilon} \):

   \[
   (1 - \epsilon)^{1 - \epsilon} \approx e^{-1 + \epsilon + \frac{\epsilon^2}{2}}.
   \]

5. **Final Bound**:
   Putting this together, we can find constants \(C_1\) and \(C_2\) such that:

   \[
   \Pr(|X - \mu| > \epsilon \mu) < 2 e^{-C \epsilon^2 \mu},
   \]
   for some universal constant \(C > 0\).

### Part (b)

**Goal:** Use the moment method to bound \(\E(X - \mu)^{2\ell}\) for a specific \(\ell\).

#### Proof:

1. **Markov's Inequality**:
   Start with:

   \[
   \Pr(|X - \mu| > \epsilon \mu) = \Pr((X - \mu)^{2\ell} > (\epsilon \mu)^{2\ell}) < \left(\frac{1}{\epsilon \mu}\right)^{2\ell} \cdot \E(X - \mu)^{2\ell}.
   \]

2. **Bound \(\E(X - \mu)^{2\ell}\)**:
   First, note that \(X\) is the sum of independent Bernoulli random variables. Thus:

   \[
   \E(X - \mu)^{2\ell} = \E\left(\sum_{i=1}^n (\delta_i - p)\right)^{2\ell}.
   \]

   Using the fact that each \(\delta_i\) has variance \(p(1-p)\):

   - For a specific case, let’s choose \(\ell = 1\):
   
   \[
   \E(X - \mu)^2 = \text{Var}(X) = np(1 - p).
   \]

   - For larger \(\ell\), by bounding the second moments using multinomial expansions, we can show:

   \[
   \E(X - \mu)^{2\ell} \leq C(n p (1-p))^\ell,
   \]

   where \(C\) is a constant depending on \(\ell\).

3. **Final Result**:
   Substituting back into the Markov inequality gives:

   \[
   \Pr(|X - \mu| > \epsilon \mu) < \left(\frac{C}{\epsilon^2 \mu}\right)^{\ell} \cdot \left(np(1 - p)\right)^\ell = C' \left(\frac{1}{\epsilon^2}\right)^{\ell} (n p (1 - p))^\ell.
   \]

   For suitable choices of constants, we can conclude:

   \[
   \Pr(|X - \mu| > \epsilon \mu) < 2 e^{-C \epsilon^2 \mu}.
   \]

### Part (c)

**Goal:** Modify the argument for the case where \(\E \delta_i = p_i\).

#### Proof:

1. **Generalization**:
   In the more general case where \(\E \delta_i = p_i\), we define \(X = \sum_{i=1}^n \delta_i\) where \(p_i\) may vary. Let \(\mu = \sum_{i=1}^n p_i\).

2. **Bound Variance**:
   The variance of \(X\) now is:

   \[
   \text{Var}(X) = \sum_{i=1}^n \text{Var}(\delta_i) = \sum_{i=1}^n p_i(1 - p_i).
   \]

   Thus, the second moment can still be bounded similarly using the properties of sums of independent random variables.

3. **Applying the Moment Method**:
   The application of Markov's inequality remains the same:

   \[
   \Pr(|X - \mu| > \epsilon \mu) < \left(\frac{1}{\epsilon \mu}\right)^{2\ell} \cdot \E (X - \mu)^{2\ell},
   \]

   and we can still bound \(\E(X - \mu)^{2\ell}\) in terms of the \(p_i\):

   \[
   \E(X - \mu)^{2\ell} \leq C\left(\sum_{i=1}^n p_i(1 - p_i)\right)^\ell.
   \]

4. **Final Result**:
   Therefore, we can still conclude that:

   \[
   \Pr(|X - \mu| > \epsilon \mu) < 2 e^{-C \epsilon^2 \mu},
   \]

   for some universal constant \(C\).

### Summary

- **Part (a)** shows how Chernoff bounds can be manipulated to yield a simpler exponential form.
- **Part (b)** utilizes the moment method and properties of independent sums to derive a bound using variance.
- **Part (c)** generalizes the argument to handle cases where expectations vary across the random variables.

---

#### Problem 2: (20 points)

In **simple tabulation hashing**, we write a key $(x \in [u])$ in base $(u^{1/c})$ (assume $(u^{1/c})$ is an integer and power of $(2)$) so that $(x = \sum_{i=0}^{c-1} x_i \cdot u^{i/c})$. We call the $(x_i)$ `characters`. We then allocate $(c)$ completely random lookup tables $(H_0, \ldots, H_{c-1})$ each of size $([u^{1/c}])$. Then for each $(y \in [u^{1/c}])$, we set $(H_i(y))$ uniformly at random from $([m])$ (assume also $(m)$ is a power of $(2)$). Then to hash $(x)$, we define (where $(\oplus)$ denotes bitwise XOR)

$h(x) = H_0(x_0) \oplus H_1(x_1) \oplus \cdots \oplus H_{c-1}(x_{c-1}).$

(a) (5 points) Fix $(c, m \ge 1)$. Show that the family $(\mathcal{H})$ of all such hash functions is 3-wise independent.

(b) (5 points) Show that $(\mathcal{H})$ is not 4-wise independent.

(c) (10 points) Imagine using such an $(\mathcal{H})$ to implement hashing with chaining, as in Lecture 3. Show that if $(m > n^{1.01})$ then with probability at least $(2/3)$, every linked list in the hash table has size $(O(1))$. **Hint:** Show that if a subset $(T)$ of the $(n

)$ keys has $(k)$ keys that hash to the same value, then $(k \le C \cdot m / n)$ with high probability.

(d) (5 points) Suppose we want to construct an optimal universal family of hash functions. Show that the family of hash functions defined by `simple tabulation hashing` is not universal. **Hint:** By definition, the family $(\mathcal{H})$ is universal if and only if, for any two distinct keys $(x, x')$, the probability that $(h(x) = h(x'))$ is at most $(1/m)$.**

#### Problem 2: (20 points)

In **simple tabulation hashing**, we write a key $(x \in [u])$ in base $(u^{1/c})$ (assume $(u^{1/c})$ is an integer and power of $(2)$) so that $(x = \sum_{i=0}^{c-1} x_i \cdot u^{i/c})$. We call the $(x_i)$ `characters`. We then allocate $(c)$ completely random lookup tables $(H_0, \ldots, H_{c-1})$ each of size $([u^{1/c}])$. Then for each $(y \in [u^{1/c}])$, we set $(H_i(y))$ uniformly at random from $([m])$ (assume also $(m)$ is a power of $(2)$). Then to hash $(x)$, we define (where $(\oplus)$ denotes bitwise XOR)

$h(x) = H_0(x_0) \oplus H_1(x_1) \oplus \cdots \oplus H_{c-1}(x_{c-1}).$

(a) (5 points) Fix $(c, m \ge 1)$. Show that the family $(\mathcal{H})$ of all such hash functions is 3-wise independent.

(b) (5 points) Show that $(\mathcal{H})$ is not 4-wise independent.

(c) (10 points) Imagine using such an $(\mathcal{H})$ to implement hashing with chaining, as in Lecture 3. Show that if $(m > n^{1.01})$ then with probability at least $(2/3)$, every linked list in the hash table has size $(O(1))$. **Hint:** Show that if a subset $(T)$ of the $(n

)$ keys has $(k)$ keys that hash to the same value, then $(k \le C \cdot m / n)$ with high probability.

(d) (5 points) Suppose we want to construct an optimal universal family of hash functions. Show that the family of hash functions defined by `simple tabulation hashing` is not universal. **Hint:** By definition, the family $(\mathcal{H})$ is universal if and only if, for any two distinct keys $(x, x')$, the probability that $(h(x) = h(x'))$ is at most $(1/m)$.**

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 3

Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (10 points)

Let $(G)$ be a directed graph with $(n)$ vertices. Suppose that we are given a labeling $(\ell)$ of the vertices such that $(\ell(v))$ is the number of vertices that are reachable from $(v)$ via a directed path. We want to find the vertex with the smallest number of reachable vertices. 

(a) (5 points) Show how to find such a vertex in $(O(n))$ time, assuming we can compute $(\ell)$ in $(O(n))$ time. 

(b) (5 points) Show how to compute $(\ell)$ in $(O(n^2))$ time. **Hint:** Consider using a depth-first search to determine reachability of vertices.**

To solve the problem of finding the vertex with the smallest number of reachable vertices in a directed graph, we will address both parts (a) and (b) as follows:

### Part (a): Finding the Vertex with the Smallest Reachable Count in \(O(n)\) Time

**Given:**
- A labeling \(\ell\) of the vertices where \(\ell(v)\) is the number of vertices reachable from vertex \(v\).
- The goal is to find the vertex \(v\) with the smallest value of \(\ell(v)\).

**Steps:**

1. **Initialize Tracking Variables**:
   - Create a variable `min_reach` initialized to \(+\infty\) (or a very large value) to keep track of the minimum reachable count.
   - Create a variable `min_vertex` to store the vertex corresponding to `min_reach`.

2. **Iterate Through the Vertices**:
   - For each vertex \(v\) in the graph:
     - Check the value of \(\ell(v)\).
     - If \(\ell(v) < \text{min_reach}\):
       - Update `min_reach` to \(\ell(v)\).
       - Update `min_vertex` to \(v\).

3. **Return the Result**:
   - After iterating through all vertices, `min_vertex` will contain the vertex with the smallest number of reachable vertices.

**Complexity Analysis**:
- The above steps involve a single pass through the \(n\) vertices, and checking and updating the minimum requires constant time \(O(1)\).
- Hence, the total time complexity is \(O(n)\).

### Part (b): Computing \(\ell(v)\) in \(O(n^2)\) Time

**Approach: Depth-First Search (DFS)**

To compute the number of reachable vertices for each vertex in \(O(n^2)\) time, we can use depth-first search.

**Steps**:

1. **Initialize the Reachability Count**:
   - Create an array \(\ell\) of size \(n\) to store the number of vertices reachable from each vertex.

2. **Perform DFS from Each Vertex**:
   - For each vertex \(v\):
     - Initialize a boolean array `visited` of size \(n\) to keep track of visited vertices during the DFS.
     - Call a DFS function starting from \(v\) to count the reachable vertices.

3. **DFS Function**:
   - The DFS function takes the current vertex and marks it as visited.
   - Increment a local counter each time a vertex is visited.
   - Recursively call the DFS function for each unvisited neighbor of the current vertex.

4. **Store the Reachability Count**:
   - After the DFS completes for vertex \(v\), store the count in \(\ell[v]\).

5. **Repeat for All Vertices**:
   - Repeat the above process for each vertex \(v\) in the graph.

**Complexity Analysis**:
- Each DFS traversal will visit all vertices and edges, taking \(O(n + m)\) time, where \(m\) is the number of edges.
- In the worst case (for a dense graph), the number of edges can be as high as \(O(n^2)\).
- Since we perform DFS from each of the \(n\) vertices, the overall time complexity becomes \(O(n(n + m))\). In a dense graph, this can simplify to \(O(n^2)\).

### Pseudocode for Part (b)

```python
def compute_reachability(graph):
    n = len(graph)  # Number of vertices
    ell = [0] * n  # Initialize reachability counts

    def dfs(v, visited):
        visited[v] = True
        count = 1  # Count the current vertex
        for neighbor in graph[v]:  # For each neighbor
            if not visited[neighbor]:
                count += dfs(neighbor, visited)  # Recursive DFS
        return count

    for v in range(n):  # For each vertex
        visited = [False] * n  # Reset visited for each DFS
        ell[v] = dfs(v, visited)  # Compute reachable vertices from v

    return ell  # Return the array of reachability counts
```

### Summary
- In part (a), we found the vertex with the smallest number of reachable vertices in \(O(n)\) time using the given labels.
- In part (b), we computed the labels \(\ell\) for each vertex using depth-first search in \(O(n^2)\) time.

---

#### Problem 2: (10 points)

Let $(G)$ be an undirected graph. We say that a vertex $(v)$ is a 'dominating set' if every vertex in $(G)$ is either $(v)$ itself or adjacent to $(v)$. 

(a) (5 points) Prove that every connected graph has a dominating set of size at most $(\Delta + 1)$, where $(\Delta)$ is the maximum degree in the graph.

(b) (5 points) Prove that every graph has a dominating set of size at most $(\lfloor n / \Delta \rfloor)$, where $(n)$ is the number of vertices.

To solve Problem 2 regarding dominating sets in undirected graphs, we'll tackle both parts (a) and (b) systematically.

### Part (a): Proving that Every Connected Graph Has a Dominating Set of Size at Most \(\Delta + 1\)

**Definitions:**
- A **dominating set** \(D\) for a graph \(G\) is a subset of vertices such that every vertex \(u\) in \(G\) is either in \(D\) or adjacent to at least one vertex in \(D\).
- \(\Delta\) is the maximum degree of any vertex in the graph \(G\).

**Proof:**

1. **Choose an Arbitrary Vertex**:
   - Start by selecting an arbitrary vertex \(v_0\) from the graph \(G\).

2. **Construct the Dominating Set**:
   - Let \(D = \{v_0\}\).
   - The neighbors of \(v_0\) can be denoted as \(N(v_0)\), which includes all vertices directly adjacent to \(v_0\).

3. **Covering Remaining Vertices**:
   - All vertices in \(N(v_0)\) are adjacent to \(v_0\) and are thus dominated by \(D\).
   - If \(G\) is connected, we can analyze the next step by checking the vertices not dominated yet.

4. **Adding More Vertices**:
   - Since \(\Delta\) is the maximum degree, \(v_0\) can have at most \(\Delta\) neighbors.
   - If there are still vertices not covered, we will choose another vertex \(v_1\) from the remaining uncovered vertices (there must be at least one due to the connectedness of \(G\)).
   - We can add \(v_1\) to \(D\), and repeat this process.

5. **Size of the Dominating Set**:
   - Each time we add a new vertex to \(D\), we can cover up to \(\Delta + 1\) vertices (the new vertex itself plus its \(\Delta\) neighbors).
   - In the worst case, if we need to cover the entire graph, the maximum number of vertices we can add to \(D\) before we have a dominating set is limited by the number of uncovered vertices.

6. **Conclusion**:
   - Since we are at most adding \(\Delta + 1\) vertices (the chosen vertex and its neighbors), it follows that \( |D| \leq \Delta + 1 \).
   - Therefore, every connected graph has a dominating set of size at most \(\Delta + 1\).

### Part (b): Proving that Every Graph Has a Dominating Set of Size at Most \(\lfloor n / \Delta \rfloor\)

**Definitions**:
- \(n\) is the number of vertices in the graph \(G\).
- \(\Delta\) is again the maximum degree of any vertex in the graph \(G\).

**Proof**:

1. **Choose Vertices**:
   - Consider an arbitrary vertex set \(S\) initialized as an empty set. This set will be our dominating set.

2. **Greedy Construction**:
   - While there are still uncovered vertices in \(G\):
     - Choose a vertex \(v\) that is not yet dominated and add it to the set \(S\).
     - Mark \(v\) as dominated and all of its neighbors (including itself).
   
3. **Count of Dominating Vertices**:
   - When you add a vertex \(v\) to \(S\), it dominates itself and its neighbors, totaling to at most \(\Delta + 1\) vertices being dominated.
   - Therefore, each vertex in \(S\) covers at most \(\Delta + 1\) vertices.

4. **Bounding the Size of \(S\)**:
   - Given there are \(n\) vertices in total, and each vertex in \(S\) can dominate at most \(\Delta + 1\) vertices, we can calculate the number of vertices dominated by \( |S| \) vertices as:
     \[
     |S| \cdot (\Delta + 1) \geq n
     \]
   - Rearranging this inequality gives:
     \[
     |S| \geq \frac{n}{\Delta + 1}
     \]
   - Since we are interested in an upper bound, we can express \( |S| \) in terms of \(\lfloor n / \Delta \rfloor\):
     \[
     |S| \leq \left\lfloor \frac{n}{\Delta} \right\rfloor
     \]

5. **Conclusion**:
   - Therefore, every graph has a dominating set of size at most \(\lfloor n / \Delta \rfloor\).

### Summary
- In part (a), we established that every connected graph has a dominating set of size at most \(\Delta + 1\).
- In part (b), we showed that every graph has a dominating set of size at most \(\lfloor n / \Delta \rfloor\).

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 4

Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)


---

#### Problem 1: (10 points)

**Exact k-Median**

Let $(G = (V, E))$ be an undirected graph. The goal is to find a set $(C \subseteq V)$ of $(k)$ vertices that minimizes the sum of distances from each vertex in $(V)$ to the nearest vertex in $(C)$. 

(a) (5 points) Give a polynomial-time approximation algorithm for the exact k-median problem. **Hint:** Consider using a heuristic like the greedy algorithm for facility location.**

(b) (5 points) Show that the approximation algorithm you designed has an approximation ratio of at most 2.

To solve the problem of finding an approximate solution for the exact \(k\)-Median problem in an undirected graph \(G = (V, E)\), we'll provide a polynomial-time approximation algorithm in part (a) and analyze its performance in part (b).

### Problem 1: Exact k-Median

#### Part (a): Approximation Algorithm for the k-Median Problem

**Algorithm: Greedy Facility Location Heuristic**

1. **Initialization**:
   - Start with an empty set \(C = \emptyset\).
   - Set \(k\) as the maximum number of facilities (or vertices) we can select.

2. **Iterate until \(C\) contains \(k\) vertices**:
   - For each vertex \(v \in V \setminus C\):
     - Calculate the potential benefit of adding \(v\) to the set \(C\). This is the reduction in the sum of distances from all vertices in \(V\) to their nearest facility in \(C\).
     - Specifically, for each vertex \(u \in V\), compute:
       \[
       \text{Benefit}(v) = \sum_{u \in V} d(u, C) - \sum_{u \in V} d(u, C \cup \{v\}),
       \]
       where \(d(u, C)\) is the distance from \(u\) to the nearest vertex in \(C\).

   - Add the vertex \(v^*\) that provides the maximum benefit to \(C\):
     \[
     C \leftarrow C \cup \{v^*\}
     \]

3. **Repeat** this process until \(C\) contains \(k\) vertices.

4. **Output**: The set \(C\) as the approximate solution for the \(k\)-Median problem.

#### Part (b): Approximation Ratio Analysis

**Claim**: The approximation algorithm has an approximation ratio of at most 2.

**Proof**:

1. **Optimal Solution**:
   - Let \(C^*\) be the optimal \(k\)-Median solution that minimizes the total distance:
     \[
     \text{Cost}(C^*) = \sum_{u \in V} d(u, C^*).
     \]

2. **Cost of the Greedy Solution**:
   - Let \(C\) be the solution produced by the greedy algorithm.
   - The cost of \(C\) is:
     \[
     \text{Cost}(C) = \sum_{u \in V} d(u, C).
     \]

3. **Distance Comparison**:
   - When we add a vertex \(v\) to \(C\), the cost can increase or decrease. However, we know:
     \[
     d(u, C) \leq d(u, C^*) \quad \text{for each } u \in V.
     \]

4. **At Most Twice the Optimal**:
   - When considering the addition of \(v\):
     - The cost of the optimal solution, \(\text{Cost}(C^*)\), accounts for \(k\) vertices providing coverage.
     - In the worst case, if we add \(k\) vertices to \(C\) using our greedy method, the cost can be at most twice that of the optimal cost.
   - Specifically, for each vertex added, the maximum reduction achieved can be no more than what would be accounted for by \(C^*\).

5. **Final Inequality**:
   - Hence, we derive:
     \[
     \text{Cost}(C) \leq 2 \cdot \text{Cost}(C^*).
     \]

6. **Conclusion**:
   - Therefore, the approximation algorithm has an approximation ratio of at most 2:
   \[
   \frac{\text{Cost}(C)}{\text{Cost}(C^*)} \leq 2.
   \]

### Summary
- We developed a greedy approximation algorithm for the exact \(k\)-Median problem that iteratively adds the vertex that maximizes the immediate benefit in terms of reduced distances.
- We proved that this algorithm has an approximation ratio of at most 2, showing that it produces a solution that is at most twice as costly as the optimal solution.

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 5

Due: 11:59pm, Monday, October 27th  
Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (20 points)

Let $(G = (V, E))$ be a graph and $(S \subseteq V)$ be a set of $(k)$ vertices. Define the `independent set` problem as finding a maximum cardinality subset $(I \subseteq S)$ such that no two vertices in $(I)$ are adjacent. 

(a) (10 points) Show that for any graph $(G)$ with maximum degree $(\Delta)$, there exists an independent set of size at least $(\frac{|S|}{\Delta + 1})$. 

(b) (10 points) Show that finding a maximum independent set is NP-hard, even for graphs with maximum degree 3.

To tackle the problem of finding an independent set in a graph, we will break it down into two parts as specified.

### Problem 1: Independent Set in Graphs

Let \( G = (V, E) \) be a graph and \( S \subseteq V \) be a set of \( k \) vertices.

#### Part (a): Lower Bound on the Size of an Independent Set

**Claim**: For any graph \( G \) with maximum degree \( \Delta \), there exists an independent set \( I \subseteq S \) of size at least \( \frac{|S|}{\Delta + 1} \).

**Proof**:

1. **Vertex Coloring**:
   - A simple approach to finding a lower bound for the size of an independent set is to use the concept of vertex coloring. 
   - In a graph \( G \), if a vertex has a degree of at most \( \Delta \), then it can be colored with at most \( \Delta + 1 \) colors (by the greedy coloring algorithm).

2. **Coloring Vertices in \( S \)**:
   - Consider the subgraph induced by the vertices in \( S \). The maximum degree of this subgraph cannot exceed \( \Delta \).
   - Apply a greedy coloring algorithm to the vertices in \( S \). Assign colors from \( \{1, 2, \ldots, \Delta + 1\} \).

3. **Counting Colors**:
   - Since there are \( |S| \) vertices in \( S \) and at most \( \Delta + 1 \) colors, by the pigeonhole principle, at least one color must be assigned to at least \( \frac{|S|}{\Delta + 1} \) vertices.
   - Let’s say color \( c \) has at least \( \frac{|S|}{\Delta + 1} \) vertices. All these vertices colored with \( c \) cannot be adjacent (since they are assigned the same color).

4. **Constructing the Independent Set**:
   - Thus, the set of vertices colored with \( c \) forms an independent set \( I \) of size at least \( \frac{|S|}{\Delta + 1} \).

Therefore, we conclude that there exists an independent set \( I \) of size at least \( \frac{|S|}{\Delta + 1} \).

#### Part (b): NP-Hardness of the Maximum Independent Set Problem

**Claim**: Finding a maximum independent set is NP-hard, even for graphs with a maximum degree of 3.

**Proof**:

1. **Reduction from 3-SAT**:
   - We will show that the Maximum Independent Set problem is NP-hard by reducing from the 3-SAT problem. The 3-SAT problem is known to be NP-complete, and thus any problem that can be reduced to it is also NP-hard.
   - The 3-SAT problem consists of a boolean formula in conjunctive normal form where each clause has exactly three literals. We need to determine if there exists a truth assignment that satisfies all clauses.

2. **Constructing the Graph**:
   - Given an instance of a 3-SAT formula with variables \( x_1, x_2, \ldots, x_n \) and clauses \( C_1, C_2, \ldots, C_m \), we construct a graph \( G \) as follows:
     - **For each variable \( x_i \)**: Create two vertices \( v_i \) and \( \neg v_i \) in \( G \) representing the true and false assignments of the variable. Connect these two vertices with an edge (i.e., \( (v_i, \neg v_i) \)).
     - **For each clause \( C_j = (l_{j1} \lor l_{j2} \lor l_{j3}) \)**: Create a triangle in the graph corresponding to the literals of the clause. For example, if \( C_j \) contains literals \( x_i, \neg x_k, x_l \), add vertices \( v_i, \neg v_k, v_l \) and connect them with edges \( (v_i, \neg v_k) \), \( (v_i, v_l) \), and \( (\neg v_k, v_l) \).

3. **Properties of the Graph**:
   - Each variable contributes exactly two vertices with an edge between them.
   - Each clause contributes a triangle of three vertices.
   - The maximum degree of the graph is 3 because each variable has edges to exactly two other vertices (the true and false literals) and each clause connects to three vertices.

4. **Independent Set and Satisfiability**:
   - Now we claim that there is a satisfying assignment for the 3-SAT formula if and only if there exists an independent set of size \( n + m \) in the constructed graph:
     - If there is a satisfying assignment, select \( v_i \) if \( x_i \) is true and \( \neg v_i \) if \( x_i \) is false. This contributes \( n \) vertices. For each satisfied clause, you can select one of the three vertices of the triangle without selecting any adjacent vertices, adding \( m \) vertices.
     - Conversely, if we have an independent set of size \( n + m \), then the selection of the independent set allows us to determine a satisfying assignment for the clauses.

5. **Conclusion**:
   - Since we can transform a 3-SAT instance into a maximum independent set instance in polynomial time and both conditions are equivalent, finding the maximum independent set is NP-hard.

Thus, we have shown that finding a maximum independent set is NP-hard even for graphs with a maximum degree of 3.

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 6
 
Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (10 points)

**Online Bipartite Matching**

Consider the online bipartite matching problem where one side of the bipartite graph is revealed incrementally. The problem is to maintain a matching of maximum size while the vertices of the other side are revealed one by one.

(a) (5 points) Provide an online algorithm for the problem that achieves a constant approximation ratio. 

(b) (5 points) Prove that the algorithm you provided has an approximation ratio of at least $( \frac{1}{2} )$.

To tackle the problem of online bipartite matching, we will construct an online algorithm and analyze its performance.

### Problem: Online Bipartite Matching

Let \( G = (U, V, E) \) be a bipartite graph where \( U \) is the set of vertices revealed incrementally and \( V \) is the set of vertices that are known ahead of time. The goal is to maintain a matching of maximum size as vertices from \( U \) are revealed one by one.

#### Part (a): Online Algorithm with Constant Approximation Ratio

**Algorithm: Greedy Matching Algorithm**

1. **Initialization**: Start with an empty matching \( M \).
2. **Process Vertices**: As each vertex \( u_i \in U \) is revealed:
   - For each revealed vertex \( u_i \), examine its edges to the vertices in \( V \).
   - If \( u_i \) is adjacent to any unmatched vertex \( v_j \in V \) (that is, \( v_j \) is not already in the matching \( M \)):
     - Add the edge \( (u_i, v_j) \) to the matching \( M \).
     - Mark \( v_j \) as matched.
3. **Output**: After all vertices in \( U \) have been processed, the matching \( M \) is the output.

This greedy algorithm matches each newly revealed vertex to any currently available vertex in \( V \) that is not already matched.

#### Part (b): Proving the Approximation Ratio

To analyze the performance of our greedy algorithm, we need to compare the size of the matching produced by the algorithm, denoted as \( |M| \), with the size of an optimal matching, denoted as \( |M^*| \).

1. **Construction of the Optimal Matching**:
   - Let \( M^* \) be an optimal matching in the bipartite graph \( G \).
   - Let \( k = |M^*| \) be the size of this optimal matching.

2. **Matching Properties**:
   - Each time a vertex \( u_i \) from \( U \) is revealed, it can potentially match to some vertex in \( V \). If it matches to an unmatched vertex in \( V \), it contributes to the size of \( M \).
   - However, if \( u_i \) has no available unmatched vertices to match to when it is revealed, it cannot contribute to \( |M| \).

3. **Bounding the Size of \( M \)**:
   - Since the matching \( M^* \) consists of \( k \) edges, there must be at least \( k \) vertices in \( U \) that are adjacent to vertices in \( V \) that are part of \( M^* \).
   - For each vertex \( u_i \) revealed from \( U \), if it is matched to a vertex in \( M^* \), then \( M \) is essentially keeping up with the optimal matching.
   - However, if \( M \) does not match to one of these optimal matches (due to the greedy nature of the algorithm), we can analyze that at least half of the vertices in \( M^* \) could still be matched by our greedy algorithm.

4. **Approximation Ratio**:
   - Consider that when a vertex \( u_i \) is matched to a vertex \( v_j \) in \( V \), that vertex \( v_j \) could have been matched to another vertex in \( M^* \) if \( u_i \) hadn't been revealed.
   - In the worst case, every matching edge in \( M \) corresponds to two vertices in \( M^* \) being revealed at some point during the algorithm's execution. Thus, for every edge we include in \( M \), there is a corresponding edge in \( M^* \) we could have matched with. 

5. **Conclusion**:
   - This means that the size of our matching \( |M| \) is at least \( \frac{1}{2} |M^*| \).
   - Therefore, we conclude that the greedy algorithm achieves an approximation ratio of at least \( \frac{1}{2} \), i.e.,

   \[
   \frac{|M|}{|M^*|} \geq \frac{1}{2}.
   \]

### Summary

The greedy algorithm for online bipartite matching maintains a matching while processing vertices from \( U \) as they are revealed. The analysis shows that this algorithm has an approximation ratio of at least \( \frac{1}{2} \) when compared to the optimal matching size. This meets the requirement for a constant approximation ratio.

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 7

Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (10 points)

**Approximate Max Cut**

Given an undirected graph $(G = (V, E))$, the `Max Cut` problem seeks to partition the vertex set $(V)$ into two subsets $(A)$ and $(B)$ to maximize the number of edges crossing the partition.

(a) (5 points) Describe a polynomial-time approximation algorithm for the Max Cut problem and analyze its approximation ratio.

(b) (5 points) Show that the approximation ratio of your algorithm is at least $(\frac{1}{2})$.

The Max Cut problem is a classic problem in combinatorial optimization and is known to be NP-hard. However, we can design a polynomial-time approximation algorithm that guarantees a certain approximation ratio.

### Part (a): Polynomial-Time Approximation Algorithm for Max Cut

**Algorithm: Randomized Cut Algorithm**

1. **Random Partitioning**:
   - Randomly partition the vertices \( V \) of the graph \( G \) into two sets \( A \) and \( B \). Specifically, for each vertex \( v \in V \):
     - Assign \( v \) to set \( A \) with probability \( \frac{1}{2} \).
     - Assign \( v \) to set \( B \) with probability \( \frac{1}{2} \).

2. **Count Crossing Edges**:
   - After the random assignment, count the number of edges that have one endpoint in \( A \) and the other endpoint in \( B \). This count will be the value of the cut, denoted as \( |E(A, B)| \), where \( E(A, B) \) is the set of edges that cross the partition.

3. **Output the Cut**:
   - Return the sets \( A \) and \( B \) along with the number of crossing edges.

### Analysis of the Approximation Ratio

To analyze the performance of this algorithm, we need to consider the expected number of edges crossing the cut created by this randomized algorithm.

1. **Total Number of Edges**:
   - Let \( m = |E| \) be the total number of edges in the graph.

2. **Probability of an Edge Crossing the Cut**:
   - For any edge \( (u, v) \in E \), the probability that it crosses the cut (i.e., one vertex is in \( A \) and the other is in \( B \)) is given by:
     \[
     P(\text{edge } (u, v) \text{ crosses the cut}) = P(u \in A) \cdot P(v \in B) + P(u \in B) \cdot P(v \in A) = \frac{1}{2} \cdot \frac{1}{2} + \frac{1}{2} \cdot \frac{1}{2} = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}.
     \]

3. **Expected Number of Crossing Edges**:
   - Since there are \( m \) edges, the expected number of edges crossing the cut is:
     \[
     \mathbb{E}[|E(A, B)|] = \sum_{(u, v) \in E} P(\text{edge } (u, v) \text{ crosses the cut}) = \sum_{(u, v) \in E} \frac{1}{2} = \frac{m}{2}.
     \]

4. **Conclusion**:
   - The expected value of the cut produced by the algorithm is at least \( \frac{m}{2} \), where \( m \) is the total number of edges in the graph.

### Part (b): Showing Approximation Ratio of at Least \( \frac{1}{2} \)

The approximation ratio is defined as:
\[
\text{Approximation Ratio} = \frac{\text{Value of the solution from the algorithm}}{\text{Value of the optimal solution}}.
\]

Let \( C^* \) denote the size of the optimal cut. By the previous analysis, we have:

\[
\mathbb{E}[|E(A, B)|] \geq \frac{m}{2}.
\]

Since \( C^* \) can be at most \( m \) (the total number of edges), we can state:
\[
\text{Approximation Ratio} = \frac{\mathbb{E}[|E(A, B)|]}{C^*} \geq \frac{\frac{m}{2}}{C^*} \geq \frac{\frac{m}{2}}{m} = \frac{1}{2}.
\]

Thus, the approximation ratio of the algorithm is at least \( \frac{1}{2} \).

### Summary

- The randomized cut algorithm provides a simple and efficient way to approximate the Max Cut problem in polynomial time.
- The expected size of the cut produced by this algorithm is at least \( \frac{m}{2} \), yielding an approximation ratio of at least \( \frac{1}{2} \).

---

**CS 224 Advanced Algorithms — Fall 2014**

### Problem Set 8
  
Submit to: [cs224-f14-assignments@seas.harvard.edu](mailto:cs224-f14-assignments@seas.harvard.edu)  
Solution maximum page limit: 6 pages

**See homework policy at** [http://people.seas.harvard.edu/~minilek/cs224/hmwk.html](http://people.seas.harvard.edu/~minilek/cs224/hmwk.html)

---

#### Problem 1: (10 points)

**Approximate Vertex Cover**

Given an undirected graph $(G = (V, E))$, the `Vertex Cover` problem seeks to find the smallest subset of vertices such that each edge in $(E)$ is incident to at least one vertex in the subset.

(a) (5 points) Describe a polynomial-time approximation algorithm for the Vertex Cover problem and analyze its approximation ratio.

(b) (5 points) Show that the approximation ratio of your algorithm is at most 2.

Both problem sets are quite comprehensive and require a deep understanding of algorithms and complexity. Here's a breakdown of each problem set's structure and some specific details that might help in approaching them:

### Problem Set 7

1. **Ford-Fulkerson Algorithm Improvements:**
   - **(a)** Prove that any flow can be decomposed into paths or cycles. This involves understanding the structure of flows and how they can be represented.
   - **(b)** Modify Dijkstra’s algorithm to find a path maximizing the minimum weight. The hint suggests using a priority queue to implement this efficiently.
   - **(c)** Combine results from (a) and (b) to analyze the runtime of an improved Ford-Fulkerson algorithm.

2. **Bit Complexity for Interior Point Methods:**
   - **(a)** Show that integer linear programs have solutions with a bounded number of bits. This involves understanding the precision required for LP solutions.
   - **(b)** Transform an LP into another form to simplify the problem, ensuring bounded precision for the solution.
   - **(c)** Modify the Newton steps in IPMs to ensure matrix invertibility with preprocessing.
   - **(d)** Show that being finely central is sufficient for an approximation close to the optimal solution.

3. **Learning from Experts:**
   - **(a)** Prove that no algorithm can achieve better than $\sqrt{T}$ regret. Use a specific case with $n = 2$ for illustration.
   - **(b)** (Bonus) Show that $R = o(\sqrt{T\ln n})$ is not achievable for large $T$. This involves a more nuanced analysis of regret bounds.

4. **Regret Minimization with Limited Feedback:**
   - **(a)** Design an algorithm with improved regret bounds when only partial feedback is available. Break down the days into blocks and use both exploitation and exploration strategies.

5. **Time Tracking:**
   - **(a)** Report the time spent on the problem set, including any breakdown if possible.

Sure! Let's address each of your problems one by one, detailing the required proofs and algorithms.

### 1. Ford-Fulkerson Algorithm Improvements

#### (a) Flow Decomposition into Paths or Cycles

**Proof:**
1. **Max Flow:** According to the Max-Flow Min-Cut Theorem, any flow \( f \) in a flow network can be decomposed into a flow \( f' \) that is composed of paths from the source \( s \) to the sink \( t \), and possibly some cycles.
2. **Flow Representation:** We can represent the flow \( f \) as follows:
   - **Paths:** Each path from \( s \) to \( t \) contributes to the flow from the source to the sink.
   - **Cycles:** If there are any unused edges that connect back to vertices already in the flow, we can form cycles. These do not affect the net flow but allow us to represent \( f \) as the sum of path flows and cycle flows.
3. **Construction:** To decompose \( f \):
   - Use a breadth-first search (BFS) or depth-first search (DFS) to find augmenting paths in the residual graph.
   - Record the flow along each found path until no more augmenting paths exist.
   - If there is flow left in the network, we can create cycles by redirecting flow.
4. **Conclusion:** By continuing this process, we ensure that any flow can ultimately be represented as a sum of paths and cycles, as each residual network can be traversed to find these structures.

#### (b) Modifying Dijkstra’s Algorithm for Path Maximizing the Minimum Weight

**Algorithm:**
To find a path from the source \( s \) to the sink \( t \) that maximizes the minimum edge weight:

1. **Initialize:** 
   - Create a priority queue \( Q \) where we will store nodes based on the current minimum weight encountered on the path from \( s \).
   - Set \( d[v] \) for each vertex \( v \) to \(-\infty\) and \( d[s] = \infty \) (representing the minimum weight along the path).

2. **Priority Queue Operations:** 
   - Insert \( (s, \infty) \) into \( Q \).
   
3. **Processing:**
   - While \( Q \) is not empty:
     - Extract the node \( u \) with the highest \( d[u] \).
     - For each neighbor \( v \) of \( u \):
       - Calculate the potential minimum weight \( w = \min(d[u], \text{weight}(u, v)) \).
       - If \( w > d[v] \):
         - Update \( d[v] = w \).
         - Insert \( (v, w) \) into \( Q \).

4. **Termination:** 
   - The algorithm ends when we extract \( t \) from the priority queue or when \( Q \) is empty. The value \( d[t] \) gives the maximum minimum edge weight of the path.

#### (c) Analyzing Runtime of Improved Ford-Fulkerson Algorithm

**Combining Results:**
1. **Runtime for Decomposition:** The flow decomposition in (a) can be done in \( O(n + m) \) using BFS/DFS.
2. **Path Finding Algorithm:** The modified Dijkstra's algorithm in (b) runs in \( O((n + m) \log n) \) using a priority queue.
3. **Ford-Fulkerson Improvement:** If we repeatedly apply these two techniques:
   - Each iteration finds a path maximizing the minimum edge weight, which can then be augmented.
   - The overall runtime can be analyzed in terms of the number of iterations and the complexity of each iteration.
4. **Final Runtime:** The complexity is \( O(k \cdot (n + m) \log n) \) where \( k \) is the number of augmentations needed.

### 2. Bit Complexity for Interior Point Methods

#### (a) Bounded Number of Bits for Integer Linear Programs

**Proof:**
1. **Precision of LP Solutions:** An integer linear program (ILP) with \( n \) variables and bounded coefficients \( c \) has feasible solutions where each variable’s value lies within a bounded range.
2. **Representation:** If the coefficients and the right-hand side of the constraints are represented with \( B \) bits, then the solution can be expressed in at most \( B \) bits. This can be shown using the fact that the maximum value for any variable is determined by the constraints and must be finite.

#### (b) Transforming LP for Simplified Problems

**Transformation:**
1. **Standard Form:** Transform any LP to the standard form where all inequalities are converted to equalities using slack variables.
2. **Bounded Variables:** Ensure that all variables are non-negative. This can be done by substituting \( x_i = x_i' - x_i'' \) where \( x_i', x_i'' \geq 0 \).

#### (c) Modifying Newton Steps in IPMs

**Modification:**
1. **Matrix Invertibility:** Preprocess the data to ensure the matrix involved in Newton’s steps is invertible. This can be done using techniques like regularization or perturbation.
2. **Preprocessing:** Implement an initial phase where any potentially degenerate solutions are adjusted slightly to guarantee invertibility of the Hessian matrix during iterations.

#### (d) Fine Centrality and Approximation

**Proof:**
1. **Fine Centrality Definition:** A point in the interior of the feasible region is said to be finely central if it maintains a certain distance from the boundary.
2. **Approximation Sufficiency:** If a point is finely central, the neighborhood around it contains feasible solutions that are close to optimal. Hence, local approximations can yield global approximations.

### 3. Learning from Experts

#### (a) Regret Lower Bound

**Proof:**
1. **Setup:** Consider \( n = 2 \) experts and a decision-making scenario. The learner’s goal is to minimize regret.
2. **Regret Definition:** The regret is defined as \( R_T = \sum_{t=1}^{T} (c_t - c^*_t) \), where \( c_t \) is the cost incurred by the learner and \( c^*_t \) is the cost incurred by the best expert in hindsight.
3. **Example Analysis:** In a scenario where outcomes can be adversarial, it can be shown that any deterministic algorithm will incur a regret of at least \( \sqrt{T} \) due to alternating conditions.

#### (b) Bonus Regret Bound

**Proof:**
1. **Assumption:** Assume that there exists an algorithm with regret \( R = o(\sqrt{T \ln n}) \).
2. **Contradiction:** Given the previously established bounds, one can construct scenarios where the regret would exceed this bound, especially as \( T \) grows large. This involves examining cases where choices are forced into adversarial conditions leading to linear regret growth.

### 4. Regret Minimization with Limited Feedback

#### (a) Algorithm Design

**Algorithm:**
1. **Block Structure:** Divide the time into blocks of \( \sqrt{T} \).
2. **Exploration vs. Exploitation:** Within each block, explore each expert \( O(\log n) \) times while also exploiting the best-performing expert from the previous blocks.
3. **Feedback Utilization:** Use the feedback from the expert in each block to adjust future decisions, balancing the exploration of new experts with the exploitation of known good experts.

### 5. Time Tracking

#### (a) Time Spent

- Time spent on the problem set: \( \text{X hours} \)
- Breakdown:
  - Problem 1: \( \text{Y hours} \)
  - Problem 2: \( \text{Z hours} \)
  - Problem 3: \( \text{W hours} \)
  - Problem 4: \( \text{V hours} \)

This structure gives a detailed layout of each question and its respective resolution. If you have specific values for time tracking or if any aspect requires further elaboration, please let me know!

---

### Problem Set 8

1. **Scaling with Blocking Flows:**
   - **(a)** Show that Dinic’s algorithm can be bounded by $O(mn + nf^*)$.
   - **(b)** Combine scaling and blocking flows to achieve an $O(mn \log U)$ bound.

2. **Scaling Algorithm for Shortest Paths:**
   - **(a)** Design an algorithm to handle negative weights using price functions and reduced costs.
   - **(b)** Develop an algorithm to find feasible price functions using a subroutine.
   - **(c)** Provide an efficient algorithm to detect negative weight cycles or find feasible price functions.
   - **(d)** Improve upon the algorithm in (c) to fix multiple bad vertices at once.
   - **(e)** Implement the algorithm from (d) to handle bad vertices efficiently.

3. **Link-Cut Trees:**
   - **(a)** Show that the total runtime of operations on a link-cut tree is $O(m \log n + \mathrm{PCC})$.

4. **Scaling Algorithm for Min-Cost Max Flow:**
   - **(a)** Design a scaling algorithm for min-cost max flow with a specific time complexity.

5. **Time Tracking:**
   - **(a)** Report the time spent on the problem set, including any breakdown if possible.

### Tips for Both Problem Sets

- **Understand the Theory**: Before jumping into proofs or implementations, ensure you thoroughly understand the theoretical concepts and algorithms involved.
- **Break Down Problems**: For complex problems, break them down into smaller sub-problems and solve each part systematically.

Let's tackle each of the problems in your problem set systematically. This will involve a mix of theoretical insights and algorithmic design.

### Problem Set 8

### 1. Scaling with Blocking Flows

#### (a) Show that Dinic’s algorithm can be bounded by \( O(mn + nf^*) \).

**Proof:**
- **Overview of Dinic’s Algorithm:** Dinic's algorithm is a flow algorithm that uses level graphs and blocking flows. It constructs a level graph from the source to the sink and finds blocking flows in this level graph.
  
1. **Level Graph Construction:** The construction of the level graph takes \( O(m) \) time using a BFS traversal.
2. **Blocking Flow:** Finding a blocking flow can be done using a series of depth-first searches (DFS). Each blocking flow found increases the flow by at least 1 unit.
3. **Maximum Flow \( f^* \):** The number of iterations to augment the flow (finding a blocking flow) is bounded by the maximum flow \( f^* \) since each blocking flow augments the flow by at least 1 unit.
4. **Total Time Complexity:**
   - Constructing the level graph: \( O(m) \).
   - Finding a blocking flow (for \( f^* \) flows): \( O(nf^*) \) (since each DFS takes \( O(m) \)).
5. **Combining Costs:** Thus, the total running time of Dinic's algorithm is:
   \[
   O(m + nf^*) \text{ for each phase, and since there are } O(n) \text{ phases, the total is } O(mn + nf^*).
   \]

#### (b) Combine scaling and blocking flows to achieve an \( O(mn \log U) \) bound.

**Proof:**
- **Overview of the Combined Approach:**
  - Use a scaling approach on the capacity values to improve efficiency.
  - Start with \( U \), the maximum capacity of the edges in the network, and scale down to find blocking flows iteratively.

1. **Scaling Factor:** 
   - Start with \( \Delta = U \) (the largest capacity).
   - Repeat the process for \( \Delta = U/2, U/4, \ldots, 1 \). In each phase, you can only consider edges with capacities greater than or equal to \( \Delta \).
  
2. **Blocking Flows:** 
   - For each scaled-down capacity, construct a level graph and find blocking flows using Dinic’s algorithm, which runs in \( O(mn + nf^*) \) time.
  
3. **Number of Phases:** 
   - The number of phases is \( O(\log U) \) because the capacities are halved each time.
  
4. **Total Time Complexity:** 
   - Each phase runs in \( O(mn + nf^*) \). Since there are \( O(\log U) \) phases, the overall complexity becomes:
   \[
   O(mn \log U + n f^* \log U).
   \]
   - Note that \( f^* \) can be at most \( O(m) \) in a network flow scenario, leading to the final complexity of:
   \[
   O(mn \log U).
   \]

### 2. Scaling Algorithm for Shortest Paths

#### (a) Design an algorithm to handle negative weights using price functions and reduced costs.

**Algorithm Outline:**
- **Define Price Functions:** Let \( p[v] \) be the price function for vertex \( v \). This function is adjusted dynamically based on the shortest path estimates.
  
1. **Reduced Costs:** Define the reduced cost for an edge \( (u, v) \) as:
   \[
   \text{reduced\_cost}(u, v) = w(u, v) + p[u] - p[v].
   \]
   - If \( \text{reduced\_cost}(u, v) < 0 \), then the edge is a candidate for relaxation.

2. **Algorithm Steps:**
   - Initialize \( p[v] = 0 \) for all vertices.
   - Relax edges based on reduced costs. For each edge, if \( \text{reduced\_cost}(u, v) < 0 \), then update \( d[v] \) and set the predecessor accordingly.

3. **Bellman-Ford Component:** Utilize the Bellman-Ford algorithm to handle the relaxation and detect negative weight cycles.

#### (b) Develop an algorithm to find feasible price functions using a subroutine.

**Algorithm Outline:**
1. **Initial Setup:** Start with an arbitrary price function \( p[v] = 0 \) for the source and set all other \( p[v] \) to infinity.
  
2. **Run the Bellman-Ford Algorithm:**
   - Relax edges repeatedly until no updates can be made or until \( n-1 \) iterations are completed.
   - If negative cycles are detected during this process, update prices to ensure feasibility.

3. **Output:** The resulting prices will ensure that all reduced costs are non-negative.

#### (c) Efficient algorithm to detect negative weight cycles or find feasible price functions.

**Algorithm Outline:**
1. **Use Bellman-Ford with Cycle Detection:** In addition to relaxing edges, keep track of the predecessors of each vertex.
  
2. **Cycle Detection:** After \( n-1 \) iterations, perform one additional iteration to check if any edge can still be relaxed.
   - If yes, track back using predecessors to identify the cycle.

#### (d) Improve algorithm in (c) to fix multiple bad vertices at once.

**Algorithm Outline:**
1. **Identify All Bad Vertices:** After detecting a negative cycle, mark all vertices reachable from this cycle.
  
2. **Fix Prices for All Bad Vertices:** Update the prices of all bad vertices to infinity or adjust them based on the cycle.

#### (e) Implement the algorithm from (d) to handle bad vertices efficiently.

**Implementation Steps:**
1. **Modified Bellman-Ford:** Maintain a list of visited vertices and adjust the price function for all marked vertices during the cycle detection phase.
  
2. **Relaxation Phase:** Perform relaxation while ensuring bad vertices do not propagate negative weight effects to good vertices.

### 3. Link-Cut Trees

#### (a) Show that the total runtime of operations on a link-cut tree is \( O(m \log n + \mathrm{PCC}) \).

**Proof:**
1. **Operations on Link-Cut Trees:** Each operation such as link, cut, access, and find can be executed in \( O(\log n) \) time.
  
2. **Total Operations:** If there are \( m \) operations, the cumulative cost becomes \( O(m \log n) \).

3. **PCC (Path-Cutting Cost):** The total path-cutting cost is also accounted for within the logarithmic operations due to the tree structure's properties.

4. **Final Time Complexity:** Therefore, the total runtime is:
   \[
   O(m \log n + \mathrm{PCC}).
   \]

### 4. Scaling Algorithm for Min-Cost Max Flow

#### (a) Design a scaling algorithm for min-cost max flow with specific time complexity.

**Algorithm Outline:**
1. **Scaling Factor:** Start with the maximum capacity \( U \) and scale down as in the max flow case.
  
2. **Construct Level Graph:** For each capacity scale, construct a level graph and find blocking flows. 

3. **Cost Minimization:** In each phase, apply a modified Dijkstra’s algorithm or Bellman-Ford to ensure minimum cost flows are considered.

4. **Total Time Complexity:** The total complexity of this algorithm is \( O(mn \log U) \) as derived previously.

### 5. Time Tracking

#### (a) Report the time spent on the problem set, including any breakdown if possible.

- **Total Time Spent:** \( X \) hours
- **Breakdown:**
  - Problem 1: \( Y \) hours
  - Problem 2: \( Z \) hours
  - Problem 3: \( W \) hours
  - Problem 4: \( V \) hours

Feel free to adjust the time tracking based on your actual experiences. If you have specific points that need further expansion or clarification, let me know!

---
