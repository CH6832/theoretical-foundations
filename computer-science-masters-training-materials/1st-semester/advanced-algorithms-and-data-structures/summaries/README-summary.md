### Advanced Algorithms and Data Structures**

This course delves deep into the design, analysis, and implementation of advanced algorithms and data structures. Students will learn how to approach computational problems both theoretically and practically, with an emphasis on real-world applications. Below is a structured learning path, inspired by MIT’s standards, for each of the key topics listed.

### **1. Divide and Conquer Algorithms**

#### **Overview**:
- Divide and conquer is a fundamental technique that splits problems into smaller subproblems, solves them recursively, and combines their solutions.

#### **Key Concepts**:
- Recurrence relations (e.g., solving with Master Theorem)

```plaintext
function solveRecurrence(T(n)):
    if n <= base_case_threshold:
        return base_case_solution
    else:
        a = number_of_subproblems
        b = size_of_subproblems
        f(n) = cost of non-recursive work
        if f(n) is polynomially smaller than n^(log_b(a)):
            return n^(log_b(a))
        else if f(n) is polynomially equal to n^(log_b(a)):
            return n^(log_b(a)) * log(n)
        else if f(n) is polynomially larger than n^(log_b(a)):
            return f(n)
```

- Binary Search, Merge Sort, Quick Sort

```plaintext
function binarySearch(array, target):
    low = 0
    high = length(array) - 1

    while low <= high:
        mid = (low + high) // 2
        if array[mid] == target:
            return mid  // Target found
        else if array[mid] < target:
            low = mid + 1  // Search in the right half
        else:
            high = mid - 1  // Search in the left half

    return -1  // Target not found
```

```plaintext
function mergeSort(array):
    if length(array) <= 1:
        return array  // Base case: array is already sorted

    mid = length(array) // 2
    left = mergeSort(array[0:mid])
    right = mergeSort(array[mid:length(array)])

    return merge(left, right)

function merge(left, right):
    result = []
    i = 0
    j = 0

    while i < length(left) and j < length(right):
        if left[i] <= right[j]:
            append left[i] to result
            i = i + 1
        else:
            append right[j] to result
            j = j + 1

    append remaining elements of left (if any) to result
    append remaining elements of right (if any) to result
    return result

```

```plaintext
function quickSort(array):
    if length(array) <= 1:
        return array  // Base case: array is already sorted

    pivot = array[length(array) // 2]
    left = []
    middle = []
    right = []

    for element in array:
        if element < pivot:
            append element to left
        else if element == pivot:
            append element to middle
        else:
            append element to right

    return quickSort(left) + middle + quickSort(right)
```

- Fast Fourier Transform (FFT) and its applications

```plaintext
function FFT(x):
    N = length(x)
    if N <= 1:
        return x  // Base case

    even = FFT(x[0:2:N])  // Even indexed elements
    odd = FFT(x[1:2:N])   // Odd indexed elements

    T = [e * exp(-2 * π * i * k / N) for k, e in enumerate(odd)]
    return [even[k] + T[k] for k in range(N // 2)] + [even[k] - T[k] for k in range(N // 2)]
```

- Karatsuba’s algorithm for fast integer multiplication

```plaintext
function karatsuba(x, y):
    if x < 10 or y < 10:  // Base case for small numbers
        return x * y

    n = max(length(x), length(y))
    half_n = n // 2

    a = x // 10^half_n
    b = x % 10^half_n
    c = y // 10^half_n
    d = y % 10^half_n

    ac = karatsuba(a, c)  // High part multiplication
    bd = karatsuba(b, d)  // Low part multiplication
    ad_plus_bc = karatsuba(a + b, c + d) - ac - bd  // Cross terms

    return ac * 10^(2 * half_n) + ad_plus_bc * 10^half_n + bd
```

#### **Reading**:
- **Textbook**: *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein (Chapter on Divide and Conquer)
- **Research Papers**: "A Fast Divide-and-Conquer Algorithm for Matrix Multiplication" by Strassen (1969)

---

### **2. Graph Algorithms and Dynamic Graph Data Structures**

#### **Overview**:
- Graph algorithms are central to numerous real-world problems in networking, navigation, and computational biology. Dynamic graph structures allow efficient updates (insertions, deletions) in graph data over time.

