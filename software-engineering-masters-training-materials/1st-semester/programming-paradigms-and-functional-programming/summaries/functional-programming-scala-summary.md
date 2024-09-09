## 1. What is Functional Programming

**Definition:**
Functional programming (FP) is a paradigm that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data. It emphasizes the use of pure functions, higher-order functions, and immutability.

**Core Principles:**

- **Immutability:** Data is immutable, meaning once created, it cannot be changed.
- **First-Class and Higher-Order Functions:** Functions are first-class citizens, and can be passed as arguments or returned from other functions.
- **Pure Functions:** Functions that have no side effects and return the same output for the same input.
- **Function Composition:** Combining functions to build more complex functions.

**Real-World Example:**

Imagine a system for calculating employee bonuses. In a functional paradigm, you might define a pure function to calculate bonuses:

```scala
def calculateBonus(salary: Double, performanceRating: Double): Double = {
  salary * (performanceRating / 100)
}
```

This function is pure because it does not modify any state and always returns the same result for the same inputs.

---

## 2. Getting Started with Functional Programming in Scala

**Setup:**
- **Install Scala:** You can use Scala’s official website to download and install Scala.
- **IDE:** Use an IDE like IntelliJ IDEA with the Scala plugin for an efficient development environment.
- **Build Tool:** Use SBT (Scala Build Tool) for managing dependencies and building Scala projects.

**Basic Scala Syntax:**
- Define immutable variables with `val` and mutable variables with `var`.
- Define functions using `def`.

**Example:**

```scala
// Immutable variable
val pi = 3.14159

// Mutable variable
var counter = 0

// Function definition
def square(x: Int): Int = x * x

println(square(5)) // Outputs: 25
```

**Real-World Example:**

A basic application might involve defining functions to handle data, such as calculating the total price of items in a shopping cart:

```scala
case class Item(name: String, price: Double)

def totalPrice(items: List[Item]): Double = {
  items.map(_.price).sum
}

val cart = List(Item("Apple", 0.99), Item("Banana", 0.59))
println(totalPrice(cart)) // Outputs: 1.58
```

---

## 3. Functional Data Structures

**Concept:**
Functional data structures are immutable and provide methods to manipulate data in a way that does not change the original structure. They often offer persistent (historical) versions of the data structure.

**Common Structures:**
- **Lists:** Linked lists or immutable lists.
- **Maps:** Immutable hash maps or sorted maps.
- **Sets:** Immutable sets.

**Examples:**

- **Immutable List:**

```scala
val list1 = List(1, 2, 3)
val list2 = list1 :+ 4 // Adding an element without modifying list1

println(list1) // Outputs: List(1, 2, 3)
println(list2) // Outputs: List(1, 2, 3, 4)
```

- **Immutable Map:**

```scala
val map1 = Map("a" -> 1, "b" -> 2)
val map2 = map1 + ("c" -> 3) // Adding a key-value pair

println(map1) // Outputs: Map(a -> 1, b -> 2)
println(map2) // Outputs: Map(a -> 1, b -> 2, c -> 3)
```

**Real-World Example:**

Using an immutable map to store user preferences:

```scala
val preferences = Map("theme" -> "dark", "notifications" -> "enabled")
val updatedPreferences = preferences + ("language" -> "en")

println(preferences) // Outputs: Map(theme -> dark, notifications -> enabled)
println(updatedPreferences) // Outputs: Map(theme -> dark, notifications -> enabled, language -> en)
```

---

## 4. Handling Errors Without Exceptions

**Concept:**
Instead of using exceptions, functional programming often uses types like `Option` and `Either` to represent the presence or absence of a value or errors.

**Types:**
- **Option:** Represents a value that might be present (`Some`) or absent (`None`).
- **Either:** Represents a value of one of two possible types (often used for error handling).

**Examples:**

- **Option:**

