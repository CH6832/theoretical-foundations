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

**Code Implementation of Red-Black Tree**

Below is a Java implementation of a Red-Black Tree that supports insertion while maintaining the necessary properties of the tree.

```
// Class representing a node in the Red-Black Tree
class RedBlackNode:
    integer data
    RedBlackNode left, right, parent
    boolean color // True for Red, False for Black

    function RedBlackNode(int data):
        this.data = data
        this.left = NULL
        this.right = NULL
        this.parent = NULL
        this.color = TRUE // New nodes are red by default

// Red-Black Tree implementation
class RedBlackTree:
    RedBlackNode root
    RedBlackNode TNULL // Sentinel node to represent null leaves

    function RedBlackTree():
        TNULL = new RedBlackNode(0)
        TNULL.color = FALSE // TNULL is black
        this.root = TNULL

    // Inorder traversal to display the tree
    function inorder():
        inorderHelper(this.root)

    // Helper function for inorder traversal
    function inorderHelper(RedBlackNode node):
        if node != TNULL:
            inorderHelper(node.left)
            print node.data
            inorderHelper(node.right)

    // Rotate left around the given node
    function leftRotate(RedBlackNode x):
        RedBlackNode y = x.right
        x.right = y.left
        if y.left != TNULL:
            y.left.parent = x
        y.parent = x.parent
        if x.parent == NULL:
            this.root = y
        else if x == x.parent.left:
            x.parent.left = y
        else:
            x.parent.right = y
        y.left = x
        x.parent = y

    // Rotate right around the given node
    function rightRotate(RedBlackNode y):
        RedBlackNode x = y.left
        y.left = x.right
        if x.right != TNULL:
            x.right.parent = y
        x.parent = y.parent
        if y.parent == NULL:
            this.root = x
        else if y == y.parent.right:
            y.parent.right = x
        else:
            y.parent.left = x
        x.right = y
        y.parent = x

    // Fix the red-black tree properties after insertion
    function fixInsert(RedBlackNode k):
        RedBlackNode u
        while k.parent.color == TRUE: // While parent is red
            if k.parent == k.parent.parent.left:
                u = k.parent.parent.right // Uncle
                if u.color == TRUE: // Case 1: Uncle is red
                    k.parent.color = FALSE // Parent becomes black
                    u.color = FALSE // Uncle becomes black
                    k.parent.parent.color = TRUE // Grandparent becomes red
                    k = k.parent.parent // Move up to the grandparent
                else:
                    if k == k.parent.right: // Case 2: Uncle is black, k is right child
                        k = k.parent
                        leftRotate(k)
                    // Case 3: Uncle is black, k is left child
                    k.parent.color = FALSE
                    k.parent.parent.color = TRUE
                    rightRotate(k.parent.parent)
            else: // Mirror of the above code for the other side
                u = k.parent.parent.left
                if u.color == TRUE: // Case 1: Uncle is red
                    k.parent.color = FALSE
                    u.color = FALSE
                    k.parent.parent.color = TRUE
                    k = k.parent.parent
                else:
                    if k == k.parent.left: // Case 2: Uncle is black, k is left child
                        k = k.parent
                        rightRotate(k)
                    // Case 3: Uncle is black, k is right child
                    k.parent.color = FALSE
                    k.parent.parent.color = TRUE
                    leftRotate(k.parent.parent)
            if k == root:
                break
        root.color = FALSE // Root must always be black

    // Insert a new node into the Red-Black Tree
    function insert(int key):
        RedBlackNode node = new RedBlackNode(key)
        node.parent = NULL
        node.left = TNULL
        node.right = TNULL

        RedBlackNode y = NULL
        RedBlackNode x = this.root

        while x != TNULL:
            y = x
            if node.data < x.data:
                x = x.left
            else:
                x = x.right

        node.parent = y
        if y == NULL:
            root = node // Tree was empty
        else if node.data < y.data:
            y.left = node
        else:
            y.right = node

        if node.parent == NULL:
            node.color = FALSE // Root is always black
            return

        if node.parent.parent == NULL:
            return

        // Fix the tree to maintain Red-Black properties
        fixInsert(node)

    // Main function to test Red-Black Tree
    function main():
        RedBlackTree tree = new RedBlackTree()
        integer[] keys = {20, 15, 25, 10, 5, 1, 30, 35, 40, 45}

        for each key in keys:
            tree.insert(key)

        // Print the inorder traversal of the tree
        tree.inorder()
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

```
// Class to represent the Hash Table with Chaining
class HashTableChaining:
    integer bucketSize // Size of the hash table (number of buckets)
    LinkedList<KeyValuePair>[] table // Array of linked lists

    // Constructor
    function HashTableChaining(integer size):
        this.bucketSize = size
        this.table = new LinkedList[bucketSize]

        // Initialize each bucket with an empty linked list
        for integer i from 0 to bucketSize - 1:
            table[i] = new LinkedList<KeyValuePair>()

    // Class representing a key-value pair
    class KeyValuePair:
        integer key
        string value

        // Constructor for KeyValuePair
        function KeyValuePair(integer key, string value):
            this.key = key
            this.value = value

    // Hash function to map a key to an index
    private function hashFunction(integer key) -> integer:
        return key mod bucketSize

    // Insert a key-value pair into the hash table
    public function insert(integer key, string value):
        integer index = hashFunction(key) // Compute the hash index
        KeyValuePair newPair = new KeyValuePair(key, value)

        // Check if the key already exists and update the value if it does
        for each KeyValuePair pair in table[index]:
            if pair.key == key:
                pair.value = value // Update the value
                return

        // If the key does not exist, add the new key-value pair to the list
        table[index].add(newPair)

    // Search for a value by key
    public function search(integer key) -> string:
        integer index = hashFunction(key) // Compute the hash index

        // Search through the linked list in the corresponding bucket
        for each KeyValuePair pair in table[index]:
            if pair.key == key:
                return pair.value // Return the found value

        return NULL // Return NULL if the key does not exist

    // Remove a key-value pair from the hash table
    public function remove(integer key):
        integer index = hashFunction(key) // Compute the hash index

        // Iterate through the linked list to find the key to remove
        for each KeyValuePair pair in table[index]:
            if pair.key == key:
                table[index].remove(pair) // Remove the key-value pair
                return // Exit the function after removal

    // Main function for testing the Hash Table
    function main():
        HashTableChaining hashTable = new HashTableChaining(10) // Create a hash table with 10 buckets

        // Insert key-value pairs into the hash table
        hashTable.insert(1, "Value1")
        hashTable.insert(2, "Value2")
        hashTable.insert(12, "Value12") // Collision example, same bucket as key 2
        hashTable.insert(3, "Value3")

        // Search for a value by key
        string result = hashTable.search(2) // Should return "Value2"
        print result

        // Remove a key-value pair
        hashTable.remove(1) // Removes the pair with key 1
        result = hashTable.search(1) // Should return NULL
        print result