#### **Key Concepts**:
- Shortest paths (Dijkstra, Bellman-Ford, Floyd-Warshall)
- Minimum spanning trees (Kruskal’s, Prim’s algorithms)
- Dynamic connectivity algorithms (link/cut trees, dynamic MST)
- Network flow algorithms (Ford-Fulkerson, Edmonds-Karp)

#### **Reading**:
- **Textbook**: *Algorithms* by Dasgupta, Papadimitriou, and Vazirani (Chapter 3 - Graph Algorithms)
- **Research Papers**: "Dynamic Trees" by Sleator and Tarjan (1981)

#### **Exercises**:
1. Implement Dijkstra’s and Bellman-Ford algorithms, and compare their performance.
2. Build a dynamic connectivity structure for a graph and analyze its time complexity.

---

### **3. Cache-Efficient Algorithms**

#### **Overview**:
- In modern computing, memory hierarchies (cache, RAM, disk) influence algorithmic performance. Cache-efficient algorithms aim to minimize data movement between levels of the memory hierarchy.

#### **Key Concepts**:
- Memory hierarchies and cache complexity

```plaintext
function cacheObliviousMatrixMultiply(A, B, C, n):
    if n == 1:  // Base case: 1x1 matrix multiplication
        C[0][0] = A[0][0] * B[0][0]
        return

    // Divide matrices into quadrants
    half_n = n // 2

    // Recursive calls for matrix multiplication
    cacheObliviousMatrixMultiply(A[0:half_n][0:half_n], B[0:half_n][0:half_n], C[0:half_n][0:half_n], half_n)
    cacheObliviousMatrixMultiply(A[0:half_n][half_n:n], B[half_n:n][0:half_n], C[0:half_n][half_n:n], half_n)
    cacheObliviousMatrixMultiply(A[half_n:n][0:half_n], B[0:half_n][0:half_n], C[half_n:n][0:half_n], half_n)
    cacheObliviousMatrixMultiply(A[half_n:n][half_n:n], B[half_n:n][0:half_n], C[half_n:n][half_n:n], half_n)

    // Combine results
    // Assuming C is divided into quadrants
    C[0:half_n][0:half_n] += C[0:half_n][0:half_n]
    C[0:half_n][half_n:n] += C[0:half_n][half_n:n]
    C[half_n:n][0:half_n] += C[half_n:n][0:half_n]
    C[half_n:n][half_n:n] += C[half_n:n][half_n:n]
```

- Cache-oblivious algorithms (matrix multiplication, sorting)

```plaintext
function cacheObliviousMatrixMultiply(A, B, C, n):
    if n == 1:  // Base case: 1x1 matrix multiplication
        C[0][0] = A[0][0] * B[0][0]
        return

    // Divide matrices into quadrants
    half_n = n // 2

    // Recursive calls for matrix multiplication
    cacheObliviousMatrixMultiply(A[0:half_n][0:half_n], B[0:half_n][0:half_n], C[0:half_n][0:half_n], half_n)
    cacheObliviousMatrixMultiply(A[0:half_n][half_n:n], B[half_n:n][0:half_n], C[0:half_n][half_n:n], half_n)
    cacheObliviousMatrixMultiply(A[half_n:n][0:half_n], B[0:half_n][0:half_n], C[half_n:n][0:half_n], half_n)
    cacheObliviousMatrixMultiply(A[half_n:n][half_n:n], B[half_n:n][0:half_n], C[half_n:n][half_n:n], half_n)

    // Combine results
    // Assuming C is divided into quadrants
    C[0:half_n][0:half_n] += C[0:half_n][0:half_n]
    C[0:half_n][half_n:n] += C[0:half_n][half_n:n]
    C[half_n:n][0:half_n] += C[half_n:n][0:half_n]
    C[half_n:n][half_n:n] += C[half_n:n][half_n:n]
```

- Recursive divide-and-conquer techniques for cache efficiency

```plaintext
function cacheObliviousMergeSort(array):
    n = length(array)
    if n <= 1:  // Base case
        return array

    mid = n // 2
    left = cacheObliviousMergeSort(array[0:mid])
    right = cacheObliviousMergeSort(array[mid:n])

    return cacheObliviousMerge(left, right)

function cacheObliviousMerge(left, right):
    result = []
    i = 0
    j = 0

    while i < length(left) and j < length(right):
        if left[i] <= right[j]:
            append left[i] to result
            i = i + 1
        else:
            append right[j] to result
            j = j + 1

    append remaining elements of left (if any) to result
    append remaining elements of right (if any) to result
    return result
```