```scala
def findElement(index: Int, list: List[Int]): Option[Int] = {
  if (index >= 0 && index < list.length) Some(list(index))
  else None
}

println(findElement(1, List(10, 20, 30))) // Outputs: Some(20)
println(findElement(5, List(10, 20, 30))) // Outputs: None
```

- **Either:**

```scala
def divide(x: Int, y: Int): Either[String, Double] = {
  if (y == 0) Left("Division by zero error")
  else Right(x.toDouble / y)
}

println(divide(10, 2)) // Outputs: Right(5.0)
println(divide(10, 0)) // Outputs: Left(Division by zero error)
```

**Real-World Example:**

A function that parses a date and returns an error if the date is invalid:

```scala
import java.time.LocalDate
import java.time.format.DateTimeParseException

def parseDate(dateString: String): Either[String, LocalDate] = {
  try {
    Right(LocalDate.parse(dateString))
  } catch {
    case _: DateTimeParseException => Left("Invalid date format")
  }
}

println(parseDate("2024-09-09")) // Outputs: Right(2024-09-09)
println(parseDate("2024-09-31")) // Outputs: Left(Invalid date format)
```

---

## 5. Strictness and Laziness

**Concept:**
- **Strictness:** Evaluation strategy where expressions are evaluated as soon as they are bound to a variable.
- **Laziness:** Evaluation strategy where expressions are evaluated only when needed.

**Scala’s `lazy` keyword:**

- **Lazy Values:** Values that are only computed when accessed.

**Examples:**

- **Strict Evaluation:**

```scala
val x = 5
val y = x + 2 // x is evaluated immediately
```

- **Lazy Evaluation:**

```scala
lazy val z = {
  println("Evaluating z")
  10
}

println("Before accessing z")
println(z) // "Evaluating z" is printed here
```

**Real-World Example:**

Consider a list of integers where you only need the first few elements:

```scala
val numbers = Stream.from(1) // Infinite stream
val firstFive = numbers.take(5) // Only takes the first 5 numbers

println(firstFive.toList) // Outputs: List(1, 2, 3, 4, 5)
```

---

## 6. Purely Functional State

**Concept:**
Managing state in a purely functional way involves using immutable data structures and pure functions. Techniques like `State` monads and functional programming patterns help manage state without mutability.

**State Monad Example:**

```scala
import scala.util.Random

// State monad type
case class State[S, A](run: S => (A, S)) {
  def map[B](f: A => B): State[S, B] = State { s =>
    val (a, newState) = run(s)
    (f(a), newState)
  }

  def flatMap[B](f: A => State[S, B]): State[S, B] = State { s =>
    val (a, newState) = run(s)
    f(a).run(newState)
  }
}

// Example usage
def randomInt: State[Int, Int] = State { seed =>
  val rand = new Random(seed)
  val nextSeed = rand.nextInt()
  (rand.nextInt(100), nextSeed)
}

val initialState = 42
val (value, newState) = randomInt.run(initialState)
println(s"Value: $value, New State: $newState")
```

**Real-World Example:**

A counter that increments a state value without mutation:

```scala
def incrementCounter(counter: Int): (Int, Int) = (counter + 1, counter + 1)

val (newCounter, updatedCounter) = incrementCounter(5)
println(newCounter) // Outputs: 6
println(updatedCounter) // Outputs: 6
```

---

## 7. Purely Functional Parallelism

**Concept:**
Parallelism in functional programming can be achieved using abstractions like parallel collections, futures, and concurrent data structures, all while maintaining immutability and avoiding side effects.

**Scala Future Example:**

```scala
import scala.concurrent.{Future, Await}
import scala.concurrent.ExecutionContext.Implicits.global
import scala.concurrent.duration._

val futureResult = Future {
  Thread.sleep(1000) // Simulate a long computation
  42
}

val result = Await.result(futureResult, 2.seconds)
println(result) // Outputs: 42
```

**Real-World Example:**

Performing parallel computations on a list of numbers:

```scala
val numbers = List(1, 2, 3, 4, 5)
val futureResults = numbers.map { n =>
  Future {
    Thread.sleep(500) // Simulate computation
    n * n
  }


}

val results = Await.result(Future.sequence(futureResults), 1.second)
println(results) // Outputs: List(1, 4, 9, 16, 25)
```

---

## 8. Property-Based Testing

**Concept:**
Property-based testing involves defining properties that should hold true for any input, rather than writing specific test cases. Frameworks like ScalaCheck help generate test cases that satisfy these properties.

**Example with ScalaCheck:**

```scala
import org.scalacheck.Prop.forAll
import org.scalacheck.Properties

object ListProperties extends Properties("List") {
  property("headOption is defined for non-empty lists") = forAll { list: List[Int] =>
    list.headOption.isDefined || list.isEmpty
  }
}
```

**Real-World Example:**

Testing that the concatenation of two lists yields a list whose length is the sum of the lengths of the two lists:

```scala
import org.scalacheck.Prop.forAll
import org.scalacheck.Properties

object ListConcatProperties extends Properties("List") {
  property("concat length") = forAll { (list1: List[Int], list2: List[Int]) =>
    (list1 ++ list2).length == (list1.length + list2.length)
  }
}
```

---

## 9. Parser Combinators

**Concept:**
Parser combinators allow you to build complex parsers from simpler ones. They work by combining small parsing functions to create more complex parsers.

**Example:**

```scala
import scala.util.parsing.combinator._

object SimpleParser extends RegexParsers {
  def number: Parser[Int] = """\d+""".r ^^ { _.toInt }
  def add: Parser[Int] = number ~ "+" ~ number ^^ {
    case n1 ~ "+" ~ n2 => n1 + n2
  }
  
  def parseExpression(input: String): ParseResult[Int] = parseAll(add, input)
}

println(SimpleParser.parseExpression("3 + 4")) // Outputs: [1.1] parsed: 7
```

**Real-World Example:**

Parsing a simple arithmetic expression:

```scala
object ArithmeticParser extends RegexParsers {
  def number: Parser[Int] = """\d+""".r ^^ { _.toInt }
  def expr: Parser[Int] = term ~ rep("+" ~ term) ^^ {
    case t ~ lst => lst.foldLeft(t) {
      case (acc, "+" ~ t2) => acc + t2
    }
  }
  def term: Parser[Int] = number
  
  def parseExpression(input: String): ParseResult[Int] = parseAll(expr, input)
}

println(ArithmeticParser.parseExpression("1 + 2 + 3")) // Outputs: [1.14] parsed: 6
```

---

## 10. Monoids

**Concept:**
A monoid is an algebraic structure with an associative binary operation and an identity element. Monoids can be used to combine elements in a functional way.

**Example:**

```scala
trait Monoid[A] {
  def combine(x: A, y: A): A
  def empty: A
}

object IntAddition extends Monoid[Int] {
  def combine(x: Int, y: Int): Int = x + y
  def empty: Int = 0
}

val sum = List(1, 2, 3, 4).reduce(IntAddition.combine)
println(sum) // Outputs: 10
```

**Real-World Example:**

Combining strings:

```scala
object StringConcatenation extends Monoid[String] {
  def combine(x: String, y: String): String = x + y
  def empty: String = ""
}

val combined = List("Hello, ", "World!").reduce(StringConcatenation.combine)
println(combined) // Outputs: Hello, World!
```

---

## 11. Monads

**Concept:**
Monads are a design pattern used to handle computations and side effects in a functional way. They provide a way to sequence operations while abstracting away the underlying complexity.

**Example with Option Monad:**

```scala
val result: Option[Int] = for {
  x <- Some(5)
  y <- Some(10)
} yield x + y

println(result) // Outputs: Some(15)
```

**Real-World Example:**

Using the `Future` monad for asynchronous computations:

```scala
import scala.concurrent.{Future, Await}
import scala.concurrent.ExecutionContext.Implicits.global
import scala.concurrent.duration._

val futureResult: Future[Int] = for {
  x <- Future.successful(10)
  y <- Future.successful(20)
} yield x + y

val result = Await.result(futureResult, 1.second)
println(result) // Outputs: 30
```

