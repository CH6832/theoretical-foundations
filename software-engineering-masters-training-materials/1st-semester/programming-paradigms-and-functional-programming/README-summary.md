## **Programming Paradigms and Functional Programming**

### **1. Introduction to Programming Paradigms**

#### **Imperative vs Declarative Programming**

**Imperative Programming** focuses on describing how a program operates, using statements that change program state.

**Declarative Programming** focuses on what the program should accomplish without specifying how to achieve it.

**Java Example (Imperative):**
```java
import java.util.ArrayList;
import java.util.List;

public class ImperativeExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            numbers.add(i);
        }
        List<Integer> evenNumbers = new ArrayList<>();
        for (int number : numbers) {
            if (number % 2 == 0) {
                evenNumbers.add(number);
            }
        }
        System.out.println(evenNumbers);
    }
}
```

**JavaScript Example (Declarative):**
```javascript
const numbers = Array.from({ length: 10 }, (_, i) => i);
const evenNumbers = numbers.filter(number => number % 2 === 0);
console.log(evenNumbers);
```

#### **Overview of Paradigms**

**Procedural Programming** emphasizes functions and the sequence of actions taken to accomplish a task.

**Object-Oriented Programming (OOP)** organizes code into objects that combine data and methods.

**Functional Programming** emphasizes pure functions and immutability.

**Java Example (Procedural):**
```java
public class ProceduralExample {
    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        int result = add(5, 3);
        System.out.println(result);
    }
}
```

**Python Example (OOP):**
```python
class Calculator:
    def add(self, a, b):
        return a + b

calc = Calculator()
result = calc.add(5, 3)
print(result)
```

**Haskell Example (Functional):**
```haskell
add :: Int -> Int -> Int
add a b = a + b

main :: IO ()
main = print (add 5 3)
```

---

### **2. Object-Oriented Programming (OOP)**

#### **Encapsulation, Inheritance, Polymorphism**

**Encapsulation** involves bundling data and methods that operate on the data within a class.

**Inheritance** allows a class to inherit fields and methods from another class.

**Polymorphism** enables objects of different classes to be treated as objects of a common superclass.

**Java Example:**
```java
class Animal {
    public void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}

public class OOPExample {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound(); // Outputs "Woof"
    }
}
```

#### **Principles of Good Object Design (SOLID)**

- **Single Responsibility Principle:** A class should have one reason to change.
- **Open/Closed Principle:** Entities should be open for extension but closed for modification.
- **Liskov Substitution Principle:** Subtypes must be substitutable for their base types.
- **Interface Segregation Principle:** Clients should not be forced to depend on interfaces they do not use.
- **Dependency Inversion Principle:** Depend on abstractions, not on concrete implementations.

**Java Example for SOLID Principles:**

```java
// Single Responsibility Principle
class User {
    private String name;
    // Getter and Setter
}

class UserPrinter {
    public void print(User user) {
        System.out.println(user.getName());
    }
}

// Open/Closed Principle
abstract class Shape {
    public abstract double area();
}

class Rectangle extends Shape {
    private double width, height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

// Liskov Substitution Principle
class ShapeAreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.area();
    }
}

// Interface Segregation Principle
interface Printable {
    void print();
}

interface Scannable {
    void scan();
}

class MultiFunctionPrinter implements Printable, Scannable {
    public void print() {
        // Implementation
    }

    public void scan() {
        // Implementation
    }
}

// Dependency Inversion Principle
interface Repository {
    void save(Object obj);
}

class MySQLRepository implements Repository {
    public void save(Object obj) {
        // MySQL save implementation
    }
}
```

---

### **3. Functional Programming Concepts**

#### **Pure Functions and Immutability**

**Pure Functions** always produce the same output for the same input and have no side effects.

**Immutability** means that once a data structure is created, it cannot be changed.

**Haskell Example (Pure Functions and Immutability):**
```haskell
-- Pure Function
add :: Int -> Int -> Int
add x y = x + y

-- Immutability in Haskell
let x = 5
let y = x + 10
-- x remains 5
```

**JavaScript Example (Pure Functions):**
```javascript
function add(a, b) {
    return a + b;
}

const result = add(5, 3);
console.log(result);
```

#### **Higher-Order Functions**

Higher-order functions take other functions as arguments or return functions as results.

**Haskell Example:**
```haskell
-- Higher-order function
applyFunction :: (Int -> Int) -> Int -> Int
applyFunction f x = f x

increment :: Int -> Int
increment x = x + 1

main :: IO ()
main = print (applyFunction increment 5)  -- Outputs 6
```

**JavaScript Example:**
```javascript
function applyFunction(fn, x) {
    return fn(x);
}

function increment(x) {
    return x + 1;
}

console.log(applyFunction(increment, 5));  // Outputs 6
```

#### **Recursion and Tail Recursion**

**Recursion** involves a function calling itself to solve a problem.

**Tail Recursion** is a special case where the recursive call is the last operation in the function.

