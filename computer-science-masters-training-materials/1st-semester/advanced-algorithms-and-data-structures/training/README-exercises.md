### **1. Divide and Conquer Algorithms**

1. **(Implementation)** Implement Karatsuba’s algorithm for fast multiplication of large integers and analyze its time complexity compared to standard multiplication.
   
2. **(Theoretical)** Prove the correctness of the Strassen matrix multiplication algorithm and analyze its time complexity.

3. **(Theoretical)** Solve the recurrence \( T(n) = 2T(n/2) + O(n) \) using the Master Theorem, and explain how it applies to the merge sort algorithm.

4. **(Implementation)** Implement the Fast Fourier Transform (FFT) algorithm for polynomial multiplication and analyze its performance.

5. **(Theoretical)** Use divide-and-conquer to solve the closest pair of points problem in \( O(n \log n) \). Explain your approach.

6. **(Theoretical)** Analyze the time complexity of the quicksort algorithm in the best case, worst case, and average case. Explain how randomized quicksort improves the average case.

7. **(Implementation)** Implement a divide-and-conquer algorithm to find the majority element in an array (an element that appears more than \( n/2 \) times) in \( O(n \log n) \).

8. **(Theoretical)** Derive the recurrence relation for matrix exponentiation using divide and conquer, and analyze its time complexity.

9. **(Implementation)** Implement the divide-and-conquer algorithm to count the number of inversions in an array.

10. **(Theoretical)** Use the Master Theorem to solve the recurrence \( T(n) = 3T(n/3) + O(n) \) and explain its application in divide-and-conquer algorithms.

---

### **2. Graph Algorithms and Dynamic Graph Data Structures**

11. **(Implementation)** Implement Dijkstra’s algorithm and compare its performance with the Bellman-Ford algorithm on various types of graphs.

12. **(Theoretical)** Prove that Kruskal’s algorithm always produces a minimum spanning tree, and analyze its time complexity using a disjoint-set data structure.

13. **(Implementation)** Implement a dynamic connectivity data structure (e.g., link/cut trees or dynamic MST) and analyze its performance for a sequence of edge insertions and deletions.

14. **(Implementation)** Implement and compare DFS-based and BFS-based algorithms for detecting strongly connected components in a directed graph.

15. **(Theoretical)** Prove the correctness of Prim’s algorithm for finding the minimum spanning tree and analyze its performance using a Fibonacci heap.

16. **(Theoretical)** Show that the Ford-Fulkerson algorithm may fail to terminate when applied to a network with irrational capacities, and explain the consequences.

17. **(Implementation)** Implement the Edmonds-Karp algorithm for computing the maximum flow in a network, and compare it with the Ford-Fulkerson algorithm.

18. **(Theoretical)** Prove that Dijkstra’s algorithm fails when negative edge weights are present, using an example graph.

19. **(Implementation)** Design and implement a dynamic graph data structure that supports efficient shortest path updates as edges are added and removed.

20. **(Theoretical)** Prove the correctness of Tarjan’s offline lowest common ancestor (LCA) algorithm and analyze its time complexity.

---

### **3. Cache-Efficient Algorithms**

21. **(Implementation)** Implement a cache-oblivious matrix multiplication algorithm and compare its cache performance with the naive \( O(n^3) \) algorithm.

22. **(Theoretical)** Prove that merge sort can be made cache-efficient by modifying the merge step to minimize cache misses, and analyze its cache complexity.

23. **(Theoretical)** Explain the working of cache-oblivious binary search, and prove that it achieves \( O(\log_B n) \) cache misses, where \( B \) is the block size.

24. **(Theoretical)** Analyze the cache performance of quicksort and merge sort in both the cache-oblivious and cache-aware models. Which is better?

25. **(Implementation)** Implement a cache-oblivious algorithm for matrix transposition, and measure its cache performance against a naive row-major order transposition.

26. **(Theoretical)** Explain how to modify quicksort to make it cache-oblivious and analyze the resulting performance.

27. **(Theoretical)** Show that any cache-oblivious algorithm for the matrix multiplication problem that uses the divide-and-conquer paradigm has an optimal cache complexity of \( O(n^3 / B + n^2) \).

28. **(Implementation)** Implement the cache-oblivious priority queue as described in the research paper by Frigo et al. and analyze its cache performance.

29. **(Theoretical)** Derive and prove the optimality of the cache-oblivious algorithm for finding the median of a set of numbers.

30. **(Implementation)** Design and implement a cache-oblivious sorting algorithm and measure its performance against traditional sorting algorithms like quicksort and mergesort.

---

### **4. Algorithmic Paradigms: Greedy, Dynamic Programming, Approximation Algorithms**

31. **(Implementation)** Implement the Huffman coding algorithm and use it to compress and decompress a text file. Analyze its performance on different datasets.

32. **(Theoretical)** Prove the correctness of the greedy algorithm for the activity selection problem and explain why a dynamic programming approach is unnecessary.

33. **(Implementation)** Implement the dynamic programming solution to the knapsack problem and compare its performance with a greedy heuristic for the fractional knapsack problem.

34. **(Theoretical)** Prove that the greedy algorithm for finding a minimum spanning tree (Kruskal’s algorithm) is optimal.

35. **(Theoretical)** Prove that the dynamic programming algorithm for the longest common subsequence problem has time complexity \( O(nm) \), where \( n \) and \( m \) are the lengths of the two strings.

36. **(Implementation)** Implement a 2-approximation algorithm for the vertex cover problem and compare it with the exact solution.

37. **(Implementation)** Implement the Bellman-Ford algorithm to solve the single-source shortest paths problem on graphs with negative weights.

38. **(Theoretical)** Analyze the performance of a dynamic programming solution to the edit distance problem and prove its optimality.

39. **(Implementation)** Implement the dynamic programming solution to the traveling salesman problem (TSP) and compare it with the performance of a greedy approximation algorithm.

40. **(Theoretical)** Prove that there is no polynomial-time algorithm for the TSP unless P=NP, but that there exists a \( \frac{3}{2} \)-approximation algorithm for the metric TSP.

---

### **5. Online and Streaming Algorithms**

41. **(Implementation)** Implement the Least Recently Used (LRU) caching algorithm and evaluate its competitive ratio compared to the optimal offline solution.

42. **(Theoretical)** Prove that the greedy algorithm for the online bipartite matching problem achieves a competitive ratio of \( 1/2 \).

43. **(Implementation)** Implement a Count-Min Sketch to estimate the frequency of elements in a stream and compare it with the exact solution in terms of memory usage and performance.

44. **(Theoretical)** Prove the correctness and analyze the competitive ratio of the paging algorithm in an online setting.

45. **(Implementation)** Design and implement an online algorithm for the k-server problem and evaluate its performance on different types of inputs.

46. **(Theoretical)** Analyze the space complexity of the Misra-Gries algorithm for finding frequent elements in a data stream and explain how it improves over naive counting.

47. **(Implementation)** Implement an algorithm to maintain the median of a data stream using two heaps, and analyze its time complexity.

48. **(Theoretical)** Prove that any online algorithm for caching has a competitive ratio of at least \( k \) in the worst case, where \( k \) is the cache size.

49. **(Implementation)** Implement an online algorithm for scheduling jobs on two machines to minimize the makespan, and analyze its competitive ratio.

50. **(Theoretical)** Analyze the competitive ratio of the greedy algorithm for the k-center problem in an online setting, and prove its bounds.
