## **Software Architecture and Design Patterns**

### **1. Introduction to Software Architecture**

#### **Architectural Styles**

**Monolithic Architecture**: A single, unified application where different modules are interlinked.

**Microservices Architecture**: The application is divided into smaller, loosely coupled services that communicate over a network.

**Service-Oriented Architecture (SOA)**: Similar to microservices but with a focus on reusable services that can be orchestrated to form larger systems.

**Layered Architecture**: Divides the application into layers with specific responsibilities (e.g., presentation, business logic, data access).

**Java Example (Monolithic Architecture)**:
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

**Java Example (Microservices Architecture)**:
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

**Architectural Trade-Offs**

- **Performance**: Monolithic systems can be faster for small applications but may become unmanageable as they grow.
- **Maintainability**: Microservices offer better maintainability by allowing independent development and deployment.
- **Scalability**: Microservices can be scaled individually, while monolithic systems require scaling the entire application.

---

### **2. SOLID Principles**

#### **Single Responsibility Principle (SRP)**

A class should have only one reason to change. It should only have one job or responsibility.

**Java Example:**
```java
// Violating SRP
class Report {
    public void generateReport() {
        // Generate report logic
    }

    public void saveToFile() {
        // Save report logic
    }
}

// Following SRP
class Report {
    public void generateReport() {
        // Generate report logic
    }
}

class ReportSaver {
    public void saveToFile(Report report) {
        // Save report logic
    }
}
```

#### **Open/Closed Principle (OCP)**

Software entities should be open for extension but closed for modification.

**Java Example:**
```java
// Before OCP
class Rectangle {
    private int width;
    private int height;

    public int getWidth() { return width; }
    public int getHeight() { return height; }
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
    private int width;
    private int height;

    public int area() {
        return width * height;
    }
}

class Circle implements Shape {
    private int radius;

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

#### **Liskov Substitution Principle (LSP)**

Subtypes must be substitutable for their base types without altering the correctness of the program.

**Java Example:**
```java
// Violating LSP
class Bird {
    public void fly() {
        // Fly logic
    }
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
    public void fly() {
        // Fly logic
    }
}

class Ostrich {
    // No fly method
}
```

#### **Interface Segregation Principle (ISP)**

Clients should not be forced to depend on interfaces they do not use.

**Java Example:**
```java
// Violating ISP
interface Worker {
    void work();
    void eat();
}

class HumanWorker implements Worker {
    public void work() {
        // Work logic
    }

    public void eat() {
        // Eat logic
    }
}

class RobotWorker implements Worker {
    public void work() {
        // Work logic
    }

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
    public void work() {
        // Work logic
    }

    public void eat() {
        // Eat logic
    }
}

class RobotWorker implements Workable {
    public void work() {
        // Work logic
    }
}
```

#### **Dependency Inversion Principle (DIP)**

Depend on abstractions, not on concrete implementations.

**Java Example:**
```java
// Violating DIP
class LightBulb {
    public void turnOn() {
        // Turn on logic
    }
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
    public void turnOn() {
        // Turn on logic
    }
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

### **3. Creational Patterns**

#### **Singleton Pattern**

Ensures that a class has only one instance and provides a global point of access to it.

**Java Example:**
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

#### **Factory Pattern**

Provides an interface for creating objects but allows subclasses to alter the type of objects that will be created.

**Java Example:**
```java
interface Product {
    void use();
}

class ConcreteProductA implements Product {
    public void use() {
        System.out.println("Using Product A");
    }
}

class ConcreteProductB implements Product {
    public void use() {
        System.out.println("Using Product B");
    }
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

#### **Builder Pattern**

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

#### **Prototype Pattern**

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

    @Override
    public String toString() {
        return "ConcretePrototype{" +
                "data='" + data + '\'' +
                '}';
    }
}
```

---

### **4. Structural Patterns**

#### **Adapter Pattern**

Allows