**Haskell Example (Recursion and Tail Recursion):**
```haskell
-- Recursive function (not tail-recursive)
factorial :: Int -> Int
factorial 0 = 1
factorial n = n * factorial (n - 1)

-- Tail-recursive function
factorialTail :: Int -> Int -> Int
factorialTail 0 acc = acc
factorialTail n acc = factorialTail (n - 1) (n * acc)

main :: IO ()
main = print (factorial 5)         -- Outputs 120
      print (factorialTail 5 1)    -- Outputs 120
```

**JavaScript Example (Recursion and Tail Recursion):**
```javascript
// Recursive function (not tail-recursive)
function factorial(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);
}

// Tail-recursive function
function factorialTail(n, acc = 1) {
    if (n === 0) return acc;
    return factorialTail(n - 1, n * acc);
}

console.log(factorial(5));         // Outputs 120
console.log(factorialTail(5));     // Outputs 120
```

#### **Closures and Lambda Expressions**

**Closures** capture the environment in which they were created, allowing functions to retain access to their lexical scope.

**Lambda Expressions** are anonymous functions used to create function objects.

**Haskell Example (Closures and Lambda Expressions):**
```haskell
-- Closure example
addN :: Int -> Int -> Int
addN n x = x + n

-- Lambda expression example
main :: IO ()
main = do
    let add5 = (\x -> x + 5)
    print (add5 10)  -- Outputs 15
```

**JavaScript Example (Closures and Lambda Expressions):**
```javascript
// Closure example
function makeAdder(n) {
    return function(x) {
        return x + n;
    };
}

const add5 = makeAdder(5);
console.log(add5(10));  // Outputs 15

// Lambda expression example
const add10 = x => x + 10;
console.log(add10(5));  // Outputs 15
```

---

### **4. Monads and Functors**

#### **The Monad Pattern**

**Monads** are abstract data types used to represent computations instead of values.

**Haskell Example (Monads):**
```haskell
-- Maybe Monad Example
safeDivide :: Int -> Int -> Maybe Int
safeDivide _ 0 = Nothing
safeDivide x y = Just (x `div` y)

main :: IO ()
main = print (safeDivide 10 2)  -- Outputs Just 5
```

#### **Functors and Applicatives**

**Functors** are types that can be mapped over.

**Applicatives** extend functors to allow for function application within a context.

**Haskell Example (Functors and Applicatives):**
```haskell
import Control.Applicative (liftA2)

-- Functor Example


data Box a = Box a
instance Functor Box where
    fmap f (Box x) = Box (f x)

-- Applicative Example
addBox :: Box Int -> Box Int -> Box Int
addBox (Box x) (Box y) = Box (x + y)

main :: IO ()
main = print (addBox (Box 5) (Box 10))  -- Outputs Box 15
```

**Scala Example (Functors and Applicatives):**
```scala
// Functor Example
trait Functor[F[_]] {
    def map[A, B](fa: F[A])(f: A => B): F[B]
}

// Box Functor Implementation
case class Box[A](value: A)
object BoxFunctor extends Functor[Box] {
    def map[A, B](fa: Box[A])(f: A => B): Box[B] = Box(f(fa.value))
}

// Applicative Example
trait Applicative[F[_]] extends Functor[F] {
    def pure[A](a: A): F[A]
    def ap[A, B](fa: F[A])(f: F[A => B]): F[B]
}

object BoxApplicative extends Applicative[Box] {
    def pure[A](a: A): Box[A] = Box(a)
    def ap[A, B](fa: Box[A])(f: Box[A => B]): Box[B] = Box(f.value(fa.value))
}

object Main extends App {
    val box1 = Box(5)
    val box2 = Box(10)
    val result = BoxApplicative.ap(box1)(Box(value => value + 10))
    println(result)  // Outputs Box(15)
}
```

---

### **5. Concurrency in Functional Programming**

#### **Functional Concurrency Models**

**Actors Model** uses actors as fundamental units of computation that communicate via message passing.

**Communicating Sequential Processes (CSP)** involves processes that communicate through channels.

**Scala Example (Actors Model):**
```scala
import akka.actor.{Actor, ActorSystem, Props}

// Define the Actor
class SimpleActor extends Actor {
    def receive = {
        case "ping" => println("pong")
        case _      => println("unknown message")
    }
}

// Main App
object Main extends App {
    val system = ActorSystem("SimpleSystem")
    val actor = system.actorOf(Props[SimpleActor], name = "simpleActor")

    actor ! "ping"  // Outputs "pong"
    actor ! "hello" // Outputs "unknown message"
}
```

#### **Asynchronous Programming**

**Futures** and **Promises** represent computations that may complete in the future.

**JavaScript Example (Promises):**
```javascript
// Function that returns a promise
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Data fetched"), 1000);
    });
}

fetchData().then(data => console.log(data));  // Outputs "Data fetched"
```

**Java Example (CompletableFuture):**
```java
import java.util.concurrent.CompletableFuture;

public class AsyncExample {
    public static void main(String[] args) {
        CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "Data fetched";
        }).thenAccept(data -> System.out.println(data)); // Outputs "Data fetched"
    }
}
```
