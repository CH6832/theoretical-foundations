> This is a sumamr yof the following book
>
> https://vowi.fsinf.at/images/b/bc/TU_Wien-Verteilte_Systeme_VO_%28G%C3%B6schka%29_-_Tannenbaum-distributed_systems_principles_and_paradigms_2nd_edition.pdf

### 2.4 Self-Management in Distributed Systems

#### 2.4.1 The Feedback Control Model
- **Explanation**: The Feedback Control Model in distributed systems revolves around the system's ability to monitor its own performance and take corrective action to maintain desired operational conditions. This is based on the principle of feedback, where the system observes its current state and compares it to a target state, adjusting its behavior accordingly.
- **Real-World Example**: In cloud computing, systems like **Amazon Web Services (AWS) Auto Scaling** use feedback control to automatically increase or decrease the number of instances running an application based on real-time demand (CPU utilization, memory usage). If the load increases, the system adds more instances, and if it decreases, it removes unnecessary instances.

#### 2.4.2 Example: Systems Monitoring with Astrolabe
- **Explanation**: **Astrolabe** is a tool for decentralized monitoring, management, and data aggregation across a distributed system. It uses a hierarchical architecture to provide summaries of system health and resource usage in large-scale environments.
- **Real-World Example**: Imagine a global content delivery network (CDN) that spans many geographical locations. Astrolabe could monitor the health of servers across continents, collecting statistics like bandwidth usage and response times. Based on this data, the system could automatically reroute traffic or replicate content to servers that are underutilized, optimizing overall system performance.

#### 2.4.3 Example: Differentiating Replication Strategies in Globule
- **Explanation**: **Globule** is a platform that supports adaptive replication of web content across distributed servers. Different replication strategies are used to balance load, improve reliability, and optimize performance.
- **Real-World Example**: Consider a news website with users from around the world. Using a system like Globule, the content could be replicated to servers closer to users geographically. For example, if a user in Asia requests content, the system could serve it from a server located in Singapore rather than from the primary server in the U.S., reducing latency and improving load times.

#### 2.4.4 Example: Automatic Component Repair Management in Jade
- **Explanation**: **Jade** is a middleware that focuses on the self-repair of components in distributed systems. It monitors system components and automatically replaces or restarts them if they fail, ensuring continuous operation.
- **Real-World Example**: In a microservices architecture, when a container (e.g., a service running in Docker) crashes, **Kubernetes** (a container orchestration platform) can be used similarly to Jade, automatically restarting the failed container or spinning up new instances to ensure uninterrupted service.

---

### 3 Processes

#### 3.1 Threads

##### 3.1.1 Introduction to Threads
- **Explanation**: Threads are smaller units of execution within a process. They allow a program to perform multiple tasks at the same time. In distributed systems, threads are used to manage multiple connections or tasks concurrently, which is crucial for scalability and performance.
- **Real-World Example**: A web server like **Apache** uses threads to handle multiple client requests simultaneously. Each thread handles an independent client request, allowing the server to respond to many users without waiting for one request to complete before starting another.

##### 3.1.2 Threads in Distributed Systems
- **Explanation**: Threads in distributed systems allow tasks to be split and processed across multiple nodes, which is key for parallel computing. This can dramatically improve the speed and efficiency of data processing.
- **Real-World Example**: In a distributed computing framework like **Apache Spark**, threads are used to parallelize data processing tasks across a cluster of computers. For example, when processing large datasets for machine learning, each thread might handle a different partition of data, speeding up computation significantly.

#### 3.2 Virtualization

##### 3.2.1 The Role of Virtualization in Distributed Systems
- **Explanation**: Virtualization enables the creation of virtual machines (VMs), where multiple operating systems or applications can run on the same physical hardware. This increases resource utilization, flexibility, and isolation in distributed systems.
- **Real-World Example**: **Amazon EC2** (Elastic Compute Cloud) is built on virtualization technology, allowing users to run multiple instances (virtual machines) on shared physical infrastructure. This means that one physical server could host multiple virtual servers, each running different applications, allowing cloud providers to maximize resource efficiency.