 incompatible interfaces to work together.

**Java Example:**
```java
// Existing interface
interface OldSystem {
    void oldMethod();
}

// New interface
interface NewSystem {
    void newMethod();
}

// Adapter class
class Adapter implements OldSystem {
    private NewSystem newSystem;

    public Adapter(NewSystem newSystem) {
        this.newSystem = newSystem;
    }

    public void oldMethod() {
        newSystem.newMethod();
    }
}
```

#### **Decorator Pattern**

Adds additional functionality to an object dynamically.

**Java Example:**
```java
interface Coffee {
    String getDescription();
    double cost();
}

class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Simple Coffee";
    }

    public double cost() {
        return 5.0;
    }
}

class MilkDecorator implements Coffee {
    private Coffee coffee;

    public MilkDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }

    public double cost() {
        return coffee.cost() + 2.0;
    }
}

public class DecoratorPatternExample {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        coffee = new MilkDecorator(coffee);
        System.out.println(coffee.getDescription() + " costs " + coffee.cost());
    }
}
```

#### **Proxy Pattern**

Controls access to an object by providing a surrogate.

**Java Example:**
```java
interface Image {
    void display();
}

class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadImageFromDisk();
    }

    private void loadImageFromDisk() {
        System.out.println("Loading " + filename);
    }

    public void display() {
        System.out.println("Displaying " + filename);
    }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}
```

#### **Facade Pattern**

Provides a simplified interface to a complex subsystem.

**Java Example:**
```java
class Computer {
    public void start() {
        System.out.println("Computer started");
    }
}

class Printer {
    public void print() {
        System.out.println("Printing");
    }
}

class ComputerFacade {
    private Computer computer;
    private Printer printer;

    public ComputerFacade() {
        computer = new Computer();
        printer = new Printer();
    }

    public void doWork() {
        computer.start();
        printer.print();
    }
}

public class FacadePatternExample {
    public static void main(String[] args) {
        ComputerFacade facade = new ComputerFacade();
        facade.doWork();
    }
}
```

#### **Composite Pattern**

Allows clients to treat individual objects and composites uniformly.

**Java Example:**
```java
import java.util.ArrayList;
import java.util.List;

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

    public void remove(Component component) {
        children.remove(component);
    }

    public void operation() {
        for (Component child : children) {
            child.operation();
        }
    }
}
```

---

### **5. Behavioral Patterns**

#### **Strategy Pattern**

Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

**Java Example:**
```java
interface Strategy {
    void execute();
}

class ConcreteStrategyA implements Strategy {
    public void execute() {
        System.out.println("Executing Strategy A");
    }
}

class ConcreteStrategyB implements Strategy {
    public void execute() {
        System.out.println("Executing Strategy B");
    }
}

class Context {
    private Strategy strategy;

    public void setStrategy(Strategy strategy) {
        this.strategy = strategy;
    }

    public void executeStrategy() {
        strategy.execute();
    }
}

public class StrategyPatternExample {
    public static void main(String[] args) {
        Context context = new Context();

        context.setStrategy(new ConcreteStrategyA());
        context.executeStrategy();

        context.setStrategy(new ConcreteStrategyB());
        context.executeStrategy();
    }
}
```

#### **Observer Pattern**

Defines a dependency between objects so that when one object changes state, all its dependents are notified.

**Java Example:**
```java
import java.util.ArrayList;
import java.util.List;

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

public class ObserverPatternExample {
    public static void main(String[] args) {
        Subject subject = new Subject();

        Observer observer1 = new ConcreteObserver("Observer 1");
        Observer observer2 = new ConcreteObserver("Observer 2");

        subject.addObserver(observer1);
        subject.addObserver(observer2);

        subject.notifyObservers("Hello Observers!");
    }
}
```

#### **Command Pattern**

Encapsulates a request as an object, thereby allowing parameterization and queuing of requests.

**Java Example:**
```java
interface Command {
    void execute();
}

class Light {
    public void turnOn() {
        System.out.println("Light is ON");
    }

    public void turnOff() {
        System.out.println("Light is OFF");
    }
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

public class CommandPatternExample {
    public static void main(String[] args) {
        Light light = new Light();
        Command lightOn = new LightOnCommand(light);
        Command lightOff = new LightOffCommand(light);

        RemoteControl remote = new RemoteControl();

        remote.setCommand(lightOn);
        remote.pressButton();

        remote.setCommand(lightOff);
        remote.pressButton();
    }
}
```

#### **Chain of Responsibility Pattern**

Passes a request along a chain of handlers.

**Java Example:**
```java
abstract class Handler {
    protected Handler next;

    public void setNext(Handler next) {
        this.next = next;
    }

    public abstract void handleRequest(String request);
}

class ConcreteHandlerA extends Handler {
    public void handleRequest(String request) {
        if (request.equals("A")) {
            System.out.println("Handler A handled request");
        } else if (next != null) {
            next.handleRequest(request);
        }
    }
}

class ConcreteHandlerB extends Handler {
    public void handleRequest(String request) {
        if (request.equals("B")) {
            System.out.println("Handler B handled request");
        } else if (next != null) {
            next.handleRequest(request);
        }
    }
}

public class ChainOfResponsibilityExample {
    public static void main(String[] args) {
        Handler handlerA = new ConcreteHandlerA();
        Handler handlerB = new ConcreteHandlerB();
        handlerA.setNext(handlerB);

        handlerA.handleRequest("A");
        handlerA.handleRequest("B");
    }
}
```

---

### **6. Distributed Systems Design Patterns**

#### **Event-Driven Architecture**

Uses events to trigger and communicate between decoupled services.

**Java Example (Simplified):**
```java
import java.util.ArrayList;
import java.util.List;

interface EventListener {
    void onEvent(String event);
}

class EventPublisher {
    private List<EventListener> listeners = new ArrayList<>();

    public void addListener(EventListener listener) {
        listeners.add(listener);
    }

    public void publishEvent(String event) {
        for (EventListener listener : listeners) {
            listener.onEvent(event);
        }
    }
}

public class EventDrivenArchitectureExample {
    public static void main(String[] args) {
        EventPublisher publisher = new EventPublisher();

        publisher.addListener(event -> System.out.println("Received event: " + event));

        publisher.publishEvent("UserSignedUp");
    }
}
```

#### **Saga Pattern**

Manages long-running transactions and maintains data consistency in distributed systems.

**Java Example (Simplified)**:
```java
// Define Sagas and their steps

class OrderSaga {
    public void execute() {
        // Step 1: Process Order
        // Step 2: Reserve Stock
        // Step 3: Payment
    }
}

public class SagaPatternExample {
    public static void main(String[] args) {
        OrderSaga saga = new OrderSaga();
        saga.execute();
    }
}
```

#### **Circuit Breakers, Retries, Fallbacks**

Manages faults in distributed systems to improve resilience.

**Java Example (Simplified)**:
```java
import java.util.Random;

class Remote

Service {
    public String request() throws Exception {
        if (new Random().nextBoolean()) {
            return "Success";
        } else {
            throw new Exception("Failure");
        }
    }
}

public class CircuitBreakerExample {
    public static void main(String[] args) {
        RemoteService service = new RemoteService();
        int retryCount = 0;
        while (retryCount < 3) {
            try {
                String response = service.request();
                System.out.println(response);
                break;
            } catch (Exception e) {
                retryCount++;
                System.out.println("Retrying... (" + retryCount + ")");
            }
        }
    }
}
```

#### **Scalability and Fault-Tolerance**

Design patterns to handle increased load and system failures.

**Java Example (Simplified)**:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ScalabilityExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(10);
        for (int i = 0; i < 100; i++) {
            executor.submit(() -> {
                // Simulate task
                System.out.println("Task executed by " + Thread.currentThread().getName());
            });
        }
        executor.shutdown();
    }
}
```

---

## **Assessment**

- **Design Pattern Implementation Tasks**: Create implementations of the design patterns discussed.
- **Architecture Design Project**: Design and document a software architecture using the principles and patterns covered.
- **Final Exam**: Test understanding of architectural styles, SOLID principles, and design patterns.

## **Resources**

- **"Design Patterns: Elements of Reusable Object-Oriented Software" by Gamma et al.**
- **"Clean Architecture" by Robert C. Martin**
