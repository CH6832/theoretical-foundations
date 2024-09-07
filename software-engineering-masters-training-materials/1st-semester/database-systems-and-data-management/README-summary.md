## **Database Systems and Data Management**

### **1. Advanced Relational Databases**

#### **Query Optimization**

Query optimization involves improving the performance of database queries. The optimizer evaluates different query execution plans to find the most efficient one.

**Key Concepts:**
- **Execution Plans:** How the database executes a query.
- **Cost Estimation:** Evaluates the cost of different execution plans based on I/O, CPU, and memory usage.
- **Indexes:** Speed up query performance by reducing the amount of data scanned.

**Java Code Example:**
For actual query optimization, Java code isn't directly used; instead, SQL and database management systems (DBMS) handle optimization. However, here's a basic example of how you might use JDBC to execute optimized queries.

```java
import java.sql.*;

public class QueryOptimization {
    private Connection connect() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        return DriverManager.getConnection(url, user, password);
    }

    public void executeOptimizedQuery() {
        String query = "SELECT * FROM employees WHERE department = ?";
        try (Connection conn = connect(); PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setString(1, "Engineering");
            ResultSet rs = pstmt.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt("id") + ", " + rs.getString("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

#### **Transaction Management (ACID)**

ACID (Atomicity, Consistency, Isolation, Durability) properties ensure reliable transaction processing.

- **Atomicity:** Transactions are all-or-nothing.
- **Consistency:** Transactions bring the database from one valid state to another.
- **Isolation:** Transactions occur independently without interference.
- **Durability:** Committed transactions are permanent.

**Java Code Example:**
```java
import java.sql.*;

