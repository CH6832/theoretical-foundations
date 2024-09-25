# Software Architecture and Design Patterns

## 1. Introduction to Software Architecture

### Architectural Styles

1. **Monolithic Architecture**: 
   A unified application where all components are interconnected. Changes in one module can affect others.

   ```plaintext
   // Monolithic Application Structure
   - User Interface
   - Business Logic
   - Database Access
   ```

2. **Microservices Architecture**: 
   An approach where the application is composed of small, independent services that communicate over a network. Each service can be developed, deployed, and scaled independently.

   ```plaintext
   // Microservices Application Structure
   - User Service
   - Notification Service
   - Order Service
   ```

3. **Service-Oriented Architecture (SOA)**: 
   Similar to microservices but emphasizes reusable services that can be orchestrated to form larger systems, facilitating inter-service communication.

4. **Layered Architecture**: 
   The application is divided into distinct layers, each with its own responsibilities. Common layers include presentation, business logic, and data access.

   ```plaintext
   // Layered Architecture Structure
   - Presentation Layer
   - Business Logic Layer
   - Data Access Layer
   ```

### Java Example (Monolithic Architecture)

```java
// A simple monolithic application
public class MonolithicApp {
    public static void main(String[] args) {
        UserService userService = new UserService();
        userService.createUser("John Doe");
    }
}

class UserService {
    private UserRepository userRepository = new UserRepository();
    
    public void createUser(String name) {
        User user = new User(name);
        userRepository.save(user);
    }
}

class UserRepository {
    public void save(User user) {
        System.out.println("User saved: " + user.getName());
    }
}

class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

### Java Example (Microservices Architecture)

```java
// Example of microservices setup (simplified)
public class MicroservicesApp {
    public static void main(String[] args) {
        UserService userService = new UserService();
        NotificationService notificationService = new NotificationService();
        
        userService.createUser("John Doe", notificationService);
    }
}

class UserService {
    public void createUser(String name, NotificationService notificationService) {
        User user = new User(name);
        System.out.println("User created: " + user.getName());
        notificationService.sendNotification("Welcome " + name);
    }
}

class NotificationService {
    public void sendNotification(String message) {
        System.out.println("Notification sent: " + message);
    }
}

class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

### Architectural Trade-Offs

- **Performance**: Monolithic systems can be faster for small applications but may become unmanageable as they grow.
- **Maintainability**: Microservices improve maintainability through independent development and deployment cycles.
- **Scalability**: Microservices allow for individual scaling, while monolithic systems necessitate scaling the entire application.

---

## 2. SOLID Principles

### Single Responsibility Principle (SRP)

A class should have only one reason to change, encapsulating a single responsibility.

**Java Example:**

```java
// Violating SRP
class Report {
    public void generateReport() { /* Generate report logic */ }
    public void saveToFile() { /* Save report logic */ }
}

// Following SRP
class Report {
    public void generateReport() { /* Generate report logic */ }
}

class ReportSaver {
    public void saveToFile(Report report) { /* Save report logic */ }
}
```

### Open/Closed Principle (OCP)

Software entities should be open for extension but closed for modification.

**Java Example:**

```java
// Before OCP
class Rectangle {
    private int width;
    private int height;
    // Methods for Rectangle
}

class AreaCalculator {
    public int calculateArea(Rectangle rectangle) {
        return rectangle.getWidth() * rectangle.getHeight();
    }
}

// After OCP
interface Shape {
    int area();
}

class Rectangle implements Shape {
    public int area() {
        return width * height;
    }
}

class Circle implements Shape {
    public int area() {
        return (int) (Math.PI * radius * radius);
    }
}

class AreaCalculator {
    public int calculateArea(Shape shape) {
        return shape.area();
    }
}
```

### Liskov Substitution Principle (LSP)

Subtypes must be substitutable for their base types without altering the correctness of the program.

**Java Example:**

```java
// Violating LSP
class Bird {
    public void fly() { /* Fly logic */ }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly");
    }
}

// Following LSP
interface Flyable {
    void fly();
}

class Sparrow implements Flyable {
    public void fly() { /* Fly logic */ }
}

class Ostrich { /* No fly method */ }
```

### Interface Segregation Principle (ISP)

Clients should not be forced to depend on interfaces they do not use.

**Java Example:**

```java
// Violating ISP
interface Worker {
    void work();
    void eat();
}

class HumanWorker implements Worker {
    public void work() { /* Work logic */ }
    public void eat() { /* Eat logic */ }
}

class RobotWorker implements Worker {
    public void work() { /* Work logic */ }
    public void eat() {
        throw new UnsupportedOperationException();
    }
}

// Following ISP
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class HumanWorker implements Workable, Eatable {
    public void work() { /* Work logic */ }
    public void eat() { /* Eat logic */ }
}

class RobotWorker implements Workable {
    public void work() { /* Work logic */ }
}
```

### Dependency Inversion Principle (DIP)

