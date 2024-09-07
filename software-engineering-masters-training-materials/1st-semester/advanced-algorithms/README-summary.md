## **Advanced Algorithms**

### **1. Advanced Data Structures**

#### **Self-Balancing Trees**

**AVL Trees**

An AVL tree is a self-balancing binary search tree where the height difference between left and right subtrees (balance factor) is at most 1. This balance ensures O(log n) time complexity for insertion, deletion, and lookup.

**Java Code Example:**
```java
class AVLTree {
    class Node {
        int key, height;
        Node left, right;

        Node(int d) {
            key = d;
            height = 1;
        }
    }

    Node root;

    // Utility function to get the height of the node
    int height(Node N) {
        if (N == null)
            return 0;
        return N.height;
    }

    // Utility function to get the balance factor of the node
    int getBalance(Node N) {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    // Right rotate utility
    Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // Left rotate utility
    Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Insert a node
    Node insert(Node node, int key) {
        // 1. Perform the normal BST insert
        if (node == null)
            return (new Node(key));

        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);
        else
            return node;

        // 2. Update height of this ancestor node
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // 3. Get the balance factor of this ancestor node to check whether
        // this node became unbalanced
        int balance = getBalance(node);

        // If this node becomes unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        // return the (unchanged) node pointer
        return node;
    }
}
```

**Red-Black Trees**

A Red-Black Tree is another type of self-balancing binary search tree where each node contains an extra bit for denoting color (red or black), used to ensure the tree remains balanced during insertions and deletions.

**Java Code Example:**
```java
// Implementation of Red-Black Tree is more complex and not fully provided here for brevity
```

#### **Hashing Techniques**

**Hash Tables with Chaining**

A hash table with chaining uses a list to handle collisions, storing multiple values in a single hash table slot.

**Java Code Example:**
```java
import java.util.LinkedList;

class HashTable {
    private LinkedList<Integer>[] table;
    private int size;

    public HashTable(int size) {
        this.size = size;
        table = new LinkedList[size];
        for (int i = 0; i < size; i++) {
            table[i] = new LinkedList<>();
        }
    }

    // Hash function
    private int hash(int key) {
        return key % size;
    }

    // Insert a key
    public void insert(int key) {
        int index = hash(key);
        table[index].add(key);
    }

    // Search for a key
    public boolean search(int key) {
        int index = hash(key);
        return table[index].contains(key);
    }

    // Delete a key
    public void delete(int key) {
        int index = hash(key);
        table[index].remove(Integer.valueOf(key));
    }
}
```

#### **Fenwick Trees, Segment Trees, and Binary Indexed Trees**

**Fenwick Tree (Binary Indexed Tree)**

A Fenwick Tree is a data structure that provides efficient methods for cumulative frequency tables.

**Java Code Example:**
```java
class FenwickTree {
    private int[] tree;
    private int size;

    public FenwickTree(int size) {
        this.size = size;
        tree = new int[size + 1];
    }

    // Update the value at index idx
    public void update(int idx, int delta) {
        for (; idx <= size; idx += idx & -idx)
            tree[idx] += delta;
    }

    // Query the prefix sum from 1 to idx
    public int query(int idx) {
        int sum = 0;
        for (; idx > 0; idx -= idx & -idx)
            sum += tree[idx];
        return sum;
    }
}
```

#### **Union-Find Structures**

**Union-Find (Disjoint Set Union)**

Union-Find is used to keep track of a partition of a set into disjoint subsets.

**Java Code Example:**
```java
class UnionFind {
    private int[] parent, rank;

    public UnionFind(int size) {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            parent[i] = i;
            rank[i] = 0;
        }
    }

    // Find the root of the set containing x
    public int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    // Union the sets containing x and y
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            // Union by rank
            if (rank[rootX] > rank[rootY])
                parent[rootY] = rootX;
            else if (rank[rootX] < rank[rootY])
                parent[rootX] = rootY;
            else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
}
```

---

### **2. Dynamic Programming**

#### **Tabulation and Memoization**

**Memoization Example**

Memoization involves storing the results of expensive function calls and reusing them when the same inputs occur again.