```

**Code Example:**

```
// Class to represent the Hash Table
class HashTable:
    LinkedList<Integer>[] table // Array of linked lists for chaining
    integer size // Size of the hash table

    // Constructor
    function HashTable(integer size):
        this.size = size
        this.table = new LinkedList[size]

        // Initialize each bucket with an empty linked list
        for integer i from 0 to size - 1:
            table[i] = new LinkedList<Integer>()

    // Hash function to map a key to an index
    private function hash(integer key) -> integer:
        return key mod size

    // Insert a key into the hash table
    public function insert(integer key):
        integer index = hash(key) // Compute the hash index
        table[index].add(key) // Add the key to the linked list at the index

    // Search for a key in the hash table
    public function search(integer key) -> boolean:
        integer index = hash(key) // Compute the hash index
        return table[index].contains(key) // Check if the key is in the linked list

    // Delete a key from the hash table
    public function delete(integer key):
        integer index = hash(key) // Compute the hash index
        table[index].remove(Integer.valueOf(key)) // Remove the key from the linked list

    // Main function for testing the Hash Table
    function main():
        HashTable hashTable = new HashTable(10) // Create a hash table with size 10

        // Insert keys into the hash table
        hashTable.insert(5)
        hashTable.insert(15) // Collision example (same bucket as key 5)
        hashTable.insert(25) // Collision example (same bucket as key 5)

        // Search for keys
        boolean found = hashTable.search(15) // Should return true
        print found
        found = hashTable.search(20) // Should return false
        print found

        // Delete a key
        hashTable.delete(15) // Removes the key 15
        found = hashTable.search(15) // Should return false
        print found