Depend on abstractions, not on concrete implementations.

**Java Example:**

```java
// Violating DIP
class LightBulb {
    public void turnOn() { /* Turn on logic */ }
}

class Switch {
    private LightBulb bulb;

    public Switch(LightBulb bulb) {
        this.bulb = bulb;
    }

    public void operate() {
        bulb.turnOn();
    }
}

// Following DIP
interface Switchable {
    void turnOn();
}

class LightBulb implements Switchable {
    public void turnOn() { /* Turn on logic */ }
}

class Switch {
    private Switchable device;

    public Switch(Switchable device) {
        this.device = device;
    }

    public void operate() {
        device.turnOn();
    }
}
```

---

## 3. Creational Patterns

### Singleton Pattern

Ensures that a class has only one instance and provides a global point of access.

**Java Example:**

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() { /* Private constructor */ }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### Factory Pattern

Provides an interface for creating objects but allows subclasses to alter the type of objects created.

**Java Example:**

```java
interface Product {
    void use();
}

class ConcreteProductA implements Product {
    public void use() { System.out.println("Using Product A"); }
}

class ConcreteProductB implements Product {
    public void use() { System.out.println("Using Product B"); }
}

class ProductFactory {
    public Product createProduct(String type) {
        if (type.equals("A")) {
            return new ConcreteProductA();
        } else if (type.equals("B")) {
            return new ConcreteProductB();
        }
        throw new IllegalArgumentException("Unknown product type");
    }
}
```

### Builder Pattern

Separates the construction of a complex object from its representation.

**Java Example:**

```java
class Car {
    private String model;
    private String color;
    private int year;

    public static class Builder {
        private String model;
        private String color;
        private int year;

        public Builder model(String model) {
            this.model = model;
            return this;
        }

        public Builder color(String color) {
            this.color = color;
            return this;
        }

        public Builder year(int year) {
            this.year = year;
            return this;
        }

        public Car build() {
            Car car = new Car();
            car.model = this.model;
            car.color = this.color;
            car.year = this.year;
            return car;
        }
    }
}

public class BuilderPatternExample {
    public static void main(String[] args) {
        Car car = new Car.Builder()
            .model("Toyota")
            .color("Red")
            .year(2024)
            .build();
        System.out.println("Car built: " + car);
    }
}
```

### Prototype Pattern

Creates a new object by copying an existing object.

**Java Example:**

```java
interface Prototype extends Cloneable {
    Prototype clone();
}

class ConcretePrototype implements Prototype {
    private String data;

    public ConcretePrototype(String data) {
        this.data = data;
    }

    @Override
    public Prototype clone() {
        return new ConcretePrototype(this.data);


    }
}

public class PrototypePatternExample {
    public static void main(String[] args) {
        ConcretePrototype original = new ConcretePrototype("Original Data");
        ConcretePrototype copy = (ConcretePrototype) original.clone();
        System.out.println("Copied data: " + copy.data);
    }
}
```

---

## 4. Structural Patterns

### Adapter Pattern

Allows incompatible interfaces to work together.

**Java Example:**

```java
interface Target {
    void request();
}

class Adaptee {
    void specificRequest() { System.out.println("Specific request"); }
}

class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void request() {
        adaptee.specificRequest();
    }
}
```

### Composite Pattern

Allows clients to treat individual objects and compositions uniformly.

**Java Example:**

```java
interface Component {
    void operation();
}

class Leaf implements Component {
    public void operation() {
        System.out.println("Leaf operation");
    }
}

class Composite implements Component {
    private List<Component> children = new ArrayList<>();

    public void add(Component component) {
        children.add(component);
    }

    public void operation() {
        for (Component child : children) {
            child.operation();
        }
    }
}
```

### Decorator Pattern

Allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class.

**Java Example:**

```java
interface Coffee {
    String getDescription();
    double cost();
}

class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple Coffee"; }
    public double cost() { return 1.0; }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
}

class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }

    public double cost() {
        return coffee.cost() + 0.5;
    }
}
```

---

## 5. Behavioral Patterns

### Strategy Pattern

Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

**Java Example:**

```java
interface Strategy {
    int execute(int a, int b);
}

class AddStrategy implements Strategy {
    public int execute(int a, int b) {
        return a + b;
    }
}

class SubtractStrategy implements Strategy {
    public int execute(int a, int b) {
        return a - b;
    }
}

class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public int executeStrategy(int a, int b) {
        return strategy.execute(a, b);
    }
}
```

### Observer Pattern

Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Java Example:**

```java
interface Observer {
    void update(String message);
}

class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    public void update(String message) {
        System.out.println(name + " received message: " + message);
    }
}

class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}
```

### Command Pattern

Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

**Java Example:**

```java
interface Command {
    void execute();
}

class Light {
    public void turnOn() { System.out.println("Light is on"); }
    public void turnOff() { System.out.println("Light is off"); }
}

class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOff();
    }
}

class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}
