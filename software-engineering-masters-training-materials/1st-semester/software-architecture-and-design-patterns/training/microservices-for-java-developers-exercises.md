> The exercises I worked through are based on the following book:
> [Microservices for Java Developers - A Hands-On Introduction to Frameworks & Containers](https://pepa.holla.cz/wp-content/uploads/2016/10/microservices-for-java-developers.pdf)

## Microservices Fundamentals

### Defining Microservices
**Q:** Define microservices and explain the benefits of using microservices architecture over monolithic architecture.  
**A:** Microservices are a software architecture style where an application is composed of small, independent services that communicate over well-defined APIs. Benefits include:
- **Scalability:** Services can be scaled independently.
- **Flexibility:** Different services can use different tech stacks.
- **Resilience:** Fault isolation ensures one service failure doesn’t bring down the whole system.
- **Faster Development Cycles:** Teams can work on different services simultaneously.

### Self-contained Systems (SCS)
**Q:** Explain what is meant by Self-contained Systems (SCS) in a microservices architecture.  
**A:** SCS is an architectural pattern where each microservice contains everything it needs to run independently, including the database and user interface, promoting decoupling and high autonomy.

### Micro and Macro Architecture
**Q:** Differentiate between micro and macro architecture in the context of microservices.  
**A:** 
- **Micro-architecture:** Involves decisions within individual services, such as frameworks, languages, or databases used.
- **Macro-architecture:** Refers to system-wide decisions like service discovery mechanisms and communication protocols (e.g., REST vs. gRPC).

## Technology Stacks

### Docker in Microservices
**Q:** How does Docker simplify deploying microservices? Write a `Dockerfile` for a simple Java Spring Boot application.  
**A:** Docker allows microservices to be packaged with all their dependencies. Here’s a sample `Dockerfile`:

```dockerfile
FROM openjdk:11-jre-slim
COPY target/myapp.jar /usr/app/
WORKDIR /usr/app
CMD ["java", "-jar", "myapp.jar"]
```

### Frontend Integration via Links
**Q:** Implement a basic microservices-based frontend integration where one service loads links from another using JavaScript and REST APIs.  
**A:** Use a simple frontend with JavaScript to fetch dynamic content from a microservice:

```html
<script>
  fetch('/api/service1').then(response => response.json()).then(data => {
    document.getElementById('content').innerHTML = data.content;
  });
</script>
```

### Server-Side Integration with Edge Side Includes (ESI)
**Q:** What is ESI, and how can it help in integrating server-side microservices? Create a basic example using Varnish as a cache server.  
**A:** ESI allows for fragment-based web page composition at the caching layer. Here’s a basic Varnish ESI setup:

```vcl
sub vcl_backend_response {
  if (beresp.status == 200) {
    set beresp.do_esi = true;
  }
}
```

### Asynchronous Microservices with Apache Kafka
**Q:** Design a simple microservice system where services communicate asynchronously using Kafka. Write the Java code to produce and consume messages in Kafka.  
**A:**
**Producer:**
```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

Producer<String, String> producer = new KafkaProducer<>(props);
producer.send(new ProducerRecord<>("my-topic", "key", "value"));
producer.close();
```
**Consumer:**
```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "test-group");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Collections.singletonList("my-topic"));
while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        System.out.println(record.value());
    }
}
```

### Synchronous Microservices with Netflix Stack
**Q:** Implement a basic Netflix Eureka service discovery mechanism in a Spring Boot application.  
**A:**
```java
@EnableEurekaServer
@SpringBootApplication
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```
In your `application.properties`:
```
server.port=8761
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

### Service Discovery with Consul
**Q:** Set up service discovery using Consul in Java. Implement a basic registration and discovery script.  
**A:**
```java
import org.consul.Consul;

Consul consul = Consul.builder().build();

// Register a service
consul.agentService().register("my-service", "service_1", 5000);

// Discover services
Map<String, Service> services = consul.agentService().getAll();
System.out.println(services);
```

### Kubernetes for Docker Containers
**Q:** Deploy a Docker-based microservice to Kubernetes. Write the Kubernetes `Deployment` YAML file for a microservice.  
**A:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-service
  template:
    metadata:
      labels:
        app: my-service
    spec:
      containers:
      - name: my-service-container
        image: my-docker-image
        ports:
        - containerPort: 8080
```

### Migration from Monolithic to Microservices Architecture
**Q:** Design a plan for migrating a monolithic application to a microservices architecture. What factors need to be considered?  
**A:**
- **Identify Boundaries:** Break the monolith into functional modules.
- **Strangler Pattern:** Gradually replace monolith functions with microservices.
- **Database Migration:** Ensure each microservice has its database or well-defined data ownership.
- **Service Communication:** Define API interfaces for each service (REST, gRPC).
- **DevOps Setup:** Deploy microservices using Docker and Kubernetes.

## Monitoring and Observability

### Monitoring with Prometheus
**Q:** Set up Prometheus monitoring for a Java Spring Boot microservice.  
**A:** Add the following dependency in `pom.xml`:

```xml
<dependency>
  <groupId>io.micrometer</groupId>
  <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```
Expose Prometheus metrics:
```java
import io.micrometer.core.annotation.Timed;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {
    @Timed
    @GetMapping("/metrics")
    public String getMetrics() {
        return "Metrics";
    }
}
```

### Log Analysis with Elastic Stack
**Q:** Write a guide to integrate Spring Boot with the Elastic Stack for log analysis.  
**A:**
1. Set up an ELK stack (ElasticSearch, Logstash, and Kibana).
2. Configure Logback to send logs to Logstash using `logback.xml`:

```xml
<appender name="logstash" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
    <destination>localhost:5000</destination>
</appender>
```

### Tracing with Zipkin
**Q:** Add distributed tracing to a Spring Boot microservice using Zipkin.  
**A:** Add the following dependency:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```
Configure the tracing endpoint in `application.properties`:
```
spring.zipkin.base-url=http://localhost:9411
```

### Fault Tolerance with Hystrix
**Q:** Implement a basic circuit breaker using Hystrix in a Java microservice.  
**A:**
```java
@HystrixCommand(fallbackMethod = "fallback")
public String getData() {
    return restTemplate.getForObject("http://some-service/api", String.class);
}

public String fallback() {
    return "Fallback response";
}
```

### API Gateway with Zuul
**Q:** Implement an API gateway for your microservices using Zuul in Spring Boot.  
**A:** Add the following dependency:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>
```
Enable Zuul with:
```java
@EnableZuulProxy
@SpringBootApplication
public class ZuulGatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(ZuulGatewayApplication.class, args);
    }
}
```

## Security and Resilience

### Data Consistency with Sagas
**Q:** Design a distributed transaction using the Saga

 pattern. Provide a Java example for a simple workflow.  
**A:** Use a simple orchestration approach where each service calls the next:

```java
public class OrderService {
    public void placeOrder(Order order) {
        // Call Inventory service
        inventoryService.reserveInventory(order);
        // Call Payment service
        paymentService.processPayment(order);
        // Commit transaction
    }
}
```

### OAuth2 Authentication
**Q:** Implement OAuth2 authentication in a Spring Boot microservice.  
**A:** Add the Spring Security OAuth2 dependency:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```
Configure security in `application.properties`:
```
spring.security.oauth2.client.registration.my-client.client-id=my-id
spring.security.oauth2.client.registration.my-client.client-secret=my-secret
```

### Rate Limiting with Bucket4j
**Q:** Implement rate limiting using Bucket4j in a Java microservice.  
**A:**
```java
Bucket bucket = Bucket.builder()
        .addLimit(Bandwidth.simple(10, Duration.ofMinutes(1)))
        .build();

if (bucket.tryConsume(1)) {
    // Process request
}
```

### API Key Management
**Q:** Design a simple API key management system for securing your microservices.  
**A:** Implement a `Filter` that checks for API keys in the request header:

```java
public class ApiKeyFilter extends OncePerRequestFilter {
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) {
        String apiKey = request.getHeader("X-API-KEY");
        if (!isValid(apiKey)) {
            response.sendError(HttpServletResponse.SC_UNAUTHORIZED);
            return;
        }
        filterChain.doFilter(request, response);
    }
}
```

### CORS Configuration
**Q:** How do you configure CORS in a Spring Boot microservice?  
**A:** Add a CORS configuration class:
```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**").allowedOrigins("http://example.com");
    }
}
```

## Advanced Topics

### Service Mesh with Istio
**Q:** What is Istio and how does it improve microservices management?  
**A:** Istio is a service mesh that provides traffic management, security, and observability for microservices. It allows developers to focus on writing code without worrying about the underlying network complexity.

### GraphQL in Microservices
**Q:** How to implement GraphQL in a Java microservice?  
**A:** Add the following dependencies to your `pom.xml`:
```xml
<dependency>
    <groupId>com.graphql-java-kickstart</groupId>
    <artifactId>graphql-spring-boot-starter</artifactId>
</dependency>
```
Define a simple GraphQL endpoint:
```java
@Component
public class Query implements GraphQLQueryResolver {
    public String hello() {
        return "Hello, GraphQL!";
    }
}
```

### Event-Driven Microservices
**Q:** What are event-driven microservices and how can they be implemented in Java?  
**A:** Event-driven microservices communicate by emitting and reacting to events. Use libraries like Spring Cloud Stream to simplify event handling:

```java
@EnableBinding(Processor.class)
public class EventPublisher {
    @Autowired
    private MessageChannel output;

    public void publishEvent(String event) {
        output.send(MessageBuilder.withPayload(event).build());
    }
}
```

### Container Orchestration with Kubernetes
**Q:** Explain the role of Kubernetes in managing microservices and write a simple command to deploy an application.  
**A:** Kubernetes automates deployment, scaling, and management of containerized applications. Use the following command to deploy:

```bash
kubectl apply -f deployment.yaml
```

### API Documentation with Swagger
**Q:** How to add Swagger documentation to a Spring Boot microservice?  
**A:** Add the following dependency:
```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
```
Configure Swagger in your application:
```java
@EnableSwagger2
@Configuration
public class SwaggerConfig {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2).select().paths(PathSelectors.any()).build();
    }
}
```