```

### Fenwick Trees Segment Trees and Binary Indexed Trees

#### Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree is a data structure that provides efficient methods for cumulative frequency tables.

**Code Example:**
```
// Class to represent the Fenwick Tree
class FenwickTree:
    integer[] tree // Array to store the Fenwick Tree values
    integer size // Size of the tree

    // Constructor
    function FenwickTree(integer size):
        this.size = size
        this.tree = new integer[size + 1] // Initialize tree with size + 1

    // Update the value at index idx
    public function update(integer idx, integer delta):
        // While idx is within bounds
        while idx <= size:
            tree[idx] += delta // Update the value at index
            idx += (idx AND -idx) // Move to the next index to update

    // Query the prefix sum from 1 to idx
    public function query(integer idx) -> integer:
        integer sum = 0 // Initialize sum to 0
        // While idx is greater than 0
        while idx > 0:
            sum += tree[idx] // Add the value at index idx to sum
            idx -= (idx AND -idx) // Move to the parent index
        return sum // Return the computed prefix sum

    // Main function for testing the Fenwick Tree
    function main():
        FenwickTree fenwickTree = new FenwickTree(10) // Create a Fenwick Tree with size 10

        // Update the Fenwick Tree
        fenwickTree.update(1, 5) // Add 5 at index 1
        fenwickTree.update(2, 3) // Add 3 at index 2
        fenwickTree.update(3, 7) // Add 7 at index 3

        // Query the prefix sums
        integer sum1 = fenwickTree.query(1) // Query sum from 1 to 1
        print sum1 // Should print 5

        integer sum2 = fenwickTree.query(2) // Query sum from 1 to 2
        print sum2 // Should print 8 (5 + 3)

        integer sum3 = fenwickTree.query(3) // Query sum from 1 to 3
        print sum3 // Should print 15 (5 + 3 + 7)
```

**Union-Find Structures**

**Union-Find (Disjoint Set Union)**

Union-Find is used to keep track of a partition of a set into disjoint subsets.

**Code Example:**
```
// Class to represent the Union-Find data structure
class UnionFind:
    integer[] parent // Array to store the parent of each element
    integer[] rank // Array to store the rank of each set

    // Constructor to initialize the Union-Find structure
    function UnionFind(integer size):
        parent = new integer[size] // Initialize parent array
        rank = new integer[size] // Initialize rank array
        // Initialize each element to be its own parent and rank to 0
        for integer i from 0 to size - 1:
            parent[i] = i // Each element is its own parent
            rank[i] = 0 // Initialize rank to 0

    // Find the root of the set containing x
    public function find(integer x) -> integer:
        if parent[x] != x: // If x is not its own parent
            parent[x] = find(parent[x]) // Path compression
        return parent[x] // Return the root of the set containing x

    // Union the sets containing x and y
    public function union(integer x, integer y):
        integer rootX = find(x) // Find the root of the set containing x
        integer rootY = find(y) // Find the root of the set containing y

        if rootX != rootY: // Only union if they are in different sets
            // Union by rank
            if rank[rootX] > rank[rootY]: // If rootX has higher rank
                parent[rootY] = rootX // Attach rootY to rootX
            else if rank[rootX] < rank[rootY]: // If rootY has higher rank
                parent[rootX] = rootY // Attach rootX to rootY
            else: // If ranks are equal
                parent[rootY] = rootX // Attach rootY to rootX
                rank[rootX]++ // Increment the rank of rootX

    // Main function for testing the Union-Find data structure
    function main():
        UnionFind uf = new UnionFind(10) // Create a Union-Find with 10 elements

        // Perform union operations
        uf.union(1, 2) // Union the sets containing 1 and 2
        uf.union(2, 3) // Union the sets containing 2 and 3
        uf.union(4, 5) // Union the sets containing 4 and 5

        // Check the roots of different elements
        integer root1 = uf.find(1) // Should return the root of set containing 1
        print root1

        integer root2 = uf.find(3) // Should return the same root as root1
        print root2

        integer root3 = uf.find(4) // Should return the root of set containing 4
        print root3

        // Check if 1 and 3 are in the same set
        boolean sameSet = (root1 == root2) // Should be true
        print sameSet

        // Check if 1 and 4 are in the same set
        sameSet = (root1 == root3) // Should be false
        print sameSet
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

