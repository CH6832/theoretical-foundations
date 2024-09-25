## **Database Systems and Data Management**

### **1. Advanced Relational Databases**

#### **Query Optimization**

Query optimization involves improving the performance of database queries. The optimizer evaluates different query execution plans to find the most efficient one.

**Key Concepts:**
- **Execution Plans:** How the database executes a query.
- **Cost Estimation:** Evaluates the cost of different execution plans based on I/O, CPU, and memory usage.
- **Indexes:** Speed up query performance by reducing the amount of data scanned.

**Pseudocode Example:**
```plaintext
CONNECT to database

SET query = "SELECT * FROM employees WHERE department = 'Engineering'"

PREPARE statement with query

EXECUTE prepared statement

FOR each row in result set DO
    PRINT row.id, row.name
END FOR

CLOSE connection
```

#### **Transaction Management (ACID)**

ACID (Atomicity, Consistency, Isolation, Durability) properties ensure reliable transaction processing.

- **Atomicity:** Transactions are all-or-nothing.
- **Consistency:** Transactions bring the database from one valid state to another.
- **Isolation:** Transactions occur independently without interference.
- **Durability:** Committed transactions are permanent.

**Pseudocode Example:**
```plaintext
CONNECT to database

BEGIN TRANSACTION

TRY
    INSERT into accounts (id, balance) VALUES (1, 1000.00)
    UPDATE accounts SET balance = balance - 500.00 WHERE id = 2
    COMMIT TRANSACTION
CATCH error
    ROLLBACK TRANSACTION
END TRY

CLOSE connection
```

#### **Indexing and Partitioning Strategies**

Indexes speed up data retrieval. Partitioning divides a table into smaller, more manageable pieces.

**Pseudocode Example:**
```plaintext
CONNECT to database

SET query = "SELECT * FROM employees WHERE last_name = 'Smith'"

PREPARE statement with query

EXECUTE prepared statement

FOR each row in result set DO
    PRINT row.id, row.first_name
END FOR

CLOSE connection
```

---

### **2. NoSQL Databases**

#### **Document-Based (MongoDB)**

MongoDB is a document-based NoSQL database that stores data in flexible, JSON-like documents.

**Pseudocode Example:**
```plaintext
CONNECT to MongoDB at localhost:27017

SELECT database "mydatabase"
SELECT collection "employees"

CREATE document with fields:
    name = "John Doe"
    department = "Engineering"
    salary = 100000

INSERT document into collection

CLOSE connection
```

#### **Key-Value Stores (Redis)**

Redis is an in-memory key-value store used for caching and high-performance data storage.

**Pseudocode Example:**
```plaintext
CONNECT to Redis at localhost

SET "key1" = "value1"
GET "key1" into value

PRINT "Stored value: " + value

CLOSE connection
```

#### **Column-Family Databases (Cassandra)**

Cassandra is a distributed NoSQL database designed for handling large amounts of data across many commodity servers.

**Pseudocode Example:**
```plaintext
CONNECT to Cassandra at 127.0.0.1

USE keyspace "mykeyspace"

INSERT INTO users (userid, username) VALUES (1, 'alice')

CLOSE connection
```

#### **Graph Databases (Neo4j)**

Neo4j is a graph database that uses graph structures for semantic queries.

**Pseudocode Example:**
```plaintext
CONNECT to Neo4j at "bolt://localhost:7687" with credentials

CREATE node "Person" with properties:
    name = "Alice"
    age = 22

CLOSE connection
```

---

### **3. Distributed Databases**

#### **CAP Theorem**

The CAP Theorem states that a distributed database can only guarantee two out of three properties: Consistency, Availability, and Partition Tolerance.

**Explanation:**
- **Consistency:** Every read receives the most recent write.
- **Availability:** Every request receives a response, either success or failure.
- **Partition Tolerance:** The system continues to operate despite network partitions.

#### **Consistency Models**

**Eventual Consistency** is a consistency model used in distributed systems where updates to a distributed system will eventually propagate to all nodes.

#### **Data Replication and Sharding**

**Data Replication** involves copying data across multiple nodes to ensure availability.

**Data Sharding** involves distributing data across multiple servers to manage large datasets and increase performance.

**Pseudocode Example:**
```plaintext
CONNECT to database

FOR each shard in list of shards DO
    CONNECT to shard
    EXECUTE query "SELECT * FROM employees"
    PRINT results
END FOR

CLOSE all connections
```

---

### **4. Data Warehousing and Big Data**

#### **Data Warehousing Architectures**

Data warehousing involves designing architectures to manage and analyze large volumes of data.

**Key Components:**
- **Data Warehouse:** Central repository for integrated data.
- **ETL (Extract, Transform, Load):** Process for extracting data from various sources, transforming it, and loading it into a data warehouse.

#### **ETL Processes**

ETL processes involve extracting data from sources, transforming it to meet business needs, and loading it into a destination database.

**Pseudocode Example:**
```plaintext
CONNECT to source database
CONNECT to destination database

EXTRACT data from source table

FOR each row in extracted data DO
    TRANSFORM data as needed
    INSERT transformed data into destination table
END FOR

CLOSE connections
```

#### **Big Data Processing Frameworks**

**Hadoop** and **Spark** are popular frameworks for processing large datasets.

**Pseudocode Example for Hadoop:**
```plaintext
SET up Hadoop job

DEFINE Mapper function:
    FOR each line in input DO
        SPLIT line into words
        FOR each word DO
            EMIT word and count 1
        END FOR
    END FOR

DEFINE Reducer function:
    FOR each key-value pair DO
        SUM counts for each word
        EMIT word and total count
    END FOR

RUN Hadoop job with input and output paths
```

**Pseudocode Example for Spark:**
```plaintext
INITIALIZE Spark context

READ input file into RDD

TRANSFORM RDD to count words:
    SPLIT lines into words
    MAP each word to (word, 1)
    REDUCE by key to sum counts

WRITE results to output path

CLOSE Spark context
```

---

### **5. Database Security**

#### **Encryption and Access Control**

**Encryption** protects data by encoding it so that only authorized parties can read it.

**Access Control** involves defining permissions for users to access different database objects.

**Pseudocode Example for Encryption:**
```plaintext
GENERATE encryption key

FUNCTION encrypt(data):
    ENCRYPT data using key
    RETURN encrypted data

FUNCTION decrypt(encryptedData):
    DECRYPT encrypted data using key
    RETURN original data

ORIGINAL_DATA = "Sensitive Data"
ENCRYPTED_DATA = encrypt(ORIGINAL_DATA)
DECRYPTED_DATA = decrypt(ENCRYPTED_DATA)

PRINT original, encrypted, decrypted data
```

#### **SQL Injection Prevention**

SQL injection is a security vulnerability that allows attackers to interfere with the queries executed by an application.

**Pseudocode Example for Prevention:**
```plaintext
CONNECT to database

SET query = "SELECT * FROM users WHERE username = ?"

PREPARE statement with query

SET username = user_input
BIND username to prepared statement

EXECUTE prepared statement

FOR each row in result set DO
    PRINT row.id, row.username
END FOR

CLOSE connection