**Java Code Example:**
```java
import java.util.HashMap;
import java.util.Map;

class Fibonacci {
    private Map<Integer, Integer> memo = new HashMap<>();

    public int fib(int n) {
        if (n <= 1) return n;
        if (memo.containsKey(n)) return memo.get(n);
        int result = fib(n - 1) + fib(n - 2);
        memo.put(n, result);
        return result;
    }
}
```

**Tabulation Example**

Tabulation involves building up a table in a bottom-up manner.

**Java Code Example:**
```java
class FibonacciTabulation {
    public int fib(int n) {
        if (n <= 1) return n;
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

#### **Advanced Problems**

**Knapsack Problem**

The 0/1 Knapsack Problem involves choosing items with given weights and values to maximize the total value without exceeding the weight limit.

**Java Code Example:**
```java
class Knapsack {
    public int knapSack(int W, int[] wt, int[] val, int n) {
        int[][] dp = new int[n + 1][W + 1];

        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (i == 0 || w == 0) {
                    dp[i][w] = 0;
                } else if (wt[i - 1] <= w) {
                    dp[i][w] = Math.max(val[i - 1] + dp[i - 1][w - wt[i - 1]], dp[i - 1][w]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }
        return dp[n][W

];
    }
}
```

**Edit Distance**

The Edit Distance problem involves finding the minimum number of operations required to transform one string into another.

**Java Code Example:**
```java
class EditDistance {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0) {
                    dp[i][j] = j;
                } else if (j == 0) {
                    dp[i][j] = i;
                } else if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1]));
                }
            }
        }
        return dp[m][n];
    }
}
```

**Longest Common Subsequence**

The Longest Common Subsequence problem involves finding the longest subsequence common to two sequences.

**Java Code Example:**
```java
class LCS {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }
}
```

---

### **3. Graph Algorithms**

#### **Shortest Paths**

**Dijkstra’s Algorithm**

Dijkstra’s algorithm finds the shortest path from a source node to all other nodes in a graph with non-negative weights.

**Java Code Example:**
```java
import java.util.*;

class Dijkstra {
    public int[] dijkstra(int[][] graph, int src) {
        int V = graph.length;
        int[] dist = new int[V];
        boolean[] sptSet = new boolean[V];

        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        pq.add(new int[]{src, 0});

        while (!pq.isEmpty()) {
            int[] u = pq.poll();
            int uNode = u[0];

            if (sptSet[uNode]) continue;
            sptSet[uNode] = true;

            for (int v = 0; v < V; v++) {
                if (!sptSet[v] && graph[uNode][v] != 0 && dist[uNode] + graph[uNode][v] < dist[v]) {
                    dist[v] = dist[uNode] + graph[uNode][v];
                    pq.add(new int[]{v, dist[v]});
                }
            }
        }
        return dist;
    }
}
```

**Bellman-Ford Algorithm**

Bellman-Ford computes shortest paths from a source vertex in graphs that may contain negative weights.

**Java Code Example:**
```java
class BellmanFord {
    public int[] bellmanFord(int[][] graph, int V, int E, int src) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        for (int i = 0; i < V - 1; i++) {
            for (int j = 0; j < E; j++) {
                int u = graph[j][0];
                int v = graph[j][1];
                int weight = graph[j][2];
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                }
            }
        }

        // Check for negative-weight cycles
        for (int j = 0; j < E; j++) {
            int u = graph[j][0];
            int v = graph[j][1];
            int weight = graph[j][2];
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                System.out.println("Graph contains negative weight cycle");
            }
        }
        return dist;
    }
}
```

#### **Maximum Flow**

**Ford-Fulkerson Algorithm**

Ford-Fulkerson computes the maximum flow in a flow network using augmenting paths.

**Java Code Example:**
```java
class FordFulkerson {
    private static final int V = 6;

    // Returns the maximum flow from s to t in the given graph
    public int fordFulkerson(int[][] graph, int s, int t) {
        int u, v;
        int[][] rGraph = new int[V][V];
        for (u = 0; u < V; u++)
            for (v = 0; v < V; v++)
                rGraph[u][v] = graph[u][v];

        int[] parent = new int[V];
        int max_flow = 0;

        while (bfs(rGraph, s, t, parent)) {
            int path_flow = Integer.MAX_VALUE;
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                path_flow = Math.min(path_flow, rGraph[u][v]);
            }

            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                rGraph[u][v] -= path_flow;
                rGraph[v][u] += path_flow;
            }