**Code Example:**
```
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

**Code Example:**
```
// Class to calculate Fibonacci numbers using memoization
class Fibonacci:
    Map<Integer, Integer> memo // HashMap to store computed Fibonacci values

    // Constructor
    function Fibonacci():
        memo = new Map<Integer, Integer>() // Initialize the memoization map

    // Function to calculate Fibonacci number at position n
    public function fib(integer n) -> integer:
        if n <= 1: // Base cases
            return n // Return n if n is 0 or 1
        if memo.containsKey(n): // Check if result is already computed
            return memo.get(n) // Return the cached result

        // Compute Fibonacci number recursively and cache it
        integer result = fib(n - 1) + fib(n - 2) 
        memo.put(n, result) // Store the computed result in the map
        return result // Return the computed Fibonacci number
```

**Advanced Problems**

**Knapsack Problem**

The 0/1 Knapsack Problem involves choosing items with given weights and values to maximize the total value without exceeding the weight limit.

**Code Example:**
```
// Class to solve the 0/1 Knapsack problem
class Knapsack:
    // Function to solve the Knapsack problem
    public function knapSack(integer W, integer[] wt, integer[] val, integer n) -> integer:
        // Create a 2D array to store the maximum value for each item and weight capacity
        integer[][] dp = new integer[n + 1][W + 1]

        // Fill the dp array
        for integer i from 0 to n: // Iterate over the number of items
            for integer w from 0 to W: // Iterate over the weight capacities
                if i == 0 or w == 0: // If no items or no capacity
                    dp[i][w] = 0 // No value can be obtained
                else if wt[i - 1] <= w: // If the weight of the current item is less than or equal to the current capacity
                    // Take the maximum of including the item or not including it
                    dp[i][w] = max(val[i - 1] + dp[i - 1][w - wt[i - 1]], dp[i - 1][w])
                else: // If the weight of the current item is more than the current capacity
                    dp[i][w] = dp[i - 1][w] // Do not include the item

        return dp[n][W] // Return the maximum value that can be obtained with n items and capacity W
```

**Edit Distance**

The Edit Distance problem involves finding the minimum number of operations required to transform one string into another.

**Code Example:**
```
// Class to calculate the Edit Distance between two strings
class EditDistance:
    // Function to calculate the minimum distance between word1 and word2
    public function minDistance(string word1, string word2) -> integer:
        integer m = length of word1 // Length of the first string
        integer n = length of word2 // Length of the second string
        
        // Create a 2D array to store the edit distances
        integer[][] dp = new integer[m + 1][n + 1]

        // Fill the dp array
        for integer i from 0 to m: // Iterate through the length of word1
            for integer j from 0 to n: // Iterate through the length of word2
                if i == 0: // If word1 is empty
                    dp[i][j] = j // Minimum operations = j (insertions)
                else if j == 0: // If word2 is empty
                    dp[i][j] = i // Minimum operations = i (deletions)
                else if word1[i - 1] == word2[j - 1]: // If last characters are the same
                    dp[i][j] = dp[i - 1][j - 1] // No operation needed
                else: // If last characters are different
                    dp[i][j] = 1 + min(dp[i - 1][j], // Deletion
                                       dp[i][j - 1], // Insertion
                                       dp[i - 1][j - 1]) // Replacement

        return dp[m][n] // Return the minimum edit distance
```

**Longest Common Subsequence**

The Longest Common Subsequence problem involves finding the longest subsequence common to two sequences.

**Code Example:**
```
// Class to calculate the Longest Common Subsequence
class LCS:
    // Function to find the length of the longest common subsequence of text1 and text2
    public function longestCommonSubsequence(string text1, string text2) -> integer:
        integer m = length of text1 // Length of the first string
        integer n = length of text2 // Length of the second string
        
        // Create a 2D array to store the lengths of longest common subsequences
        integer[][] dp = new integer[m + 1][n + 1]

        // Fill the dp array
        for integer i from 1 to m: // Iterate over the length of text1
            for integer j from 1 to n: // Iterate over the length of text2
                if text1[i - 1] == text2[j - 1]: // If characters match
                    dp[i][j] = dp[i - 1][j - 1] + 1 // Increment LCS length
                else: // If characters do not match
                    dp[i][j] = max(dp[i - 1][j], // LCS without the current character of text1
                                   dp[i][j - 1]) // LCS without the current character of text2

        return dp[m][n] // Return the length of the longest common subsequence
