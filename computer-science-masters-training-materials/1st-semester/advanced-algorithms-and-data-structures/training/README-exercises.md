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

### 1. **Divide-and-Conquer Algorithms**

#### **(Theoretical) Quicksort Time Complexity**
1. **Best Case**: \(O(n \log n)\) - This occurs when the pivot divides the array into two equal halves.
2. **Worst Case**: \(O(n^2)\) - This occurs when the pivot is the smallest or largest element, leading to unbalanced partitions.
3. **Average Case**: \(O(n \log n)\) - With random pivot selection, the expected partition sizes are balanced on average.

**Randomized Quicksort**: It selects a pivot randomly, reducing the probability of encountering the worst-case scenario. This improves the average case by increasing the likelihood of balanced partitions, leading to more efficient sorting.

---

#### **(Implementation) Majority Element in Array**
```plaintext
function findMajorityElement(array):
    def majorityUtil(array, left, right):
        if left == right:
            return array[left]
        
        mid = (left + right) // 2
        leftMajority = majorityUtil(array, left, mid)
        rightMajority = majorityUtil(array, mid + 1, right)
        
        leftCount = countInRange(array, leftMajority, left, right)
        rightCount = countInRange(array, rightMajority, left, right)

        if leftCount > (right - left + 1) // 2:
            return leftMajority
        if rightCount > (right - left + 1) // 2:
            return rightMajority
        return None  // No majority element

    return majorityUtil(array, 0, length(array) - 1)

function countInRange(array, element, left, right):
    count = 0
    for i from left to right:
        if array[i] == element:
            count += 1
    return count
```

---

#### **(Theoretical) Matrix Exponentiation Recurrence Relation**
1. **Recurrence Relation**: 
   \[
   T(n) = T(n/2) + O(1)
   \]
   - This indicates that to compute \(A^n\), we recursively compute \(A^{n/2}\) and multiply.

2. **Time Complexity**: By the Master Theorem, this solves to \(O(\log n)\).

---

#### **(Implementation) Count Inversions in an Array**
```plaintext
function countInversions(array):
    if length(array) < 2:
        return 0
    
    mid = length(array) // 2
    left = array[0:mid]
    right = array[mid:length(array)]
    
    inversions = countInversions(left) + countInversions(right)

    i = j = k = 0
    while i < length(left) and j < length(right):
        if left[i] <= right[j]:
            array[k] = left[i]
            i += 1
        else:
            array[k] = right[j]
            inversions += (length(left) - i)  // Count inversions
            j += 1
        k += 1

    while i < length(left):
        array[k] = left[i]
        i += 1
        k += 1
    
    while j < length(right):
        array[k] = right[j]
        j += 1
        k += 1

    return inversions
```

---

#### **(Theoretical) Master Theorem Analysis**
1. **Recurrence**: \( T(n) = 3T(n/3) + O(n) \)
2. **Application**:
   - Here, \(a = 3\), \(b = 3\), and \(f(n) = O(n)\).
   - Using the Master Theorem, since \(f(n)\) grows polynomially slower than \(n^{\log_b a} = n^{\log_3 3} = n\), we can apply case 1:
   \[
   T(n) = \Theta(n^{\log_3 3}) = \Theta(n \log n)
   \]

---

#### **(Implementation) Median of Two Sorted Arrays**
```plaintext
function findMedianSortedArrays(nums1, nums2):
    if length(nums1) > length(nums2):
        nums1, nums2 = nums2, nums1
    
    x = length(nums1)
    y = length(nums2)
    low = 0
    high = x

    while low <= high:
        partitionX = (low + high) // 2
        partitionY = (x + y + 1) // 2 - partitionX

        maxX = (partitionX == 0) ? -∞ : nums1[partitionX - 1]
        minX = (partitionX == x) ? +∞ : nums1[partitionX]
        maxY = (partitionY == 0) ? -∞ : nums2[partitionY - 1]
        minY = (partitionY == y) ? +∞ : nums2[partitionY]

        if maxX <= minY and maxY <= minX:
            if (x + y) % 2 == 0:
                return (max(maxX, maxY) + min(minX, minY)) / 2
            else:
                return max(maxX, maxY)
        elif maxX > minY:
            high = partitionX - 1
        else:
            low = partitionX + 1
```