            max_flow += path_flow;
        }
        return max_flow;
    }

    private boolean bfs(int[][] rGraph, int s, int t, int[] parent) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();
        queue.add(s);
        visited[s] = true;
        parent[s] = -1;

        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int v = 0; v < V; v++) {
                if (!visited[v] && rGraph[u][v] > 0) {
                    queue.add(v);
                    visited[v] = true;
                    parent[v] = u;
                    if (v == t)
                        return true;
                }
            }
        }
        return false;
    }
}
```

#### **Minimum Spanning Trees**

**Prim’s Algorithm**

Prim’s algorithm finds a minimum spanning tree for a connected weighted graph.

**Java Code Example:**
```java
class PrimMST {
    public int primMST(int[][] graph) {
        int V = graph.length;
        int[] key = new int[V];
        boolean[] mstSet = new boolean[V];
        int[][] parent = new int[V][V];

        for (int i = 0; i < V; i++) {
            key[i] = Integer.MAX_VALUE;
            mstSet[i] = false;
        }
        key[0] = 0;
        parent[0][0] = -1;

        for (int count = 0; count < V - 1; count++) {
            int u = minKey(key, mstSet);
            mstSet[u] = true;

            for (int v = 0; v < V; v++) {
                if (graph[u][v] != 0 && !mstSet[v] && graph[u][v] < key[v]) {
                    parent[v][u] = graph[u][v];
                    key[v] = graph[u][v];
                }
            }
        }

        int mst_weight = 0;
        for (int i = 1; i < V; i++)
            mst_weight += parent[i][i];

        return mst_weight;
    }

    private int minKey(int[] key, boolean[] mstSet) {
        int min = Integer.MAX_VALUE;
        int min_index = -1;

        for (int v = 0; v < key.length; v++) {
            if (!mstSet[v] && key[v] < min) {
                min = key[v];
                min_index = v;
            }
        }

        return min_index;
    }
}
```

#### **NP-Hard and Approximation Algorithms**

**Traveling Salesman Problem (TSP)**

**Greedy Approximation Algorithm**

A common approximation for TSP is the Greedy algorithm, which builds the tour by repeatedly choosing the nearest unvisited city.

**Java Code Example:**
```java
import java.util.ArrayList;
import java.util.List;

class TSPGreedy {
    public List<Integer> tspGreedy(int[][] graph) {
        int V = graph.length;
        boolean[] visited = new boolean[V];
        List<Integer> tour = new ArrayList<>();
        int currVertex = 0;
        tour.add(currVertex);
        visited[currVertex] = true;

        for (int i = 1; i < V; i++) {
            int nextVertex = -1;
            int minDist = Integer.MAX_VALUE;
            for (

int j = 0; j < V; j++) {
                if (!visited[j] && graph[currVertex][j] < minDist) {
                    minDist = graph[currVertex][j];
                    nextVertex = j;
                }
            }
            tour.add(nextVertex);
            visited[nextVertex] = true;
            currVertex = nextVertex;
        }

        return tour;
    }
}
```

---

### **4. Randomized Algorithms**

#### **Monte Carlo and Las Vegas Algorithms**

**Monte Carlo Algorithms**

Monte Carlo algorithms use randomness to solve problems, providing probabilistic guarantees on the results.

**Java Code Example:**
```java
import java.util.Random;

class MonteCarloPi {
    public double estimatePi(int numSamples) {
        int insideCircle = 0;
        Random rand = new Random();

        for (int i = 0; i < numSamples; i++) {
            double x = rand.nextDouble();
            double y = rand.nextDouble();
            if (x * x + y * y <= 1) {
                insideCircle++;
            }
        }

        return 4.0 * insideCircle / numSamples;
    }
}
```

**Las Vegas Algorithms**

Las Vegas algorithms always produce the correct result, but their runtime can be variable and is often based on randomness.

**Java Code Example:**
```java
// Example of Las Vegas algorithms can be more complex and context-specific
```