- External memory models

```plaintext
function divideAndConquerMax(array, low, high):
    if low == high:  // Base case: single element
        return array[low]

    mid = (low + high) // 2
    leftMax = divideAndConquerMax(array, low, mid)
    rightMax = divideAndConquerMax(array, mid + 1, high)

    return max(leftMax, rightMax)
```

#### **Reading**:
- **Textbook**: *Introduction to Algorithms* by Cormen et al. (Chapter 15: Dynamic Programming)
- **Research Papers**: "Optimal Cache-Oblivious Algorithms" by Frigo et al. (1999)

#### **Exercises**:
1. Implement a cache-oblivious matrix multiplication algorithm.
2. Analyze cache performance of quicksort and merge sort algorithms.

---

### **4. Algorithmic Paradigms: Greedy, Dynamic Programming, Approximation Algorithms**

#### **Overview**:
- Greedy algorithms make local decisions with the hope of finding a global optimum.
- Dynamic programming solves problems by combining solutions to subproblems.
- Approximation algorithms provide near-optimal solutions in polynomial time for NP-hard problems.

#### **Key Concepts**:
- Greedy Algorithms: Activity selection, Huffman coding, Kruskal’s and Prim’s algorithms

```plaintext
function activitySelection(activities):
    sort activities by finish time
    selectedActivities = []
    lastFinishTime = 0

    for activity in activities:
        if activity.start >= lastFinishTime:
            append activity to selectedActivities
            lastFinishTime = activity.finish

    return selectedActivities
```

```plaintext
function huffmanCoding(characters, frequencies):
    priorityQueue = createPriorityQueue()

    // Create a leaf node for each character and add it to the priority queue
    for each character, frequency in frequencies:
        enqueue priorityQueue with newNode(character, frequency)

    while size(priorityQueue) > 1:
        left = dequeue(priorityQueue)
        right = dequeue(priorityQueue)
        newNode = createNode(left.frequency + right.frequency)
        newNode.left = left
        newNode.right = right
        enqueue priorityQueue with newNode

    return buildCode(priorityQueue.peek())
```

```plaintext
function kruskal(graph):
    edges = sort(graph.edges by weight)
    disjointSet = createDisjointSet(graph.vertices)
    mst = []

    for edge in edges:
        if disjointSet.find(edge.start) != disjointSet.find(edge.end):
            disjointSet.union(edge.start, edge.end)
            append edge to mst

    return mst
```

```plaintext

```

- Dynamic Programming: Knapsack, Longest common subsequence, Edit distance

```plaintext
function knapsack(weights, values, capacity):
    n = length(weights)
    dp = array of size (n+1) x (capacity+1)

    for i from 0 to n:
        for w from 0 to capacity:
            if i == 0 or w == 0:
                dp[i][w] = 0
            else if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], values[i-1] + dp[i-1][w - weights[i-1]])
            else:
                dp[i][w] = dp[i-1][w]

    return dp[n][capacity]
```