---

#### **(Theoretical) Binary Search Proof of Correctness**
1. **Correctness**: The algorithm continuously halves the search space.
2. **Time Complexity**: The time complexity is \(O(\log n)\) since each iteration reduces the search space by half.

---

#### **(Implementation) 0/1 Knapsack Problem**
```plaintext
function knapsack(values, weights, capacity):
    n = length(values)
    dp = array[0..n][0..capacity]

    for i from 0 to n:
        for w from 0 to capacity:
            if i == 0 or w == 0:
                dp[i][w] = 0
            elif weights[i - 1] <= w:
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])
            else:
                dp[i][w] = dp[i - 1][w]
    
    return dp[n][capacity]
```

---

#### **(Theoretical) Maximum Subarray Problem with Divide-and-Conquer**
- **Approach**: Divide the array into two halves and recursively find the maximum subarray in the left half, right half, and across the midpoint. 
- **Correctness**: This captures all possible maximum subarrays.
- **Time Complexity**: The time complexity is \(O(n \log n)\).

---

#### **(Implementation) Sort a Linked List**
```plaintext
function mergeSort(head):
    if head == null or head.next == null:
        return head

    middle = getMiddle(head)
    nextToMiddle = middle.next
    middle.next = null

    left = mergeSort(head)
    right = mergeSort(nextToMiddle)

    return sortedMerge(left, right)

function sortedMerge(left, right):
    if left == null:
        return right
    if right == null:
        return left

    if left.data <= right.data:
        left.next = sortedMerge(left.next, right)
        return left
    else:
        right.next = sortedMerge(left, right.next)
        return right

function getMiddle(head):
    if head == null:
        return head
    slow = head
    fast = head.next

    while fast != null and fast.next != null:
        slow = slow.next
        fast = fast.next.next

    return slow
```

---

