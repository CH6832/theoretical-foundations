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

**Java Example (Message Passing with Sockets):**
```java
import java.io.*;
import java.net.*;

public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(1234);
        Socket socket = serverSocket.accept();
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        String message = in.readLine();
        System.out.println("Received: " + message);
        out.println("Message received");
    }
}
```

**Java Example (Message Passing with Sockets - Client):**
```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 1234);
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        out.println("Hello, Server!");
        System.out.println("Server says: " + in.readLine());
    }
}
```

#### **Client-Server and Peer-to-Peer Architectures**
- **Client-Server**: Centralized server providing resources to clients.
- **Peer-to-Peer (P2P)**: Decentralized network where each node (peer) can act as both client and server.

**Practical Exercise:**
- **Build a Simple Client-Server Application** using Java sockets.

### **2. Consensus Algorithms**

#### **Leader Election**
- **Goal**: Elect a leader among distributed nodes for coordination.

**Java Example (Leader Election - Simplified):**
```java
import java.util.Random;

public class LeaderElection {
    public static void main(String[] args) {
        int id = new Random().nextInt(100);
        int leaderId = findLeader(id, new int[]{1, 2, 3, 4, 5});
        System.out.println("Leader ID: " + leaderId);
    }

    static int findLeader(int nodeId, int[] nodeIds) {
        int leader = nodeId;
        for (int id : nodeIds) {
            if (id > leader) leader = id;
        }
        return leader;
    }
}
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

**Python Example (Simple DHT Implementation):**
```python
class DHT:
    def __init__(self):
        self.table = {}

    def put(self, key, value):
        self.table[key] = value

    def get(self, key):
        return self.table.get(key, "Not Found")

dht = DHT()
dht.put("key1", "value1")
print(dht.get("key1"))
```

#### **Data Replication and Consistency Protocols**
- **Quorum-based Replication**: Ensures that a certain number of replicas agree before a write is considered successful.

**Practical Exercise:**
- **Implement a Simple Quorum-based Replication System** using Python or Java.

### **4. Fault Tolerance and Reliability**

#### **Failover Techniques**
- **Failover**: Switching to a backup system or node when the primary one fails.

**Java Example (Failover Simulation):**
```java
public class FailoverExample {
    public static void main(String[] args) {
        try {
            System.out.println("Primary server running...");
            throw new Exception("Primary server failed");
        } catch (Exception e) {
            System.out.println("Switching to backup server...");
        }
    }
}
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

**Java Example (Secure Socket Communication):**
```java
import javax.net.ssl.*;
import java.io.*;
import java.security.KeyStore;

public class SecureServer {
    public static void main(String[] args) throws Exception {
        KeyStore keyStore = KeyStore.getInstance("JKS");
        keyStore.load(new FileInputStream("keystore.jks"), "password".toCharArray());

        KeyManagerFactory keyManagerFactory = KeyManagerFactory.getInstance("SunX509");
        keyManagerFactory.init(keyStore, "password".toCharArray());

        SSLContext sslContext = SSLContext.getInstance("TLS");
        sslContext.init(keyManagerFactory.getKeyManagers(), null, null);

        SSLServerSocketFactory serverSocketFactory = sslContext.getServerSocketFactory();
        SSLServerSocket serverSocket = (SSLServerSocket) serverSocketFactory.createServerSocket(1234);
        SSLSocket socket = (SSLSocket) serverSocket.accept();
        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        String message = in.readLine();
        System.out.println("Received: " + message);
        out.println("Message received securely");
    }
}
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
