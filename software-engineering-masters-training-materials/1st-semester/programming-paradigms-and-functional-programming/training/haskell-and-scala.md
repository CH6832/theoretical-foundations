Certainly! Here’s a list of 20 exercises each for Haskell and Scala to help you solidify your skills and demonstrate proficiency. Each exercise varies in difficulty, covering fundamental concepts to advanced topics.

### **Haskell Exercises**

1. **Factorial Calculation:**
   - Implement a function to calculate the factorial of a number.

2. **Fibonacci Sequence:**
   - Write a function to generate the nth Fibonacci number.

3. **Palindrome Checker:**
   - Create a function to check if a given string is a palindrome.

4. **Sum of Squares:**
   - Implement a function to compute the sum of squares of a list of integers.

5. **List Reversal:**
   - Write a function to reverse a list without using built-in functions.

6. **Filter Even Numbers:**
   - Implement a function to filter out even numbers from a list.

7. **Merge Sort:**
   - Create an implementation of the merge sort algorithm.

8. **Matrix Multiplication:**
   - Implement matrix multiplication for 2x2 matrices.

9. **Implement `Maybe` Monad:**
   - Define a simple version of the `Maybe` monad and implement basic operations.

10. **File I/O:**
    - Write a function to count the number of lines in a file.

11. **Parse a CSV File:**
    - Implement a function to parse a CSV file into a list of lists of strings.

12. **Generate Primes:**
    - Write a function to generate all prime numbers up to a given number using the Sieve of Eratosthenes.

13. **Create a Binary Tree:**
    - Implement a simple binary tree and provide functions for insertion and traversal.

14. **Convert to Roman Numerals:**
    - Implement a function that converts an integer to a Roman numeral.

15. **Concurrent Programming:**
    - Write a program using `forkIO` to print "Hello" and "World" concurrently.

16. **Custom List Monad:**
    - Create a custom monad based on lists and demonstrate its use.

17. **Implement `Applicative`:**
    - Implement the `Applicative` type class for a simple custom type.

18. **Parse JSON Data:**
    - Use a JSON library to parse JSON data and extract specific fields.

19. **Software Transactional Memory:**
    - Implement a counter using STM (Software Transactional Memory) for safe concurrent updates.

20. **Property-Based Testing:**
    - Write property-based tests for a function using the `QuickCheck` library.

### **Scala Exercises**

1. **Factorial Calculation:**
   - Implement a recursive function to calculate the factorial of a number.

2. **Fibonacci Sequence:**
   - Write a function to generate the nth Fibonacci number.

3. **Palindrome Checker:**
   - Create a function to check if a given string is a palindrome.

4. **Sum of Squares:**
   - Implement a function to compute the sum of squares of a list of integers.

5. **List Reversal:**
   - Write a function to reverse a list without using built-in functions.

6. **Filter Even Numbers:**
   - Implement a function to filter out even numbers from a list.

7. **Merge Sort:**
   - Create an implementation of the merge sort algorithm.

8. **Matrix Multiplication:**
   - Implement matrix multiplication for 2x2 matrices.

9. **Define a Trait and Implement:**
   - Define a trait `Shape` with methods for area and perimeter. Implement this trait for `Circle` and `Rectangle`.

10. **File I/O:**
    - Write a function to count the number of lines in a file.

11. **Parse JSON Data:**
    - Use a JSON library (e.g., `play-json` or `circe`) to parse JSON data and extract specific fields.

12. **Generate Primes:**
    - Write a function to generate all prime numbers up to a given number using the Sieve of Eratosthenes.

13. **Custom Collection Class:**
    - Implement a custom collection class that behaves like a stack with `push`, `pop`, and `peek` methods.

14. **Convert to Roman Numerals:**
    - Implement a function that converts an integer to a Roman numeral.

15. **Concurrency with Futures:**
    - Use Scala’s `Future` to perform concurrent computations and combine results.

16. **Pattern Matching:**
    - Write a function that uses pattern matching to decode a simple algebraic data type.

17. **Create an Actor System:**
    - Use Akka to create a basic actor system with actors that send messages to each other.

18. **Implement a Monad:**
    - Define and implement a custom monad in Scala, demonstrating basic monadic operations.

19. **Software Transactional Memory:**
    - Use `scala.concurrent.stm` to manage a shared counter with concurrent updates.

20. **Property-Based Testing:**
    - Write property-based tests using a library like `ScalaCheck` to test functions and properties.

### **Example Implementations**

#### **Haskell Example: List Reversal**

```haskell
reverseList :: [a] -> [a]
reverseList = foldl (flip (:)) []
```

#### **Scala Example: List Reversal**

```scala
def reverseList[A](list: List[A]): List[A] = list.foldLeft(List.empty[A])((acc, elem) => elem :: acc)
```

#### **Haskell Example: Matrix Multiplication**

```haskell
type Matrix = [[Int]]

multiplyMatrices :: Matrix -> Matrix -> Matrix
multiplyMatrices a b = [[ sum $ zipWith (*) ar bc | bc <- transpose b ] | ar <- a]
```

#### **Scala Example: Matrix Multiplication**

```scala
def multiplyMatrices(a: Array[Array[Int]], b: Array[Array[Int]]): Array[Array[Int]] = {
  val rowsA = a.length
  val colsA = a(0).length
  val colsB = b(0).length
  val c = Array.ofDim[Int](rowsA, colsB)
  
  for (i <- 0 until rowsA; j <- 0 until colsB) {
    c(i)(j) = (0 until colsA).map(k => a(i)(k) * b(k)(j)).sum
  }
  
  c
}
```

Feel free to adjust the difficulty or add variations to these exercises based on your needs. Completing these exercises should help you demonstrate a deep understanding of Haskell and Scala. Let me know if you need further details or explanations on any of the exercises!