```

## Graph Algorithms

### Shortest Paths

#### Dijkstra’s Algorithm

Dijkstra’s algorithm finds the shortest path from a source node to all other nodes in a graph with non-negative weights.

**Code Example:**
```
// Class to implement Dijkstra's algorithm
class Dijkstra:
    // Function to find the shortest paths from source node 'src' in a graph
    public function dijkstra(integer[][] graph, integer src) -> integer[]:
        integer V = length of graph // Number of vertices in the graph
        integer[] dist = new integer[V] // Array to store shortest distances
        boolean[] sptSet = new boolean[V] // Array to track vertices included in shortest path tree

        // Initialize distances to infinity and source distance to 0
        for integer i from 0 to V - 1:
            dist[i] = infinity
        dist[src] = 0 // Distance to source is 0

        // Create a priority queue to store vertices and their distances
        PriorityQueue<int[]> pq = new PriorityQueue<>(comparator that compares by distance)
        pq.add([src, 0]) // Add source node to priority queue

        // Loop until the priority queue is empty
        while not pq.isEmpty():
            int[] u = pq.poll() // Extract the vertex with the smallest distance
            integer uNode = u[0] // Current node

            // If uNode is already in the shortest path tree, skip it
            if sptSet[uNode] == true:
                continue
            sptSet[uNode] = true // Mark the current node as processed

            // Iterate through all vertices adjacent to uNode
            for integer v from 0 to V - 1:
                // Check if v is not in the shortest path tree and there is an edge
                if sptSet[v] == false and graph[uNode][v] != 0:
                    // If the new distance is shorter, update the distance
                    if dist[uNode] + graph[uNode][v] < dist[v]:
                        dist[v] = dist[uNode] + graph[uNode][v] // Update distance
                        pq.add([v, dist[v]]) // Add v to the priority queue with updated distance

        return dist // Return the array of shortest distances
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

**Code Example:**
```
// Class to implement the Bellman-Ford algorithm
class BellmanFord:
    // Function to find the shortest paths from source node 'src'
    // graph: Array of edges where each edge is represented as [u, v, weight]
    // V: Number of vertices
    // E: Number of edges
    // src: Source vertex
    public function bellmanFord(integer[][] graph, integer V, integer E, integer src) -> integer[]:
        // Initialize distances to all vertices as infinite
        integer[] dist = new integer[V]
        for integer i from 0 to V - 1:
            dist[i] = infinity
        dist[src] = 0 // Distance to source is 0

        // Relax all edges |V| - 1 times
        for integer i from 0 to V - 2:
            for integer j from 0 to E - 1:
                integer u = graph[j][0] // Start vertex of edge
                integer v = graph[j][1] // End vertex of edge
                integer weight = graph[j][2] // Weight of edge
                // Check if the distance can be shortened
                if dist[u] != infinity and dist[u] + weight < dist[v]:
                    dist[v] = dist[u] + weight // Update distance

        // Check for negative-weight cycles
        for integer j from 0 to E - 1:
            integer u = graph[j][0] // Start vertex of edge
            integer v = graph[j][1] // End vertex of edge
            integer weight = graph[j][2] // Weight of edge
            // If we can still shorten the distance, there is a negative-weight cycle
            if dist[u] != infinity and dist[u] + weight < dist[v]:
                print("Graph contains negative weight cycle")

        return dist // Return the array of shortest distances
```

#### Maximum Flow

**Ford-Fulkerson Algorithm**

Ford-Fulkerson computes the maximum flow in a flow network using augmenting paths.

