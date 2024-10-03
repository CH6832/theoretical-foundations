## **Programming Paradigms and Functional Programming**

### **1. Introduction to Programming Paradigms**

#### **Imperative vs Declarative Programming**

**Imperative Programming** focuses on describing how a program operates, using statements that change program state.

**Declarative Programming** focuses on what the program should accomplish without specifying how to achieve it.

**Pseudocode Example (Imperative):**
```
CREATE list numbers
FOR i FROM 0 TO 9
    ADD i TO numbers
END FOR

CREATE list evenNumbers
FOR number IN numbers
    IF number MOD 2 EQUALS 0 THEN
        ADD number TO evenNumbers
    END IF
END FOR

PRINT evenNumbers
```

**Pseudocode Example (Declarative):**
```
SET numbers TO [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
SET evenNumbers TO FILTER numbers WHERE number MOD 2 EQUALS 0
PRINT evenNumbers
```

#### **Overview of Paradigms**

**Procedural Programming** emphasizes functions and the sequence of actions taken to accomplish a task.

**Object-Oriented Programming (OOP)** organizes code into objects that combine data and methods.

**Functional Programming** emphasizes pure functions and immutability.

**Pseudocode Example (Procedural):**
```
FUNCTION add(a, b)
    RETURN a + b
END FUNCTION

SET result TO add(5, 3)
PRINT result
```

**Pseudocode Example (OOP):**
```
CLASS Calculator
    FUNCTION add(a, b)
        RETURN a + b
    END FUNCTION
END CLASS

SET calc TO new Calculator()
SET result TO calc.add(5, 3)
PRINT result
```

**Pseudocode Example (Functional):**
```
FUNCTION add(a, b)
    RETURN a + b
END FUNCTION

PRINT add(5, 3)
```

---

### **2. Object-Oriented Programming (OOP)**

#### **Encapsulation, Inheritance, Polymorphism**

**Encapsulation** involves bundling data and methods that operate on the data within a class.

**Inheritance** allows a class to inherit fields and methods from another class.

**Polymorphism** enables objects of different classes to be treated as objects of a common superclass.

**Pseudocode Example:**
```
CLASS Animal
    FUNCTION makeSound()
        PRINT "Animal sound"
    END FUNCTION
END CLASS

CLASS Dog INHERITS Animal
    FUNCTION makeSound()
        PRINT "Woof"
    END FUNCTION
END CLASS

SET myDog TO new Dog()
myDog.makeSound()  // Outputs "Woof"
```

#### **Principles of Good Object Design (SOLID)**

- **Single Responsibility Principle:** A class should have one reason to change.
- **Open/Closed Principle:** Entities should be open for extension but closed for modification.
- **Liskov Substitution Principle:** Subtypes must be substitutable for their base types.
- **Interface Segregation Principle:** Clients should not be forced to depend on interfaces they do not use.
- **Dependency Inversion Principle:** Depend on abstractions, not on concrete implementations.

**Pseudocode Example for SOLID Principles:**

```
// Single Responsibility Principle
CLASS User
    PROPERTY name
    // Getter and Setter
END CLASS

CLASS UserPrinter
    FUNCTION print(user)
        PRINT user.name
    END FUNCTION
END CLASS

// Open/Closed Principle
ABSTRACT CLASS Shape
    FUNCTION area() RETURNING NUMBER
END CLASS

CLASS Rectangle INHERITS Shape
    PROPERTY width, height

    FUNCTION constructor(width, height)
        SET this.width TO width
        SET this.height TO height
    END FUNCTION

    FUNCTION area()
        RETURN this.width * this.height
    END FUNCTION
END CLASS

// Liskov Substitution Principle
CLASS ShapeAreaCalculator
    FUNCTION calculateArea(shape)
        RETURN shape.area()
    END FUNCTION
END CLASS

// Interface Segregation Principle
INTERFACE Printable
    FUNCTION print()
END INTERFACE

INTERFACE Scannable
    FUNCTION scan()
END INTERFACE

CLASS MultiFunctionPrinter IMPLEMENTS Printable, Scannable
    FUNCTION print()
        // Implementation
    END FUNCTION

    FUNCTION scan()
        // Implementation
    END FUNCTION
END CLASS

// Dependency Inversion Principle
INTERFACE Repository
    FUNCTION save(obj)
END INTERFACE

CLASS MySQLRepository IMPLEMENTS Repository
    FUNCTION save(obj)
        // MySQL save implementation
    END FUNCTION
END CLASS
```

---

### **3. Functional Programming Concepts**

#### **Pure Functions and Immutability**

**Pure Functions** always produce the same output for the same input and have no side effects.

**Immutability** means that once a data structure is created, it cannot be changed.