```plaintext
function lcs(X, Y):
    m = length(X)
    n = length(Y)
    dp = array of size (m+1) x (n+1)

    for i from 0 to m:
        for j from 0 to n:
            if i == 0 or j == 0:
                dp[i][j] = 0
            else if X[i-1] == Y[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

```plaintext
function lcs(X, Y):
    m = length(X)
    n = length(Y)
    dp = array of size (m+1) x (n+1)

    for i from 0 to m:
        for j from 0 to n:
            if i == 0 or j == 0:
                dp[i][j] = 0
            else if X[i-1] == Y[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

```plaintext
function editDistance(str1, str2):
    m = length(str1)
    n = length(str2)
    dp = array of size (m+1) x (n+1)

    for i from 0 to m:
        for j from 0 to n:
            if i == 0:
                dp[i][j] = j  // Insertions
            else if j == 0:
                dp[i][j] = i  // Deletions
            else if str1[i-1] == str2[j-1]:
                dp[i][j] = dp[i-1][j-1]  // No cost
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])  // Insert, Delete, Replace

    return dp[m][n]
```

- Approximation Algorithms: Vertex cover, Traveling Salesman Problem (TSP), Set cover

```plaintext
function vertexCover(graph):
    cover = []
    edges = graph.edges

    while edges is not empty:
        edge = pick an arbitrary edge from edges
        cover.append(edge.start)
        cover.append(edge.end)

        // Remove all edges covered by edge
        remove edges that are covered by edge

    return cover
```

```plaintext
function tspGreedy(graph):
    visited = set()
    tour = []
    currentCity = start city

    while size(visited) < number of cities:
        tour.append(currentCity)
        visited.add(currentCity)

        nextCity = find nearest unvisited city
        currentCity = nextCity

    tour.append(start city)  // Returning to starting city
    return tour
```

```plaintext
function setCover(universe, sets):
    cover = []
    coveredElements = set()

    while coveredElements is not equal to universe:
        bestSet = null
        maxNewElements = 0

        for each set in sets:
            newElements = set - coveredElements
            if size(newElements) > maxNewElements:
                maxNewElements = size(newElements)
                bestSet = set

        coveredElements.addAll(bestSet)
        cover.append(bestSet)
        remove bestSet from sets

    return cover
```

#### **Reading**:
- **Textbook**: *Algorithms* by Dasgupta et al. (Chapter 6: Dynamic Programming, Chapter 8: Greedy Algorithms)
- **Research Papers**: "A Constant-Factor Approximation Algorithm for the k-MST Problem" (Arora & Karloff)

#### **Exercises**:
1. Implement the knapsack problem using both dynamic programming and a greedy approach. Compare the results.
2. Analyze the performance of the 2-approximation algorithm for vertex cover.

---

### **5. Online and Streaming Algorithms**

#### **Overview**:
- Online algorithms make decisions without knowledge of future inputs, often with the goal of minimizing regret.
- Streaming algorithms process massive data streams using limited memory and typically focus on estimating properties of the data.

#### **Key Concepts**:

- Competitive analysis and performance ratios

```plaintext
function competitiveRatio(lruCache, accessSequence):
    optimalCost = calculateOptimalCost(accessSequence)  // Cost of optimal offline solution
    lruCost = calculateLRUCost(lruCache, accessSequence)  // Cost incurred by LRU
    return lruCost / optimalCost  // Competitive ratio
```

- Online problems: caching, online bipartite matching

```plaintext
function competitiveRatio(lruCache, accessSequence):
    optimalCost = calculateOptimalCost(accessSequence)  // Cost of optimal offline solution
    lruCost = calculateLRUCost(lruCache, accessSequence)  // Cost incurred by LRU
    return lruCost / optimalCost  // Competitive ratio
```

- Streaming algorithms: count-min sketch, frequency moments, heavy hitters

```plaintext
function findHeavyHitters(stream, threshold):
    sketch = CountMinSketch(width, depth)
    
    for item in stream:
        sketch.update(item)

    heavyHitters = []
    for item in uniqueItems(stream):
        if sketch.estimate(item) > threshold:
            append item to heavyHitters

    return heavyHitters
```

```plaintext
class CountMinSketch:
    function __init__(width, depth):
        this.width = width  // Number of columns
        this.depth = depth  // Number of hash functions
        this.table = array of size (depth x width) initialized to 0
        this.hashFunctions = generateHashFunctions(depth)

    function update(item):
        for i from 0 to depth:
            index = hashFunctions[i](item) % width
            this.table[i][index] += 1

    function estimate(item):
        minCount = infinity
        for i from 0 to depth:
            index = hashFunctions[i](item) % width
            minCount = min(minCount, this.table[i][index])
        return minCount
```

#### **Reading**:
- **Textbook**: *Approximation Algorithms* by Vijay Vazirani (Chapters on Online Algorithms)
- **Research Papers**: "A Competitive Analysis of Online Algorithms" by Sleator and Tarjan (1985)

#### **Exercises**:
1. Implement the Least Recently Used (LRU) caching algorithm and analyze its competitive ratio.
2. Build a count-min sketch to estimate frequency moments of a stream.

---

### **6. Parallel and Distributed Algorithms**

#### **Overview**:
- Parallel algorithms run on multiple processors simultaneously, while distributed algorithms operate on data distributed across different nodes or locations.
- These algorithms are key to optimizing large-scale computational problems in modern multi-core and cloud computing environments.

#### **Key Concepts**:
- Parallel computation models: PRAM, MapReduce

```plaintext
ParallelQuicksort(array, low, high)
    if low < high then
        pivotIndex = Partition(array, low, high)
        
        # Parallel region starts here
        # Fork two threads to sort the left and right subarrays
        # Each thread runs the ParallelQuicksort on different parts of the array
        # Note: OpenMP pragma for parallel execution
        # pragma omp parallel
        {
            # pragma omp task
            ParallelQuicksort(array, low, pivotIndex - 1)
            
            # pragma omp task
            ParallelQuicksort(array, pivotIndex + 1, high)
        }
        # Wait for all tasks to finish
        # pragma omp taskwait
    end if

Partition(array, low, high)
    pivot = array[high]
    i = low - 1
    for j from low to high - 1 do
        if array[j] < pivot then
            i = i + 1
            Swap(array[i], array[j])
    end for
    Swap(array[i + 1], array[high])
    return i + 1
```

- Parallel sorting and searching
- Distributed consensus algorithms: Paxos, Raft

```plaintext
RaftAlgorithm()
    InitializeServer()
    while true do
        if I am the leader then
            SendHeartbeat()
            ReceiveClientRequests()
            AppendEntriesToLog()
        else
            WaitForLeader()
        end if
        
        if electionTimeout() then
            StartElection()
        end if
    end while

StartElection()
    IncrementCurrentTerm()
    VoteCount = 1  # Vote for self
    for each server in cluster do
        if RequestVote(server, CurrentTerm, MyLog) then
            VoteCount += 1
        end if
    end for
    if VoteCount > majority then
        BecomeLeader()
    end if

RequestVote(server, term, log)
    if term < CurrentTerm then
        return false
    if log is at least as up-to-date as MyLog then
        GrantVote()
        return true
    return false

SendHeartbeat()
    for each server in cluster do
        SendAppendEntries(server, CurrentTerm, MyLog)

AppendEntriesToLog()
    for each client request do
        Append request to log
        Commit log entry
        Send response to client
    end for
```

- Load balancing and parallel graph algorithms

```plaintext
LoadBalancingAlgorithm(tasks, servers)
    while tasks are not empty do
        for each server in servers do
            if server is underloaded then
                task = GetNextTask(tasks)
                Assign(task, server)
                if task is null then
                    break
                end if
            end if
        end for
    end while

GetNextTask(tasks)
    if tasks is not empty then
        return tasks.pop()  # Get and remove the next task
    return null

Assign(task, server)
    server.addTask(task)  # Add task to the server's workload
```

```plaintext
ParallelBFS(graph, startNode)
    Initialize a queue Q
    Mark startNode as visited
    Q.enqueue(startNode)

    while Q is not empty do
        # Parallel region for processing nodes in the queue
        # pragma omp parallel
        {
            node = Q.dequeue()  # Thread-safe dequeue
            for each neighbor in graph[node] do
                if neighbor is not visited then
                    Mark neighbor as visited
                    Q.enqueue(neighbor)
                end if
            end for
        }
    end while
```

#### **Reading**:
- **Textbook**: *Introduction to Parallel Algorithms* by Joseph JaJa (Chapters on Parallel Search and Sort)
- **Research Papers**: "Time-Work Tradeoffs for Parallel Algorithms" by Blelloch (1996)

#### **Exercises**:
1. Implement parallel quicksort using OpenMP and compare its performance to the sequential version.
2. Build a distributed consensus mechanism based on the Raft algorithm.

---

### **Modern Resources**

#### **Primary Textbook**:
- **Algorithms** by S. Dasgupta, C.H. Papadimitriou, U.V. Vazirani
  - This book takes a modern approach to algorithm design, emphasizing theoretical understanding and practical applications. It covers the basics of each algorithmic paradigm as well as advanced topics.

#### **MIT OpenCourseWare Courses**:
1. **6.851: Advanced Data Structures** (OCW)
   - [Link to OCW Course](https://ocw.mit.edu/courses/6-851-advanced-data-structures-spring-2012/)

2. **6.046J: Design and Analysis of Algorithms** (OCW)
   - [Link to OCW Course](https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2015/)

#### **Research Papers**:
- "Fast Matrix Multiplication" by Virginia Vassilevska Williams (2012)
  - Key breakthrough in improving the time complexity of matrix multiplication.
- "Optimal Cache-Oblivious Algorithms" by Frigo, Leiserson, Prokop, and Ramachandran (1999)
  - Introduces the cache-oblivious model and develops algorithms that optimize cache usage without knowledge of cache parameters.