---

## 12. Applicative and Traversable Functors

**Concept:**
- **Applicative Functors:** Allow applying functions wrapped in a context (e.g., `Option`, `Future`) to values wrapped in a context.
- **Traversable Functors:** Allow traversing a structure and applying a function to each element, while maintaining the structure.

**Example with `Option`:**

```scala
import scala.util.Try

val option1: Option[Int] = Some(5)
val option2: Option[Int] = Some(10)

val result: Option[Int] = (option1, option2).mapN(_ + _)
println(result) // Outputs: Some(15)
```

**Real-World Example:**

Using `Future` with `traverse`:

```scala
import scala.concurrent.{Future, Await}
import scala.concurrent.ExecutionContext.Implicits.global
import scala.concurrent.duration._

val futures: List[Future[Int]] = List(Future.successful(1), Future.successful(2), Future.successful(3))

val combinedFuture: Future[List[Int]] = Future.sequence(futures)

val result = Await.result(combinedFuture, 1.second)
println(result) // Outputs: List(1, 2, 3)
```

---

## 13. External Effects and I/O

**Concept:**
Handling external effects like I/O in a functional programming context involves using abstractions that represent these effects in a pure way, such as using the `IO` monad from libraries like Cats Effect.

**Example with `IO`:**

```scala
import cats.effect.{IO, IOApp}

object Main extends IOApp.Simple {
  def run: IO[Unit] = for {
    _ <- IO(println("Hello, world!"))
    _ <- IO(println("Goodbye, world!"))
  } yield ()
}
```

**Real-World Example:**

Reading from and writing to a file:

```scala
import cats.effect.{IO, IOApp}
import java.nio.file.{Files, Paths}

object FileExample extends IOApp.Simple {
  def run: IO[Unit] = for {
    _ <- IO(Files.write(Paths.get("example.txt"), "Hello, world!".getBytes))
    content <- IO(Files.readAllBytes(Paths.get("example.txt")))
    _ <- IO(println(new String(content)))
  } yield ()
}
```

---

## 14. Local Effects and Mutable States

**Concept:**
Managing local effects and mutable states in functional programming typically involves techniques such as `State` monads or encapsulating mutable state within immutable structures.

**Example with State Monad:**

```scala
case class State[S, A](run: S => (A, S)) {
  def map[B](f: A => B): State[S, B] = State { s =>
    val (a, newState) = run(s)
    (f(a), newState)
  }

  def flatMap[B](f: A => State[S, B]): State[S, B] = State { s =>
    val (a, newState) = run(s)
    f(a).run(newState)
  }
}

def incrementState(value: Int): State[Int, Int] = State { state =>
  (value + state, state + 1)
}

val initialState = 0
val (result, finalState) = incrementState(5).run(initialState)
println(result) // Outputs: 5
println(finalState) // Outputs: 1
```

**Real-World Example:**

Simulating a counter that increments within a state:

```scala
case class Counter(count: Int) {
  def increment: Counter = copy(count = count + 1)
}

val initialCounter = Counter(0)
val incrementedCounter = initialCounter.increment
println(incrementedCounter.count) // Outputs: 1
```

---

## 15. Stream Processing and Incremental I/O

**Concept:**
Stream processing involves handling data in a way that supports incremental processing and can deal with potentially infinite data sources.

**Example with Scala Streams:**

```scala
val numbers = Stream.from(1)
val firstTen = numbers.take(10).toList

println(firstTen) // Outputs: List(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

**Real-World Example:**

Processing a large file line by line:

```scala
import scala.io.Source

def processLines(fileName: String): Unit = {
  val source = Source.fromFile(fileName)
  try {
    for (line <- source.getLines()) {
      println(line)
    }
  } finally {
    source.close()
  }
}

processLines("largeFile.txt")
```