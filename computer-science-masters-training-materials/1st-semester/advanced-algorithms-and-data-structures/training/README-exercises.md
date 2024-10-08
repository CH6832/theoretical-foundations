### **1. Divide and Conquer Algorithms**

----

**(Implementation)** Implement Karatsuba’s algorithm for fast multiplication of large integers and analyze its time complexity compared to standard multiplication.


- **Readings:**
  - [Karatsuba's Algorithm - 6.006 Revew Session](https://courses.csail.mit.edu/6.006/spring11/exams/notes3-karatsuba)
  - [Karatsuba algorithm](https://en.wikipedia.org/wiki/Karatsuba_algorithm)

- Python

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

"""Karatsuba Multiplication example."""

def number_of_digits(z):
    count=0
    for c in str(z):
        count=count+1
    return count

def karatsuba_multiplication(x, y):
    if x < 10 or y < 10:
        return x * y

    max_num = max(number_of_digits(x), number_of_digits(y))

    m = max_num // 2

    high_1 = x // **m
    low_1 = x % **m
    high_2 = y // **m
    low_2 = y % **m

    z_0 = karatsuba_multiplication(low_1, low_2)
    z_1 = karatsuba_multiplication((high_1 + low_1), (high_2 + low_2))
    z_2 = karatsuba_multiplication(high_1, high_2)

    return (z_2 * **(2*m)) + ((z_1 - z_2 - z_0) * **m) + z_0


if __name__ == "__main__":
    a = 24132
    b = 438541
    print(karatsuba_multiplication(a, b))
    print(a * b)
```

- Java

```java
public class KaratsubaMultiplication {

    public static int numberOfDigits(long z) {
        return String.valueOf(z).length();
    }

    public static long karatsubaMultiplication(long x, long y) {
        // Base case: if x or y is a single-digit number, multiply directly
        if (x < 10 || y < 10) {
            return x * y;
        }

        int maxNum = Math.max(numberOfDigits(x), numberOfDigits(y));

        int m = maxNum / 2;

        long high1 = x / (long) Math.pow(10, m);
        long low1 = x % (long) Math.pow(10, m);
        long high2 = y / (long) Math.pow(10, m);
        long low2 = y % (long) Math.pow(10, m);

        long z0 = karatsubaMultiplication(low1, low2);
        long z1 = karatsubaMultiplication((high1 + low1), (high2 + low2));
        long z2 = karatsubaMultiplication(high1, high2);

        return (z2 * (long) Math.pow(10, 2 * m)) + ((z1 - z2 - z0) * (long) Math.pow(10, m)) + z0;
    }

    public static void main(String[] args) {
        long a = 24132;
        long b = 438541;

        System.out.println("Karatsuba Result: " + karatsubaMultiplication(a, b));
        System.out.println("Standard Multiplication Result: " + (a * b));
    }
}
```

- C++

```cpp
#include <iostream>
#include <cmath>
#include <string>

using namespace std;

int number_of_digits(long long z) {
    return to_string(z).length();
}

long long karatsuba_multiplication(long long x, long long y) {
    // Base case: if x or y is a single-digit number, multiply directly
    if (x < 10 || y < 10) {
        return x * y;
    }

    int max_num = max(number_of_digits(x), number_of_digits(y));

    int m = max_num / 2;

    long long high1 = x / pow(10, m);
    long long low1 = x % (long long) pow(10, m);
    long long high2 = y / pow(10, m);
    long long low2 = y % (long long) pow(10, m);

    long long z0 = karatsuba_multiplication(low1, low2);
    long long z1 = karatsuba_multiplication((high1 + low1), (high2 + low2));
    long long z2 = karatsuba_multiplication(high1, high2);

    return (z2 * pow(10, 2 * m)) + ((z1 - z2 - z0) * pow(10, m)) + z0;
}

int main() {
    long long a = 24132;
    long long b = 438541;

    cout << "Karatsuba Result: " << karatsuba_multiplication(a, b) << endl;
    cout << "Standard Multiplication Result: " << (a * b) << endl;

    return 0;
}
```

----

**(Theoretical)** Prove the correctness of the Strassen matrix multiplication algorithm and analyze its time complexity.


- **Readings:**
  - [Strassen algorithm](https://en.wikipedia.org/wiki/Strassen_algorithm)
  - [Strassen's Algorithm proof](https://cs.stackexchange.com/questions/14907/strassens-algorithm-proof)

----

**(Theoretical)** Solve the recurrence $( T(n) = aT(n/b) + f(n) )$ using the Master Theorem, and explain how it applies to the merge sort algorithm.


- **Readings:**
  - [1 Solving recurrences-  1.3 Master theorem](https://web.stanford.edu/class/archive/cs/cs161/cs161.1168/lecture3.pdf) 

----

**(Implementation)** Implement the Fast Fourier Transform (FFT) algorithm for polynomial multiplication and analyze its performance.


- **Readings:**
  - [Fast fourier transform](https://en.wikipedia.org/wiki/Fast_Fourier_transform)

- Python

```python
import math

# Function to solve the recurrence using Master Theorem
def solve_recurrence(a, b, d):
    """
    Solve the recurrence T(n) = aT(n/b) + O(n^d) using the Master Theorem.
    
    Parameters:
    a (int): The coefficient for the recursive term.
    b (int): The divisor for the recursive problem size.
    d (int): The exponent of the non-recursive work term (f(n) = O(n^d)).
    
    Returns:
    str: Asymptotic complexity of T(n).
    """
    
    # Step 1: Calculate log_b(a)
    log_b_a = math.log(a) / math.log(b)
    
    # Step 2: Compare log_b(a) with d to determine the case
    if log_b_a > d:
        # Case 1: Recursion dominates
        return f"O(n^{log_b_a:.2f})"
    
    elif log_b_a == d:
        # Case 2: Both recursion and external work are equally contributing
        return f"O(n^{d} log n)"
    
    else:
        # Case 3: External work dominates
        return f"O(n^{d})"

# Example: Applying to the Merge Sort recurrence
def merge_sort_complexity():
    a = 2  # Two recursive calls
    b = 2  # The problem size is halved in each call
    d = 1  # Merging takes linear time O(n)

    result = solve_recurrence(a, b, d)
    print(f"Time complexity of Merge Sort using Master Theorem: {result}")

# Run the example
merge_sort_complexity()
```

- Java

```java
public class MasterTheorem {
    
    // Function to solve the recurrence using Master Theorem
    public static String solveRecurrence(int a, int b, int d) {
        // Calculate log_b(a)
        double log_b_a = Math.log(a) / Math.log(b);

        // Compare log_b(a) with d to determine the case
        if (log_b_a > d) {
            // Case 1: Recursion dominates
            return "O(n^" + String.format("%.2f", log_b_a) + ")";
        } else if (log_b_a == d) {
            // Case 2: Both recursion and external work are equally contributing
            return "O(n^" + d + " log n)";
        } else {
            // Case 3: External work dominates
            return "O(n^" + d + ")";
        }
    }

    // Example: Applying to the Merge Sort recurrence
    public static void mergeSortComplexity() {
        int a = 2; // Two recursive calls
        int b = 2; // The problem size is halved in each call
        int d = 1; // Merging takes linear time O(n)

        String result = solveRecurrence(a, b, d);
        System.out.println("Time complexity of Merge Sort using Master Theorem: " + result);
    }

    public static void main(String[] args) {
        mergeSortComplexity();
    }
}
```

- C++

```c++
#include <iostream>
#include <cmath>
#include <iomanip> // for std::setprecision

std::string solveRecurrence(int a, int b, int d) {
    // Calculate log_b(a)
    double log_b_a = std::log(a) / std::log(b);

    // Compare log_b(a) with d to determine the case
    if (log_b_a > d) {
        // Case 1: Recursion dominates
        std::ostringstream oss;
        oss << "O(n^" << std::fixed << std::setprecision(2) << log_b_a << ")";
        return oss.str();
    } else if (log_b_a == d) {
        // Case 2: Both recursion and external work are equally contributing
        return "O(n^" + std::to_string(d) + " log n)";
    } else {
        // Case 3: External work dominates
        return "O(n^" + std::to_string(d) + ")";
    }
}

// Example: Applying to the Merge Sort recurrence
void mergeSortComplexity() {
    int a = 2; // Two recursive calls
    int b = 2; // The problem size is halved in each call
    int d = 1; // Merging takes linear time O(n)

    std::string result = solveRecurrence(a, b, d);
    std::cout << "Time complexity of Merge Sort using Master Theorem: " << result << std::endl;
}

int main() {
    mergeSortComplexity();
    return 0;
}
```

----

**(Theoretical)** Use divide-and-conquer to solve the closest pair of points problem in \( O(n \log n) \). Explain your approach.


- Python

```python
import math

def main():
    points = [(2, 3), (12, 30), (40, 50), (5, 1), (12, 10), (3, 4)]
    print(f"The smallest distance is {closest_pair(points)}")  

# Function to calculate the distance between two points
def distance(p1, p2):
    return math.sqrt((p1[0] - p2[0])**2 + (p1[1] - p2[1])**2)

# Brute force method to find the closest pair for small number of points
def brute_force(points):
    min_dist = float('inf')
    n = len(points)
    for i in range(n):
        for j in range(i + 1, n):
            min_dist = min(min_dist, distance(points[i], points[j]))
    return min_dist

# Function to find the closest pair in the strip
def closest_in_strip(strip, d):
    min_dist = d
    strip.sort(key=lambda p: p[1])  # Sort by y-coordinate

    for i in range(len(strip)):
        for j in range(i + 1, len(strip)):
            if (strip[j][1] - strip[i][1]) < min_dist:
                min_dist = min(min_dist, distance(strip[i], strip[j]))
    return min_dist

# Recursive function to find the closest pair
def closest_recursive(points_x, points_y):
    n = len(points_x)
    if n <= 3:
        return brute_force(points_x)

    mid = n // 2
    mid_point = points_x[mid]

    left_x = points_x[:mid]
    right_x = points_x[mid:]
    
    left_y = list(filter(lambda p: p[0] <= mid_point[0], points_y))
    right_y = list(filter(lambda p: p[0] > mid_point[0], points_y))

    d_left = closest_recursive(left_x, left_y)
    d_right = closest_recursive(right_x, right_y)

    d = min(d_left, d_right)

    strip = [p for p in points_y if abs(p[0] - mid_point[0]) < d]

    return min(d, closest_in_strip(strip, d))

# Main function to find the closest pair of points
def closest_pair(points):
    points_x = sorted(points, key=lambda p: p[0])  # Sort by x-coordinate
    points_y = sorted(points, key=lambda p: p[1])  # Sort by y-coordinate
    return closest_recursive(points_x, points_y)

if __name__ == "__main__":
    main()
```

- Java

```java
import java.util.Arrays;

public class ClosestPair {

    // Function to calculate the distance between two points
    public static double distance(int[] p1, int[] p2) {
        return Math.sqrt(Math.pow(p1[0] - p2[0], 2) + Math.pow(p1[1] - p2[1], 2));
    }

    // Brute force method for small number of points
    public static double bruteForce(int[][] points) {
        double minDist = Double.MAX_VALUE;
        for (int i = 0; i < points.length; i++) {
            for (int j = i + 1; j < points.length; j++) {
                minDist = Math.min(minDist, distance(points[i], points[j]));
            }
        }
        return minDist;
    }

    // Function to find the closest pair in the strip
    public static double closestInStrip(int[][] strip, double d) {
        double minDist = d;
        Arrays.sort(strip, (p1, p2) -> Integer.compare(p1[1], p2[1]));  // Sort by y-coordinate

        for (int i = 0; i < strip.length; i++) {
            for (int j = i + 1; j < strip.length && (strip[j][1] - strip[i][1]) < minDist; j++) {
                minDist = Math.min(minDist, distance(strip[i], strip[j]));
            }
        }
        return minDist;
    }

    // Recursive function to find the closest pair
    public static double closestRecursive(int[][] pointsX, int[][] pointsY) {
        int n = pointsX.length;
        if (n <= 3) {
            return bruteForce(pointsX);
        }

        int mid = n / 2;
        int[] midPoint = pointsX[mid];

        int[][] leftX = Arrays.copyOfRange(pointsX, 0, mid);
        int[][] rightX = Arrays.copyOfRange(pointsX, mid, n);

        int[][] leftY = Arrays.stream(pointsY).filter(p -> p[0] <= midPoint[0]).toArray(int[][]::new);
        int[][] rightY = Arrays.stream(pointsY).filter(p -> p[0] > midPoint[0]).toArray(int[][]::new);

        double dLeft = closestRecursive(leftX, leftY);
        double dRight = closestRecursive(rightX, rightY);

        double d = Math.min(dLeft, dRight);

        int[][] strip = Arrays.stream(pointsY).filter(p -> Math.abs(p[0] - midPoint[0]) < d).toArray(int[][]::new);

        return Math.min(d, closestInStrip(strip, d));
    }

    // Main function to find the closest pair
    public static double closestPair(int[][] points) {
        int[][] pointsX = Arrays.copyOf(points, points.length);
        int[][] pointsY = Arrays.copyOf(points, points.length);

        Arrays.sort(pointsX, (p1, p2) -> Integer.compare(p1[0], p2[0]));  // Sort by x-coordinate
        Arrays.sort(pointsY, (p1, p2) -> Integer.compare(p1[1], p2[1]));  // Sort by y-coordinate

        return closestRecursive(pointsX, pointsY);
    }

    // Example usage
    public static void main(String[] args) {
        int[][] points = {{2, 3}, {12, 30}, {40, 50}, {5, 1}, {12, 10}, {3, 4}};
        System.out.println("The smallest distance is " + closestPair(points));
    }
}
```

- C++

```c++
#include <iostream>
#include <cmath>
#include <vector>
#include <algorithm>

using namespace std;

struct Point {
    int x, y;
};

// Function to calculate the distance between two points
double distance(const Point& p1, const Point& p2) {
    return sqrt(pow(p1.x - p2.x, 2) + pow(p1.y - p2.y, 2));
}

// Brute force method for small number of points
double bruteForce(const vector<Point>& points) {
    double minDist = DBL_MAX;
    for (size_t i = 0; i < points.size(); ++i) {
        for (size_t j = i + 1; j < points.size(); ++j) {
            minDist = min(minDist, distance(points[i], points[j]));
        }
    }
    return minDist;
}

// Function to find the closest pair in the strip
double closestInStrip(vector<Point>& strip, double d) {
    double minDist = d;
    sort(strip.begin(), strip.end(), [](const Point& p1, const Point& p2) {
        return p1.y < p2.y;
    });

    for (size_t i = 0; i < strip.size(); ++i) {
        for (size_t j = i + 1; j < strip.size() && (strip[j].y - strip[i].y) < minDist; ++j) {
            minDist = min(minDist, distance(strip[i], strip[j]));
        }
    }
    return minDist;
}

// Recursive function to find the closest pair
double closestRecursive(vector<Point>& pointsX, vector<Point>& pointsY) {
    int n = pointsX.size();
    if (n <= 3) {
        return bruteForce(pointsX);
    }

    int mid = n / 2;
    Point midPoint = pointsX[mid];

    vector<Point> leftX(pointsX.begin(), pointsX.begin() + mid);
    vector<Point> rightX(pointsX.begin() + mid, pointsX.end());

    vector<Point> leftY, rightY;
    for (const auto& p : pointsY) {
        if (p.x <= midPoint.x) {
            leftY.push_back(p);
        } else {
            rightY.push_back(p);
        }
    }

    double dLeft = closestRecursive(leftX, leftY);
    double dRight = closestRecursive(rightX, rightY);

    double d = min(dLeft, dRight);

    vector<Point> strip;
    for (const auto& p : pointsY) {
        if (abs(p.x - midPoint.x) < d) {
            strip.push_back(p);
        }
    }

    return min(d, closestInStrip(strip, d));
}

// Main function to find the closest pair of points
double closestPair(vector<Point>& points) {
    vector<Point> pointsX = points, pointsY = points;

    sort(pointsX.begin(), pointsX.end(), [](const Point& p1, const Point& p2) {
        return p1.x < p2.x;
    });
    sort(pointsY.begin(), pointsY.end(), [](const Point& p1, const Point& p2) {
        return p1.y < p2.y;
    });

    return closestRecursive(pointsX, pointsY);
}

// Example usage
int main() {
    vector<Point> points = {{2, 3}, {12, 30}, {40, 50}, {5, 1}, {12, 10}, {3, 4}};
    cout << "The smallest distance is " << closestPair(points) << endl;
    return 0;
}
```

---

**(Theoretical)** Analyze the time complexity of the quicksort algorithm in the best case, worst case, and average case. Explain how randomized quicksort improves the average case.

**(Implementation)** Implement a divide-and-conquer algorithm to find the majority element in an array (an element that appears more than \( n/2 \) times) in \( O(n \log n) \).

**(Theoretical)** Derive the recurrence relation for matrix exponentiation using divide and conquer, and analyze its time complexity.

**(Implementation)** Implement the divide-and-conquer algorithm to count the number of inversions in an array.

**(Theoretical)** Use the Master Theorem to solve the recurrence \( T(n) = 3T(n/3) + O(n) \) and explain its application in divide-and-conquer algorithms.

**(Implementation)** Implement the divide-and-conquer approach to find the median of two sorted arrays.

**(Theoretical)** Prove the correctness of the recursive binary search algorithm and analyze its time complexity.

**(Implementation)** Implement a divide-and-conquer algorithm to solve the 0/1 knapsack problem and analyze its performance.

**(Theoretical)** Explain how the divide-and-conquer approach can be applied to solve the maximum subarray problem (Kadane’s algorithm).

**(Implementation)** Develop an algorithm using divide-and-conquer to sort a linked list.

**(Theoretical)** Prove the optimality of the divide-and-conquer approach in calculating the convex hull of a set of points in the plane.

**(Implementation)** Implement a divide-and-conquer algorithm to calculate the power of a number \( x^n \).

**(Theoretical)** Discuss the implications of using divide-and-conquer for solving differential equations and provide an example.

**(Implementation)** Create a divide-and-conquer solution for the "Game of Life" simulation and analyze its complexity.

**(Theoretical)** Analyze the space complexity of various divide-and-conquer algorithms and suggest ways to minimize space usage.

---

### **2. Graph Algorithms and Dynamic Graph Data Structures**

**(Implementation)** Implement Dijkstra’s algorithm and compare its performance with the Bellman-Ford algorithm on various types of graphs.

**(Theoretical)** Prove that Kruskal’s algorithm always produces a minimum spanning tree, and analyze its time complexity using a disjoint-set data structure.

**(Implementation)** Implement a dynamic connectivity data structure (e.g., link/cut trees or dynamic MST) and analyze its performance for a sequence of edge insertions and deletions.

**(Implementation)** Implement and compare DFS-based and BFS-based algorithms for detecting strongly connected components in a directed graph.

**(Theoretical)** Prove the correctness of Prim’s algorithm for finding the minimum spanning tree and analyze its performance using a Fibonacci heap.

**(Theoretical)** Show that the Ford-Fulkerson algorithm may fail to terminate when applied to a network with irrational capacities, and explain the consequences.

**(Implementation)** Implement the Edmonds-Karp algorithm for computing the maximum flow in a network, and compare it with the Ford-Fulkerson algorithm.

**(Theoretical)** Prove that Dijkstra’s algorithm fails when negative edge weights are present, using an example graph.

**(Implementation)** Design and implement a dynamic graph data structure that supports efficient shortest path updates as edges are added and removed.

**(Theoretical)** Prove the correctness of Tarjan’s offline lowest common ancestor (LCA) algorithm and analyze its time complexity.

**(Implementation)** Implement an algorithm to find all articulation points in a graph using DFS.

**(Theoretical)** Discuss the applications of the Floyd-Warshall algorithm and analyze its time complexity.

**(Implementation)** Create an implementation of the A* search algorithm for pathfinding and analyze its performance.

**(Theoretical)** Prove the correctness of the Johnson algorithm for finding the shortest paths in a weighted graph.

**(Implementation)** Implement a randomized algorithm for finding a minimum spanning tree and compare it to deterministic approaches.

**(Theoretical)** Explain the role of the cut property in graph algorithms and prove its significance in finding a minimum spanning tree.

**(Implementation)** Create an algorithm to detect cycles in an undirected graph using union-find.

**(Theoretical)** Prove that the bipartite graph checking algorithm is efficient and describe its complexity.

**(Implementation)** Implement the Chinese postman problem algorithm and analyze its performance.

**(Theoretical)** Discuss the limitations of traditional graph traversal algorithms on dynamic graphs and suggest improvements.

---

### **3. Cache-Efficient Algorithms**

**(Implementation)** Implement a cache-oblivious matrix multiplication algorithm and compare its cache performance with the naive \( O(n^3) \) algorithm.

**(Theoretical)** Prove that merge sort can be made cache-efficient by modifying the merge step to minimize cache misses, and analyze its cache complexity.

**(Theoretical)** Explain the working of cache-oblivious binary search, and prove that it achieves \( O(\log_B n) \) cache misses, where \( B \) is the block size.

**(Theoretical)** Analyze the cache performance of quicksort and merge sort in both the cache-oblivious and cache-aware models. Which is better?

**(Implementation)** Implement a cache-oblivious algorithm for matrix transposition, and measure its cache performance against a naive row-major order transposition.

**(Theoretical)** Explain how to modify quicksort to make it cache-oblivious and analyze the resulting performance.

**(Theoretical)** Show that any cache-oblivious algorithm for the matrix multiplication problem that uses the divide-and-conquer paradigm has an optimal cache complexity of \( O(n^3 / B + n^2) \).

**(Implementation)** Implement the cache-oblivious priority queue as described in the research paper by Frigo et al. and analyze its cache performance.

**(Theoretical)** Derive and prove the optimality of the cache-oblivious algorithm for finding the median of a set of numbers.

**(Implementation)** Design and implement a cache-oblivious sorting algorithm and measure its performance against traditional sorting algorithms like quicksort and mergesort.

**(Theoretical)** Discuss the principles behind cache-efficient algorithms and how they differ from traditional algorithms in terms of data access patterns.

**(Implementation)** Create a cache-oblivious binary tree traversal algorithm and compare its performance to traditional approaches.

**(Theoretical)** Analyze the cache efficiency of dynamic programming algorithms and suggest optimizations.

**(Implementation)** Implement a cache-aware version of the Strassen algorithm and compare it with the cache-oblivious version.

**(Theoretical)** Prove the optimality of cache-efficient algorithms in terms of data locality and memory access patterns.

---

### **4. Algorithmic Paradigms: Greedy, Dynamic Programming, Approximation Algorithms**

**(Implementation)** Implement the Huffman coding algorithm and use it to compress and decompress a text file. Analyze its performance on different datasets.

**(Theoretical)** Prove the correctness of the greedy algorithm for the activity selection problem and explain why a dynamic programming approach is unnecessary.

**(Implementation)** Implement the dynamic programming solution to the knapsack problem and compare its performance with a greedy heuristic for the fractional knapsack problem.

**(Theoretical)** Prove that the greedy algorithm for finding a minimum spanning tree (Kruskal’s algorithm) is optimal.

**(Theoretical)** Prove that the dynamic programming algorithm for the longest common subsequence problem has time complexity \( O(nm) \), where \( n \) and \( m \) are the lengths of the two strings.

**(Implementation)** Implement a 2-approximation algorithm for the vertex cover problem and compare it with the exact solution.

**(Implementation)** Implement the Bellman-Ford algorithm to solve the single-source shortest paths problem on graphs with negative weights.

**(Theoretical)** Analyze the performance of a dynamic programming solution to the edit distance problem and prove its optimality.

**(Implementation)** Implement the dynamic programming solution to the traveling salesman problem (TSP) and compare it with the performance of a greedy approximation algorithm.

**(Theoretical)** Prove that there is no polynomial-time algorithm for the TSP unless P=NP, but that there exists a \( \frac{3}{2} \)-approximation algorithm for the metric TSP.

**(Implementation)** Implement a greedy algorithm for the coin change problem and analyze its performance compared to dynamic programming.

**(Theoretical)** Prove the correctness of the dynamic programming approach to solving the rod cutting problem.

**(Implementation)** Create a dynamic programming algorithm for solving the subset sum problem and compare it with a brute force approach.

**(Theoretical)** Discuss the trade-offs between greedy and dynamic programming approaches in optimization problems.

**(Implementation)** Implement a 3-approximation algorithm for the metric TSP and compare its results with exact solutions.

---

### **5. Online and Streaming Algorithms**

**(Implementation)** Implement the Least Recently Used (LRU) caching algorithm and evaluate its competitive ratio compared to the optimal offline solution.

**(Theoretical)** Prove that the greedy algorithm for the online bipartite matching problem achieves a competitive ratio of \( 1/2 \).

**(Implementation)** Implement a Count-Min Sketch to estimate the frequency of elements in a stream and compare it with the exact solution in terms of memory usage and performance.

**(Theoretical)** Prove the correctness and analyze the competitive ratio of the paging algorithm in an online setting.

**(Implementation)** Design and implement an online algorithm for the k-server problem and evaluate its performance on different types of inputs.

**(Theoretical)** Analyze the space complexity of the Misra-Gries algorithm for finding frequent elements in a data stream and explain how it improves over naive counting.

**(Implementation)** Implement an algorithm to maintain the median of a data stream using two heaps, and analyze its time complexity.

**(Theoretical)** Prove that any online algorithm for caching has a competitive ratio of at least \( k \) in the worst case, where \( k \) is the cache size.

**(Implementation)** Implement an online algorithm for scheduling jobs on two machines to minimize the makespan, and analyze its competitive ratio.

**(Theoretical)** Analyze the competitive ratio of the greedy algorithm for the k-center problem in an online setting, and prove its bounds.

**(Implementation)** Design a streaming algorithm to find the kth smallest element in a stream of numbers.

**(Theoretical)** Prove the optimality of the Randomized Online Algorithm for the ski rental problem.

**(Implementation)** Implement a dynamic sketching algorithm for estimating the number of distinct elements in a data stream.

**(Theoretical)** Discuss the limitations of online algorithms in terms of approximation ratios and provide examples.

**(Implementation)** Create a sliding window algorithm for calculating the average of a stream of numbers.

**(Theoretical)** Analyze the impact of delay in online algorithms and how it affects performance guarantees.

---

### **6. Advanced Topics and Research-Oriented Exercises**

**(Theoretical)** Explore and summarize recent advancements in quantum algorithms, focusing on their potential impact on classical algorithms.

**(Implementation)** Implement a machine learning algorithm and analyze its computational complexity.

**(Theoretical)** Discuss the challenges of implementing algorithms in a distributed environment and propose potential solutions.

**(Implementation)** Create a visual representation of an algorithm’s execution, such as a sorting algorithm, using a programming language of your choice.

**(Theoretical)** Analyze the implications of parallel computing on traditional algorithm design and implementation.

**(Implementation)** Develop an algorithm that integrates concepts from artificial intelligence for solving optimization problems.

**(Theoretical)** Explore the differences between deterministic and probabilistic algorithms, providing examples of each.

**(Implementation)** Create an application that uses algorithms for real-time data processing and analyze its performance.

**(Theoretical)** Research and present the implications of the P vs NP problem in modern computing.

**(Implementation)** Implement a genetic algorithm for solving a complex optimization problem and compare its performance with other algorithms.

**(Theoretical)** Discuss the role of algorithms in machine learning and data mining, and their impact on the accuracy of predictions.

**(Implementation)** Create a project that implements multiple algorithms to solve the same problem and analyze their performance in various scenarios.

**(Theoretical)** Investigate the effects of algorithmic bias in machine learning and propose ways to mitigate it.

**(Implementation)** Design an interactive tool that allows users to visualize and manipulate different algorithms in real-time.