**Code Example:**
```
class FordFulkerson:
    constant integer V = 6 // Number of vertices in the graph

    // Function to compute the maximum flow from source 's' to sink 't'
    public function fordFulkerson(integer[][] graph, integer s, integer t) -> integer:
        integer u, v
        integer[][] rGraph = new integer[V][V] // Residual graph
        // Initialize residual graph with the capacities of the original graph
        for integer u from 0 to V - 1:
            for integer v from 0 to V - 1:
                rGraph[u][v] = graph[u][v]

        integer[] parent = new integer[V] // Array to store the path
        integer max_flow = 0 // Initialize maximum flow

        // While there is a path from source to sink in the residual graph
        while bfs(rGraph, s, t, parent):
            integer path_flow = infinity // Initialize path flow
            // Find the maximum flow through the path found by BFS
            for v from t to s:
                u = parent[v]
                path_flow = min(path_flow, rGraph[u][v]) // Minimum capacity in the path

            // update residual capacities of the edges and reverse edges
            for v from t to s:
                u = parent[v]
                rGraph[u][v] -= path_flow // Decrease the capacity of the edge
                rGraph[v][u] += path_flow // Increase the capacity of the reverse edge

            max_flow += path_flow // Add path flow to overall flow

        return max_flow // Return the maximum flow found

    // Function to perform BFS on the residual graph
    private function bfs(integer[][] rGraph, integer s, integer t, integer[] parent) -> boolean:
        boolean[] visited = new boolean[V] // Array to track visited vertices
        Queue<Integer> queue = new Queue<Integer>() // Queue for BFS
        queue.add(s) // Start from the source
        visited[s] = true
        parent[s] = -1 // Source has no parent

        // BFS loop
        while not queue.isEmpty():
            integer u = queue.poll() // Get the front of the queue

            for integer v from 0 to V - 1:
                // If the vertex is not visited and there is a remaining capacity
                if not visited[v] and rGraph[u][v] > 0:
                    queue.add(v) // Add to queue
                    visited[v] = true // Mark as visited
                    parent[v] = u // Set parent of v
                    if v == t: // If we reached the sink
                        return true // Path found

        return false // No path found
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

**Code Example**:

The following Java code implements Prim’s Algorithm to find the Minimum Spanning Tree (MST) of a given graph. The graph is represented using an adjacency matrix where `graph[i][j]` indicates the weight of the edge between vertices `i` and `j`.

```
class PrimMST:
    /**
     * Computes the weight of the Minimum Spanning Tree (MST) using Prim's Algorithm.
     * 
     * @param graph 2D array representing the adjacency matrix of the graph
     * @return Total weight of the MST
     */
    public function primMST(integer[][] graph) -> integer:
        integer V = length of graph // Number of vertices in the graph
        integer[] key = new integer[V] // Key values used to pick the minimum weight edge
        boolean[] mstSet = new boolean[V] // To track vertices included in the MST
        integer[][] parent = new integer[V][V] // To store the parent of each vertex in the MST

        // Initialize all keys as INFINITE and mstSet as false
        for integer i from 0 to V - 1:
            key[i] = infinity // Use infinity to denote MAX_VALUE
            mstSet[i] = false // All vertices are initially not included in the MST
        key[0] = 0 // Start with the first vertex
        parent[0][0] = -1 // The first node is the root of the MST

        // Find the MST for V-1 vertices
        for integer count from 0 to V - 2:
            // Pick the minimum key vertex from the set of vertices not yet included in MST
            integer u = minKey(key, mstSet)
            mstSet[u] = true // Include this vertex in the MST

            // Update the key and parent values of the adjacent vertices
            for integer v from 0 to V - 1:
                // Update key if graph[u][v] is smaller than key[v] and v is not yet included in the MST
                if graph[u][v] != 0 and not mstSet[v] and graph[u][v] < key[v]:
                    parent[v][u] = graph[u][v] // Update parent to reflect the new edge in the MST
                    key[v] = graph[u][v] // Update the key to reflect the new minimum edge weight

        // Calculate the total weight of the MST
        integer mst_weight = 0
        for integer i from 1 to V - 1:
            mst_weight += parent[i][i] // Sum the weights of the MST edges

        return mst_weight // Return the total weight of the MST

    /**
     * Finds the vertex with the minimum key value from the set of vertices not yet included in the MST.
     * 
     * @param key Array of key values
     * @param mstSet Boolean array representing whether vertices are included in the MST
     * @return Index of the vertex with the minimum key value
     */
    private function minKey(integer[] key, boolean[] mstSet) -> integer:
        integer min = infinity // Initialize minimum key value
        integer min_index = -1 // Initialize index of the minimum key value

        for integer v from 0 to length of key - 1:
            // Update min_index if the vertex is not in mstSet and has a smaller key value
            if not mstSet[v] and key[v] < min:
                min = key[v]
                min_index = v

        return min_index // Return the index of the vertex with the minimum key value
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

**Code for Brute Force Solution**:

