# Distributed Systems

## Course Overview
This course covers fundamental concepts and practical aspects of distributed systems, including system design, communication protocols, consensus algorithms, fault tolerance, and security. Students will gain hands-on experience with distributed frameworks and technologies.

## Course Content

### **1. Introduction to Distributed Systems**

#### **Models and Assumptions**
- **Distributed System Models**: Shared Memory, Message Passing.
- **Assumptions**: Network reliability, node failures, latency.

#### **Message-Passing vs Shared Memory**
- **Message-Passing**: Processes communicate by sending and receiving messages.
- **Shared Memory**: Processes communicate by reading from and writing to a shared memory space.

**Pseudocode Example (Message Passing with Sockets - Server):**
```
START Server
    CREATE ServerSocket at port 1234
    WAIT for client connection
    ACCEPT client connection
    READ message from client
    PRINT "Received: " + message
    SEND "Message received" to client
END Server
```

**Pseudocode Example (Message Passing with Sockets - Client):**
```
START Client
    CREATE Socket to "localhost" at port 1234
    SEND "Hello, Server!" to server
    READ response from server
    PRINT "Server says: " + response
END Client
```

#### **Client-Server and Peer-to-Peer Architectures**
- **Client-Server**: Centralized server providing resources to clients.
- **Peer-to-Peer (P2P)**: Decentralized network where each node (peer) can act as both client and server.

**Practical Exercise:**
- **Build a Simple Client-Server Application** using sockets.

### **2. Consensus Algorithms**

#### **Leader Election**
- **Goal**: Elect a leader among distributed nodes for coordination.

**Pseudocode Example (Leader Election - Simplified):**
```
START LeaderElection
    nodeId = RANDOM integer between 0 and 100
    leaderId = FIND_LEADER(nodeId, [1, 2, 3, 4, 5])
    PRINT "Leader ID: " + leaderId

FUNCTION FIND_LEADER(nodeId, nodeIds)
    leader = nodeId
    FOR each id IN nodeIds
        IF id > leader THEN
            leader = id
    RETURN leader
END LeaderElection
```

#### **Paxos, Raft, Byzantine Fault Tolerance (BFT)**
- **Paxos**: Algorithm for achieving consensus in a network of unreliable processors.
- **Raft**: Simplified consensus algorithm for managing a replicated log.
- **Byzantine Fault Tolerance (BFT)**: Consensus algorithm that can handle nodes behaving maliciously.

**Practical Exercise:**
- **Implement a Simplified Raft Protocol** or use a library to understand consensus in action.

### **3. Distributed Data Storage**

#### **Consistency Models**
- **Strong Consistency**: All nodes see the same data at the same time.
- **Eventual Consistency**: Data will eventually be consistent across nodes.

#### **Distributed Hash Tables (DHT)**
- **DHT**: Data is distributed across nodes using a hash function.

**Pseudocode Example (Simple DHT Implementation):**
```
CLASS DHT
    FUNCTION INIT()
        table = {}

    FUNCTION PUT(key, value)
        table[key] = value

    FUNCTION GET(key)
        RETURN table[key] IF key EXISTS ELSE "Not Found"
END DHT

dht = NEW DHT()
dht.PUT("key1", "value1")
PRINT dht.GET("key1")
```

#### **Data Replication and Consistency Protocols**
- **Quorum-based Replication**: Ensures that a certain number of replicas agree before a write is considered successful.

**Practical Exercise:**
- **Implement a Simple Quorum-based Replication System** using a language of your choice.

### **4. Fault Tolerance and Reliability**

#### **Failover Techniques**
- **Failover**: Switching to a backup system or node when the primary one fails.

**Pseudocode Example (Failover Simulation):**
```
START FailoverExample
    PRINT "Primary server running..."
    RAISE Exception "Primary server failed"
    CATCH Exception e
        PRINT "Switching to backup server..."
END FailoverExample
```

#### **Partition Tolerance, Load Balancing**
- **Partition Tolerance**: System's ability to continue functioning despite network partitioning.
- **Load Balancing**: Distributing load across multiple servers to ensure no single server is overwhelmed.

**Practical Exercise:**
- **Set Up a Load Balancer** using a cloud provider or open-source tool (e.g., HAProxy).

### **5. Security in Distributed Systems**

#### **Secure Communication**
- **TLS (Transport Layer Security)**: Ensures secure communication over the network.
- **SSL (Secure Sockets Layer)**: Legacy protocol for secure communication.

**Pseudocode Example (Secure Socket Communication - Server):**
```
START SecureServer
    LOAD KeyStore from "keystore.jks" with password "password"
    INITIALIZE KeyManagerFactory with KeyStore
    CREATE SSLContext with KeyManagerFactory
    CREATE SSLServerSocket at port 1234
    WAIT for secure client connection
    ACCEPT secure client connection
    READ message from client
    PRINT "Received: " + message
    SEND "Message received securely" to client
END SecureServer
```

#### **Distributed Authentication and Authorization**
- **OAuth**: Authorization framework for securing APIs.
- **JWT (JSON Web Tokens)**: Standard for securely transmitting information between parties.

**Practical Exercise:**
- **Implement OAuth Authentication** for a web application.

---

## **Assessment**

- **Distributed Systems Design Project**: Design and implement a distributed system addressing key principles and practices.
- **Midterm and Final Exams**: Test understanding of distributed system concepts and techniques.
- **Lab Assignments**: Use frameworks like Apache Kafka and Zookeeper to build distributed applications and manage coordination.

## **Resources**

- **"Distributed Systems: Principles and Paradigms" by Andrew Tanenbaum**
- **Research Papers**: On consensus algorithms and distributed storage systems.
