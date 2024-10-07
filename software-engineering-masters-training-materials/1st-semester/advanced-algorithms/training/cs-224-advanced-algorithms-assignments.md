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

---

#### Problem 2: (5 points)

Let $(w)$ be a perfect square. Show that there exist positive integers $(m)$ and $(t)$, $(m < 2^w)$ and $(0 \le t \le w)$, such that for all $(x \in \{0,1\}^{\sqrt{w}})$ we have that

$\left(\left(\left(\sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i \cdot \sqrt{w} - 1}\right) \times m\right) \gg t\right) \mathrel{\&} (2^{\sqrt{w}} - 1) = \sum_{i=1}^{\sqrt{w}} x_i \cdot 2^{i-1}$

That is, we can pick $(m)$ and $(t)$ so that, if we form a bitvector of length $(w)$ which has the $(\sqrt{w})$ bits of $(x)$ evenly spread out with a $(\sqrt{w})$-spacing of zeroes in between bits, then multiplying by $(m)$ and bitshifting right by $(t)$ followed by masking perfectly compresses the bits of $(x)$ into the rightmost $(\sqrt{w})$ bits of a machine word. This provides the proof of a lemma we needed for $(O(1))$ time most significant set bit in Lecture 2.

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

---

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

---

#### Problem 2: (10 points)

Let $(G)$ be an undirected graph. We say that a vertex $(v)$ is a 'dominating set' if every vertex in $(G)$ is either $(v)$ itself or adjacent to $(v)$. 

(a) (5 points) Prove that every connected graph has a dominating set of size at most $(\Delta + 1)$, where $(\Delta)$ is the maximum degree in the graph.

(b) (5 points) Prove that every graph has a dominating set of size at most $(\lfloor n / \Delta \rfloor)$, where $(n)$ is the number of vertices.

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
