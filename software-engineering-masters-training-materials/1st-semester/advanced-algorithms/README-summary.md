# Advanced Algorithms

- [Advanced Algorithms](#advanced-algorithms)
  - [Advanced Data Structures](#advanced-data-structures)
    - [Self-Balancing Trees](#self-balancing-trees)
      - [AVL Trees](#avl-trees)
      - [Red-Black Trees](#red-black-trees)
      - [Chaining Mechanism](#chaining-mechanism)
    - [Fenwick Trees Segment Trees and Binary Indexed Trees](#fenwick-trees-segment-trees-and-binary-indexed-trees)
      - [Fenwick Tree (Binary Indexed Tree)](#fenwick-tree-binary-indexed-tree)
  - [Dynamic Programming](#dynamic-programming)
    - [Tabulation and Memoization](#tabulation-and-memoization)
  - [Graph Algorithms](#graph-algorithms)
    - [Shortest Paths](#shortest-paths)
      - [Dijkstra’s Algorithm](#dijkstras-algorithm)
      - [Bellman-Ford Algorithm](#bellman-ford-algorithm)
      - [Maximum Flow](#maximum-flow)
      - [Minimum Spanning Trees](#minimum-spanning-trees)
  - [Complexity Theory and Approximation](#complexity-theory-and-approximation)
    - [NP-Hard and Approximation Algorithms](#np-hard-and-approximation-algorithms)
      - [Traveling Salesman Problem (TSP)](#traveling-salesman-problem-tsp)
      - [Greedy Approximation Algorithm](#greedy-approximation-algorithm)
  - [Algorithmique Techniques](#algorithmique-techniques)
    - [Randomized Algorithms](#randomized-algorithms)
    - [Monte Carlo and Las Vegas Algorithms](#monte-carlo-and-las-vegas-algorithms)
      - [Monte Carlo Algorithms](#monte-carlo-algorithms)
      - [Las Vegas Algorithms](#las-vegas-algorithms)

## Advanced Data Structures

### Self-Balancing Trees

#### AVL Trees

**Key Concepts of AVL Trees**

1. **Binary Search Tree Property**:
   - Like any **binary search tree (BST)**, an AVL tree follows the basic properties of a BST:
     - The **left subtree** of a node contains nodes with keys **less than** the node's key.
     - The **right subtree** of a node contains nodes with keys **greater than** the node's key.
     - Both the left and right subtrees must also be binary search trees.

2. **Balance Factor**:
   - The **balance factor** of a node in an AVL tree is the difference in height between its left and right subtrees.
   - Mathematically, this is expressed as:
     \[
     \text{Balance Factor} = \text{Height of Left Subtree} - \text{Height of Right Subtree}
     \]
   - For a balanced AVL tree, the balance factor must be one of **{-1, 0, +1}**.
     - **Balance factor of 0**: The left and right subtrees are of the same height.
     - **Balance factor of -1**: The right subtree is taller than the left subtree by one level.
     - **Balance factor of +1**: The left subtree is taller than the right subtree by one level.

   If any node has a balance factor that deviates from this range (i.e., it becomes less than -1 or greater than +1), the tree needs to be **rebalanced**.

3. **Tree Rotation** (Balancing the Tree):
   - To maintain the balance of the AVL tree after insertion or deletion, **tree rotations** are used.
   - There are **four types of rotations** used in AVL trees to restore balance:
     1. **Single Right Rotation (LL Rotation)**: This occurs when a node is inserted into the **left subtree of the left child**. It requires a right rotation.
     2. **Single Left Rotation (RR Rotation)**: This occurs when a node is inserted into the **right subtree of the right child**. It requires a left rotation.
     3. **Left-Right Rotation (LR Rotation)**: This occurs when a node is inserted into the **right subtree of the left child**. It requires a left rotation followed by a right rotation.
     4. **Right-Left Rotation (RL Rotation)**: This occurs when a node is inserted into the **left subtree of the right child**. It requires a right rotation followed by a left rotation.

   The goal of rotations is to restore the tree to a balanced state while preserving the binary search tree property.

**Operations on AVL Trees**

1. **Insertion**:
   - Insertion in an AVL tree is similar to that in a regular binary search tree. However, after the insertion, the balance factor of each node is updated, starting from the inserted node up to the root.
   - If the balance factor of any node becomes **+2** or **-2**, the tree is rebalanced using rotations.
   - Time Complexity: **O(log n)**, where **n** is the number of nodes in the tree.

2. **Deletion**:
   - Deletion in an AVL tree is also similar to a standard BST deletion. After the deletion of a node, the balance factors of the affected nodes are recalculated.
   - If the balance factor of any node becomes **+2** or **-2**, rotations are applied to restore balance.
   - Deletion may require multiple rotations to fully restore balance.
   - Time Complexity: **O(log n)**.

3. **Search/Lookup**:
   - Searching for a node in an AVL tree works the same way as in a regular binary search tree: the algorithm recursively traverses the tree, either left or right, depending on the value being searched.
   - Due to the balanced nature of AVL trees, searching is efficient.
   - Time Complexity: **O(log n)**.

**Advantages of AVL Trees**

- **Self-Balancing**: The AVL tree remains balanced at all times, ensuring efficient operations for insertion, deletion, and search. This guarantees that the height of the tree remains logarithmic relative to the number of nodes, i.e., **O(log n)** height.
  
- **Faster Lookups**: Due to its stricter balancing condition (compared to other self-balancing trees like red-black trees), AVL trees tend to have faster lookup times in practice, as they maintain a more strictly balanced structure.

**Disadvantages of AVL Trees**

- **More Rotations**: To maintain strict balance, AVL trees may require more rotations after insertions and deletions compared to other balanced trees like red-black trees. This can make insertion and deletion operations slightly more expensive.
  
- **Memory Overhead**: Each node in an AVL tree requires extra memory to store its balance factor, which adds a small overhead compared to simpler tree structures.

**Comparison with Other Self-Balancing Trees**

- **AVL vs. Red-Black Trees**: Red-black trees are another type of self-balancing binary search tree. While AVL trees guarantee a height difference of at most 1, red-black trees allow a height difference of up to 2x, making them less strictly balanced. As a result, AVL trees have better lookup times but may require more rotations during insertions and deletions.
  
- **AVL vs. Splay Trees**: Splay trees adjust their structure based on access patterns, bringing frequently accessed elements closer to the root. AVL trees do not consider access patterns but focus solely on balance, making AVL trees more efficient for uniformly accessed data.

**Example of an AVL Tree**

**Insertion Example**

Consider inserting the following sequence of values into an AVL tree:  
**10, 20, 30, 40, 50, 25**

1. After inserting 10, 20, and 30, the tree becomes unbalanced with a balance factor of **-2** at the root. To fix this, a **left rotation** is performed around 20:
   ```
       20
      /  \
    10    30
   ```

2. Insert 40 and 50. The balance factor becomes **-2** at node 30, so a left rotation is performed at node 30:
   ```
       20
      /  \
    10    40
         /  \
       30    50
   ```

3. Insert 25. This requires a **right-left rotation** at node 40:
   ```
       20
      /  \
    10    30
         /  \
       25    40
                \
                 50
   ```

After the rotations, the tree is balanced with all nodes having a balance factor of {-1, 0, +1}.

#### Red-Black Trees

A **Red-Black Tree** is a self-balancing binary search tree, where each node has an extra attribute: the color, which can either be **red** or **black**. This coloring scheme helps maintain balance with less frequent restructuring than AVL trees, resulting in a good balance between lookup speed and insertion/deletion efficiency.

The Red-Black Tree enforces the following **properties**:
1. **Node Color**: Each node is either red or black.
2. **Root Property**: The root is always black.
3. **Leaf Property**: All leaves (null nodes) are black.
4. **Red Property**: No two consecutive red nodes are allowed (a red node cannot have a red parent).
5. **Black Height Property**: Every path from a node to its descendant leaves must have the same number of black nodes.

These properties ensure that the longest path from the root to any leaf is at most twice the length of the shortest path, guaranteeing an **O(log n)** time complexity for insertion, deletion, and lookup.

**Java Code Implementation of Red-Black Tree**

Below is a Java implementation of a Red-Black Tree that supports insertion while maintaining the necessary properties of the tree.

```java
// Class representing a node in the Red-Black Tree
class RedBlackNode {
    int data;
    RedBlackNode left, right, parent;
    boolean color; // True for Red, False for Black

    public RedBlackNode(int data) {
        this.data = data;
        left = right = parent = null;
        color = true; // New nodes are red by default
    }
}

// Red-Black Tree implementation
class RedBlackTree {
    private RedBlackNode root;
    private RedBlackNode TNULL; // Sentinel node to represent null leaves

    public RedBlackTree() {
        TNULL = new RedBlackNode(0);
        TNULL.color = false; // TNULL is black
        root = TNULL;
    }

    // Inorder traversal to display the tree
    public void inorder() {
        inorderHelper(this.root);
    }

    // Helper function for inorder traversal
    private void inorderHelper(RedBlackNode node) {
        if (node != TNULL) {
            inorderHelper(node.left);
            System.out.print(node.data + " ");
            inorderHelper(node.right);
        }
    }

    // Rotate left around the given node
    private void leftRotate(RedBlackNode x) {
        RedBlackNode y = x.right;
        x.right = y.left;
        if (y.left != TNULL) {
            y.left.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null) {
            this.root = y;
        } else if (x == x.parent.left) {
            x.parent.left = y;
        } else {
            x.parent.right = y;
        }
        y.left = x;
        x.parent = y;
    }

    // Rotate right around the given node
    private void rightRotate(RedBlackNode y) {
        RedBlackNode x = y.left;
        y.left = x.right;
        if (x.right != TNULL) {
            x.right.parent = y;
        }
        x.parent = y.parent;
        if (y.parent == null) {
            this.root = x;
        } else if (y == y.parent.right) {
            y.parent.right = x;
        } else {
            y.parent.left = x;
        }
        x.right = y;
        y.parent = x;
    }

    // Fix the red-black tree properties after insertion
    private void fixInsert(RedBlackNode k) {
        RedBlackNode u;
        while (k.parent.color == true) { // While parent is red
            if (k.parent == k.parent.parent.left) {
                u = k.parent.parent.right; // Uncle
                if (u.color == true) {
                    // Case 1: Uncle is red
                    k.parent.color = false; // Parent becomes black
                    u.color = false; // Uncle becomes black
                    k.parent.parent.color = true; // Grandparent becomes red
                    k = k.parent.parent; // Move up to the grandparent
                } else {
                    // Case 2: Uncle is black, and k is right child
                    if (k == k.parent.right) {
                        k = k.parent;
                        leftRotate(k);
                    }
                    // Case 3: Uncle is black, and k is left child
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    rightRotate(k.parent.parent);
                }
            } else {
                // Mirror of the above code for the other side
                u = k.parent.parent.left;
                if (u.color == true) {
                    // Case 1: Uncle is red
                    k.parent.color = false;
                    u.color = false;
                    k.parent.parent.color = true;
                    k = k.parent.parent;
                } else {
                    // Case 2: Uncle is black, and k is left child
                    if (k == k.parent.left) {
                        k = k.parent;
                        rightRotate(k);
                    }
                    // Case 3: Uncle is black, and k is right child
                    k.parent.color = false;
                    k.parent.parent.color = true;
                    leftRotate(k.parent.parent);
                }
            }
            if (k == root) {
                break;
            }
        }
        root.color = false; // Root must always be black
    }

    // Insert a new node into the Red-Black Tree
    public void insert(int key) {
        RedBlackNode node = new RedBlackNode(key);
        node.parent = null;
        node.left = TNULL;
        node.right = TNULL;

        RedBlackNode y = null;
        RedBlackNode x = this.root;

        while (x != TNULL) {
            y = x;
            if (node.data < x.data) {
                x = x.left;
            } else {
                x = x.right;
            }
        }

        node.parent = y;
        if (y == null) {
            root = node; // Tree was empty
        } else if (node.data < y.data) {
            y.left = node;
        } else {
            y.right = node;
        }

        if (node.parent == null) {
            node.color = false; // Root is always black
            return;
        }

        if (node.parent.parent == null) {
            return;
        }

        // Fix the tree to maintain Red-Black properties
        fixInsert(node);
    }

    // Main function to test Red-Black Tree
    public static void main(String[] args) {
        RedBlackTree tree = new RedBlackTree();

        int[] keys = {20, 15, 25, 10, 5, 1, 30, 35, 40, 45};

        for (int key : keys) {
            tree.insert(key);
        }

        // Print the inorder traversal of the tree
        tree.inorder();
    }
}
```

**Explanation of the Code**:

1. **Node Structure**:
   - Each node in the Red-Black Tree has an integer `data`, a color (true for red, false for black), and pointers to left, right, and parent nodes.
   - We use a sentinel node `TNULL` to represent null nodes, and it is always black.

2. **Rotations**:
   - **Left and Right rotations** are standard operations in self-balancing trees to maintain balance. The tree structure is modified in these rotations to preserve the binary search tree properties and balance the tree after insertions or deletions.

3. **Insertion**:
   - A node is inserted similarly to a binary search tree.
   - After insertion, the `fixInsert` method is called to ensure that the Red-Black Tree properties are maintained. The method handles various cases, including re-coloring and rotations, to ensure the tree remains balanced.

4. **Inorder Traversal**:
   - The `inorder()` method prints the values of the tree in sorted order. This is useful to verify the structure of the tree.

**Time Complexity**:

- **Insertion, Deletion, Search**: O(log n), because the Red-Black Tree ensures that the height of the tree remains logarithmic relative to the number of nodes.

**Conclusion**:

The Red-Black Tree balances itself using color properties and rotations, making it an efficient data structure for dynamic sets where insertions and deletions are frequent. This Java implementation handles insertion while preserving Red-Black Tree properties. Deletion is similar but more complex and involves additional re-balancing steps.

**Hash Tables with Chaining**

A **Hash Table with Chaining** is a data structure that uses an array (often called a **hash table**) to store key-value pairs. It efficiently supports operations like **insert**, **search**, and **delete** in average-case **O(1)** time complexity. However, in real-world scenarios, when two or more keys hash to the same index (a phenomenon known as a **collision**), the hash table needs to handle these collisions effectively. **Chaining** is one of the most commonly used collision resolution techniques.

**Key Concepts of Hash Tables with Chaining**

1. **Hash Function**:
   - A **hash function** maps a key (of arbitrary size) to an index (bucket) in the hash table. This index is used to store the value associated with the key.
   - A typical hash function is something like:
     \[
     h(key) = key \% table\_size
     \]
     where `table_size` is the size of the array used for the hash table.
   - The goal is to distribute keys uniformly across the hash table to minimize collisions.

2. **Collisions**:
   - A **collision** occurs when two different keys map to the same index in the hash table. In this case, the hash table needs a strategy to resolve the collision.
   - In **hashing with chaining**, each bucket in the hash table stores a linked list (or another dynamic data structure like a list) to hold multiple key-value pairs that hash to the same index.

#### Chaining Mechanism

- In **chaining**, every slot (bucket) in the hash table is associated with a list (or chain) of key-value pairs. When a collision occurs, the new key-value pair is simply appended to the list at the corresponding bucket.
  
- In other words, if two keys hash to the same index, instead of overwriting the existing value, both values are stored in a list (or chain) attached to that index.

**Example**

Assume a hash table has a size of 10, and the hash function is:
\[
h(key) = key \% 10
\]
Now consider inserting keys 15, 25, 35:
- For **key 15**: \( h(15) = 15 \% 10 = 5 \). It is stored at index 5.
- For **key 25**: \( h(25) = 25 \% 10 = 5 \). This collides with key 15, so it is added to the chain at index 5.
- For **key 35**: \( h(35) = 35 \% 10 = 5 \). This also collides with keys 15 and 25, so it is added to the chain at index 5.

Now, the hash table at index 5 will have a chain (list) containing the values 15, 25, and 35.

**Operations on Hash Table with Chaining**

1. **Insertion**:
   - The hash function is used to compute the index (bucket) where the key-value pair should be inserted.
   - If no collision occurs (i.e., the bucket is empty), the key-value pair is directly stored at that index.
   - If a collision occurs, the key-value pair is appended to the list (chain) at that index.
   - **Time Complexity**: The average-case time complexity is **O(1)**, assuming the hash function distributes the keys evenly across the hash table.

2. **Search**:
   - To search for a key, the hash function is applied to the key to find the corresponding bucket.
   - The linked list at the bucket is searched for the desired key.
   - In the average case (when collisions are rare), the time complexity is **O(1)**. However, in the worst case (if many keys map to the same bucket), the time complexity could degrade to **O(n)**, where **n** is the number of keys stored at that bucket.

3. **Deletion**:
   - To delete a key-value pair, the hash function is applied to the key to locate the appropriate bucket.
   - The linked list (chain) at that bucket is searched for the key, and once found, the key-value pair is removed from the list.
   - **Time Complexity**: Like search, deletion also operates in **O(1)** time in the average case, but in the worst case, it could be **O(n)** if many keys map to the same bucket.

**Advantages of Hash Tables with Chaining**

1. **Dynamic Chain Growth**:
   - Since chains (linked lists) can grow dynamically, there is no fixed limit on the number of key-value pairs that can be stored in a bucket, making the hash table flexible in handling collisions.

2. **Simple Implementation**:
   - The concept of chaining is simple and easy to implement. By using a linked list, we can easily handle collisions without needing to resize the hash table frequently.

3. **Handles High Load Factors**:
   - A **load factor** is the ratio of the number of elements stored to the number of buckets in the hash table. A hash table with chaining can handle a high load factor since the linked lists allow for multiple elements to be stored in a single bucket.

**Disadvantages of Hash Tables with Chaining**

1. **Extra Space for Linked Lists**:
   - Chaining requires additional space for pointers in the linked list, increasing the overall memory usage of the hash table.

2. **Performance Degradation with High Collisions**:
   - If the hash function does not distribute the keys evenly, some buckets may have very long chains, resulting in search, insert, and delete operations degrading to **O(n)** time complexity.

3. **Poor Cache Performance**:
   - Accessing elements in a linked list can result in poor cache performance compared to probing methods (e.g., open addressing) where data is stored contiguously in memory.

**Example: Hash Table with Chaining in Java**

Below is an implementation of a Hash Table with Chaining in Java using a linked list for each bucket.

```java
import java.util.LinkedList;

// Class to represent the Hash Table with Chaining
class HashTableChaining {
    private int bucketSize; // Size of the hash table (number of buckets)
    private LinkedList<KeyValuePair>[] table; // Array of linked lists

    // Constructor
    public HashTableChaining(int size) {
        bucketSize = size;
        table = new LinkedList[bucketSize];

        // Initialize each bucket with an empty linked list
        for (int i = 0; i < bucketSize; i++) {
            table[i] = new LinkedList<>();
        }
    }

    // Class representing a key-value pair
    class KeyValuePair {
        int key;
        String value;

        public KeyValuePair(int key, String value) {
            this.key = key;
            this.value = value;
        }
    }

    // Hash function to map a key to an index
    private int hashFunction(int key) {
        return key % bucketSize;
    }

    // Insert a key-value pair into the hash table
    public void insert(int key, String value) {
        int index = hashFunction(key); // Compute the hash index
        KeyValuePair newPair = new KeyValuePair(key, value);

        // Check if the key already exists and update the value if it does
        for (KeyValuePair pair : table[index]) {
            if (pair.key == key) {
                pair.value = value; // Update the value
                return;
            }
        }

        // If the key does not exist, add the new key-value pair to the list
        table[index].add(newPair);
    }

    // Search for a value by key
```

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

### Fenwick Trees Segment Trees and Binary Indexed Trees

#### Fenwick Tree (Binary Indexed Tree)

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

**Union-Find Structures**

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

## Dynamic Programming

**Dynamic Programming (DP)** is a powerful algorithmic technique used to solve optimization problems by breaking them down into simpler subproblems and solving each subproblem only once, storing their solutions to avoid redundant computations. It is particularly effective for problems that exhibit overlapping subproblems and optimal substructure properties.

**When to Use Dynamic Programming**

Dynamic programming is employed when:
- **Subproblem Overlap**: A problem can be broken down into overlapping subproblems. Instead of recomputing the solutions to these subproblems multiple times, DP solves each subproblem once and stores its result.
- **Optimal Substructure**: The solution to the problem can be constructed efficiently from the solutions of its subproblems. In other words, the optimal solution to the problem contains optimal solutions to its subproblems.

Common examples where dynamic programming is used include:
- **Fibonacci Sequence**: Efficiently computing Fibonacci numbers.
- **Knapsack Problem**: Finding the most valuable combination of items that fit within a given capacity.
- **Shortest Path Problems**: Finding the shortest path in weighted graphs (e.g., Dijkstra’s algorithm).
- **Edit Distance**: Computing the minimum number of operations required to transform one string into another.

**Advantages of Dynamic Programming**

1. **Efficiency**: By storing the results of subproblems, DP avoids redundant calculations, which can lead to significant improvements in time complexity compared to naive recursive approaches.
2. **Optimal Solutions**: DP guarantees an optimal solution by exploring all possible ways to solve the problem and selecting the best one.
3. **Versatility**: It can be applied to a wide range of problems, from combinatorial optimization to string processing and resource allocation.

**Disadvantages of Dynamic Programming**

1. **Space Complexity**: DP often requires additional space to store the results of subproblems, which can be significant for large problems. This can be mitigated in some cases using space optimization techniques.
2. **Complexity**: Designing and implementing a DP solution can be complex, particularly for problems where the state space or transition function is not straightforward.
3. **Overhead**: The overhead of managing and storing intermediate results can be considerable, especially if the problem does not have a large amount of overlapping subproblems.

In summary, dynamic programming is a technique that can transform a problem with exponential time complexity into one with polynomial time complexity by leveraging previously computed results. While it can be highly effective, it requires careful consideration of space and implementation complexity.

### Tabulation and Memoization

**Memoization Example**

Memoization is a technique used to optimize programs by storing the results of expensive function calls and reusing those results when the same inputs occur again. This helps avoid redundant computations and can significantly improve the performance of recursive algorithms.
When to Use Memoization

    Recursive Algorithms with Overlapping Subproblems:
        When you have a recursive algorithm where the same subproblems are solved multiple times. For example, in algorithms that involve dynamic programming or divide-and-conquer strategies, memoization can be particularly effective.

    Dynamic Programming:
        Memoization is often used in dynamic programming to store results of subproblems to avoid redundant calculations. It can be applied to problems where you need to build solutions to larger problems based on the solutions to smaller subproblems.

    Computationally Expensive Operations:
        When a function has a high computational cost, and its results can be reused. This is common in scenarios where the same inputs might be processed multiple times.

    Recursive Data Structures:
        When working with recursive data structures like trees or graphs, memoization can help to avoid reprocessing the same nodes or states.

Daily Use Cases

    Algorithm Optimization:
        In competitive programming or algorithm design, memoization is used to optimize recursive algorithms to make them feasible for larger input sizes.

    Web Development:
        In web applications, memoization can be used in caching mechanisms to store the results of expensive operations like database queries or API calls.

    Data Processing:
        When processing large datasets, memoization can be used to cache intermediate results of complex computations, such as in data analysis or scientific simulations.

    Machine Learning:
        Memoization can be applied in machine learning for caching results of expensive computations or model evaluations to speed up training and prediction.

Example: Fibonacci Sequence

To illustrate memoization, let’s consider an example where we compute Fibonacci numbers. The naive recursive approach has an exponential time complexity due to redundant calculations. Memoization optimizes this by storing intermediate results.

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

**Advanced Problems**

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

## Graph Algorithms

### Shortest Paths

#### Dijkstra’s Algorithm

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

#### Bellman-Ford Algorithm

Bellman-Ford computes shortest paths from a source vertex in graphs that may contain negative weights.

When to Use Bellman-Ford Algorithm

    Graphs with Negative Weights:
        The Bellman-Ford algorithm is specifically designed to work with graphs that may have edges with negative weights. If the graph contains negative weight edges but no negative weight cycles, Bellman-Ford can still compute the shortest paths.

    Negative Weight Cycle Detection:
        One of the strengths of Bellman-Ford is its ability to detect negative weight cycles. If a graph contains a negative weight cycle (i.e., a cycle that reduces the path length indefinitely), Bellman-Ford can identify this and indicate that no solution exists for the shortest path problem due to the cycle.

    Sparse Graphs:
        While Bellman-Ford is less efficient than Dijkstra's algorithm in general, it can be preferable in sparse graphs with negative weights. It has a time complexity of O(V * E) where V is the number of vertices and E is the number of edges. For graphs where E is small relative to V^2, this can be practical.

    Single-Source Shortest Path Problem in Large Graphs:
        In scenarios where you need to compute shortest paths from a single source to all other vertices, and negative weights are involved, Bellman-Ford is a suitable choice.

    Educational and Theoretical Contexts:
        Bellman-Ford is often used in educational settings to teach the principles of shortest path algorithms, especially due to its ability to handle negative weights and its straightforward implementation.

Examples of Use Cases

    Financial Systems:
        In financial systems where transactions or currency exchanges involve negative rates (e.g., discounts or credits), Bellman-Ford can be used to calculate optimal transaction paths and detect arbitrage opportunities (negative weight cycles).

    Network Routing:
        In network routing algorithms where bandwidth or latency might be represented as negative weights (e.g., gains in signal quality), Bellman-Ford can help determine the shortest path in such networks.

    Optimization Problems:
        In various optimization problems, such as scheduling and resource allocation, where costs might have negative components, Bellman-Ford can be used to find optimal paths or detect cycles that lead to infinite reductions in costs.

    Graph-based Games:
        In game development, particularly in scenarios where certain moves or paths have negative costs (e.g., losing points), Bellman-Ford can help in optimizing game strategies and paths.

Time and Space Complexity

    Time Complexity: O(V * E) where V is the number of vertices and E is the number of edges.
        This is because Bellman-Ford performs relaxation operations for all edges over V-1 iterations.
    Space Complexity: O(V)
        Space is needed to store the distance values for each vertex and the graph representation.

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

#### Maximum Flow

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

#### Minimum Spanning Trees

**Minimum Spanning Trees (MSTs)** are used to find the subset of edges in a connected, undirected graph that connects all the vertices with the minimum total edge weight. They are fundamental in network design and optimization. Here are some common real-world scenarios where MSTs are used:

**1. Network Design**

- **Telecommunications Networks**: In designing communication networks (e.g., phone networks, internet infrastructure), MST algorithms help in laying out the network with the least total cost while ensuring all nodes are connected.
  
- **Computer Networks**: MSTs are used in the design of computer networks to minimize the cost of connecting various network nodes (computers, servers) with minimal cabling or wireless connections.

- **Transportation Networks**: MSTs are useful in designing efficient transportation networks, such as road systems or railways, where the goal is to connect all cities with the minimum construction cost.

**2. Resource Optimization**

- **Power Grid Design**: In the design of electrical grids, MSTs help in determining the optimal way to connect power stations and consumers to minimize the total length of power lines while ensuring reliable distribution.

- **Pipeline Layout**: For the oil and gas industry, MSTs assist in designing pipelines to connect different drilling sites and refineries with minimal piping cost.

**3. Facility Layout**

- **Manufacturing Plants**: MSTs can be used in facility layout problems where machinery and workstations need to be connected efficiently to minimize the cost of material handling or conveyor belts.

- **Warehouse Design**: In logistics, MSTs can help in designing warehouse layouts to minimize the distance traveled by goods between different storage areas.

**4. Graph-Based Problems**

- **Clustering and Data Analysis**: MSTs are used in clustering algorithms to group similar items or data points together. For example, in hierarchical clustering, MSTs can help in identifying clusters by connecting items with minimal total distance.

- **Image Segmentation**: In computer vision, MSTs can be used to segment images into regions by connecting pixels or regions with minimal edge weight, which can be useful for object detection and recognition.

**5. Optimization Problems**

- **Network Reliability**: MSTs help in ensuring network reliability by providing a structure that minimizes the impact of network failures and ensures all nodes remain connected with minimal additional connections.

- **Tour Planning**: When planning efficient routes or tours that need to visit multiple points with minimal travel cost, MSTs can be used as a baseline for heuristic solutions.

**Prim's Algorithm**

**Prim’s Algorithm** is a classic algorithm used to find the Minimum Spanning Tree (MST) of a connected weighted graph. The MST is a subset of the edges that connect all vertices in the graph without any cycles and with the minimum possible total edge weight.

**Algorithm Overview**:

- **Start**: Initialize with a single vertex.
- **Grow**: Expand the MST by adding the smallest edge that connects a vertex in the MST with a vertex outside the MST.
- **Repeat**: Continue until all vertices are included in the MST.

**Key Characteristics**:

- **Greedy Approach**: Prim’s algorithm always selects the minimum weight edge that extends the current MST.
- **Efficiency**: It runs in O(V^2) time with an adjacency matrix, but can be improved to O(E log V) with a priority queue.

**Java Code Example**:

The following Java code implements Prim’s Algorithm to find the Minimum Spanning Tree (MST) of a given graph. The graph is represented using an adjacency matrix where `graph[i][j]` indicates the weight of the edge between vertices `i` and `j`.

```java
class PrimMST {
    /**
     * Computes the weight of the Minimum Spanning Tree (MST) using Prim's Algorithm.
     * 
     * @param graph 2D array representing the adjacency matrix of the graph
     * @return Total weight of the MST
     */
    public int primMST(int[][] graph) {
        int V = graph.length; // Number of vertices in the graph
        int[] key = new int[V]; // Key values used to pick the minimum weight edge
        boolean[] mstSet = new boolean[V]; // To track vertices included in the MST
        int[][] parent = new int[V][V]; // To store the parent of each vertex in the MST

        // Initialize all keys as INFINITE and mstSet as false
        for (int i = 0; i < V; i++) {
            key[i] = Integer.MAX_VALUE; // Use MAX_VALUE to denote infinity
            mstSet[i] = false; // All vertices are initially not included in the MST
        }
        key[0] = 0; // Start with the first vertex
        parent[0][0] = -1; // The first node is the root of the MST

        // Find the MST for V-1 vertices
        for (int count = 0; count < V - 1; count++) {
            // Pick the minimum key vertex from the set of vertices not yet included in MST
            int u = minKey(key, mstSet);
            mstSet[u] = true; // Include this vertex in the MST

            // Update the key and parent values of the adjacent vertices
            for (int v = 0; v < V; v++) {
                // Update key if graph[u][v] is smaller than key[v] and v is not yet included in the MST
                if (graph[u][v] != 0 && !mstSet[v] && graph[u][v] < key[v]) {
                    parent[v][u] = graph[u][v]; // Update parent to reflect the new edge in the MST
                    key[v] = graph[u][v]; // Update the key to reflect the new minimum edge weight
                }
            }
        }

        // Calculate the total weight of the MST
        int mst_weight = 0;
        for (int i = 1; i < V; i++)
            mst_weight += parent[i][i]; // Sum the weights of the MST edges

        return mst_weight; // Return the total weight of the MST
    }

    /**
     * Finds the vertex with the minimum key value from the set of vertices not yet included in the MST.
     * 
     * @param key Array of key values
     * @param mstSet Boolean array representing whether vertices are included in the MST
     * @return Index of the vertex with the minimum key value
     */
    private int minKey(int[] key, boolean[] mstSet) {
        int min = Integer.MAX_VALUE; // Initialize minimum key value
        int min_index = -1; // Initialize index of the minimum key value

        for (int v = 0; v < key.length; v++) {
            // Update min_index if the vertex is not in mstSet and has a smaller key value
            if (!mstSet[v] && key[v] < min) {
                min = key[v];
                min_index = v;
            }
        }

        return min_index; // Return the index of the vertex with the minimum key value
    }
}
```

**Explanation**:

1. **Initialization**:
   - **`key[]`**: Keeps track of the minimum weight edge connecting a vertex to the growing MST.
   - **`mstSet[]`**: Boolean array to check if a vertex is included in the MST.
   - **`parent[][]`**: 2D array to store the parent of each vertex in the MST.

2. **Algorithm Execution**:
   - **Finding the Minimum Key Vertex**: The `minKey()` method identifies the vertex with the smallest key value that has not yet been included in the MST.
   - **Updating Keys and Parents**: For each vertex added to the MST, update the key and parent values of its adjacent vertices.

3. **MST Weight Calculation**:
   - After constructing the MST, compute the total weight by summing up the weights of the edges in the MST stored in `parent[][]`.

**Note**: The use of a 2D array `parent[][]` in this example is not typical. Usually, a single-dimensional `parent[]` array is sufficient to store parent relationships in MST algorithms. The provided code serves to illustrate the concept but may need adjustment for practical implementations.

## Complexity Theory and Approximation

### NP-Hard and Approximation Algorithms

**NP-Hard** problems are those for which no known polynomial-time algorithms exist to find an exact solution, and solving them efficiently for all instances is considered computationally infeasible. Approximation algorithms are used to find near-optimal solutions within a reasonable amount of time for such problems. One well-known NP-Hard problem is the **Traveling Salesman Problem (TSP)**.

#### Traveling Salesman Problem (TSP)

To illustrate the Traveling Salesman Problem (TSP), let's consider a simple example with 4 cities. We'll use both the brute-force approach to find the exact solution and a greedy algorithm to provide an approximation.

**Problem Statement**

Given 4 cities with the following distances between them:

- **Distances Matrix**:
  - City 0 to City 1: 10
  - City 0 to City 2: 15
  - City 0 to City 3: 20
  - City 1 to City 2: 35
  - City 1 to City 3: 25
  - City 2 to City 3: 30

We want to find the shortest route that visits each city exactly once and returns to the starting city.

**1. Brute Force Solution**

We'll use the brute force approach to find the exact solution. This method evaluates all possible permutations of cities and calculates the total distance for each permutation to find the minimum.

**Java Code for Brute Force Solution**:

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class TSPBruteForce {
    private int[][] graph;
    private int V;

    public TSPBruteForce(int[][] graph) {
        this.graph = graph;
        this.V = graph.length;
    }

    public int findShortestPath() {
        List<Integer> vertices = new ArrayList<>();
        for (int i = 1; i < V; i++) {
            vertices.add(i);
        }

        int minPath = Integer.MAX_VALUE;
        List<Integer> minTour = null;

        do {
            int currentPathWeight = calculatePathWeight(vertices);
            if (currentPathWeight < minPath) {
                minPath = currentPathWeight;
                minTour = new ArrayList<>(vertices);
            }
        } while (nextPermutation(vertices));

        System.out.println("Minimum Path: " + minTour);
        return minPath;
    }

    private int calculatePathWeight(List<Integer> vertices) {
        int pathWeight = 0;
        int currentVertex = 0;

        for (int nextVertex : vertices) {
            pathWeight += graph[currentVertex][nextVertex];
            currentVertex = nextVertex;
        }

        pathWeight += graph[currentVertex][0]; // Return to the start node
        return pathWeight;
    }

    private boolean nextPermutation(List<Integer> vertices) {
        int i = vertices.size() - 1;
        while (i > 0 && vertices.get(i - 1) >= vertices.get(i)) {
            i--;
        }
        if (i <= 0) {
            return false;
        }

        int j = vertices.size() - 1;
        while (vertices.get(j) <= vertices.get(i - 1)) {
            j--;
        }

        Collections.swap(vertices, i - 1, j);
        Collections.reverse(vertices.subList(i, vertices.size()));

        return true;
    }

    public static void main(String[] args) {
        int[][] graph = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        };
        TSPBruteForce tsp = new TSPBruteForce(graph);
        System.out.println("Shortest Path Cost: " + tsp.findShortestPath());
    }
}
```

**2. Greedy Approximation Algorithm**

The greedy algorithm constructs the route by always choosing the nearest unvisited city.

**Java Code for Greedy Algorithm**:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class TSPGreedy {
    private int[][] graph;
    private int V;

    public TSPGreedy(int[][] graph) {
        this.graph = graph;
        this.V = graph.length;
    }

    public List<Integer> findShortestPath() {
        boolean[] visited = new boolean[V];
        List<Integer> tour = new ArrayList<>();
        int currentVertex = 0;

        tour.add(currentVertex);
        visited[currentVertex] = true;

        for (int i = 1; i < V; i++) {
            int nearestVertex = findNearestVertex(currentVertex, visited);
            tour.add(nearestVertex);
            visited[nearestVertex] = true;
            currentVertex = nearestVertex;
        }

        tour.add(0); // Return to the start node
        return tour;
    }

    private int findNearestVertex(int currentVertex, boolean[] visited) {
        int minDistance = Integer.MAX_VALUE;
        int nearestVertex = -1;

        for (int i = 0; i < V; i++) {
            if (!visited[i] && graph[currentVertex][i] < minDistance) {
                minDistance = graph[currentVertex][i];
                nearestVertex = i;
            }
        }

        return nearestVertex;
    }

    public static void main(String[] args) {
        int[][] graph = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        };
        TSPGreedy tsp = new TSPGreedy(graph);
        List<Integer> tour = tsp.findShortestPath();
        System.out.println("Tour: " + tour);
        int tourCost = calculateTourCost(graph, tour);
        System.out.println("Tour Cost: " + tourCost);
    }

    private static int calculateTourCost(int[][] graph, List<Integer> tour) {
        int cost = 0;
        for (int i = 0; i < tour.size() - 1; i++) {
            cost += graph[tour.get(i)][tour.get(i + 1)];
        }
        return cost;
    }
}
```

**Explanation**

- **Brute Force Approach**:
  - Evaluates all permutations of cities to find the shortest route.
  - Suitable for small instances due to its factorial time complexity.
  - In this example, it finds the exact shortest path and prints it along with the cost.

- **Greedy Algorithm**:
  - Constructs a route by always choosing the nearest unvisited city.
  - Provides an approximation to the TSP.
  - In this example, it constructs a tour and prints the tour along with its cost.

These examples illustrate how the TSP can be approached with both exact and heuristic methods, depending on the size of the problem and the desired balance between accuracy and computational efficiency.

Certainly! Here's a detailed breakdown of the time and space complexity for both the brute-force and greedy approaches to solving the Traveling Salesman Problem (TSP):

**1. Brute Force Approach**

**Time Complexity**:
- The brute-force approach generates all possible permutations of the cities to evaluate each possible tour. 
- For `n` cities, the number of permutations is `n!` (factorial), where `n!` denotes the number of ways to arrange `n` items.
- Thus, the time complexity of the brute-force approach is `O(n!)`, which is factorial time complexity. This is extremely inefficient for large values of `n` due to the rapid growth of factorial numbers.

**Space Complexity**:
- The primary space usage comes from storing the distances between cities and the permutations.
- The space complexity is `O(n)` for storing the distances in an `n x n` matrix.
- Additional space is required for storing permutations and intermediate results. However, this space is relatively small compared to the factorial growth of permutations.
- Overall, the space complexity can be approximated as `O(n)` for practical purposes.

**2. Greedy Algorithm**

**Time Complexity**:
- The greedy algorithm constructs the tour by iteratively choosing the nearest unvisited city.
- In each step, it needs to find the nearest city from the current city. This requires scanning all unvisited cities.
- For each of the `n` cities, finding the nearest city involves a linear scan of the remaining `n - 1` cities. 
- Therefore, the time complexity is `O(n^2)`, where `n` is the number of cities. This is polynomial time complexity, making it more feasible for larger instances compared to the brute-force approach.

**Space Complexity**:
- The primary space usage includes the distance matrix, which is `O(n^2)`, and arrays or lists to keep track of visited cities and the tour.
- Additional space is used for storing the tour and visited status, which is `O(n)`.
- Overall, the space complexity is `O(n^2)` due to the distance matrix.

**Summary**

- **Brute Force Approach**:
  - **Time Complexity**: `O(n!)`
  - **Space Complexity**: `O(n)`

- **Greedy Algorithm**:
  - **Time Complexity**: `O(n^2)`
  - **Space Complexity**: `O(n^2)`

The brute-force approach guarantees finding the optimal solution but is infeasible for large numbers of cities due to its exponential time complexity. The greedy algorithm provides a heuristic solution with polynomial time complexity, making it suitable for larger instances, although it does not guarantee the optimal solution.

#### Greedy Approximation Algorithm

The **Greedy Approximation Algorithm** for TSP is one of the simplest approximation approaches. It builds the tour incrementally by always choosing the nearest unvisited city from the current city. This approach does not guarantee the optimal solution but can provide a reasonably good solution with less computational effort.

**Characteristics**:
- **Heuristic Approach**: The algorithm does not guarantee an optimal solution but provides a feasible solution quickly.
- **Efficiency**: The time complexity is linear in terms of the number of cities, making it suitable for larger instances.
- **Approximation Quality**: The performance of the greedy algorithm can vary depending on the distribution of cities and distances.

**Java Code Example:**

The following Java code implements the Greedy Approximation Algorithm for TSP. This code assumes that the distance between cities is represented as a 2D array where `graph[i][j]` denotes the distance from city `i` to city `j`.

```java
import java.util.ArrayList;
import java.util.List;

class TSPGreedy {
    /**
     * Computes a tour using the Greedy Approximation Algorithm for the Traveling Salesman Problem (TSP).
     * 
     * @param graph 2D array representing the distance between each pair of cities
     * @return List of integers representing the tour, starting from city 0
     */
    public List<Integer> tspGreedy(int[][] graph) {
        int V = graph.length; // Number of cities
        boolean[] visited = new boolean[V]; // Array to keep track of visited cities
        List<Integer> tour = new ArrayList<>(); // List to store the tour
        int currVertex = 0; // Start the tour from the first city
        tour.add(currVertex); // Add the starting city to the tour
        visited[currVertex] = true; // Mark the starting city as visited

        // Iterate through the remaining cities
        for (int i = 1; i < V; i++) {
            int nextVertex = -1; // Index of the next city to visit
            int minDist = Integer.MAX_VALUE; // Minimum distance initialized to infinity
            
            // Find the nearest unvisited city
            for (int j = 0; j < V; j++) {
                // Check if the city is unvisited and if the distance is smaller than the current minimum distance
                if (!visited[j] && graph[currVertex][j] < minDist) {
                    minDist = graph[currVertex][j]; // Update the minimum distance
                    nextVertex = j; // Update the next city to visit
                }
            }
            
            // Add the nearest city to the tour
            tour.add(nextVertex);
            visited[nextVertex] = true; // Mark the city as visited
            currVertex = nextVertex; // Move to the next city
        }

        // Return the tour as a list of city indices
        return tour;
    }

    public static void main(String[] args) {
        // Example graph: 4 cities with distances between them
        int[][] graph = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        };

        TSPGreedy tsp = new TSPGreedy();
        List<Integer> tour = tsp.tspGreedy(graph);
        
        System.out.println("Greedy TSP Tour: " + tour);
    }
}
```

**Explanation**:

- **Graph Representation**: The graph is represented as a 2D array where `graph[i][j]` gives the distance between city `i` and city `j`.
- **Initialization**: Start from the first city (city 0), mark it as visited, and add it to the tour.
- **Greedy Selection**: For each city, select the nearest unvisited city and update the current city to this newly selected city.
- **Tour Construction**: Continue this process until all cities are visited, resulting in a tour that starts from city 0 and includes all cities.

**Note**: This code does not handle returning to the starting city or dealing with edge cases such as disconnected graphs. In practical applications, additional considerations might be needed to complete the tour and handle various constraints.

## Algorithmique Techniques

### Randomized Algorithms

### Monte Carlo and Las Vegas Algorithms

Monte Carlo and Las Vegas algorithms are two types of randomized algorithms that use randomness in different ways to solve problems efficiently. Here's a more detailed explanation of each, along with Java code examples:

#### Monte Carlo Algorithms

**Monte Carlo algorithms** use randomness to provide approximate solutions to problems. They are particularly useful when exact solutions are computationally infeasible. These algorithms offer probabilistic guarantees, meaning that the solution provided is correct with high probability, but not guaranteed to be correct every time.

**Characteristics**:
- **Probabilistic Output**: The result may be approximate or incorrect, but the probability of correctness can be quantified.
- **Performance**: They are often used when the problem can be solved more quickly or feasibly using random sampling rather than deterministic methods.
- **Applications**: Monte Carlo algorithms are commonly used in simulations, optimization problems, and numerical integration.

**Java Code Example: Monte Carlo Method for Estimating Pi**

The following Java code demonstrates how to use a Monte Carlo algorithm to estimate the value of π (Pi) by randomly sampling points in a unit square and checking if they fall inside a unit circle.

```java
import java.util.Random;

class MonteCarloPi {
    // Method to estimate the value of Pi using the Monte Carlo method
    public double estimatePi(int numSamples) {
        int insideCircle = 0;
        Random rand = new Random();

        // Generate numSamples random points
        for (int i = 0; i < numSamples; i++) {
            double x = rand.nextDouble(); // Random x-coordinate
            double y = rand.nextDouble(); // Random y-coordinate
            // Check if the point is inside the unit circle
            if (x * x + y * y <= 1) {
                insideCircle++;
            }
        }

        // Estimate Pi using the ratio of points inside the circle to total points
        return 4.0 * insideCircle / numSamples;
    }

    public static void main(String[] args) {
        MonteCarloPi mcPi = new MonteCarloPi();
        int numSamples = 1000000; // Number of samples to generate
        double piEstimate = mcPi.estimatePi(numSamples);
        System.out.println("Estimated value of Pi: " + piEstimate);
    }
}
```

**Explanation**:

- **Random Sampling**: Points are randomly generated within a unit square.
- **Inside Circle Check**: Points that lie inside the unit circle are counted.
- **Estimation**: The ratio of points inside the circle to the total number of points is used to estimate π.

#### Las Vegas Algorithms

**Las Vegas algorithms** also use randomness, but they always produce the correct result. The runtime of these algorithms, however, can be variable and depends on the random choices made during execution. The randomness affects the speed or efficiency of obtaining the result rather than the correctness of the result itself.

**Characteristics**:

- **Guaranteed Correctness**: The algorithm will always provide a correct result, but the time to find that result may vary.
- **Randomness in Runtime**: The runtime can be influenced by random decisions or probabilistic factors, which may lead to faster or slower performance.
- **Applications**: They are often used in probabilistic algorithms where an exact or optimal solution is needed, but the process to obtain it may be randomized to improve expected performance.

**Java Code Example:**

While Las Vegas algorithms are often more complex and context-specific, a classic example is the **Randomized QuickSort** algorithm. Here’s a simplified version demonstrating a randomized approach to sorting:

```java
import java.util.Random;

class RandomizedQuickSort {
    private static final Random rand = new Random();

    // Method to perform Randomized QuickSort
    public void sort(int[] arr, int low, int high) {
        if (low < high) {
            // Partition the array
            int pivotIndex = partition(arr, low, high);
            // Recursively sort the subarrays
            sort(arr, low, pivotIndex - 1);
            sort(arr, pivotIndex + 1, high);
        }
    }

    // Method to partition the array around a random pivot
    private int partition(int[] arr, int low, int high) {
        int pivotIndex = low + rand.nextInt(high - low + 1);
        int pivot = arr[pivotIndex];
        // Swap pivot with the last element
        swap(arr, pivotIndex, high);
        int i = low;
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                swap(arr, i, j);
                i++;
            }
        }
        // Place the pivot in the correct position
        swap(arr, i, high);
        return i;
    }

    // Method to swap elements in the array
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = { 10, 7, 8, 9, 1, 5 };
        RandomizedQuickSort sorter = new RandomizedQuickSort();
        sorter.sort(arr, 0, arr.length - 1);
        System.out.println("Sorted array: ");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

**Explanation**:

- **Random Pivot Selection**: The algorithm selects a random pivot index for partitioning the array.
- **Correctness**: The algorithm always produces a correctly sorted array, but the time taken can vary depending on the pivot choices.

Both Monte Carlo and Las Vegas algorithms leverage randomness to achieve their goals, but they do so in different ways: Monte Carlo algorithms provide probabilistic results, while Las Vegas algorithms ensure correctness but with varying runtimes.