```
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

**Code for Greedy Algorithm**:

```
class TSPGreedy:
    private integer[][] graph
    private integer V

    // Constructor to initialize the graph and the number of vertices
    public function TSPGreedy(integer[][] graph):
        this.graph = graph
        this.V = length of graph // Number of vertices in the graph

    // Function to find the shortest path using a greedy approach
    public function findShortestPath() -> List<Integer>:
        boolean[] visited = new boolean[V] // To track visited vertices
        List<Integer> tour = new ArrayList<>()
        integer currentVertex = 0 // Start from vertex 0

        tour.add(currentVertex) // Add starting vertex to the tour
        visited[currentVertex] = true // Mark the starting vertex as visited

        for integer i from 1 to V - 1: // Loop through remaining vertices
            integer nearestVertex = findNearestVertex(currentVertex, visited) // Find the nearest unvisited vertex
            tour.add(nearestVertex) // Add nearest vertex to the tour
            visited[nearestVertex] = true // Mark it as visited
            currentVertex = nearestVertex // Move to the nearest vertex

        tour.add(0) // Return to the start node
        return tour // Return the complete tour

    // Function to find the nearest unvisited vertex from the current vertex
    private function findNearestVertex(integer currentVertex, boolean[] visited) -> integer:
        integer minDistance = infinity // Initialize minimum distance to infinity
        integer nearestVertex = -1 // Initialize nearest vertex

        for integer i from 0 to V - 1: // Iterate through all vertices
            if !visited[i] and graph[currentVertex][i] < minDistance: // Check if the vertex is unvisited and has a smaller distance
                minDistance = graph[currentVertex][i] // Update minimum distance
                nearestVertex = i // Update nearest vertex

        return nearestVertex // Return the nearest unvisited vertex

    // Main function to execute the program
    public static function main(String[] args):
        integer[][] graph = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        }
        TSPGreedy tsp = new TSPGreedy(graph) // Create instance of TSPGreedy
        List<Integer> tour = tsp.findShortestPath() // Find the shortest tour
        print("Tour: ", tour) // Print the tour
        integer tourCost = calculateTourCost(graph, tour) // Calculate the cost of the tour
        print("Tour Cost: ", tourCost) // Print the tour cost

    // Function to calculate the total cost of the tour
    private static function calculateTourCost(integer[][] graph, List<Integer> tour) -> integer:
        integer cost = 0
        for integer i from 0 to length of tour - 2: // Loop through the tour
            cost += graph[tour.get(i)][tour.get(i + 1)] // Add the edge weights to the total cost
        return cost // Return the total tour cost
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

**Code Example:**

The following Java code implements the Greedy Approximation Algorithm for TSP. This code assumes that the distance between cities is represented as a 2D array where `graph[i][j]` denotes the distance from city `i` to city `j`.