##### 3.2.2 Architectures of Virtual Machines
- **Explanation**: VM architectures can be classified into full virtualization (where each VM operates as a complete system) and paravirtualization (where the VMs are aware of each other and share some resources).
- **Real-World Example**: **VMware** provides full virtualization, allowing companies to run different operating systems (Windows, Linux) on the same server for development, testing, or production environments without any interference between the systems.

#### 3.3 Clients

##### 3.3.1 Networked User Interfaces
- **Explanation**: Networked User Interfaces are the front end that interacts with users in a distributed system, typically over a network. They serve as the bridge between users and the system.
- **Real-World Example**: A web browser, such as **Google Chrome**, serves as a networked user interface. It allows users to access distributed web services (like Gmail or YouTube), sending requests and displaying results from servers spread across the globe.

##### 3.3.2 Client-Side Software for Distribution Transparency
- **Explanation**: Client-side software hides the complexity of the underlying distributed system from the user. It makes remote resources and operations appear local, providing distribution transparency.
- **Real-World Example**: **Dropbox** provides an interface where users can manage files locally on their device, but behind the scenes, the files are stored and replicated across multiple data centers globally. Users are unaware of this complexity and simply see Dropbox as a folder on their computer.

---

### 3.4 Servers

#### 3.4.1 General Design Issues
- **Explanation**: Servers in distributed systems must be designed to handle concurrency, manage state, and ensure reliability. A server must efficiently handle multiple client requests, manage resources, and ensure availability.
- **Real-World Example**: A social media platform like **Facebook** uses thousands of servers globally to handle millions of concurrent users. Each server must manage multiple requests simultaneously, store data, and ensure that user posts and updates are synchronized in real-time.

#### 3.4.2 Server Clusters
- **Explanation**: A server cluster is a group of servers that work together to improve performance, scalability, and fault tolerance. The system distributes requests across the cluster to ensure no single server is overwhelmed.
- **Real-World Example**: **Google Search** uses a massive server cluster to distribute search queries. The requests are balanced across many servers to ensure fast response times, even under heavy load. If one server fails, another takes its place without users noticing.

#### 3.4.3 Managing Server Clusters
- **Explanation**: Managing server clusters involves ensuring that the load is balanced, failures are handled, and resources are allocated efficiently. Modern systems also use monitoring tools and automation for management.
- **Real-World Example**: **Kubernetes** is widely used to manage server clusters in a cloud environment. It automates tasks like load balancing, scaling applications up or down, and handling the recovery of failed nodes or services, ensuring high availability and performance.

---

### 3.5 Code Migration

#### 3.5.1 Approaches to Code Migration
- **Explanation**: Code migration involves moving software components or programs from one node in a distributed system to another. This can be done to optimize resource use or for load balancing.
- **Real-World Example**: A **Java applet** is a classic example where code is sent from a web server to a client’s browser for execution. Modern examples include serverless computing platforms like **AWS Lambda**, where code is automatically deployed to different regions based on user proximity to ensure low latency.

#### 3.5.2 Migration and Local Resources
- **Explanation**: Migrating code often requires access to local resources, such as files or databases, on the node where the code will execute. Managing access to these resources can be challenging, especially when the source and destination environments are different.
- **Real-World Example**: In cloud environments, an application might migrate between data centers. For instance, if an app migrates from AWS Europe to AWS North America, it must still access a shared database, requiring careful handling of network latencies and data consistency.

#### 3.5.3 Migration in Heterogeneous Systems
- **Explanation**: Heterogeneous systems are environments where different hardware, operating systems, or middleware exist. Code migration between these systems is complex because the migrated code needs to adapt to the new environment.
- **Real-World Example**: **Docker** allows developers to package applications with all dependencies, ensuring that the application can run in any environment (Linux, Windows) without changes, simplifying migration between heterogeneous systems.