#### **(Theoretical) Convex Hull Optimality Proof**
- **Optimality**: The divide-and-conquer method (like Graham's scan) has a time complexity of \(O(n \log n)\) and is optimal for convex hull problems because it efficiently manages the sorting and merging of points.
  
---

#### **(Implementation) Power Calculation**
```plaintext
function power(x, n):
    if n == 0:
        return 1
    half = power(x, n // 2)
    if n % 2 == 0:
        return half * half
    else:
        return x * half * half
```

---

#### **(Theoretical) Differential Equations and Divide-and-Conquer**
- **Application**: Divide-and-conquer can be used to solve differential equations through methods such as the finite difference method. The problem is divided into smaller segments, solved independently, and then combined to form a solution.

---

#### **(Implementation) Game of Life Simulation**
```plaintext
function gameOfLife(board):
    rows = length(board)
    cols = length(board[0])

    directions = [(1, 0), (-1, 0), (0, 1), (0, -1), (1, 1), (-1, -1), (1, -1), (-1, 1)]

    function countLiveNeighbors(r, c):
        count = 0
        for direction in directions:
            nr = r + direction[0]
            nc = c + direction[1]
            if 0 <= nr < rows and 0 <= nc < cols and abs(board[nr][nc]) == 1:
                count += 1
        return count

    for r

 from 0 to rows - 1:
        for c from 0 to cols - 1:
            liveNeighbors = countLiveNeighbors(r, c)
            if board[r][c] == 1 and (liveNeighbors < 2 or liveNeighbors > 3):
                board[r][c] = -1  // Mark for death
            if board[r][c] == 0 and liveNeighbors == 3:
                board[r][c] = 2  // Mark for birth

    for r from 0 to rows - 1:
        for c from 0 to cols - 1:
            if board[r][c] > 0:
                board[r][c] = 1
            else:
                board[r][c] = 0
```

---

#### **(Theoretical) Space Complexity in Divide-and-Conquer**
- **Analysis**: Generally, the space complexity can be linear in terms of input size for algorithms that utilize auxiliary space for merging or storing results (e.g., merge sort). Techniques like in-place algorithms can be employed to minimize space.

---

### 2. **Graph Algorithms and Dynamic Graph Data Structures**

#### **(Implementation) Dijkstra’s Algorithm**
```plaintext
function dijkstra(graph, source):
    dist = array filled with infinity
    dist[source] = 0
    priorityQueue = empty min-heap
    add (0, source) to priorityQueue

    while priorityQueue is not empty:
        currentDist, currentNode = extract-min from priorityQueue
        
        for each neighbor in graph[currentNode]:
            distance = currentDist + edgeWeight(currentNode, neighbor)
            if distance < dist[neighbor]:
                dist[neighbor] = distance
                add (distance, neighbor) to priorityQueue
                
    return dist
```

#### **(Theoretical) Kruskal’s Algorithm**
- **Proof of Minimum Spanning Tree (MST)**: By considering the cut property and using a disjoint-set data structure, we can prove that adding the minimum weight edge that does not form a cycle leads to an MST.
- **Time Complexity**: \(O(E \log E)\) where \(E\) is the number of edges.

---

#### **(Implementation) Dynamic Connectivity Data Structure**
```plaintext
class LinkCutTree:
    // Define necessary methods for link, cut, find root, and connected checks

function dynamicConnectivity(operations):
    for operation in operations:
        if operation is a link:
            linkCutTree.link(nodeA, nodeB)
        elif operation is a cut:
            linkCutTree.cut(nodeA, nodeB)
        elif operation is a connected check:
            return linkCutTree.connected(nodeA, nodeB)
```

---

#### **(Implementation) Strongly Connected Components (SCCs)**
```plaintext
function tarjansSCC(graph):
    index = 0
    stack = []
    lowlinks = array filled with -1
    indices = array filled with -1
    onStack = array filled with false

    for v in graph:
        if indices[v] == -1:
            strongconnect(v)

    function strongconnect(v):
        nonlocal index
        indices[v] = index
        lowlinks[v] = index
        index += 1
        stack.push(v)
        onStack[v] = true

        for neighbor in graph[v]:
            if indices[neighbor] == -1:
                strongconnect(neighbor)
                lowlinks[v] = min(lowlinks[v], lowlinks[neighbor])
            elif onStack[neighbor]:
                lowlinks[v] = min(lowlinks[v], indices[neighbor])

        if lowlinks[v] == indices[v]:
            scc = []
            while true:
                w = stack.pop()
                onStack[w] = false
                scc.push(w)
                if w == v:
                    break
            return scc
```

---

#### **(Theoretical) Prim’s Algorithm**
- **Correctness**: It maintains a tree that grows by adding the lowest weight edge connected to the tree. A Fibonacci heap provides efficient minimum extractions.
- **Performance**: \(O(E + V \log V)\).

---

#### **(Theoretical) Ford-Fulkerson and Irrational Capacities**
- **Failure to Terminate**: In cases where edge capacities are irrational, the flow may not converge, potentially leading to infinite cycles.

---

#### **(Implementation) Edmonds-Karp Algorithm**
```plaintext
function edmondsKarp(graph, source, sink):
    maxFlow = 0
    while true:
        parent = array filled with -1
        queue = empty queue
        queue.enqueue(source)
        parent[source] = source

        while queue is not empty:
            currentNode = queue.dequeue()
            for neighbor in graph[currentNode]:
                if parent[neighbor] == -1 and capacity(currentNode, neighbor) > 0:
                    parent[neighbor] = currentNode
                    queue.enqueue(neighbor)
                    if neighbor == sink:
                        break

        if parent[sink] == -1:
            break  // No more augmenting paths

        pathFlow = infinity
        s = sink
        while s != source:
            pathFlow = min(pathFlow, capacity(parent[s], s))
            s = parent[s]

        maxFlow += pathFlow

        v = sink
        while v != source:
            u = parent[v]
            decreaseCapacity(u, v, pathFlow)
            increaseCapacity(v, u, pathFlow)
            v = parent[v]

    return maxFlow
```

---

#### **(Theoretical) Dijkstra’s Algorithm and Negative Weights**
- **Proof**: If a negative edge exists, Dijkstra's algorithm may select the incorrect path initially, leading to suboptimal distance calculations. A counter-example is a triangle with negative weight on one edge.

---

#### **(Implementation) Dynamic Shortest Path Updates**
```plaintext
class DynamicGraph:
    // Implement methods for adding and removing edges

function dynamicShortestPathUpdates(graph, edges):
    for edge in edges:
        if edge.action is add:
            graph.addEdge(edge.u, edge.v, edge.weight)
        elif edge.action is remove:
            graph.removeEdge(edge.u, edge.v)
```

---

#### **(Theoretical) Tarjan’s LCA Algorithm**
- **Correctness**: The algorithm effectively finds the LCA by employing depth-first search and tracking the paths.
- **Time Complexity**: \(O(n)\) for preprocessing.

---

#### **(Implementation) Articulation Points**
```plaintext
function findArticulationPoints(graph):
    index = 0
    lowlinks = array filled with -1
    indices = array filled with -1
    articulationPoints = set()

    function dfs(v, parent):
        nonlocal index
        indices[v] = lowlinks[v] = index
        index += 1
        children = 0
        
        for neighbor in graph[v]:
            if neighbor == parent:
                continue
            if indices[neighbor] == -1:
                children += 1
                dfs(neighbor, v)
                lowlinks[v] = min(lowlinks[v], lowlinks[neighbor])
                if parent != -1 and lowlinks[neighbor] >= indices[v]:
                    articulationPoints.add(v)
            else:
                lowlinks[v] = min(lowlinks[v], indices[neighbor])

        if parent == -1 and children > 1:
            articulationPoints.add(v)

    for v in graph:
        if indices[v] == -1:
            dfs(v, -1)

    return articulationPoints
```

---

#### **(Theoretical) Floyd-Warshall Algorithm Applications**
- **Applications**: Used for finding shortest paths between all pairs in dense graphs, particularly in transitive closure and detecting negative cycles.
- **Time Complexity**: \(O(V^3)\).

---

#### **(Implementation) A* Search Algorithm**
```plaintext
function aStar(graph, start, goal):
    openSet = empty priority queue
    openSet.push(start)
    cameFrom = empty map

    gScore = array filled with infinity
    gScore[start] = 0
    fScore = array filled with infinity
    fScore[start] = heuristic(start, goal)

    while openSet is not empty:
        current = openSet.extract-min()

        if current == goal:
            return reconstructPath(cameFrom, current)

        for neighbor in graph.neighbors(current):
            tentativeGScore = gScore[current] + distance(current, neighbor)
            if tentativeGScore < gScore[neighbor]:
                cameFrom[neighbor] = current
                gScore[neighbor] = tentativeGScore
                fScore[neighbor] = gScore[neighbor] + heuristic(neighbor, goal)
                if neighbor not in openSet:
                    openSet.push(neighbor)

    return empty  // Path not found

function reconstructPath(cameFrom, current):
    totalPath = []
    while current in cameFrom:
        totalPath.prepend(current)
        current = cameFrom[current]
    return totalPath
```

---

#### **(Theoretical) Johnson’s Algorithm for Shortest Paths**
- **Correctness**: Uses reweighting to handle negative weights, ensuring all paths are correctly calculated.
- **Time Complexity**: \(O(V^2 \log V + VE)\).

---

#### **(Implementation) Randomized Minimum Spanning Tree**
```plaintext
function randomizedMST(graph):
    edges = shuffle(graph.edges)  // Randomly shuffle edges
    mst = empty set
    unionFind = createUnionFind(graph.vertices)

    for edge in edges:
        if unionFind.find(edge.u) != unionFind.find(edge.v):
            mst.add(edge)
            unionFind.union(edge.u, edge.v)

    return mst
```

---

#### **(Theoretical) Cut Property in Graph Algorithms**


- **Proof**: The minimum cut that separates vertices in the graph must contain at least one edge from the minimum spanning tree, ensuring optimality.

---

#### **(Implementation) Cycle Detection with Union-Find**
```plaintext
function hasCycle(graph):
    unionFind = createUnionFind(graph.vertices)

    for edge in graph.edges:
        if unionFind.find(edge.u) == unionFind.find(edge.v):
            return true  // Cycle found
        unionFind.union(edge.u, edge.v)

    return false  // No cycle found
```

---

#### **(Theoretical) Bipartite Graph Checking**
- **Correctness**: Using BFS or DFS, the graph can be colored in two colors to check for bipartiteness.
- **Complexity**: \(O(V + E)\).

---

#### **(Implementation) Chinese Postman Problem**
```plaintext
function chinesePostman(graph):
    eulerianPath = findEulerianPath(graph)
    if eulerianPath exists:
        return eulerianPath
    else:
        // Handle odd degree vertices
        addEdgesToMakeEulerian(graph)
        return findEulerianPath(graph)

function findEulerianPath(graph):
    // Implementation of finding Eulerian Path
```

---

#### **(Theoretical) Limitations of Traditional Graph Algorithms**
- **Dynamic Graph Challenges**: Traditional algorithms often require a complete traversal of the graph, which can be inefficient for dynamic changes. Using data structures like link-cut trees can improve performance.

---

### 3. **Cache-Efficient Algorithms**

#### **(Implementation) Cache-Oblivious Matrix Multiplication**
```plaintext
function cacheObliviousMatrixMultiplication(A, B, C, n):
    if n <= 64:  // Base case for small matrices
        for i from 0 to n-1:
            for j from 0 to n-1:
                C[i][j] += A[i][k] * B[k][j]
    else:
        mid = n / 2
        cacheObliviousMatrixMultiplication(A[0:mid, 0:mid], B[0:mid, 0:mid], C[0:mid, 0:mid], mid)
        // Recursive calls for other quadrants...
```

#### **(Theoretical) Merge Sort Cache Efficiency**
- **Proof**: By organizing the merge step to fit within cache lines, we can reduce cache misses significantly compared to naive merge operations.

---

#### **(Theoretical) Cache-Oblivious Binary Search**
- **Working**: It effectively reduces the number of cache misses to \( O(\log_B n) \) by accessing data in a way that respects the underlying memory hierarchy.

---

#### **(Theoretical) Quicksort Cache Performance**
- **Analysis**: In general, quicksort performs better than merge sort in practice, but its cache performance can degrade with poor pivot choices leading to unbalanced partitions.

---

#### **(Implementation) Cache-Oblivious Matrix Transposition**
```plaintext
function cacheObliviousTranspose(matrix, result, n):
    if n <= 64:
        for i from 0 to n-1:
            for j from 0 to n-1:
                result[j][i] = matrix[i][j]
    else:
        mid = n / 2
        cacheObliviousTranspose(matrix[0:mid, 0:mid], result[0:mid, 0:mid], mid)
        // Transpose other quadrants...
```

---

#### **(Theoretical) Cache-Oblivious Quicksort**
- **Modification**: By partitioning arrays in a way that respects cache lines, we can optimize data access patterns leading to improved cache performance.

---

#### **(Theoretical) Optimal Cache Complexity for Matrix Multiplication**
- **Proof**: It can be shown that the access pattern of any cache-oblivious algorithm fits within the bounds of \( O(n^3 / B + n^2) \).

---

#### **(Implementation) Cache-Oblivious Priority Queue**
```plaintext
class CacheObliviousPriorityQueue:
    // Define methods for insert, extract-min, and maintain heap property

function priorityQueueExample():
    pq = CacheObliviousPriorityQueue()
    for element in data:
        pq.insert(element)
    while not pq.isEmpty():
        print(pq.extractMin())
```

---

#### **(Theoretical) Cache-Oblivious Median Finding**
- **Optimality**: Cache-oblivious algorithms can find the median in \( O(n) \) cache accesses, ensuring efficient data locality.

---

#### **(Implementation) Cache-Oblivious Sorting Algorithm**
```plaintext
function cacheObliviousSort(array, n):
    if n <= 1:
        return array
    mid = n / 2
    left = cacheObliviousSort(array[0:mid], mid)
    right = cacheObliviousSort(array[mid:n], n - mid)
    return merge(left, right)

function merge(left, right):
    // Merging logic ensuring cache efficiency
```

---

#### **(Theoretical) Principles of Cache-Efficient Algorithms**
- **Differences**: Cache-efficient algorithms prioritize minimizing cache misses through optimal data access patterns, contrasting traditional algorithms that may not consider memory hierarchy.

---

#### **(Implementation) Cache-Oblivious Binary Tree Traversal**
```plaintext
function cacheObliviousTreeTraversal(node):
    if node is null:
        return
    cacheObliviousTreeTraversal(node.left)
    visit(node)
    cacheObliviousTreeTraversal(node.right)
```

---

#### **(Theoretical) Cache Efficiency in Dynamic Programming**
- **Optimization Suggestions**: Techniques such as blocking can improve cache locality, significantly enhancing performance in memory-intensive algorithms.

---

#### **(Implementation) Cache-Aware Strassen’s Algorithm**
```plaintext
function strassen(A, B, C, n):
    if n <= 64:  // Base case
        standardMatrixMultiply(A, B, C, n)
    else:
        // Strassen’s algorithm steps
```

---

#### **(Theoretical) Optimality of Cache-Efficient Algorithms**
- **Proof**: It can be shown that cache-efficient algorithms can minimize memory access time, leading to better overall performance.

---

### 4. **Algorithmic Paradigms: Greedy, Dynamic Programming, Approximation Algorithms**

#### **(Implementation) Huffman Coding Algorithm**
```plaintext
function huffmanCoding(frequencies):
    priorityQueue = createPriorityQueue(frequencies)
    
    while priorityQueue.size() > 1:
        left = priorityQueue.extractMin()
        right = priorityQueue.extractMin()
        mergedNode = createNode(left.frequency + right.frequency)
        priorityQueue.insert(mergedNode)

    return constructCodes(priorityQueue.extractMin())
```

---

#### **(Theoretical) Activity Selection Problem**
- **Correctness**: Greedy choice guarantees optimality as it always selects the next non-overlapping activity, ensuring maximum selection.
- **Dynamic Programming**: Not necessary as the greedy approach yields the optimal solution directly.

---

#### **(Implementation) Dynamic Programming Knapsack Problem**
```plaintext
function knapsack(weights, values, capacity):
    n = length(weights)
    dp = array filled with 0

    for i from 0 to n-1:
        for w from capacity down to weights[i]:
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])

    return dp[capacity]
```

---

#### **(Theoretical) Minimum Spanning Tree Optimality (Kruskal)**
- **Proof**: By adding the smallest edge that doesn’t create a cycle, Kruskal’s algorithm builds a valid MST.

---

#### **(Theoretical) Longest Common Subsequence Complexity**
- **Proof**: The DP table has dimensions \( O(nm) \) for strings of lengths \( n \) and \( m \).

---

#### **(Implementation) Vertex Cover 2-Approximation Algorithm**
```plaintext
function vertexCover(graph):
    cover = empty set
    while graph has edges:
        edge = pick an arbitrary edge (u, v)
        cover.add(u)
        cover.add(v)
        remove edges incident to u and v from graph
    return cover
```

---

#### **(Implementation) Bellman-Ford Algorithm**
```plaintext
function bellmanFord(graph, source):
    dist = array filled with infinity
    dist[source] = 0

    for i from 0 to length(graph) - 1:
        for edge in graph.edges:
            if dist[edge.u] + edge.weight < dist[edge.v]:
                dist[edge.v] = dist[edge.u] + edge.weight

    return dist
```

---

#### **(Theoretical) Edit Distance Complexity**
- **Analysis**: The optimality is ensured by the DP formulation, with complexity derived from filling a 2D table of size \( O(nm) \).

---

#### **(Implementation) Traveling Salesman Problem (TSP)**
```plaintext
function tsp(graph, start):
    n = length(graph)
    dp = array filled with infinity
    dp[0][1] = 0  // Starting point

    for mask from 1 to (1 << n) - 1:
        for u from 0 to n-1:
            for v from 0 to n-1:
                if mask & (1 << v) == 0:  // If v is not visited
                    dp[mask | (1 << v)][v] = min(dp[mask | (1 << v)][v], dp[mask][u] + graph[u][v])

    return min(dp[(1 << n) - 1][u] + graph[u][start] for u in range(n))
```

---

#### **(

Theoretical) Approximation Algorithms for NP-Hard Problems**
- **Proof of Approximation**: Algorithms like the greedy approach for set cover provide solutions within a logarithmic factor of the optimal.

---

#### **(Implementation) Minimum Cost Perfect Matching**
```plaintext
function minCostPerfectMatching(graph):
    // Use algorithms like Hungarian or Edmonds-Karp to find minimum cost perfect matching
```
