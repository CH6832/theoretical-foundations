# Software Architecture and Design Principles Exercises

### **Part I: Introduction**

- **Design and Architecture Identification**: Choose a software application you use daily (e.g., a mobile app or a web service). Identify and describe its design and architecture. What are its major components and how do they interact?

- **Value Comparison**: Create a table comparing two systems—one with good architecture and one with poor architecture. Describe how the architecture affects the system's behavior and maintainability.

### **Part II: Programming Paradigms**

- **Structured Programming**: Write a program to calculate the factorial of a number using structured programming principles. Include functions for validation, calculation, and output.

- **Object-Oriented Programming**: Design a simple class hierarchy for an online store system. Create classes for `Product`, `Customer`, and `Order`. Implement basic attributes and methods.

- **Functional Programming**: Write a functional program that takes a list of numbers, applies a transformation (e.g., square each number), and then calculates the sum of the transformed numbers.

### **Part III: Design Principles**

- **Single Responsibility Principle (SRP)**: Refactor a given piece of code that violates SRP. For example, if a class manages both user data and user notifications, split it into separate classes.

- **Open-Closed Principle (OCP)**: Modify a system where new features need to be added without altering existing code. For example, extend a basic shape drawing application to support new shapes.

- **Liskov Substitution Principle (LSP)**: Identify a scenario where a subclass violates LSP. Refactor the code to ensure that subclasses can replace their base classes without altering expected behavior.

- **Interface Segregation Principle (ISP)**: Design an interface for a printer system. Initially, it includes multiple methods (e.g., `print()`, `scan()`, `fax()`). Refactor it into smaller, more focused interfaces.

- **Dependency Inversion Principle (DIP)**: Refactor a piece of code where high-level modules depend on low-level modules directly. Use interfaces or abstractions to achieve dependency inversion.

### **Part IV: Component Principles**

- **Component Design**: Design a component-based architecture for a blog system. Identify and describe components such as `PostManager`, `CommentManager`, and `UserProfile`.

- **Component Cohesion**: Analyze a given codebase for cohesion. Identify and refactor components or classes that have mixed responsibilities or low cohesion.

- **Component Coupling**: Create a diagram showing components with low coupling and high cohesion for an inventory management system. Explain how these design choices improve modularity.

### **Part V: Architecture**

- **Layered Architecture**: Design a layered architecture for an e-commerce application. Define the layers (e.g., presentation, business logic, data access) and describe their responsibilities and interactions.

- **Boundaries and Independence**: Define boundaries for a user authentication system. Describe how you would ensure that the authentication logic is independent from other parts of the application.

- **Policy and Level**: Create a policy for handling business rules in an application. Describe how this policy helps in separating different levels of the system (e.g., business logic vs. data access).

- **Business Rules Implementation**: Implement business rules for a reservation system. Define entities, use cases, and request/response models that adhere to the business rules.

- **Screaming Architecture**: Evaluate the architecture of a given system and assess whether it "screams" its purpose. Propose changes if the architecture does not clearly reflect the system’s main functionality.

- **Clean Architecture**: Design a clean architecture for a simple task management application. Identify the core components and how they should interact to adhere to the Dependency Rule.

- **Service-Oriented Architecture**: Design a service-oriented architecture for a social media application. Identify services like `UserService`, `PostService`, and `NotificationService`, and describe their responsibilities and interactions.

### **Part VI: Advanced Topics**

- **Microservices**: Develop a microservices architecture for an online bookstore. Define services such as `InventoryService`, `OrderService`, and `UserService`, and outline how they communicate.

- **Event-Driven Architecture**: Design an event-driven architecture for a real-time chat application. Describe how events are published, subscribed to, and handled.

- **API Gateway**: Propose an API gateway for a multi-service application. Explain how it handles requests and routes them to the appropriate services.

- **Monitoring and Logging**: Design a monitoring and logging solution for a distributed application. Identify key metrics to track and how logs will be aggregated.

### **Part VII: Case Studies**

- **Case Study Analysis**: Analyze a case study of a video sales system. Identify key components, dependencies, and architectural decisions. Suggest improvements based on design principles and patterns discussed.

- **Refactoring Legacy Systems**: Choose a legacy codebase and propose a plan for refactoring it using modern design patterns. Outline the risks and expected outcomes of the refactoring process.

### **Part VIII: Continuous Improvement**

- **Design Pattern Implementation**: Select a design pattern (e.g., Observer, Strategy) and implement it in a small project. Document the rationale behind choosing this pattern.

- **Code Review Process**: Create a checklist for conducting code reviews focused on design principles and patterns. Use this checklist during a peer review session.

- **Collaborative Design Session**: Organize a collaborative design session to create an architecture diagram for a new application. Document the discussions and decisions made.

- **Feedback Loop Implementation**: Propose a feedback loop for continuous improvement in a software development team. Identify how to gather feedback and measure improvements.

- **Software Development Lifecycle**: Analyze the software development lifecycle of a project you've been involved in. Identify areas for improvement in terms of architecture and design practices.

- **Design Patterns in Real Projects**: Investigate a successful open-source project and identify design patterns used throughout the codebase. Discuss their effectiveness and alternatives.

- **Learning from Failures**: Research a software project that failed due to architectural decisions. Summarize the lessons learned and how they could inform future projects.

- **Cross-Functional Team Collaboration**: Propose strategies for enhancing collaboration between development and operations teams in a DevOps environment, focusing on architectural alignment.

### **Part IX: Research and Development**

- **Emerging Technologies**: Research an emerging technology (e.g., serverless computing, blockchain) and describe how it impacts software architecture. Discuss potential use cases.

- **Designing for Scalability**: Design a scalable architecture for a video streaming service. Describe how you would handle increased traffic and maintain performance.

- **Technical Debt Management**: Create a plan for managing technical debt in an existing codebase. Identify areas of debt and propose actionable steps for remediation.

- **Security Architecture**: Develop a security architecture for a web application. Identify potential vulnerabilities and propose measures to mitigate risks.

### **Part X: Reflection**

- **Personal Growth Reflection**: Reflect on your learning journey regarding software architecture and design principles. Identify key takeaways and how you plan to apply them in future projects.