```
class TSPGreedy:
    /**
     * Computes a tour using the Greedy Approximation Algorithm for the Traveling Salesman Problem (TSP).
     * 
     * @param graph 2D array representing the distance between each pair of cities
     * @return List of integers representing the tour, starting from city 0
     */
    public function tspGreedy(integer[][] graph) -> List<Integer>:
        integer V = length of graph // Number of cities
        boolean[] visited = new boolean[V] // Array to keep track of visited cities
        List<Integer> tour = new ArrayList<> // List to store the tour
        integer currVertex = 0 // Start the tour from the first city
        tour.add(currVertex) // Add the starting city to the tour
        visited[currVertex] = true // Mark the starting city as visited

        // Iterate through the remaining cities
        for integer i from 1 to V - 1:
            integer nextVertex = -1 // Index of the next city to visit
            integer minDist = infinity // Minimum distance initialized to infinity
            
            // Find the nearest unvisited city
            for integer j from 0 to V - 1:
                // Check if the city is unvisited and if the distance is smaller than the current minimum distance
                if !visited[j] and graph[currVertex][j] < minDist:
                    minDist = graph[currVertex][j] // Update the minimum distance
                    nextVertex = j // Update the next city to visit
            
            // Add the nearest city to the tour
            tour.add(nextVertex) // Add the nearest city to the tour
            visited[nextVertex] = true // Mark the city as visited
            currVertex = nextVertex // Move to the next city

        // Return the tour as a list of city indices
        return tour // Return the completed tour

    public static function main(String[] args):
        // Example graph: 4 cities with distances between them
        integer[][] graph = {
            {0, 10, 15, 20},
            {10, 0, 35, 25},
            {15, 35, 0, 30},
            {20, 25, 30, 0}
        }

        TSPGreedy tsp = new TSPGreedy() // Create an instance of TSPGreedy
        List<Integer> tour = tsp.tspGreedy(graph) // Compute the TSP tour
        
        print("Greedy TSP Tour: ", tour) // Output the tour
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

**Code Example: Monte Carlo Method for Estimating Pi**

The following Java code demonstrates how to use a Monte Carlo algorithm to estimate the value of π (Pi) by randomly sampling points in a unit square and checking if they fall inside a unit circle.

```
class MonteCarloPi:
    // Method to estimate the value of Pi using the Monte Carlo method
    public function estimatePi(integer numSamples) -> double:
        integer insideCircle = 0 // Counter for points inside the unit circle
        Random rand = new Random() // Random number generator

        // Generate numSamples random points
        for integer i from 0 to numSamples - 1:
            double x = rand.nextDouble() // Generate a random x-coordinate in [0, 1)
            double y = rand.nextDouble() // Generate a random y-coordinate in [0, 1)
            
            // Check if the point is inside the unit circle (x^2 + y^2 <= 1)
            if (x * x + y * y <= 1):
                insideCircle = insideCircle + 1 // Increment counter for inside points

        // Estimate Pi using the ratio of points inside the circle to total points
        return 4.0 * insideCircle / numSamples // Return the estimated value of Pi

    public static function main(String[] args):
        MonteCarloPi mcPi = new MonteCarloPi() // Create an instance of MonteCarloPi
        integer numSamples = 1000000 // Number of samples to generate
        double piEstimate = mcPi.estimatePi(numSamples) // Estimate Pi using the Monte Carlo method
        
        print("Estimated value of Pi: ", piEstimate) // Output the estimated value of Pi
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

**Code Example:**

While Las Vegas algorithms are often more complex and context-specific, a classic example is the **Randomized QuickSort** algorithm. Here’s a simplified version demonstrating a randomized approach to sorting:

```
class RandomizedQuickSort:
    // Static variable for random number generation
    private static Random rand = new Random()

    // Method to perform Randomized QuickSort
    public function sort(array arr, integer low, integer high):
        if low < high:
            // Partition the array and get the pivot index
            integer pivotIndex = partition(arr, low, high)
            // Recursively sort the left and right subarrays
            sort(arr, low, pivotIndex - 1)
            sort(arr, pivotIndex + 1, high)

    // Method to partition the array around a random pivot
    private function partition(array arr, integer low, integer high) -> integer:
        // Choose a random pivot index between low and high
        integer pivotIndex = low + rand.nextInt(high - low + 1)
        integer pivot = arr[pivotIndex] // Get the pivot value
        swap(arr, pivotIndex, high) // Move pivot to the end
        integer i = low // Initialize the index for smaller elements

        // Rearrange the array based on the pivot value
        for integer j from low to high - 1:
            if arr[j] < pivot:
                swap(arr, i, j) // Swap smaller element to the front
                i = i + 1 // Move the boundary of smaller elements

        // Move the pivot to its correct position
        swap(arr, i, high)
        return i // Return the index of the pivot

    // Method to swap elements in the array
    private function swap(array arr, integer i, integer j):
        integer temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp

    // Main method to test the Randomized QuickSort
    public static function main(String[] args):
        // Initialize an array to sort
        array arr = [10, 7, 8, 9, 1, 5]
        RandomizedQuickSort sorter = new RandomizedQuickSort() // Create an instance of RandomizedQuickSort
        sorter.sort(arr, 0, arr.length - 1) // Sort the array
        
        print("Sorted array: ") // Print the sorted array
        for integer num in arr:
            print(num + " ") // Output each sorted element
```

**Explanation**:

- **Random Pivot Selection**: The algorithm selects a random pivot index for partitioning the array.
- **Correctness**: The algorithm always produces a correctly sorted array, but the time taken can vary depending on the pivot choices.

Both Monte Carlo and Las Vegas algorithms leverage randomness to achieve their goals, but they do so in different ways: Monte Carlo algorithms provide probabilistic results, while Las Vegas algorithms ensure correctness but with varying runtimes.