public class TransactionManagement {
    private Connection connect() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        return DriverManager.getConnection(url, user, password);
    }

    public void performTransaction() {
        String insert1 = "INSERT INTO accounts (id, balance) VALUES (?, ?)";
        String insert2 = "UPDATE accounts SET balance = balance - ? WHERE id = ?";

        try (Connection conn = connect()) {
            conn.setAutoCommit(false);
            try (PreparedStatement pstmt1 = conn.prepareStatement(insert1);
                 PreparedStatement pstmt2 = conn.prepareStatement(insert2)) {

                pstmt1.setInt(1, 1);
                pstmt1.setDouble(2, 1000.00);
                pstmt1.executeUpdate();

                pstmt2.setDouble(1, 500.00);
                pstmt2.setInt(2, 2);
                pstmt2.executeUpdate();

                conn.commit();
            } catch (SQLException e) {
                conn.rollback();
                e.printStackTrace();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

#### **Indexing and Partitioning Strategies**

Indexes speed up data retrieval. Partitioning divides a table into smaller, more manageable pieces.

**Java Code Example:**
Indexing and partitioning are typically configured at the DBMS level, not via Java. However, here's how you might interact with an indexed table:

```java
import java.sql.*;

public class IndexingExample {
    private Connection connect() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        return DriverManager.getConnection(url, user, password);
    }

    public void queryWithIndex() {
        String query = "SELECT * FROM employees WHERE last_name = ?";
        try (Connection conn = connect(); PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setString(1, "Smith");
            ResultSet rs = pstmt.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt("id") + ", " + rs.getString("first_name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

### **2. NoSQL Databases**

#### **Document-Based (MongoDB)**

MongoDB is a document-based NoSQL database that stores data in flexible, JSON-like documents.

**Java Code Example:**
```java
import com.mongodb.MongoClient;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import org.bson.Document;

public class MongoDBExample {
    public static void main(String[] args) {
        try (MongoClient mongoClient = new MongoClient("localhost", 27017)) {
            MongoDatabase database = mongoClient.getDatabase("mydatabase");
            MongoCollection<Document> collection = database.getCollection("employees");

            Document doc = new Document("name", "John Doe")
                            .append("department", "Engineering")
                            .append("salary", 100000);
            collection.insertOne(doc);
        }
    }
}
```

#### **Key-Value Stores (Redis)**

Redis is an in-memory key-value store used for caching and high-performance data storage.

**Java Code Example:**
```java
import redis.clients.jedis.Jedis;

public class RedisExample {
    public static void main(String[] args) {
        try (Jedis jedis = new Jedis("localhost")) {
            jedis.set("key1", "value1");
            String value = jedis.get("key1");
            System.out.println("Stored value: " + value);
        }
    }
}
```

#### **Column-Family Databases (Cassandra)**

Cassandra is a distributed NoSQL database designed for handling large amounts of data across many commodity servers.

**Java Code Example:**
```java
import com.datastax.driver.core.Cluster;
import com.datastax.driver.core.Session;

public class CassandraExample {
    public static void main(String[] args) {
        Cluster cluster = Cluster.builder().addContactPoint("127.0.0.1").build();
        try (Session session = cluster.connect("mykeyspace")) {
            session.execute("INSERT INTO users (userid, username) VALUES (1, 'alice')");
        }
        cluster.close();
    }
}
```

#### **Graph Databases (Neo4j)**

Neo4j is a graph database that uses graph structures for semantic queries.

**Java Code Example:**
```java
import org.neo4j.driver.AuthTokens;
import org.neo4j.driver.Driver;
import org.neo4j.driver.GraphDatabase;
import org.neo4j.driver.Session;
import org.neo4j.driver.Transaction;

public class Neo4jExample {
    public static void main(String[] args) {
        Driver driver = GraphDatabase.driver("bolt://localhost:7687", AuthTokens.basic("username", "password"));
        try (Session session = driver.session()) {
            try (Transaction tx = session.beginTransaction()) {
                tx.run("CREATE (a:Person {name: 'Alice', age: 22})");
                tx.commit();
            }
        }
        driver.close();
    }
}
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

**Java Code Example:**
Eventual consistency is more of a conceptual model, not something typically demonstrated with Java code. However, it’s often implemented in NoSQL databases like Cassandra.

#### **Data Replication and Sharding**

**Data Replication** involves copying data across multiple nodes to ensure availability.

**Data Sharding** involves distributing data across multiple servers to manage large datasets and increase performance.

**Java Code Example:**
Sharding and replication are typically managed by the database system, not directly with Java code. Here's how you might connect to a sharded database setup:

```java
import java.sql.*;

public class ShardedDatabaseExample {
    private Connection connectToShard(String shard) throws SQLException {
        String url = "jdbc:mysql://" + shard + "/mydatabase";
        String user = "root";
        String password = "password";
        return DriverManager.getConnection(url, user, password);
    }

    public void queryFromShard(String shard) {
        String query = "SELECT * FROM employees";
        try (Connection conn = connectToShard(shard); PreparedStatement pstmt = conn.prepareStatement(query)) {
            ResultSet rs = pstmt.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt("id") + ", " + rs.getString("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

### **4. Data Warehousing and Big Data**

#### **Data Warehousing Architectures**

Data warehousing involves designing architectures to manage and analyze large volumes of data.

**Key Components:**
- **Data Warehouse:** Central repository for integrated data.
- **ETL (Extract, Transform, Load):** Process for extracting data from various sources, transforming it, and loading it into a data warehouse.

#### **ETL Processes**

ETL processes involve extracting data from sources, transforming it to meet business needs

, and loading it into a destination database.

**Java Code Example:**
```java
import java.sql.*;

public class ETLProcess {
    public void extractTransformLoad() {
        String sourceUrl = "jdbc:mysql://localhost:3306/source_db";
        String destinationUrl = "jdbc:mysql://localhost:3306/destination_db";
        String extractQuery = "SELECT * FROM source_table";
        String insertQuery = "INSERT INTO destination_table (col1, col2) VALUES (?, ?)";

        try (Connection sourceConn = DriverManager.getConnection(sourceUrl, "user", "password");
             Connection destConn = DriverManager.getConnection(destinationUrl, "user", "password");
             Statement stmt = sourceConn.createStatement();
             ResultSet rs = stmt.executeQuery(extractQuery);
             PreparedStatement pstmt = destConn.prepareStatement(insertQuery)) {

            while (rs.next()) {
                pstmt.setString(1, rs.getString("col1"));
                pstmt.setString(2, rs.getString("col2"));
                pstmt.executeUpdate();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

#### **Big Data Processing Frameworks**

**Hadoop** and **Spark** are popular frameworks for processing large datasets.

**Java Code Example for Hadoop:**
```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCount {
    public static class TokenizerMapper extends Mapper<Object, Text, Text, IntWritable> {
        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
            String[] words = value.toString().split("\\s+");
            for (String str : words) {
                word.set(str);
                context.write(word, one);
            }
        }
    }

    public static class IntSumReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

**Java Code Example for Spark:**
```java
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.api.java.function.Function2;
import org.apache.spark.SparkConf;
import scala.Tuple2;

public class SparkWordCount {
    public static void main(String[] args) {
        SparkConf conf = new SparkConf().setAppName("WordCount").setMaster("local");
        JavaSparkContext sc = new JavaSparkContext(conf);

        JavaPairRDD<String, Integer> counts = sc.textFile("input.txt")
            .flatMap(line -> Arrays.asList(line.split(" ")).iterator())
            .mapToPair(word -> new Tuple2<>(word, 1))
            .reduceByKey((i1, i2) -> i1 + i2);

        counts.saveAsTextFile("output");
        sc.close();
    }
}
```

---

### **5. Database Security**

#### **Encryption and Access Control**

**Encryption** protects data by encoding it so that only authorized parties can read it.

**Access Control** involves defining permissions for users to access different database objects.

**Java Code Example for Encryption:**
```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.util.Base64;

public class EncryptionExample {
    private static final String ALGORITHM = "AES";

    public static String encrypt(String data, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        cipher.init(Cipher.ENCRYPT_MODE, key);
        byte[] encrypted = cipher.doFinal(data.getBytes());
        return Base64.getEncoder().encodeToString(encrypted);
    }

    public static String decrypt(String encryptedData, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance(ALGORITHM);
        cipher.init(Cipher.DECRYPT_MODE, key);
        byte[] decoded = Base64.getDecoder().decode(encryptedData);
        byte[] decrypted = cipher.doFinal(decoded);
        return new String(decrypted);
    }

    public static void main(String[] args) throws Exception {
        KeyGenerator keyGen = KeyGenerator.getInstance(ALGORITHM);
        SecretKey key = keyGen.generateKey();

        String originalData = "Sensitive Data";
        String encryptedData = encrypt(originalData, key);
        String decryptedData = decrypt(encryptedData, key);

        System.out.println("Original: " + originalData);
        System.out.println("Encrypted: " + encryptedData);
        System.out.println("Decrypted: " + decryptedData);
    }
}
```

#### **SQL Injection Prevention**

SQL injection is a security vulnerability that allows attackers to interfere with the queries executed by an application.

**Java Code Example for Prevention:**
Using prepared statements helps prevent SQL injection by separating SQL code from data.

```java
import java.sql.*;

public class SQLInjectionPrevention {
    private Connection connect() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";
        return DriverManager.getConnection(url, user, password);
    }

    public void safeQuery(String username) {
        String query = "SELECT * FROM users WHERE username = ?";
        try (Connection conn = connect(); PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setString(1, username);
            ResultSet rs = pstmt.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt("id") + ", " + rs.getString("username"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