**Pseudocode Example (Pure Functions and Immutability):**
```
// Pure Function
FUNCTION add(x, y)
    RETURN x + y
END FUNCTION

// Immutability
SET x TO 5
SET y TO x + 10
// x remains 5
```

**Pseudocode Example (Pure Functions):**
```
FUNCTION add(a, b)
    RETURN a + b
END FUNCTION

SET result TO add(5, 3)
PRINT result
```

#### **Higher-Order Functions**

Higher-order functions take other functions as arguments or return functions as results.

**Pseudocode Example:**
```
FUNCTION applyFunction(f, x)
    RETURN f(x)
END FUNCTION

FUNCTION increment(x)
    RETURN x + 1
END FUNCTION

PRINT applyFunction(increment, 5)  // Outputs 6
```

#### **Recursion and Tail Recursion**

**Recursion** involves a function calling itself to solve a problem.

**Tail Recursion** is a special case where the recursive call is the last operation in the function.

**Pseudocode Example (Recursion and Tail Recursion):**
```
// Recursive function (not tail-recursive)
FUNCTION factorial(n)
    IF n EQUALS 0 THEN
        RETURN 1
    END IF
    RETURN n * factorial(n - 1)
END FUNCTION

// Tail-recursive function
FUNCTION factorialTail(n, acc)
    IF n EQUALS 0 THEN
        RETURN acc
    END IF
    RETURN factorialTail(n - 1, n * acc)
END FUNCTION

PRINT factorial(5)         // Outputs 120
PRINT factorialTail(5, 1)  // Outputs 120
```

#### **Closures and Lambda Expressions**

**Closures** capture the environment in which they were created, allowing functions to retain access to their lexical scope.

**Lambda Expressions** are anonymous functions used to create function objects.

**Pseudocode Example (Closures and Lambda Expressions):**
```
// Closure example
FUNCTION addN(n)
    RETURN FUNCTION(x)
        RETURN x + n
    END FUNCTION
END FUNCTION

SET add5 TO addN(5)
PRINT add5(10)  // Outputs 15

// Lambda expression example
SET add10 TO FUNCTION(x) RETURN x + 10
PRINT add10(5)  // Outputs 15
```

---

### **4. Monads and Functors**

#### **The Monad Pattern**

**Monads** are abstract data types used to represent computations instead of values.

**Pseudocode Example (Monads):**
```
// Maybe Monad Example
FUNCTION safeDivide(x, y)
    IF y EQUALS 0 THEN
        RETURN Nothing
    END IF
    RETURN Just(x DIV y)
END FUNCTION

PRINT safeDivide(10, 2)  // Outputs Just 5
```

#### **Functors and Applicatives**

**Functors** are types that can be mapped over.

**Applicatives** extend functors to allow for function application within a context.

**Pseudocode Example (Functors and Applicatives):**
```
// Functor Example
CLASS Box
    PROPERTY value
END CLASS

FUNCTION fmap(f, box)
    RETURN new Box(f(box.value))
END FUNCTION

// Applicative Example
FUNCTION addBox(box1, box2)
    RETURN new Box(box1.value + box2.value)
END FUNCTION

PRINT addBox(new Box(5), new Box(10))  // Outputs Box(15)
```

---

### **5. Concurrency in Functional Programming**

#### **Functional Concurrency Models**

**Actors Model** uses actors as fundamental units of computation that communicate via message passing.

**Communicating Sequential Processes (CSP)** involves processes that communicate through channels.

**Pseudocode Example (Actors Model):**
```
DEFINE Actor SimpleActor
    FUNCTION receive(message)
        IF message EQUALS "ping" THEN
            PRINT "pong"
        ELSE
            PRINT "unknown message"
        END IF
    END FUNCTION
END Actor

SET actor TO new SimpleActor()
actor.receive("ping")  // Outputs "pong"
actor.receive("hello") // Outputs "unknown message"
```

#### **Asynchronous Programming**

**Futures** and **Promises** represent computations that may complete in the future.

**Pseudocode Example (Promises):**
```
FUNCTION fetchData()
    RETURN new Promise(resolve, reject) DO
        WAIT 1 SECOND
        RESOLVE("Data fetched")
    END FUNCTION
END FUNCTION

fetchData().then(data) DO
    PRINT data  // Outputs "Data fetched"
END FUNCTION
```

**Pseudocode Example (CompletableFuture):**
```
FUNCTION main()
    SET future TO CompletableFuture.supplyAsync() DO
        WAIT 1 SECOND
        RETURN "Data fetched"
    END FUNCTION

    future.thenAccept(data) DO
        PRINT data  // Outputs "Data fetched"
    END FUNCTION


END FUNCTION
``` 
