### **Part I: Introduction**

1. **Design and Architecture Identification**: 
   - **Exercise**: Choose a software application you use daily (e.g., a mobile app or a web service). Identify and describe its design and architecture. What are its major components and how do they interact?

2. **Value Comparison**:
   - **Exercise**: Create a table comparing two systems—one with good architecture and one with poor architecture. Describe how the architecture affects the system's behavior and maintainability.

### **Part II: Programming Paradigms**

3. **Structured Programming**:
   - **Exercise**: Write a program to calculate the factorial of a number using structured programming principles. Include functions for validation, calculation, and output.

4. **Object-Oriented Programming**:
   - **Exercise**: Design a simple class hierarchy for an online store system. Create classes for `Product`, `Customer`, and `Order`. Implement basic attributes and methods.

5. **Functional Programming**:
   - **Exercise**: Write a functional program that takes a list of numbers, applies a transformation (e.g., square each number), and then calculates the sum of the transformed numbers.

### **Part III: Design Principles**

6. **Single Responsibility Principle (SRP)**:
   - **Exercise**: Refactor a given piece of code that violates SRP. For example, if a class manages both user data and user notifications, split it into separate classes.

7. **Open-Closed Principle (OCP)**:
   - **Exercise**: Modify a system where new features need to be added without altering existing code. For example, extend a basic shape drawing application to support new shapes.

8. **Liskov Substitution Principle (LSP)**:
   - **Exercise**: Identify a scenario where a subclass violates LSP. Refactor the code to ensure that subclasses can replace their base classes without altering expected behavior.

9. **Interface Segregation Principle (ISP)**:
   - **Exercise**: Design an interface for a printer system. Initially, it includes multiple methods (e.g., `print()`, `scan()`, `fax()`). Refactor it into smaller, more focused interfaces.

10. **Dependency Inversion Principle (DIP)**:
    - **Exercise**: Refactor a piece of code where high-level modules depend on low-level modules directly. Use interfaces or abstractions to achieve dependency inversion.

### **Part IV: Component Principles**

11. **Component Design**:
    - **Exercise**: Design a component-based architecture for a blog system. Identify and describe components such as `PostManager`, `CommentManager`, and `UserProfile`.

12. **Component Cohesion**:
    - **Exercise**: Analyze a given codebase for cohesion. Identify and refactor components or classes that have mixed responsibilities or low cohesion.

13. **Component Coupling**:
    - **Exercise**: Create a diagram showing components with low coupling and high cohesion for an inventory management system. Explain how these design choices improve modularity.

### **Part V: Architecture**

14. **Layered Architecture**:
    - **Exercise**: Design a layered architecture for an e-commerce application. Define the layers (e.g., presentation, business logic, data access) and describe their responsibilities and interactions.

15. **Boundaries and Independence**:
    - **Exercise**: Define boundaries for a user authentication system. Describe how you would ensure that the authentication logic is independent from other parts of the application.

16. **Policy and Level**:
    - **Exercise**: Create a policy for handling business rules in an application. Describe how this policy helps in separating different levels of the system (e.g., business logic vs. data access).

17. **Business Rules Implementation**:
    - **Exercise**: Implement business rules for a reservation system. Define entities, use cases, and request/response models that adhere to the business rules.

18. **Screaming Architecture**:
    - **Exercise**: Evaluate the architecture of a given system and assess whether it "screams" its purpose. Propose changes if the architecture does not clearly reflect the system’s main functionality.

19. **Clean Architecture**:
    - **Exercise**: Design a clean architecture for a simple task management application. Identify the core components and how they should interact to adhere to the Dependency Rule.

20. **Service-Oriented Architecture**:
    - **Exercise**: Design a service-oriented architecture for a social media application. Identify services like `UserService`, `PostService`, and `NotificationService`, and describe their responsibilities and interactions.

### **Bonus: Case Study**

21. **Case Study Analysis**:
    - **Exercise**: Analyze a case study of a video sales system (similar to the one described in Chapter 33). Identify key components, dependencies, and architectural decisions. Suggest improvements based on design principles and patterns discussed.
