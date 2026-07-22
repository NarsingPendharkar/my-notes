
<<<<<<< HEAD
**Java 11** was released in **September 2018** and is an **LTS (Long-Term Support)** version. Many enterprise applications still run on Java 11 because of its stability, long support cycle, and important productivity enhancements. Java 11 introduced features that simplify coding, improve HTTP communication, enhance string handling, and improve JVM performance.

### 1. Local Variable Syntax for Lambda Parameters

Before Java 11, you could not use `var` in lambda parameters consistently.

##### Before

```java
BiFunction<String, String, String> fullName =
        (firstName, lastName) -> firstName + " " + lastName;
```

##### Java 11

```java
BiFunction<String, String, String> fullName =
        (var firstName, var lastName) -> firstName + " " + lastName;
```

##### Why Use It?

Useful when applying annotations.

```java
(var name, var age) -> System.out.println(name);
```

***

### 2. New HTTP Client API (Standard)

One of the most important Java 11 features.

Before Java 11 developers used:

* HttpURLConnection
* Apache HttpClient
* OkHttp

Java 11 introduced a modern HTTP Client API supporting:

* HTTP/1.1
* HTTP/2
* Asynchronous calls
* WebSockets

##### Simple GET Request

```java
HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
        .uri(URI.create("https://api.example.com"))
        .build();

HttpResponse<String> response =
        client.send(request,
                HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

##### Async Request

```java
client.sendAsync(request,
        HttpResponse.BodyHandlers.ofString())
      .thenApply(HttpResponse::body)
      .thenAccept(System.out::println);
```

##### Interview Question

**Why use Java 11 HttpClient?**

Answer:

* Built into JDK
* Supports HTTP/2
* Supports asynchronous programming
* Better API than HttpURLConnection

***

### 3. String Methods

Java 11 introduced several useful String methods.

***

**3.1 isBlank()**

Checks whether a string contains only whitespaces.

##### Before

```java
str.trim().isEmpty();
```

##### Java 11

```java
String str = "    ";

System.out.println(str.isBlank());
```

Output:

```text
true
```

***

** 3.2 lines()**

Converts multi-line text into Stream<String>.

```java
String text = """
Java
Spring
Angular
""";

text.lines()
    .forEach(System.out::println);
```

Output:

```text
Java
Spring
Angular
```

***

** 3.3 strip()**

Unicode-aware trim.

##### Before

```java
str.trim();
```

##### Java 11

```java
String text = "   Hello Java  ";

System.out.println(text.strip());
```

Output:

```text
Hello Java
```

***

**3.4 stripLeading()**

```java
String text = "    Java";

System.out.println(text.stripLeading());
```

Output:

```text
Java
```

***

**3.5 stripTrailing()**

```java
String text = "Java    ";

System.out.println(text.stripTrailing());
```

Output:

```text
Java
```

***

**3.6 repeat()**

Repeat a String multiple times.

```java
String line = "-".repeat(20);

System.out.println(line);
```

Output:

```text
--------------------
```

***

### 4. Files Utility Methods

Reading and writing files became simpler.

**Read String from File
**
```java
String content =
        Files.readString(Path.of("employee.txt"));

System.out.println(content);
```

***

**Write String to File**
```java
Files.writeString(
        Path.of("employee.txt"),
        "Employee Data");
```

Before Java 11, developers typically used readers/writers or byte arrays.

***

### 5. Optional Improvements

***

**isEmpty()**

Before

```java
if(!optional.isPresent()) {
}
```

Java 11

```java
if(optional.isEmpty()) {
}
```

Example

```java
Optional<String> name = Optional.empty();

System.out.println(name.isEmpty());
```

Output

```text
true
```

***

### 6. Collection to Array

Easier conversion from collection to array.

##### Before

```java
String[] arr =
        list.toArray(new String[0]);
```

##### Java 11

```java
String[] arr =
        list.toArray(String[]::new);
```

Example

```java
List<String> skills =
        List.of("Java", "Spring", "Angular");

String[] array =
        skills.toArray(String[]::new);
```

***

### 7. Running Java Without Compilation

Huge productivity feature.

Create:

```java
Hello.java
```

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Java 11");
    }
}
```

Run directly:

```bash
java Hello.java
```

No need:

```bash
javac Hello.java
java Hello
```

Useful for:

* Learning Java
* Scripts
* Automation

***

### 8. Nest-Based Access Control

Java allows nested classes to access private members more efficiently.

##### Example

```java
class Employee {

    private String name = "Narsing";

    class Address {

        void print() {
            System.out.println(name);
        }
    }
}
```

The JVM now handles this access more efficiently.

***

### 9. Epsilon Garbage Collector

A "No-Op" garbage collector.

It:

* Allocates memory
* Never frees memory

Example JVM startup:

```bash
java -XX:+UnlockExperimentalVMOptions
     -XX:+UseEpsilonGC
     App
```

##### Use Cases

* Performance testing
* Benchmarking
* GC behavior analysis

***

### 10. Flight Recorder (JFR)

Flight Recorder became available in OpenJDK.

Used for:

* Performance troubleshooting
* CPU analysis
* Memory analysis
* Thread monitoring

Start recording:

```bash
java -XX:StartFlightRecording=filename=app.jfr
```

Analyze later using:

```text
Java Mission Control
```

***

### 11. Z Garbage Collector (Experimental)

Low-latency GC designed for large heaps.

Benefits:

* Millisecond pause times
* Huge memory support
* High throughput applications

Example

```bash
java -XX:+UnlockExperimentalVMOptions
     -XX:+UseZGC
```

##### Suitable For

* Banking systems
* Trading applications
* Large microservices platforms

***

### 12. TLS 1.3 Support

Java 11 adds TLS 1.3.

Benefits:

* Faster handshake
* Improved security
* Better encryption

Used automatically by HTTPS communications.


***


**Calling REST API**

```java
HttpClient client = HttpClient.newHttpClient();

HttpRequest request =
        HttpRequest.newBuilder()
                .uri(URI.create(
                  "https://jsonplaceholder.typicode.com/users"))
                .GET()
                .build();

HttpResponse<String> response =
        client.send(request,
              HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

***

**Example 2: String Formatting**

```java
String report =
        "=".repeat(30);

System.out.println(report);
```

Output

```text
==============================
```

***

**Example 3: Read File**

```java
String xml =
        Files.readString(Path.of("employee.xml"));

System.out.println(xml);
```

Useful for your large XML processing scenarios.


***



---
## Java 17 Features (LTS) 

**Java 17** was released in **September 2021** and is a **Long-Term Support (LTS)** release. It became the preferred upgrade path for many organizations moving from Java 8 and Java 11. 

***

### 1. Records ✅

Records reduce boilerplate code for DTOs and immutable data classes.

##### Before Java 17

```java
public class Employee {
    private final String name;
    private final int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }

    // equals(), hashCode(), toString()
}
```

##### Java 17

```java
public record Employee(String name, int age) {}
```

Usage:

```java
Employee emp = new Employee("Narsing", 35);

System.out.println(emp.name());
System.out.println(emp.age());
```

The compiler automatically generates constructor, getters, `equals()`, `hashCode()`, and `toString()`. 

***

### 2. Sealed Classes ✅

Restrict which classes can extend or implement a type.

```java
public sealed class Vehicle
        permits Car, Bike {
}

final class Car extends Vehicle {
}

final class Bike extends Vehicle {
}
```

Now no other class can extend `Vehicle`.

##### Benefits

* Better domain modeling
* More secure inheritance
* Works well with pattern matching

***

### 3. Pattern Matching for instanceof ✅

Removes explicit type casting.

##### Before

```java
if (obj instanceof String) {
    String str = (String) obj;
    System.out.println(str.length());
}
```

##### Java 17

```java
if (obj instanceof String str) {
    System.out.println(str.length());
}
```

Cleaner and less error-prone. 

***

### 4. Text Blocks ✅

Writing multi-line JSON, SQL, XML becomes easier.

##### Before

```java
String json = "{\n" +
              " \"name\":\"Narsing\",\n" +
              " \"age\":35\n" +
              "}";
```

##### Java 17

```java
String json = """
        {
            "name":"Narsing",
            "age":35
        }
        """;
```

Useful for SQL queries and REST payloads.

***

### 5. Switch Expressions ✅

Switch can now return values.

##### Before

```java
String dayType;

switch(day) {
    case "SATURDAY":
    case "SUNDAY":
        dayType = "Weekend";
        break;
    default:
        dayType = "Weekday";
}
```

##### Java 17

```java
String dayType = switch(day) {
    case "SATURDAY", "SUNDAY" -> "Weekend";
    default -> "Weekday";
};
```

Less code and no accidental fall-through. 

***

### 6. Helpful NullPointerException ✅

##### Before

```java
employee.getAddress().getCity();
```

Error:

```text
NullPointerException
```

##### Java 17

```text
Cannot invoke "Address.getCity()"
because "employee.getAddress()" is null
```

Much easier debugging.

***



### Java 21 
(released as an **LTS - Long Term Support** version) introduced several important features focused on **concurrency, pattern matching, collections, and developer productivity**.

#### 1. Virtual Threads (Final Feature) ⭐ Most Important

Virtual threads are lightweight threads managed by the JVM. You can create millions of them without exhausting OS resources.

##### Before Java 21

```java
Thread thread = new Thread(() -> {
    System.out.println("Processing...");
});
thread.start();
```

##### Java 21

```java
Thread.startVirtualThread(() -> {
    System.out.println("Running in virtual thread");
});
```

##### Executor Example

```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    for (int i = 0; i < 10000; i++) {
        executor.submit(() -> {
            System.out.println(Thread.currentThread());
        });
    }
}
```

**Use Case:** Microservices, APIs, database calls, I/O-intensive applications. 

**Q: Why are Virtual Threads important?**

**Answer:**  
Traditional threads are mapped 1:1 to OS threads and are expensive. Virtual threads are JVM-managed lightweight threads, allowing millions of concurrent tasks with minimal memory consumption. They simplify scalable I/O-bound applications without requiring reactive programming frameworks. 

***

#### 2. Pattern Matching for Switch (Final)

No need for multiple `instanceof` checks.

##### Before

```java
if (obj instanceof String) {
    System.out.println(((String) obj).toUpperCase());
} else if (obj instanceof Integer) {
    System.out.println(obj);
}
```

##### Java 21

```java
Object obj = "Hello";

switch (obj) {
    case String s -> System.out.println(s.toUpperCase());
    case Integer i -> System.out.println(i * 2);
    default -> System.out.println("Unknown");
}
```

More readable and type-safe.

***

#### 3. Record Patterns (Final)

Allows extracting values from records directly.

##### Record

```java
record Employee(String name, int age) {}
```

##### Java 21

```java
Employee emp = new Employee("Narsing", 35);

if (emp instanceof Employee(String name, int age)) {
    System.out.println(name);
    System.out.println(age);
}
```

No need to write:

```java
emp.name();
emp.age();
```

repeatedly. 

***

#### 4. Sequenced Collections

Adds support for accessing first and last elements consistently.

```java
SequencedCollection<String> names = new LinkedList<>();

names.add("A");
names.add("B");
names.add("C");

System.out.println(names.getFirst());
System.out.println(names.getLast());
```

Useful when working with ordered collections.

***

#### 5. Unnamed Classes and Instance Main Method (Preview)

Good for beginners and simple programs.

##### Before

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Java");
    }
}
```

##### Java 21

```java
void main() {
    System.out.println("Hello Java 21");
}
```

Much less boilerplate. 

***

#### 6. String Templates (Preview)

Safer and cleaner string interpolation.

```java
String name = "Narsing";

String message = STR."Hello \{name}";
```

Output:

```text
Hello Narsing
```

Similar to JavaScript template literals. 

***

#### 7. Structured Concurrency (Preview)

Helps manage multiple related tasks as a single unit.

```java
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {

    Future<String> user =
            scope.fork(() -> getUser());

    Future<String> orders =
            scope.fork(() -> getOrders());

    scope.join();
    scope.throwIfFailed();

    System.out.println(user.resultNow());
    System.out.println(orders.resultNow());
}
```

Useful for microservices calling multiple downstream services concurrently. 

***

#### 8. Generational ZGC

Improves garbage collection performance and memory management for large applications. Particularly useful for low-latency systems and high-throughput enterprise applications.

***
=======
>>>>>>> 85f7f2df062c1da896c87be0d668988aad33a809






# circuit breaker in depth :

In microservices architecture, a **Circuit Breaker** is a design pattern used to prevent a failure in one service from cascading down to other services. Think of it exactly like an electrical circuit breaker in your house: when a fault occurs (like a short circuit), the breaker trips to stop the flow of electricity, protecting the rest of your home.

In Spring Boot, the modern standard for implementing this pattern is **Resilience4j** (which replaced the deprecated Netflix Hystrix).

---

## 1. The Three Core States

A circuit breaker operates as a finite state machine with three main states:

* **CLOSED:** Everything is working normally. Requests flow directly to the downstream service. The circuit breaker monitors the success/failure rate of these calls.
* **OPEN:** The downstream service is failing, and the error threshold has been breached. The circuit breaker **trips**, meaning it immediately rejects incoming requests and diverts them to a fallback method without hitting the broken service. This gives the service time to recover.
* **HALF-OPEN:** After a configured wait duration, the circuit breaker enters this state to test if the underlying service has recovered. It permits a limited, configurable number of requests to pass through.
* If they **succeed**, the circuit closes, and normal operation resumes.
* If they **fail**, the circuit trips back to **OPEN**.



---

## 2. Sliding Windows: How Failure is Calculated

Resilience4j doesn't just look at the *last* request; it uses a **Sliding Window** to evaluate metrics. You can configure this in two ways:

1. **Count-Based Sliding Window:** Evaluates the last `N` requests (e.g., the last 100 calls). If 50% of those 100 calls fail, the circuit opens.
2. **Time-Based Sliding Window:** Evaluates requests made in the last `N` seconds (e.g., the last 30 seconds).

---

## 3. Implementing Resilience4j in Spring Boot

### Step 1: Add Dependencies

To get started, add the Resilience4j starter along with Spring Boot AOP (required for annotations) to your `pom.xml`:

```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <groupId>resilience4j-spring-boot3</groupId>
    <version>2.2.0</version> </dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>

```

### Step 2: Configure via `application.yml`

This is where the "in-depth" control happens. You fine-tune how and when the circuit trips:

```yaml
resilience4j:
  circuitbreaker:
    instances:
      inventoryService:
        slidingWindowType: COUNT_BASED
        slidingWindowSize: 10              # Tracks the last 10 requests
        failureRateThreshold: 50           # Trips if 50% (5 out of 10) fail
        slowCallRateThreshold: 70          # Trips if 70% of calls take too long
        slowCallDurationThreshold: 2000ms  # A call taking > 2s is considered "slow"
        waitDurationInOpenState: 10000ms   # Waits 10s in OPEN before moving to HALF-OPEN
        permittedNumberOfCallsInHalfOpenState: 3 # Sends 3 trial requests in HALF-OPEN
        automaticTransitionFromOpenToHalfOpenEnabled: true

```

### Step 3: Coding the Circuit Breaker & Fallback

Apply the `@CircuitBreaker` annotation to your service method. You should always supply a `fallbackMethod` to handle the failure gracefully.

```java
import io.github.resilience4j.circuitbreaker.annotation.CircuitBreaker;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class OrderService {

    private final RestTemplate restTemplate;

    public OrderService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    // "inventoryService" matches the key used in application.yml
    @CircuitBreaker(name = "inventoryService", fallbackMethod = "getInventoryFallback")
    public String checkInventory(Long productId) {
        return restTemplate.getForObject("http://inventory-service/api/products/" + productId, String.class);
    }

    // The fallback method MUST have the same signature as the core method, 
    // plus an extra parameter for the Exception caught.
    public String getInventoryFallback(Long productId, Throwable throwable) {
        // Log the error and return cached or default data
        System.out.println("Circuit is OPEN or Service failed. Error: " + throwable.getMessage());
        return "Inventory status temporarily unavailable (Fallback Data)";
    }
}

```

---

## 4. Advanced Production Concepts

When architecting production-grade microservices, keep these core behaviors in mind:

* **Thread Safety:** Resilience4j is built on Top of `Vavr`, utilizing atomic operations and functional data structures. It is completely thread-safe with very low memory overhead.
* **Exception Handling (Ignore vs. Record):** By default, all exceptions count as failures. However, you don't want a `404 Not Found` (client error) to trip a circuit meant to catch server crashes. You can configure this explicitly:
```yaml
resilience4j.circuitbreaker.instances.inventoryService:
  recordExceptions:
    - org.springframework.web.client.HttpServerErrorException # Count 5xx
  ignoreExceptions:
    - org.springframework.web.client.HttpClientErrorException # Ignore 4xx

```


* **Monitoring with Actuator:** You can expose the state of your circuit breakers to monitoring tools like Prometheus and Grafana. By adding `spring-boot-starter-actuator`, you gain access to the `/actuator/circuitbreakers` endpoint to view real-time failure rates and states.

---------------------------------------------------------------------------------------------------------

# Bean Life cycle 

In Spring, a **Bean** is simply an object that is instantiated, assembled, and managed by the Spring IoC (Inversion of Control) Container. The lifecycle of a Spring bean is incredibly robust, allowing you to hook into almost every stage of its existence—from creation to destruction.

Here is an in-depth breakdown of how a Spring Bean moves through the container.

---

## 1. High-Level Phases of the Lifecycle

The bean lifecycle can be broadly divided into four distinct phases:

```
[ Instantiate ] ──> [ Populate Properties ] ──> [ Initialization Stage ] ──> [ Ready for Use ] ──> [ Destruction Stage ]

```

1. **Instantiation:** The container finds the bean’s definition (via XML, Java config `@Bean`, or component scanning `@Component`) and creates an instance of the bean class using reflection (similar to calling `new MyBean()`).
2. **Populate Properties (Dependency Injection):** Spring looks at dependencies required by the bean (via `@Autowired`, setter injection, or constructor injection) and injects them.
3. **Initialization:** A series of post-processors and awareness interfaces run to configure the bean, followed by custom initialization methods.
4. **Destruction:** When the application context shuts down, the container cleans up resources using custom destruction hooks.

---

## 2. Step-by-Step Execution Flow

If we zoom into the exact sequence of events, especially during the crucial **Initialization** phase, Spring follows a precise internal script:

### Phase A: Awareness Interfaces

Once dependencies are injected, Spring checks if the bean implements any `Aware` interfaces. These interfaces "awaken" the bean to its environment by injecting infrastructure objects:

* **`BeanNameAware`:** Injects the ID/Name of the bean.
* **`BeanFactoryAware`:** Injects the owning `BeanFactory`.
* **`ApplicationContextAware`:** Injects the active `ApplicationContext` (giving the bean access to the whole environment, events, and resource loading).

### Phase B: Bean Post-Processors (Pre-Initialization)

Spring invokes the `postProcessBeforeInitialization()` method of all registered **`BeanPostProcessor`** beans.

* *Deep Dive:* This is where Spring's `@PostConstruct` annotation is actually processed behind the scenes by the `CommonAnnotationBeanPostProcessor`.

### Phase C: Initialization Methods

This is where you execute custom setup logic (like opening database connections or starting a thread pool). Spring looks for hooks in this exact order:

1. **`InitializingBean` interface:** Executes the overridden `afterPropertiesSet()` method. *(Not recommended for modern apps as it tightly couples your code to Spring).*
2. **Custom `initMethod`:** Executes a method defined via `@Bean(initMethod = "customInit")` or XML configuration.

### Phase D: Bean Post-Processors (Post-Initialization)

Spring invokes the `postProcessAfterInitialization()` method of the `BeanPostProcessor` beans.

* *Deep Dive:* This is arguably the most powerful step in Spring. If your bean requires Aspect-Oriented Programming (AOP)—like `@Transactional` or `@Async`—Spring will intercept the bean here and wrap your original object in a **Dynamic Proxy** object.

### Phase E: Destruction Hook

When the `ApplicationContext` closes, Spring gracefully cleans up the bean using these triggers in order:

1. **`@PreDestroy`:** Methods annotated with this are executed first.
2. **`DisposableBean` interface:** Executes the `destroy()` method.
3. **Custom `destroyMethod`:** Executes a method defined via `@Bean(destroyMethod = "customDestroy")`.

---

## 3. Code Example: Seeing it in Action

Here is a practical implementation showcasing the modern annotations, legacy interfaces, and custom declarations together:

```java
import jakarta.annotation.PostConstruct;
import jakarta.annotation.PreDestroy;
import org.springframework.beans.factory.BeanNameAware;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.DisposableBean;
import org.springframework.stereotype.Component;

@Component
public class DatabaseConnector implements BeanNameAware, InitializingBean, DisposableBean {

    private String beanName;

    public DatabaseConnector() {
        System.out.println("1. Constructor: Bean Instantiated");
    }

    // 1. Aware Interface
    @Override
    public void setBeanName(String name) {
        this.beanName = name;
        System.out.println("2. BeanNameAware: Bean Name set to -> " + name);
    }

    // 2. PostConstruct Annotation
    @PostConstruct
    public void postConstruct() {
        System.out.println("3. @PostConstruct: Executed before initialization interfaces");
    }

    // 3. InitializingBean Interface
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("4. InitializingBean: afterPropertiesSet executed");
    }

    // 4. Custom Init Method (If configured via @Bean(initMethod = "customInit"))
    public void customInit() {
        System.out.println("5. Custom Init: Executed last in initialization");
    }

    // -- BEAN IS NOW READY FOR USE --

    // 5. PreDestroy Annotation
    @PreDestroy
    public void preDestroy() {
        System.out.println("6. @PreDestroy: Executed before destruction interfaces");
    }

    // 6. DisposableBean Interface
    @Override
    public void destroy() throws Exception {
        System.out.println("7. DisposableBean: destroy executed");
    }
}

```

---

## 4. Crucial Interview/Architecture Gotchas

* **Bean Scopes Matter:** The entire lifecycle applies fully to **Singleton** beans. For **Prototype** beans, Spring instantiates, configures, and initializes the bean, then hands it over to the client. *Spring does not manage the destruction phase of Prototype beans*—you must clean up their resources manually.
* **Constructor Injection vs. `@PostConstruct`:** Field-level `@Autowired` variables are `null` inside a constructor because dependencies haven't been injected yet. If you need to run setup logic using dependencies right after they are ready, you *must* use `@PostConstruct` (or switch to constructor injection entirely).













# LRU Cache 

An **LRU (Least Recently Used) Cache** is a fixed-size caching strategy that discards the least recently accessed items first when the cache reaches its capacity limit. It operates on the principle of **temporal locality**: if you accessed a piece of data recently, you are highly likely to access it again soon.

To make a cache production-grade, both lookups (`get`) and insertions (`put`) must execute in constant time, or **$O(1)$ time complexity**.

---

## 1. The Core Data Structure: Why One Isn't Enough

To achieve $O(1)$ for both reading and writing, an LRU Cache combined two distinct data structures into one cohesive hybrid: a **Hash Map** and a **Doubly Linked List**.

```
[ Hash Map ] ──(Lookups)──> [ Doubly Linked List ] ──(Ordering)──> [ Head (Most Recent) / Tail (Least Recent) ]

```

### Why a Doubly Linked List?

A linked list makes it incredibly easy to move elements around. If an item is accessed, we can snip it out of its current position and splice it onto the **Head** (representing the most recently used item) in $O(1)$ time. The **Tail** of the list always represents the oldest, least recently used item. If the cache is full, we simply evict the node at the tail.

### Why a Hash Map?

A linked list alone has $O(n)$ search time because you have to traverse it sequentially. By pairing it with a Hash Map, the map's **keys** point directly to the **nodes** inside the Doubly Linked List. This grants instant $O(1)$ access to any node without searching the entire list.

---

## 2. Deep Dive: How the Operations Work

Imagine an LRU Cache with a capacity of **3**.

### The `put(key, value)` Operation

1. **Case A: Key already exists.** * Update the node's value.
* Move the node to the **Head** of the doubly linked list (since it was just updated).


2. **Case B: Key is new, and cache is NOT full.**
* Create a new node.
* Add it to the Hash Map.
* Insert it at the **Head** of the list.


3. **Case C: Key is new, and cache IS full.**
* Locate the node at the **Tail** of the list.
* Delete that node's key from the Hash Map.
* Remove the node from the list (eviction).
* Insert the brand-new node at the **Head** and add it to the Hash Map.



### The `get(key)` Operation

1. Look up the key in the Hash Map.
2. If it doesn't exist, return `-1` or `null`.
3. If it does exist, the map returns the node pointer. Before returning the value, **move this node to the Head** of the doubly linked list because it just became the most recently used item.

---

## 3. Pure Java Implementation (From Scratch)

While you could cheat in Java by extending `LinkedHashMap` (which has built-in LRU support via its structural access-order flag), interviews and deep architectural reviews require writing the underlying mechanics manually.

```java
import java.util.HashMap;
import java.util.Map;

public class LRUCache {

    // Internal Node structure for the Doubly Linked List
    private static class Node {
        int key;
        int value;
        Node prev;
        Node next;

        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private final int capacity;
    private final Map<Integer, Node> map;
    private final Node head; // Dummy head
    private final Node tail; // Dummy tail

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();
        
        // Initialize dummy head and tail to avoid null-pointer checks during node splicing
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        Node node = map.get(key);
        moveToHead(node); // Refresh item priority
        return node.value;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            node.value = value; // Update value
            moveToHead(node);
        } else {
            Node newNode = new Node(key, value);
            map.put(key, newNode);
            addNode(newNode);

            if (map.size() > capacity) {
                // Evict the least recently used item from the tail
                Node tailNode = this.tail.prev;
                removeNode(tailNode);
                map.remove(tailNode.key);
            }
        }
    }

    // --- Helper Methods for List Manipulation ---
    
    // Always insert right after the dummy head
    private void addNode(Node node) {
        node.prev = head;
        node.next = head.next;

        head.next.prev = node;
        head.next = node;
    }

    // Break the links around an existing node
    private void removeNode(Node node) {
        Node prevNode = node.prev;
        Node nextNode = node.next;

        prevNode.next = nextNode;
        nextNode.prev = prevNode;
    }

    // Moving a node to the front means removing it from its current spot, then adding it to head
    private void moveToHead(Node node) {
        removeNode(node);
        addNode(node);
    }
}

```

---

## 4. Architectural Trade-offs & Limitations

While LRU is incredibly popular (used under the hood in Redis, Memcached, and database buffer pools), it isn't flawless:

* **Concurrency Overhead:** The implementation above is **not thread-safe**. If multiple threads call `get()` or `put()` concurrently, structural links will break. Making it thread-safe requires synchronization lock mechanisms (like `ReentrantReadWriteLock`), which introduces contention and slows down throughput.
* **The "One-Hit Wonder" Flaw:** LRU is highly vulnerable to sequential scans. If an application suddenly queries 10,000 unique records consecutively that it will never ask for again, an LRU cache will evict its *entire* history of frequently used data to make room for these one-hit wonders.
* **Alternative Patterns:** To combat this flaw, modern high-throughput applications often turn to variations like **LFU (Least Frequently Used)** or hybrid approaches like **W-TinyLFU** (used by the popular Java caching library Caffeine), which tracks *how many times* an item is called alongside how recently it was called.


Using `LinkedHashMap` is the ultimate "cheat code" for implementing an LRU Cache in Java. Instead of manually wiring up a `HashMap` and managing the pointers of a custom `DoublyLinkedList`, Java's built-in `LinkedHashMap` actually provides all of this machinery right out of the box.

Here is an in-depth look at how it works under the hood and how to implement it cleanly.

---

## 1. The Secret Weapon: The Access-Order Flag

By default, a `LinkedHashMap` maintains elements in **insertion-order** (the order in which keys are put into the map). However, it contains a special constructor that lets you flip this behavior to **access-order**:

```java
public LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)

```

If `accessOrder` is set to `true`, every time you call `.get()` or `.put()` on a key, `LinkedHashMap` automatically detaches that underlying node from its current position and splices it to the end of its internal doubly linked list.

This means:

* **The Head (Start of iteration):** Becomes the Least Recently Used (LRU) element.
* **The Tail (End of iteration):** Becomes the Most Recently Used (MRU) element.

---

## 2. The Hook: `removeEldestEntry`

To make it a true fixed-size cache, we need a way to evict the oldest entry automatically when the capacity limit is breached. `LinkedHashMap` provides a protected method designed exactly for this hook:

```java
protected boolean removeEldestEntry(Map.Entry<K,V> eldest) {
    return false; // Default behavior: never remove old entries
}

```

By overriding this method to return `true` when the map size exceeds our maximum capacity, `LinkedHashMap` will automatically evict the head of the list (the least recently accessed item) every time a new item is added.

---

## 3. Implementation Code

Here is how incredibly concise an LRU cache becomes when utilizing `LinkedHashMap`:

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCacheLinkedHashMap<K, V> extends LinkedHashMap<K, V> {
    
    private final int maxCapacity;

    public LRUCacheLinkedHashMap(int maxCapacity) {
        // initialCapacity: maxCapacity + 1 to prevent immediate resizing
        // loadFactor: 0.75f (standard default)
        // accessOrder: true (this enables the LRU tracking behavior)
        super(maxCapacity + 1, 0.75f, true);
        this.maxCapacity = maxCapacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        // Automatically returns true and deletes the eldest item 
        // when the map outgrows the allowed capacity.
        return this.size() > maxCapacity;
    }

    // Optional: Standard helper wrappers if you don't want to expose raw Map methods
    public V getCache(K key) {
        return super.getOrDefault(key, null);
    }

    public void putCache(K key, V value) {
        super.put(key, value);
    }
}

```

---

## 4. Crucial Production Nuances

While using `LinkedHashMap` saves you dozens of lines of code, you must be aware of its architectural limitations in production environments:

### 1. It is NOT Thread-Safe

Just like a standard `HashMap`, `LinkedHashMap` will break structurally if multiple threads attempt to access or modify it concurrently. Worse yet, because `accessOrder=true`, even a seemingly passive **`get()` call is actually a structural modification** (it reorders the internal list pointers).

To use it in a multi-threaded environment, you must wrap it using `Collections.synchronizedMap`:

```java
Map<String, String> cache = Collections.synchronizedMap(new LRUCacheLinkedHashMap<>(100));

```

### 2. Lock Contention

Even when wrapped in `Collections.synchronizedMap`, the entire map is guarded by a single, monolithic mutual-exclusion lock. This means if Thread A is calling `.get()`, Thread B must wait entirely to call `.get()` or `.put()`.

For high-throughput systems, this becomes a severe bottleneck. This is why advanced frameworks like **Caffeine** or **Guava Cache** do not use synchronized wrappers; instead, they utilize ring buffers and concurrent log-stripping structures to record read/write data access asynchronously without locking execution threads.


---------------------------------------------------------------------------------------------------------------------------------------


1. Copy by Value (Pass by Value)

Description

Copy by value means a copy of the actual data is passed, not the original reference.
Changes made to the copied variable do NOT affect the original variable.

Example

int a = 10;
int b = a; // copy by value

b = 20;

System.out.println(a); // 10 (unchanged)
System.out.println(b); // 20

Key Points

Separate memory locations

Safe (no side effects)

Used for primitive types in Java



---

2. Copy by Reference

Description

Copy by reference means the reference (address) of the object is copied, not the actual object.
Both variables point to the same memory location, so changes affect both.

Example

class Person {
    String name;
}

Person p1 = new Person();
p1.name = "Narsing";

Person p2 = p1; // reference copy

p2.name = "Raj";

System.out.println(p1.name); // Raj (changed)
System.out.println(p2.name); // Raj

Key Points

Same memory location shared

Changes reflect in all references

Used for objects in Java



---

3. Shallow Copy

Description

Shallow copy creates a new object, but copies references of nested objects.
So, inner objects are still shared.

Example

class Address {
    String city;
}

class Person {
    String name;
    Address address;
}

Address addr = new Address();
addr.city = "Pune";

Person p1 = new Person();
p1.name = "Narsing";
p1.address = addr;

// Shallow copy
Person p2 = p1;

p2.address.city = "Mumbai";

System.out.println(p1.address.city); // Mumbai (affected)

Key Points

Outer object is new (sometimes), but inner objects are shared

Faster, less memory

Risk of unintended changes



---

4. Deep Copy

Description

Deep copy creates a completely independent copy, including all nested objects.
Changes in one object do NOT affect the other.

Example

class Address {
    String city;
}

class Person {
    String name;
    Address address;
}

Address addr = new Address();
addr.city = "Pune";

Person p1 = new Person();
p1.name = "Narsing";
p1.address = addr;

// Deep copy
Person p2 = new Person();
p2.name = p1.name;

Address newAddr = new Address();
newAddr.city = p1.address.city;
p2.address = newAddr;

p2.address.city = "Mumbai";

System.out.println(p1.address.city); // Pune (unchanged)
System.out.println(p2.address.city); // Mumbai

Key Points

Completely separate memory

No shared references

Safer but more memory & processing



---

🔥 Quick Comparison

Concept	Memory Sharing	Changes Affect Original	Used For

Copy by Value	❌ No	❌ No	Primitives
Copy by Reference	✅ Yes	✅ Yes	Objects
Shallow Copy	⚠️ Partial	⚠️ Yes (nested)	Fast copy
Deep Copy	❌ No	❌ No	Safe copy



---

If you want, I can give interview-ready tricky questions on these topics (very commonly asked for Java dev roles).




In interviews, explain your project in a clear structure:
1) Project Overview → 2) Your Module → 3) Features → 4) Architecture → 5) Your Responsibilities → 6) Challenges.
This helps the interviewer quickly understand your experience.

Below is a good interview explanation format you can use.


---

Project Explanation – YONO 2.0 Rewards Module

1. Project Overview

Project: YONO 2.0 (Digital Banking Platform)

YONO 2.0 is a digital banking platform where customers can access banking services like payments, shopping, offers, and reward programs in a single application.

One of the modules in the platform is the Rewards Module, which allows customers to earn, track, and redeem reward points based on their banking activities.


---

2. My Module – Rewards

I worked on the Rewards Module, which manages reward points lifecycle including earning, unlocking, redeeming, and expiring points.

The main goal of this module is to increase user engagement by rewarding customers for using banking services.


---

3. Key Features I Implemented

1️⃣ Reward Points Dashboard

Users can see different types of reward points such as:

Total Points – All reward points earned by the user

Available Points – Points that can be redeemed

Unlocking Points – Points that will be available after some conditions

Expiring Points – Points that will expire soon


Example API:

GET /rewards/summary/{customerId}

Response:

{
 "totalPoints": 5000,
 "availablePoints": 3500,
 "unlockingPoints": 1000,
 "expiringPoints": 500
}


---

2️⃣ Reward Points Transaction History

Users can view complete transaction history of reward points.

Transactions include:

Points Earned

Points Redeemed

Points Expired

Points Returned

Unlocking Soon Transactions

Expiring Soon Transactions


Example API:

GET /rewards/transactions?type=earned


---

3️⃣ Reward Points Calculator

Users can calculate how many reward points they will get for different services like:

Bill payments

Shopping

Card transactions

Partner services


Example:

If a user spends ₹1000, they may earn 100 reward points.

Example API:

POST /rewards/calculate


---

4️⃣ Offers & Vouchers

Users can view different types of offers such as:

Available offers

Voucher deals

Affiliate partner offers


Example:

Amazon voucher

Flipkart coupon

Travel partner discounts



---

5️⃣ Reward Redemption

Users can redeem reward points for:

Gift vouchers

Shopping coupons

Partner offers


Example API:

POST /rewards/redeem


---

4. Architecture (How Services Work)

In our system we followed Microservices Architecture.

Main services involved:

API Gateway – Entry point for all client requests

Rewards Service – Manages reward points logic

User Service – Customer profile

Transaction Service – Banking transactions

Offer Service – Deals and vouchers


Flow

1. User opens Rewards section in mobile app


2. Request goes to API Gateway


3. Gateway routes request to Rewards Microservice


4. Rewards service fetches data from database


5. Response returned to mobile application




---

5. Technologies Used

Backend:

Java

Spring Boot

Spring Data JPA

Hibernate


Database:

Oracle / MySQL


Microservices Tools:

API Gateway

Config Server

Service Registry

Docker

Kubernetes


Monitoring:

Zipkin

ELK


CI/CD:

Git

Jenkins pipeline

SonarQube

JUnit

Fortify

JFrog

Kubernetes deployment



---

6. My Responsibilities

My responsibilities in the project were:

Developing REST APIs for rewards management

Implementing reward calculation logic

Creating transaction history APIs

Integrating offers and redemption services

Writing JUnit test cases

Fixing production bugs

Participating in code reviews

Supporting CI/CD deployment pipeline



---

7. Challenges Faced (Important for Interview)

One challenge was handling reward points expiration logic.

Points expire after a specific period, so we implemented a scheduled job that checks for expiring points and updates their status.

Example:

@Scheduled(cron = "0 0 1 * * ?")

This job runs daily and marks points as expired.


---

8. Impact of the Module

This module helped:

Increase customer engagement

Encourage more banking transactions

Improve customer retention



---

Short 1-Minute Interview Version (Very Important)

If interviewer says “Explain your project briefly”, say this:

> I worked on the Rewards Module of YONO 2.0, where users can track and manage their reward points earned from banking activities.
In this module, users can view total, available, unlocking, and expiring reward points along with detailed transaction history such as earned, redeemed, expired, and returned points.
We also implemented a reward points calculator where users can estimate points for different banking services.
Additionally, users can view available offers, vouchers, and affiliate deals and redeem their reward points for those offers.
I was mainly responsible for developing REST APIs using Spring Boot, implementing reward calculation logic, managing transaction history, and integrating redemption and offers services in a microservices architecture.




---

If you want, I can also give 20 interview questions that interviewer will ask specifically from THIS project (very common in Java 3+ years interviews).


Explain this module in interviews using a simple flow: purpose → features → how it works → your role.


---

Project Explanation – Customer Promotion & Marketing Notification Management

1. Module Overview

I worked on the Customer Promotion and Marketing Notification Management module.

The purpose of this module is to allow users to control marketing notifications they receive from the banking application such as promotional offers, campaigns, and product updates.

Users can enable, disable, or pause notifications for different communication channels.


---

2. Key Features

1️⃣ Notification Preference Management

Users can control notifications for multiple channels:

SMS Notifications

Email Notifications

In-App Notifications

Notification Center Messages


Users can:

Enable notifications

Disable notifications

Pause notifications for a certain time


Example API:

POST /notification/preferences

Example request:

{
 "customerId": "12345",
 "sms": true,
 "email": false,
 "inApp": true
}


---

2️⃣ Pause Notifications Feature

Users can temporarily pause marketing notifications for a selected duration.

Available pause durations:

1 Month

3 Months

6 Months


Example:

If a user pauses notifications for 3 months, they will not receive promotional alerts during that period.


---

3️⃣ Notification Preference Storage

All user preferences are stored in the database.

Example fields stored:

customerId

smsPreference

emailPreference

inAppPreference

pauseStartDate

pauseEndDate


Example entity:

class NotificationPreference {
    private String customerId;
    private boolean smsEnabled;
    private boolean emailEnabled;
    private boolean inAppEnabled;
    private LocalDate pauseUntil;
}


---

4. Data Warehouse Synchronization

User preferences are also synchronized with the Data Warehouse.

Purpose:

Marketing systems use this data to decide whether a user should receive a notification or not.

Flow:

1️⃣ User updates notification preference in the app
2️⃣ Preference stored in application database
3️⃣ Data is synced to Data Warehouse
4️⃣ Marketing campaign systems read this data
5️⃣ Notifications are sent only to eligible users


---

5. Notification Flow (Architecture)

Step-by-step flow:

1. User updates notification preference in the mobile app


2. Request goes to API Gateway


3. Gateway routes request to Notification Management Service


4. Service stores preference in database


5. Data is synced with Data Warehouse


6. Marketing system checks preference before sending notification




---

6. Technologies Used

Backend:

Java

Spring Boot

Spring Data JPA


Database:

Oracle / MySQL


Architecture:

Microservices

REST APIs


Integration:

Data Warehouse synchronization

Notification services



---

7. My Responsibilities

In this module I worked on:

Developing APIs for managing notification preferences

Implementing pause notification logic

Storing and updating user preferences in the database

Integrating with data warehouse synchronization

Handling validation and preference checks

Writing unit test cases

Fixing production issues



---

8. Example Logic (Pause Notification)

Before sending notification we check:

if(currentDate.isBefore(preference.getPauseUntil())){
    // Do not send notification
}

This ensures users do not receive notifications during the pause period.


---

1-Minute Interview Explanation (Best Answer)

You can say this in interviews:

> I worked on the Customer Promotion and Marketing Notification Management module where users can manage their marketing notification preferences. Users can enable or disable notifications for different channels like SMS, email, and in-app notifications. They can also pause promotional notifications for a duration of 1, 3, or 6 months. These preferences are stored in the database and synchronized with the data warehouse so that marketing systems can check user preferences before sending notifications. My role involved developing REST APIs using Spring Boot, implementing the pause notification logic, managing preference storage, and integrating the service with downstream systems.




---

If you want, I can also give 15 interviewer questions they will definitely ask from this notification module (with answers) for 3+ years Java developer interviews.


Add this point when explaining your module because it shows real backend experience (batch processing, scheduling, DB handling). Present it like this in an interview.


---

Batch Job for Notification Preference Expiry

1. Requirement

In the Marketing Notification Management module, users can pause notifications for 1 month, 3 months, or 6 months.

When the pause period expires, we needed to:

1. Remove expired records from the preferences table


2. Move them to a history table for audit and tracking.




---

2. Solution Implemented

We implemented a scheduled batch job that runs periodically and performs the following steps:

1️⃣ Check records where pause expiry date is less than current date
2️⃣ Move those records to notification_preference_history table
3️⃣ Delete them from the active preferences table

This helps to:

Keep the main table clean

Improve database performance

Maintain historical data for audit



---

3. Example Table Structure

Preferences Table (Active Records)

notification_preferences

customer_id	sms_enabled	email_enabled	pause_until

101	true	false	2026-04-01



---

History Table

notification_preferences_history

Stores expired records for auditing.


---

4. Batch Job Implementation (Example)

We used Spring Boot Scheduled Job.

@Scheduled(cron = "0 0 2 * * ?")
public void processExpiredPreferences() {

    List<Preference> expired = preferenceRepository
            .findByPauseUntilBefore(LocalDate.now());
    
    historyRepository.saveAll(expired);
    
    preferenceRepository.deleteAll(expired);
}

This job runs daily at 2 AM.


---

5. Why Batch Job is Important

Benefits:

Prevents large table size

Improves query performance

Maintains historical audit data

Ensures automatic cleanup



---

6. Your Role

In this implementation, I:

Designed the expiry handling logic

Implemented Spring scheduled batch job

Developed database queries for expired records

Implemented data migration to history table

Tested the job to ensure data consistency



---

Best 2–3 Line Interview Answer

If interviewer asks “Did you implement any batch processing?”

You can say:

> Yes, I implemented a scheduled batch job in the notification preference module. When a user's pause notification period expires, the job identifies those records, moves them to a history table for audit purposes, and deletes them from the active preferences table to keep the main table optimized.


SBI (NBC) Application is a core banking management system supporting 24,000+ branches and 200,000+ users worldwide

Built using a modern Java-based architecture, replacing legacy banking systems

Designed for high scalability, performance, and reliability in large-scale banking operations

Enables bank tellers, loan officers, and customer service representatives to perform daily tasks efficiently

Supports key functionalities like banking transactions, account management, and customer interactions

Improves operational efficiency and ensures a seamless banking experience across branches

Provides a centralized platform for handling core banking activities in real time


If you want, I can also convert this into resume bullet points with impact (using action verbs + metrics) 👍
# Spring Boot with Spring Batch

Spring Batch is a lightweight yet robust framework designed for batch processing, the automated execution of large data tasks without human intervention. It provides reusable components for logging, transaction management, job scheduling, retries and error handling.
When integrated with Spring Boot, it simplifies batch job configuration and execution, allowing developers to focus on the business logic instead of boilerplate setup.

---

### What is Batch Processing

Batch processing refers to executing repetitive, data-intensive tasks in bulk. Typical examples include:

- Processing large datasets
- Database migration
- Generating reports
- ETL (Extract, Transform, Load) operations

Spring Batch is purpose-built for such use cases by splitting jobs into smaller, manageable steps that can run sequentially or in parallel.

---

### Jobs, Steps and Flow

A Job in Spring Batch represents the complete batch process, while Steps define the logical phases within that job.

**Job: **Encapsulates the full batch process, consisting of multiple steps.
**Step:** Represents one stage of a job — typically involves reading, processing and writing data.
**Flow:** Defines the execution order of steps. You can create conditional or parallel flows (e.g., Step 2 runs only if Step 1 succeeds).

> Each step operates in three distinct phases: ItemReader, ItemProcessor and ItemWriter.

---

### Core Components of Spring Batch

**1. ItemReader**
Reads input data from a source such as a database, file, or message queue. It reads one record at a time and passes it to the processor.

```java

public class StringReader implements ItemReader<String> {
    private String[] data = {"Spring", "Batch", "Example"};
    private int index = 0;

    @Override
    public String read() {
        return index < data.length ? data[index++] : null;
    }
}
```

**2. ItemProcessor**
Applies business logic or transformation on each item read by the reader.

public class StringProcessor implements ItemProcessor<String, String> {

```java
    @Override
    public String process(String item) {
        return item.toUpperCase(); // Transform text to uppercase
    }
}
```

**3. ItemWriter**
Writes the processed data to the desired output, such as a database or console.

```java
public class ConsoleWriter implements ItemWriter<String> {
    @Override
    public void write(List<? extends String> items) {
        for (String item : items) {
            System.out.println(item);
        }
    }
}
```

### Chunk-Oriented Processing

Spring Batch processes data in chunks, not all at once.
Each step reads and processes individual items, but commits them in groups defined by a chunk size, improving both performance and transaction management.

```java

stepBuilderFactory.get("step")
    .<String, String>chunk(10)
    .reader(reader())
    .processor(processor())
    .writer(writer())
    .build();
```

---

In this example:

> 10 items are read and processed.
> Once the chunk limit is reached, all 10 items are written in a single transaction.
> Job Repository and Metadata
> The Job Repository maintains execution metadata for jobs and steps, including:

**JobInstance:** Represents a unique execution configuration.
**JobExecution:** Tracks job runs, including status and timestamps.
**StepExecution:** Records details of each step execution.

This allows restartability (resume from failure point) and monitoring of batch executions. A relational database (e.g., MySQL, HSQLDB) typically stores this metadata.

Transaction Management and Error Handling\*\*\*\*
Spring Batch ensures transactional integrity — if a step fails, its changes can be rolled back.

##### Error Handling Strategies:

**Retry:** Automatically retry failed steps.
**Skip:** Ignore certain failed records.
**Listeners:** Run custom logic before or after steps.

```java
.step("step")
    .<String, String>chunk(10)
    .reader(reader())
    .processor(processor())
    .writer(writer())
    .faultTolerant()
    .retry(Exception.class)
    .retryLimit(3)
    .build();
```

---

### Scheduling Batch Jobs

You can schedule jobs using Spring's @Scheduled annotation or tools like Quartz.:

```java
@EnableScheduling
public class BatchScheduler {

    @Autowired
    private JobLauncher jobLauncher;
    @Autowired
    private Job job;

    @Scheduled(cron = "0 0 12 * * ?") // Runs every day at noon
    public void runJob() throws Exception {
        JobParameters parameters = new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters();
        jobLauncher.run(job, parameters);
    }
}
```

1. Spring cloud Feign
   micrservices call another microservices
   ways to talk
   http protocal using rest api easy implementation
   another way is queue and messages using kafka and rabitmq

2. Spring cloud netfilx eureka
   we have lots of ms and if any one of ms changes its url then it need to be updated in all ms where its call so to avoid that
   we use eureka server which is service discovery and registry so all ms are registerd and called by service name not by url so url and port dependancy is removed here

3. Spring clound loadBlancer
   std ms calling ad ms we have multiple instaces for address ms in this case spring cloud loadbalancer help to send request to all instances equally

4. spring cloud Gateway

entry point of all requests

5.Fault torance
one ms is down so it should not impact on another ms




Method Overloading vs. Method Overriding
Feature 	Method Overloading	Method Overriding
Concept	Defining multiple methods in the same class with the same name but different parameters (different signature).	Redefining a method in a subclass that is already defined in its superclass with the exact same signature.
Polymorphism	Compile-time (static) polymorphism.	Run-time (dynamic) polymorphism.
Purpose	To perform a single operation in different ways based on input data types/count.	To provide a specific implementation of a general method defined by the parent class.
Requirements	Must have different parameter lists. Return type can be different.	Must have the exact same signature (name, parameters, and return type).
When to use Interface vs. Abstract Class
Feature 	Interface	Abstract Class
Contract	Defines a contract without providing any implementation details. Can only contain abstract methods and constants.	Can provide both method declarations (abstract methods) and method implementations (concrete methods).
Multiple Inheritance	A class can implement multiple interfaces.	A class can only inherit from one abstract class (single inheritance).
Use Case: Structure	Best for defining capabilities or contracts across unrelated classes (e.g., [Serializable]).	Best for defining a common base class with shared functionality and state for closely related classes.
Use Case: Evolution	Less flexible to add new methods later, as all implementing classes must update.	More flexible, as new concrete methods can be added to the abstract class without breaking existing subclasses.
Marker Interface
A marker interface is an empty interface in programming languages like Java that contains no methods or fields [2]. It "marks" a class with a special property or capability, providing metadata to the compiler or runtime environment that the class can be treated in a specific way [3]. 
Why use a Marker Interface?
Marker interfaces are used to indicate that a class possesses a certain characteristic or permission required by the runtime environment or framework, without needing to define a formal contract or implementation [3]. 
Common examples include:
Serializable in Java: Marks a class so that its instances can be written to a stream (serialized) [2]. The Java runtime checks for this interface to allow the serialization process.
Cloneable in Java: Indicates that an object can be copied or cloned using the clone() method [2].
Security Permissions: Frameworks might use marker interfaces to denote classes that require specific security permissions or can participate in certain operations. 




--------------------------------------------------------

Here are **brief, interview-ready answers** 👇

---

### 1) **equals() & hashCode() purpose**

* `equals()` → compares **logical equality** (content comparison)
* `hashCode()` → returns **hash value** for object (used in hashing)

👉 **Contract**:
If `equals()` is true → `hashCode()` must be same

---

### equals() & hashCode() in HashMap / HashSet

* **HashMap**

  1. `hashCode()` → find bucket
  2. `equals()` → find exact key inside bucket
* **HashSet**

  * Uses both to **avoid duplicates**

---

### 2) **Dependency Injection (DI)**

* Providing dependencies from outside instead of creating inside class
* Achieved via:

  * Constructor Injection ✅ (best)
  * Setter Injection
* Helps in **loose coupling & testability**

---

### 3) **Designing a class**

* Follow:

  * **Single Responsibility Principle (SRP)**
  * Proper **encapsulation (private fields + getters/setters)**
  * Use **interfaces**
  * Keep it **loosely coupled**
  * Immutable where possible

---

### 4) **Checked Exception**

**Advantages**

* Compile-time safety
* Forces handling

**Disadvantages**

* Boilerplate code
* Reduces readability
* Overuse → bad design

---

### 5) **Upper vs Lower Bound**

* `<? extends Animal>` → **read only** (covariant)
* `<? super Animal>` → **write allowed** (contravariant)

👉 Rule:
**PECS → Producer Extends, Consumer Super**

---

### 6) **Can Map key be mutable?**

❌ Not recommended

* If key changes → `hashCode()` changes → map can't find it
  👉 Always use **immutable keys**

---

### 7) **Effectively Final Variable**

* Variable whose value is **assigned once**
* Used in:

  * **Lambda expressions**
  * **Anonymous classes**

---

### 8) **Heap Generation Movement**

* Objects move:

  * **Young Gen → Old Gen**
* Happens during **Garbage Collection (GC)** when object survives multiple cycles

---

### 9) **Designing a class (again)**

* Same as Q3:

  * SRP
  * Encapsulation
  * Loose coupling
  * High cohesion

---

### 10) **final keyword purpose**

* `final variable` → constant
* `final method` → cannot override
* `final class` → cannot extend

---

### 11) **Bounded Wildcards purpose**

* Restrict generic types
* Improve **type safety**
* Enable **flexibility in APIs**

---

### 12) **Problem in given code**

```java
public Boolean isCondition(Boolean value){
    if(!value.equals(Boolean.false)){
        return true;
    }else{
        return false;
    }
}
```

❌ Issues:

* **NullPointerException risk** → `value` can be null
* Unnecessary complexity

✅ Better:

```java
return Boolean.TRUE.equals(value);
```

---

### 14) **Design patterns for testability**

* **Dependency Injection**
* **Factory Pattern**
* **Strategy Pattern**
* **Repository Pattern**
* **Mocking-friendly design**

---

### 15) **Best way to follow design principles**

* Follow **SOLID principles**
* Use:

  * Interfaces
  * DI
  * Composition over inheritance
* Write **clean, modular code**

---

### 16) **How to create mutable class**

* Provide **setters**
* Do not use `final` for fields
* Allow modification after creation

Example:

```java
class User {
    private String name;

    public void setName(String name){
        this.name = name;
    }
}
```

---

If you want, I can convert this into **clean markdown notes or PDF format for revision** 👍
We are writing software to collect and manage data on how fast racers can complete obstacle courses. An obstacle course is a series of difficult physical challenges (like walls, hurdles, and ponds) that a racer must go through.

Each course consists of multiple obstacles. The software stores how long it takes for racers to finish each obstacle, and provides useful statistics based on those times.

Definitions:
* A "run" is a particular attempt to complete an entire obstacle course
* A "run collection" is a group of runs on a particular course by the user.
* An "obstacle" is a portion of a course. We track how long it takes to finish each portion of the course

For example, here are some times for an obstacle course with four obstacles:

Obstacles:    O1  O2  O3  O4
    Run 1:      3   4   5   6    (total: 18 seconds)
    Run 2:      4   4   4   5    (total: 17 seconds)
    Run 3:      4   5   4   6    (total: 19 seconds)
    Run 4:      5   5   3        (13 seconds, but run is incomplete)

All of these runs for one obstacle course (including the incomplete run) make up a run collection.

To begin with, we present you with two tasks:

import java.util.*;

class Course {
  /* Data about a particular course. */
  public String title;  // The name of the obstacle course
  public int obstacleCount;  // The number of obstacles in the course

 public Course(String courseTitle, int obstacles) {
    title = courseTitle;
    obstacleCount = obstacles;
  }

 @Override
  public boolean equals(Object o) {
    if(!(o instanceof Course)) { return false; }
    Course c = (Course) o;
    return c.title == this.title && c.obstacleCount == this.obstacleCount;
  }

 @Override
  public int hashCode() {
    return (title == null ? 0 : title.hashCode()) * obstacleCount; 
  }
}

class Run {
  /* Data and methods about a single run of the obstacle course */
  public Course course; // The Course object this run is for
  public boolean complete; // true if the run is a full run of the course
                            // false if the run is in progress or was aborted
  public List<Integer> obstacleTimes; // The times it took to complete each obstacle

 public Run(Course runCourse) {
    course = runCourse;
    complete = false;
    obstacleTimes = new ArrayList<>();
  }

 public void addObstacleTime(int obstacleTime) {
    // When an obstacle is completed, add the time to the current run.
    // Params:
    //   obstacleTime: the time in seconds it took to complete the obstacle
    if(complete) {
      throw new IllegalStateException("Cannot add obstacle to complete run");
    }
    obstacleTimes.add(obstacleTime);
    if(obstacleTimes.size() == course.obstacleCount) {
      complete = true;
    }
  }

 public int getRunTime() {
    // Returns the total time this run has taken.
    // If the run is not complete, it returns the time taken so far.
    return obstacleTimes.stream().mapToInt(Integer::intValue).sum();  
  }
}

class RunCollection {
  public Course course; // the Course this RunCollection is for
  public List<Run> runs;  // the Run objects for this particular course

 public RunCollection(Course collectionCourse) {
    course = collectionCourse;
    runs = new ArrayList<>();
  }

  public int getNumRuns() {
    // Returns the number of runs in this collection
    return runs.size();
  }

  public void addRun(Run run) {
    // Adds a run to this collection
    if(!run.course.equals(course)) {
      throw new IllegalArgumentException("run's Course is not the same as the RunCollection's");
    }
    runs.add(run);
  }
#######Bug in the below method: 
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

}

public class Solution {
  public static void main(String[] argv) {
    testRun();
    testRunCollection();
  }

 // This is not a complete test suite, but tests some basic functionality of the above code, and
  // shows some examples of using the code.
  public static void testRun() {
    System.out.println("Running testRun");
    Course testCourse = new Course("Test course", 2);
    Run testRun = new Run(testCourse);
    testRun.addObstacleTime(3);
    assert !testRun.complete : "Test run should not be complete";
    testRun.addObstacleTime(5);
    assert testRun.complete : "Test run should be complete";
    assert testRun.obstacleTimes.equals(new ArrayList<Integer>(List.of(3, 5))) :
      "obstacleTimes should be [3, 5], was " + testRun.obstacleTimes;
    assert testRun.getRunTime() == 8 : "getRunTime should return 8, returned " + testRun.getRunTime();
    try {
      testRun.addObstacleTime(4);
      assert false : "adding obstacle time to complete run should throw";
    } catch(IllegalStateException e) {
      // expected
    }
  }

 public static RunCollection makeRunCollection(Course course, int[][] obstacleData) {
    // Create a new RunCollection for test purposes.
    // Params:
    //   course: the Course object this RunCollection is for
    //   obstacleData: an int[][]. Each int[] represents obstacle times for a single
    //                 run of the course.
    RunCollection runCollection = new RunCollection(course);
    for(int[] runData : obstacleData) {
      Run run = new Run(course);
      for(int obstacleTime : runData) {
        run.addObstacleTime(obstacleTime);
      }
      runCollection.addRun(run);
    }
    return runCollection;
  }

 public static void testRunCollection() {
    // Tests basic RunCollection functionality

   //    Obstacles: O1  O2  O3  O4
    //    Run 1:      3   4   5   6    (total: 18 seconds)
    //    Run 2:      4   4   4   5    (total: 17 seconds)
    //    Run 3:      4   5   4   6    (total: 19 seconds)
    //    Run 4:      5   5   3        (13 seconds, but run is incomplete)
    System.out.println("Running testRunCollection");
    int[][] obstacleData = new int[][] {{3, 4, 5, 6},
                                        {4, 4, 4, 5},
                                        {4, 5, 4, 6},
                                        {5, 5, 3}};
    Course testCourse = new Course("Test course", 4);
    RunCollection runCollection = makeRunCollection(testCourse, obstacleData);

    int numRuns = obstacleData.length;
    assert runCollection.getNumRuns() == numRuns : "number of runs should be " + numRuns + ", was " + runCollection.getNumRuns();
    assert runCollection.personalBest() == 17 : 
      "personalBest should be 17, was " + runCollection.personalBest();

 

 }
}

The RunCollection test expects personalBest() to return 17, which is the best completed run time. But the current implementation returns 13, because it’s incorrectly including an incomplete run

The fix is to consider only completed runs when computing personalBest().”

So we filter by run.complete == true:

Filter: runs.stream().filter(r -> r.complete)
Then min of getRunTime() among completed runs only

If no completed runs exist, return something safe like Integer.MAX_VALUE (or 0 / Optional depending on design).

The test fails because personalBest() computes the minimum time across all runs, including incomplete ones. In our data, run 4 is incomplete with a partial time of 13 seconds, which is less than any completed run, so personalBest() returns 13. But personal best should only be based on completed runs, and the best completed run is 17. The fix is to filter the stream to only complete runs before taking the min.”


Answer : update
  public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

to


public int personalBest() {
    // Returns the best *completed* finish time achieved in this RunCollection
    return runs.stream()
               .filter(r -> r.complete)
               .mapToInt(Run::getRunTime)
               .min()
               .orElse(Integer.MAX_VALUE);
  }


Task 2 : 
bestOfBests represents the fastest possible full run if everything went perfectly. To compute it, I take the minimum time for each obstacle index across all runs, including incomplete runs, and then sum those minima.”

The course has N = course.obstacleCount obstacles.
For each obstacle index i from 0 to N-1:

Look across all runs.
Consider only runs that actually have a recorded time for obstacle i (i.e., run.obstacleTimes.size() > i).
Find the minimum time for that obstacle.


Add those minimum times together to get the final “perfect run” time.

“Incomplete runs might still contain a fast time for obstacle 1, 2, or 3, so they should be included when taking the minimum per obstacle.”

If no run has a recorded time for some obstacle i, then we can’t compute a complete ‘best possible full run’. In that case, I’ll return Integer.MAX_VALUE (similar to how personalBest returns MAX_VALUE when nothing is found).”

If R is number of runs and N is obstacle count:

Time: O(R × N)
Space: O(1) extra (besides input)


public int bestOfBests() {
    // For each obstacle index, take the fastest recorded time across all runs (even incomplete),
    // then sum those fastest times.
    int total = 0;

   for (int i = 0; i < course.obstacleCount; i++) {
      int bestForObstacle = Integer.MAX_VALUE;

     for (Run r : runs) {
        if (r.obstacleTimes.size() > i) {
          bestForObstacle = Math.min(bestForObstacle, r.obstacleTimes.get(i));
        }
      }
     
     // If no run had this obstacle time recorded, we can't compute a full best-of-bests.
      if (bestForObstacle == Integer.MAX_VALUE) {
        return Integer.MAX_VALUE;
      }
     
     total += bestForObstacle;
    }

   return total;
  }

Obstacle Problem:
Question   : /*
We are writing software to collect and manage data on how fast racers can complete obstacle courses. An obstacle course is a series of difficult physical challenges (like walls, hurdles, and ponds) that a racer must go through.

Each course consists of multiple obstacles. The software stores how long it takes for racers to finish each obstacle, and provides useful statistics based on those times.

Definitions:
* A "run" is a particular attempt to complete an entire obstacle course
* A "run collection" is a group of runs on a particular course by the user.
* An "obstacle" is a portion of a course. We track how long it takes to finish each portion of the course

For example, here are some times for an obstacle course with four obstacles:

Obstacles:    O1  O2  O3  O4
    Run 1:      3   4   5   6    (total: 18 seconds)
    Run 2:      4   4   4   5    (total: 17 seconds)
    Run 3:      4   5   4   6    (total: 19 seconds)
    Run 4:      5   5   3        (13 seconds, but run is incomplete)

All of these runs for one obstacle course (including the incomplete run) make up a run collection.

To begin with, we present you with two tasks:
1-1) Read through and understand the code below. Please take as much time as necessary, and feel free to run the code.
1-2) The test for RunCollection is not passing due to a bug in the code. Make the necessary changes to RunCollection to fix the bug.


2) We would like to implement a new function in RunCollection called "bestOfBests". This is a measure of how fast a run could be if everything went perfectly, and is determined by taking the fastest times for each obstacle across all runs (even incomplete ones) and summing them.

Implement this function, and add a test to verify that it works.
*/

 


import java.util.*;

class Course {
  /* Data about a particular course. */
  public String title;  // The name of the obstacle course
  public int obstacleCount;  // The number of obstacles in the course

 public Course(String courseTitle, int obstacles) {
    title = courseTitle;
    obstacleCount = obstacles;
  }

 @Override
  public boolean equals(Object o) {
    if(!(o instanceof Course)) { return false; }
    Course c = (Course) o;
    return c.title == this.title && c.obstacleCount == this.obstacleCount;
  }

 @Override
  public int hashCode() {
    return (title == null ? 0 : title.hashCode()) * obstacleCount; 
  }
}

class Run {
  /* Data and methods about a single run of the obstacle course */
  public Course course; // The Course object this run is for
  public boolean complete; // true if the run is a full run of the course
                            // false if the run is in progress or was aborted
  public List<Integer> obstacleTimes; // The times it took to complete each obstacle

 public Run(Course runCourse) {
    course = runCourse;
    complete = false;
    obstacleTimes = new ArrayList<>();
  }

 public void addObstacleTime(int obstacleTime) {
    // When an obstacle is completed, add the time to the current run.
    // Params:
    //   obstacleTime: the time in seconds it took to complete the obstacle
    if(complete) {
      throw new IllegalStateException("Cannot add obstacle to complete run");
    }
    obstacleTimes.add(obstacleTime);
    if(obstacleTimes.size() == course.obstacleCount) {
      complete = true;
    }
  }

 public int getRunTime() {
    // Returns the total time this run has taken.
    // If the run is not complete, it returns the time taken so far.
    return obstacleTimes.stream().mapToInt(Integer::intValue).sum();  
  }
}

class RunCollection {
  public Course course; // the Course this RunCollection is for
  public List<Run> runs;  // the Run objects for this particular course

 public RunCollection(Course collectionCourse) {
    course = collectionCourse;
    runs = new ArrayList<>();
  }

  public int getNumRuns() {
    // Returns the number of runs in this collection
    return runs.size();
  }

  public void addRun(Run run) {
    // Adds a run to this collection
    if(!run.course.equals(course)) {
      throw new IllegalArgumentException("run's Course is not the same as the RunCollection's");
    }
    runs.add(run);
  }
#######Bug in the below method: 
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

#######Above issue Bug Fix
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().filter(v->v.complete).mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

//New Functionality implemented code for the 2nd Question
public int bestOfBest() {
    int total = 0;
    for (int i = 0; i < course.obstacleCount; i++) {
        // to find the minimum time
        int minTime = Integer.MAX_VALUE;
        for (Run run : runs) {
            // run reached the obstacles
            if (run.obstacleTimes.size() > i) {
                minTime = Math.min(minTime, run.obstacleTimes.get(i));
            }
        }
        // condition that checks if no such run exist
        if (minTime == Integer.MAX_VALUE) {
            throw new IllegalStateException("No recorded time for obstacles: "+ i);
        }
        total = total + minTime;
    }
    System.out.println("Fastest run completed in time is :" +total+ " Seconds");
    return total;

}

 

}

public class Solution {
  public static void main(String[] argv) {
    testRun();
    testRunCollection();
  }

 // This is not a complete test suite, but tests some basic functionality of the above code, and
  // shows some examples of using the code.
  public static void testRun() {
    System.out.println("Running testRun");
    Course testCourse = new Course("Test course", 2);
    Run testRun = new Run(testCourse);
    testRun.addObstacleTime(3);
    assert !testRun.complete : "Test run should not be complete";
    testRun.addObstacleTime(5);
    assert testRun.complete : "Test run should be complete";
    assert testRun.obstacleTimes.equals(new ArrayList<Integer>(List.of(3, 5))) :
      "obstacleTimes should be [3, 5], was " + testRun.obstacleTimes;
    assert testRun.getRunTime() == 8 : "getRunTime should return 8, returned " + testRun.getRunTime();
    try {
      testRun.addObstacleTime(4);
      assert false : "adding obstacle time to complete run should throw";
    } catch(IllegalStateException e) {
      // expected
    }
  }

 public static RunCollection makeRunCollection(Course course, int[][] obstacleData) {
    // Create a new RunCollection for test purposes.
    // Params:
    //   course: the Course object this RunCollection is for
    //   obstacleData: an int[][]. Each int[] represents obstacle times for a single
    //                 run of the course.
    RunCollection runCollection = new RunCollection(course);
    for(int[] runData : obstacleData) {
      Run run = new Run(course);
      for(int obstacleTime : runData) {
        run.addObstacleTime(obstacleTime);
      }
      runCollection.addRun(run);
    }
    return runCollection;
  }

 public static void testRunCollection() {
    // Tests basic RunCollection functionality

   //    Obstacles: O1  O2  O3  O4
    //    Run 1:      3   4   5   6    (total: 18 seconds)
    //    Run 2:      4   4   4   5    (total: 17 seconds)
    //    Run 3:      4   5   4   6    (total: 19 seconds)
    //    Run 4:      5   5   3        (13 seconds, but run is incomplete)
    System.out.println("Running testRunCollection");
    int[][] obstacleData = new int[][] {{3, 4, 5, 6},
                                        {4, 4, 4, 5},
                                        {4, 5, 4, 6},
                                        {5, 5, 3}};
    Course testCourse = new Course("Test course", 4);
    RunCollection runCollection = makeRunCollection(testCourse, obstacleData);

    int numRuns = obstacleData.length;
    assert runCollection.getNumRuns() == numRuns : "number of runs should be " + numRuns + ", was " + runCollection.getNumRuns();
    assert runCollection.personalBest() == 17 : 
      "personalBest should be 17, was " + runCollection.personalBest();

 

 }
}

The RunCollection test expects personalBest() to return 17, which is the best completed run time. But the current implementation returns 13, because it’s incorrectly including an incomplete run

The fix is to consider only completed runs when computing personalBest().”

So we filter by run.complete == true:

Filter: runs.stream().filter(r -> r.complete)
Then min of getRunTime() among completed runs only

If no completed runs exist, return something safe like Integer.MAX_VALUE (or 0 / Optional depending on design).

The test fails because personalBest() computes the minimum time across all runs, including incomplete ones. In our data, run 4 is incomplete with a partial time of 13 seconds, which is less than any completed run, so personalBest() returns 13. But personal best should only be based on completed runs, and the best completed run is 17. The fix is to filter the stream to only complete runs before taking the min.”


Answer : update
  public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

to


public int personalBest() {
    // Returns the best *completed* finish time achieved in this RunCollection
    return runs.stream()
               .filter(r -> r.complete)
               .mapToInt(Run::getRunTime)
               .min()
               .orElse(Integer.MAX_VALUE);
  }


Task 2 : 
bestOfBests represents the fastest possible full run if everything went perfectly. To compute it, I take the minimum time for each obstacle index across all runs, including incomplete runs, and then sum those minima.”

The course has N = course.obstacleCount obstacles.
For each obstacle index i from 0 to N-1:

Look across all runs.
Consider only runs that actually have a recorded time for obstacle i (i.e., run.obstacleTimes.size() > i).
Find the minimum time for that obstacle.


Add those minimum times together to get the final “perfect run” time.

“Incomplete runs might still contain a fast time for obstacle 1, 2, or 3, so they should be included when taking the minimum per obstacle.”

If no run has a recorded time for some obstacle i, then we can’t compute a complete ‘best possible full run’. In that case, I’ll return Integer.MAX_VALUE (similar to how personalBest returns MAX_VALUE when nothing is found).”

If R is number of runs and N is obstacle count:

Time: O(R × N)
Space: O(1) extra (besides input)


public int bestOfBests() {
    // For each obstacle index, take the fastest recorded time across all runs (even incomplete),
    // then sum those fastest times.
    int total = 0;

   for (int i = 0; i < course.obstacleCount; i++) {
      int bestForObstacle = Integer.MAX_VALUE;

     for (Run r : runs) {
        if (r.obstacleTimes.size() > i) {
          bestForObstacle = Math.min(bestForObstacle, r.obstacleTimes.get(i));
        }
      }
     
     // If no run had this obstacle time recorded, we can't compute a full best-of-bests.
      if (bestForObstacle == Integer.MAX_VALUE) {
        return Integer.MAX_VALUE;
      }
     
     total += bestForObstacle;
    }

   return total;
  }

Test case: 2nd Question
//bestOfBests: 3+4+3+5 = 15
assert runCollection.bestOfBest() == 15 : "bestOfBests should be 15, was "+runCollection.bestOfBest();



We are writing software to analyze logs for toll booths on a highway. This highway is a divided highway with limited access; the only way on to or off of the highway is through a toll booth.
There are three types of toll booths:
* ENTRY (E in the diagram) toll booths, where a car goes through a booth as it enters the highway.
* EXIT (X in the diagram) toll booths, where a car goes through a booth as it exits the highway.
* MAINROAD (M in the diagram), which have sensors that record a license plate as a car drives through at full speed.

        Exit Booth                         Entry Booth
            |                                   |
            X                                   E
             \                                 /
---<------------<---------M---------<-----------<---------<----
                                         (West-bound side)
===============================================================
                                         (East-bound side)
------>--------->---------M--------->--------->--------->------
             /                                 \
            E                                   X
            |                                   |
        Entry Booth                         Exit Booth
For our first task:
1-1) Read through and understand the code and comments below. Feel free to run the code and tests.
1-2) The tests are not passing due to a bug in the code. Make the necessary changes to LogEntry to fix the bug.
*/
class LogEntry {
  /**
   * Represents an entry from a single log line. Log lines look like this in the file:
   *
   * 34400.409 SXY288 210E ENTRY
   *
   * Where:
   * * 34400.409 is the timestamp in seconds since the software was started.
   * * SXY288 is the license plate of the vehicle passing through the toll booth.
   * * 210E is the location and traffic direction of the toll booth. Here, the toll
   *     booth is at 210 kilometers from the start of the tollway, and the E indicates
   *     that the toll booth was on the east-bound traffic side. Tollbooths are placed
   *     every ten kilometers.
   * * ENTRY indicates which type of toll booth the vehicle went through. This is one of
   *     "ENTRY", "EXIT", or "MAINROAD".
   **/
  private final String timestamp;
  private final String licensePlate;
  private final String boothType;
  private final int location;
  private final String direction;
  public LogEntry(String logLine) {
    String[] tokens = logLine.split(" ");
    this.timestamp = tokens[0];
    this.licensePlate = tokens[1];
    this.boothType = tokens[3];
    this.location =
      Integer.parseInt(tokens[2].substring(0, tokens[2].length() - 1));
    String directionLetter = tokens[2].substring(tokens[2].length() - 1);
    if (directionLetter.equals("E")) {
      this.direction = "EAST";
    } else if (directionLetter.equals("W")) {
      this.direction = "WEST";
    } else {
      throw new IllegalArgumentException();
    }
  }
  public String getTimestamp() {
    return timestamp;
  }
  public String getLicensePlate() {
    return licensePlate;
  }
  public String getBoothType() {
    return boothType;
  }
  public int getLocation() {
    return location;
  }
  public String getDirection() {
    return direction;
  }
  @Override
  public String toString() {
    return String.format(
      "<LogEntry timestamp: %f  license: %s  location: %d  direction: %s  booth type: %s>",
      timestamp,
      licensePlate,
      location,
      direction,
      boothType
    );
  }
}
class LogFile {
  /*
   * Represents a file containing a number of log lines, converted to LogEntry
   * objects.
   */
   List<LogEntry> logEntries;
   public LogFile(BufferedReader reader) throws IOException {
     this.logEntries = new ArrayList<>();
     String line = reader.readLine();
     while (line != null) {
      LogEntry logEntry = new LogEntry(line.strip());
      this.logEntries.add(logEntry);
      line = reader.readLine();
     }
   }
   public LogEntry get(int index) {
     return this.logEntries.get(index);
   }
   public int size() {
     return this.logEntries.size();
   }
 }
 public class Solution {
   public static void main(String[] argv) throws IOException {
     testLogFile();
     testLogEntry();
   }
   public static void testLogFile() throws IOException {
     System.out.println("Running testLogFile");
     try (
      BufferedReader reader = new BufferedReader(
        new FileReader("/content/test/tollbooth_small.log")
      );
     ) {
      LogFile logFile = new LogFile(reader);
      assertEquals(13, logFile.size());
      for (LogEntry entry : logFile.logEntries) {
        assert (entry instanceof LogEntry);
      }
     }
   }
   public static void testLogEntry() {
     System.out.println("Running testLogEntry");
     String logLine = "44776.619 KTB918 310E MAINROAD";
     LogEntry logEntry = new LogEntry(logLine);
     assertEquals(44776.619f, logEntry.getTimestamp(), 0.0001);
     assertEquals("KTB918", logEntry.getLicensePlate());
     assertEquals(310, logEntry.getLocation());
     assertEquals("EAST", logEntry.getDirection());
     assertEquals("MAINROAD", logEntry.getBoothType());
     logLine = "52160.132 ABC123 400W ENTRY";
     logEntry = new LogEntry(logLine);
     assertEquals(52160.132f, logEntry.getTimestamp(), 0.0001);
     assertEquals("ABC123", logEntry.getLicensePlate());
     assertEquals(400, logEntry.getLocation());
     assertEquals("WEST", logEntry.getDirection());
     assertEquals("ENTRY", logEntry.getBoothType());
   }
 }

1-2) The tests are not passing due to a bug in the code. Make the necessary changes to LogEntry to fix the bug.

The bug is that timestamp is stored as a String, but the tests treat it as a float (assertEquals(44776.619f, logEntry.getTimestamp(), ...)).
So the test fails either due to type mismatch (won’t compile in real JUnit) or because the toString() uses %f which expects a numeric type, not a String.

Walkthrough

“The unit test expects getTimestamp() to return a numeric value because it compares it using floating point assert with a delta.”
assertEquals(44776.619f, logEntry.getTimestamp(), 0.0001);


In LogEntry, timestamp is declared as private final String timestamp; and assigned using tokens[0] directly. So we never parse it to a numeric type.”
String.format("<LogEntry timestamp: %f ...>", timestamp, ...)
%f expects a float/double → this is inconsistent with storing a String.


Because timestamp isn’t numeric, the getter doesn’t match how the rest of the program and tests use it. It breaks comparisons, sorting, and formatted output.”

Fix is to store timestamp as double (or float) and parse it in the constructor. Then getTimestamp() should return the numeric type, and toString() will work correctly with %f.”

String[] tokens = logLine.split(" "); ----> String[] tokens = logLine.split("\\s+");

convert private final String timestamp; ---> private final float timestamp;
convert this.timestamp = tokens[0]; -> this.timestamp = Double.parseDouble(tokens[0]);
convert public String getTimestamp() { ---> public float getTimestamp() {


“The tests are failing because timestamp is stored as a String in LogEntry, but the tests treat it as a numeric value and compare it using floating-point assert with a delta. Also toString() formats timestamp using %f, which expects a numeric type. The fix is to change timestamp to a double or float, parse it in the constructor using Double.parseDouble(tokens[0]), and return that numeric value from getTimestamp(). This aligns implementation with how hash-based comparisons and formatting are intended, and the tests pass.”


2-1)  Write a function to count number of journeys.   

Logs are processed in timestamp order (or the file already is).
A journey starts at ENTRY and ends at EXIT.
MAINROAD entries don’t affect journey count.
If an EXIT appears with no prior ENTRY for that plate+direction, we ignore it (incomplete journey).
A car cannot be on two journeys at once on the same direction; we track “active” journeys.


“I need to track which vehicles are currently on the highway—meaning they’ve entered but not yet exited. That’s a membership problem: is this vehicle currently active or not?”

When I see an ENTRY, I mark the vehicle as active.
When I see an EXIT, I check if it was active.

If yes → I count one completed journey and remove it from active.
If no → it’s an unmatched exit, so ignore or log it.

Why Set is perfect:

add, remove, contains are average O(1).
We don’t need ordering or counts per vehicle — just “active or not”.

A vehicle is identified by license plate, and I also include direction because the same plate could appear on both sides or direction matters in logs.”
"ABC123|EAST"
“I’ll keep an integer journeys = 0 to count completed journeys, and a Set<String> active to store currently active vehicles.”


journeys tracks the output.
active tracks cars that are currently inside the highway.

“I scan logs one by one in time order. Each entry is either ENTRY, EXIT, or MAINROA
For every entry:

Extract type = getBoothType()
Build key = plate + "|" + direction

If it’s an ENTRY

“ENTRY means the car has started a journey. I add it to the active set.”


active.add(key)

If entry duplicates happen, Set naturally avoids duplicates.

“Even if the same ENTRY appears twice, Set prevents duplicate state, and we still count only when it exits.”

“EXIT means the car is leaving the highway. I only count a journey if we had a matching active entry.”

So:

If active contains the key → remove it and increment journeys.
If not found → ignore it as invalid/incomplete logs.

In code, I use:

if (active.remove(key)) journeys++;

Explain why this is nice:

“remove() returns true only if the key existed, so I can combine the check and removal in one operation.”

“Time is O(n) because I scan the log once. Space is O(a) where a is the number of cars currently active on the highway.”


public int countJourneys() {
    Set<String> activeJourneys = new HashSet<>();
    int journeys = 0;

    for (LogEntry entry : logEntries) {
      String key = entry.getLicensePlate() + "|" + entry.getDirection();
      String type = entry.getBoothType();
     
      if ("ENTRY".equals(type)) {
        // Start journey (or keep it active if already active)
        activeJourneys.add(key);
     
      } else if ("EXIT".equals(type)) {
        // Count only if there was a previous unmatched ENTRY
        if (activeJourneys.remove(key)) {
          journeys++;
        }
      }
      // MAINROAD does not affect journey boundaries
    }
     
    return journeys;
  }

3-1) We would like to catch people who are driving at unsafe speeds on the highway. To help us do that, we would like to identify journeys where a driver does either of the following:
* Drive 130 km/h or greater in any individual 10km segment of tollway.
* Drive 120 km/h or greater in any two 10km segments of tollway.

For example, consider the following journey:
1000.000 TST002 270W ENTRY
1275.000 TST002 260W EXIT

In this case, the driver of TST002 drove 10 km in 275 seconds. We can calculate
that this driver drove an average speed of ~130.91km/hr over this segment:

10 km * 3600 sec/hr
------------------- = 130.91 km/hr
      275 sec

Note that:
* A license plate may have multiple journeys in one file, and if they drive at unsafe speeds in both journeys, both should be counted.
* We do not mark speeding if they are not on the highway (i.e. for any driving between an EXIT and ENTRY event).
* Speeding is only marked once per journey. For example, if there are 4 segments 120km/h or greater, or multiple segments 130km/h or greater, the journey is only counted once.

q. Write a function catchSpeeders in LogFile that returns a collection of license plates that drove at unsafe speeds during a journey in the LogFile.
     If the same license plate drives at unsafe speeds during two different journeys, the license plate should appear twice (once for each journey they drove at unsafe speeds).

Maintain journey state :


private static class JourneyState {
    LogEntry last;           // last log entry seen on-highway
    int segments120OrMore;   // count of 10km segments >= 120 km/h
    boolean flagged;         // whether speeding already detected for this journey

    JourneyState(LogEntry start) {
      this.last = start;
      this.segments120OrMore = 0;
      this.flagged = false;
    }
  }


public List<String> catchSpeeders() {
    Map<String, JourneyState> active = new HashMap<>();
    List<String> speeders = new ArrayList<>();

    for (LogEntry e : logEntries) {
      String type = e.getBoothType();
      String key = e.getLicensePlate() + "|" + e.getDirection();
     
      if ("ENTRY".equals(type)) {
        // Start or restart a journey for this plate+direction
        active.put(key, new JourneyState(e));
        continue;
      }
     
      JourneyState state = active.get(key);
      if (state == null) {
        // Not on the highway (or missing ENTRY); ignore this record.
        continue;
      }
     
      // We are on-highway: compute segment stats from state.last -> e
      float dt = e.getTimestamp() - state.last.getTimestamp(); // seconds
      int distanceKm = Math.abs(e.getLocation() - state.last.getLocation());
     
      // Update last regardless; but only compute speeds if we have a valid segment
      state.last = e;
     
      if (dt <= 0 || distanceKm <= 0) {
        // Non-increasing time or no movement: ignore segment
      } else {
        int segments = distanceKm / 10; // number of 10km segments
        if (segments > 0) {
          float speedKmh = (distanceKm * 3600.0f) / dt;
     
          if (speedKmh >= 130.0f) {
            state.flagged = true;
          }
          if (speedKmh >= 120.0f) {
            state.segments120OrMore += segments;
            if (state.segments120OrMore >= 2) {
              state.flagged = true;
            }
          }
        }
      }
     
      if ("EXIT".equals(type)) {
        // Journey ends here; count at most once for this journey
        if (state.flagged) {
          speeders.add(e.getLicensePlate());
        }
        active.remove(key);
      }
    }
     
    return speeders;
  }
 ---------------------------------------------------------------------------

hi

What is the purpose of the equals() and hashCode() method of object class in Java?

equals() and hashCode(), explain role of equals() and hashCode() for hashmap & hashset?

2) What is Dependency Injection (DI) in Java?

3) How we are designing a class?

4) what is the advantage and disadvantage of checked exception?

5) what is the advantage of upper bound and lower bound (<? extends Animal>, <? super Animal>)?

6) Can a map key mutable or not? why?

7) What is effectively final variable and how is it used?

8) When the variables are moved from one to another heap generation

9) How we are designing a class?

10) What is the purpose of  final keyword?

11) What is the purpose of bounded wildcards in Generics?

12) Given below code what is the problem with it :
public Boolean isCondition(Boolean value){
   if(!value.equals(Boolean.false)){
    return true;
  }else{
             return false;
  }
}

13)

14) How Design patterns that can apply to make a class more testable
15) What is the best way to implement code following design principles?
16) How to create mutable class.

We are writing software to collect and manage data on how fast racers can complete obstacle courses. An obstacle course is a series of difficult physical challenges (like walls, hurdles, and ponds) that a racer must go through.

Each course consists of multiple obstacles. The software stores how long it takes for racers to finish each obstacle, and provides useful statistics based on those times.

Definitions:
* A "run" is a particular attempt to complete an entire obstacle course
* A "run collection" is a group of runs on a particular course by the user.
* An "obstacle" is a portion of a course. We track how long it takes to finish each portion of the course

For example, here are some times for an obstacle course with four obstacles:

Obstacles:    O1  O2  O3  O4
    Run 1:      3   4   5   6    (total: 18 seconds)
    Run 2:      4   4   4   5    (total: 17 seconds)
    Run 3:      4   5   4   6    (total: 19 seconds)
    Run 4:      5   5   3        (13 seconds, but run is incomplete)

All of these runs for one obstacle course (including the incomplete run) make up a run collection.

To begin with, we present you with two tasks:

import java.util.*;

class Course {
  /* Data about a particular course. */
  public String title;  // The name of the obstacle course
  public int obstacleCount;  // The number of obstacles in the course

 public Course(String courseTitle, int obstacles) {
    title = courseTitle;
    obstacleCount = obstacles;
  }

 @Override
  public boolean equals(Object o) {
    if(!(o instanceof Course)) { return false; }
    Course c = (Course) o;
    return c.title == this.title && c.obstacleCount == this.obstacleCount;
  }

 @Override
  public int hashCode() {
    return (title == null ? 0 : title.hashCode()) * obstacleCount; 
  }
}

class Run {
  /* Data and methods about a single run of the obstacle course */
  public Course course; // The Course object this run is for
  public boolean complete; // true if the run is a full run of the course
                            // false if the run is in progress or was aborted
  public List<Integer> obstacleTimes; // The times it took to complete each obstacle

 public Run(Course runCourse) {
    course = runCourse;
    complete = false;
    obstacleTimes = new ArrayList<>();
  }

 public void addObstacleTime(int obstacleTime) {
    // When an obstacle is completed, add the time to the current run.
    // Params:
    //   obstacleTime: the time in seconds it took to complete the obstacle
    if(complete) {
      throw new IllegalStateException("Cannot add obstacle to complete run");
    }
    obstacleTimes.add(obstacleTime);
    if(obstacleTimes.size() == course.obstacleCount) {
      complete = true;
    }
  }

 public int getRunTime() {
    // Returns the total time this run has taken.
    // If the run is not complete, it returns the time taken so far.
    return obstacleTimes.stream().mapToInt(Integer::intValue).sum();  
  }
}

class RunCollection {
  public Course course; // the Course this RunCollection is for
  public List<Run> runs;  // the Run objects for this particular course

 public RunCollection(Course collectionCourse) {
    course = collectionCourse;
    runs = new ArrayList<>();
  }

  public int getNumRuns() {
    // Returns the number of runs in this collection
    return runs.size();
  }

  public void addRun(Run run) {
    // Adds a run to this collection
    if(!run.course.equals(course)) {
      throw new IllegalArgumentException("run's Course is not the same as the RunCollection's");
    }
    runs.add(run);
  }
#######Bug in the below method: 
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

}

public class Solution {
  public static void main(String[] argv) {
    testRun();
    testRunCollection();
  }

 // This is not a complete test suite, but tests some basic functionality of the above code, and
  // shows some examples of using the code.
  public static void testRun() {
    System.out.println("Running testRun");
    Course testCourse = new Course("Test course", 2);
    Run testRun = new Run(testCourse);
    testRun.addObstacleTime(3);
    assert !testRun.complete : "Test run should not be complete";
    testRun.addObstacleTime(5);
    assert testRun.complete : "Test run should be complete";
    assert testRun.obstacleTimes.equals(new ArrayList<Integer>(List.of(3, 5))) :
      "obstacleTimes should be [3, 5], was " + testRun.obstacleTimes;
    assert testRun.getRunTime() == 8 : "getRunTime should return 8, returned " + testRun.getRunTime();
    try {
      testRun.addObstacleTime(4);
      assert false : "adding obstacle time to complete run should throw";
    } catch(IllegalStateException e) {
      // expected
    }
  }

 public static RunCollection makeRunCollection(Course course, int[][] obstacleData) {
    // Create a new RunCollection for test purposes.
    // Params:
    //   course: the Course object this RunCollection is for
    //   obstacleData: an int[][]. Each int[] represents obstacle times for a single
    //                 run of the course.
    RunCollection runCollection = new RunCollection(course);
    for(int[] runData : obstacleData) {
      Run run = new Run(course);
      for(int obstacleTime : runData) {
        run.addObstacleTime(obstacleTime);
      }
      runCollection.addRun(run);
    }
    return runCollection;
  }

 public static void testRunCollection() {
    // Tests basic RunCollection functionality

   //    Obstacles: O1  O2  O3  O4
    //    Run 1:      3   4   5   6    (total: 18 seconds)
    //    Run 2:      4   4   4   5    (total: 17 seconds)
    //    Run 3:      4   5   4   6    (total: 19 seconds)
    //    Run 4:      5   5   3        (13 seconds, but run is incomplete)
    System.out.println("Running testRunCollection");
    int[][] obstacleData = new int[][] {{3, 4, 5, 6},
                                        {4, 4, 4, 5},
                                        {4, 5, 4, 6},
                                        {5, 5, 3}};
    Course testCourse = new Course("Test course", 4);
    RunCollection runCollection = makeRunCollection(testCourse, obstacleData);

    int numRuns = obstacleData.length;
    assert runCollection.getNumRuns() == numRuns : "number of runs should be " + numRuns + ", was " + runCollection.getNumRuns();
    assert runCollection.personalBest() == 17 : 
      "personalBest should be 17, was " + runCollection.personalBest();

 

 }
}

The RunCollection test expects personalBest() to return 17, which is the best completed run time. But the current implementation returns 13, because it’s incorrectly including an incomplete run

The fix is to consider only completed runs when computing personalBest().”

So we filter by run.complete == true:

Filter: runs.stream().filter(r -> r.complete)
Then min of getRunTime() among completed runs only

If no completed runs exist, return something safe like Integer.MAX_VALUE (or 0 / Optional depending on design).

The test fails because personalBest() computes the minimum time across all runs, including incomplete ones. In our data, run 4 is incomplete with a partial time of 13 seconds, which is less than any completed run, so personalBest() returns 13. But personal best should only be based on completed runs, and the best completed run is 17. The fix is to filter the stream to only complete runs before taking the min.”


Answer : update
  public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

to


public int personalBest() {
    // Returns the best *completed* finish time achieved in this RunCollection
    return runs.stream()
               .filter(r -> r.complete)
               .mapToInt(Run::getRunTime)
               .min()
               .orElse(Integer.MAX_VALUE);
  }


Task 2 : 
bestOfBests represents the fastest possible full run if everything went perfectly. To compute it, I take the minimum time for each obstacle index across all runs, including incomplete runs, and then sum those minima.”

The course has N = course.obstacleCount obstacles.
For each obstacle index i from 0 to N-1:

Look across all runs.
Consider only runs that actually have a recorded time for obstacle i (i.e., run.obstacleTimes.size() > i).
Find the minimum time for that obstacle.


Add those minimum times together to get the final “perfect run” time.

“Incomplete runs might still contain a fast time for obstacle 1, 2, or 3, so they should be included when taking the minimum per obstacle.”

If no run has a recorded time for some obstacle i, then we can’t compute a complete ‘best possible full run’. In that case, I’ll return Integer.MAX_VALUE (similar to how personalBest returns MAX_VALUE when nothing is found).”

If R is number of runs and N is obstacle count:

Time: O(R × N)
Space: O(1) extra (besides input)


public int bestOfBests() {
    // For each obstacle index, take the fastest recorded time across all runs (even incomplete),
    // then sum those fastest times.
    int total = 0;

   for (int i = 0; i < course.obstacleCount; i++) {
      int bestForObstacle = Integer.MAX_VALUE;

     for (Run r : runs) {
        if (r.obstacleTimes.size() > i) {
          bestForObstacle = Math.min(bestForObstacle, r.obstacleTimes.get(i));
        }
      }
     
     // If no run had this obstacle time recorded, we can't compute a full best-of-bests.
      if (bestForObstacle == Integer.MAX_VALUE) {
        return Integer.MAX_VALUE;
      }
     
     total += bestForObstacle;
    }

   return total;
  }

Obstacle Problem:
Question   : /*
We are writing software to collect and manage data on how fast racers can complete obstacle courses. An obstacle course is a series of difficult physical challenges (like walls, hurdles, and ponds) that a racer must go through.

Each course consists of multiple obstacles. The software stores how long it takes for racers to finish each obstacle, and provides useful statistics based on those times.

Definitions:
* A "run" is a particular attempt to complete an entire obstacle course
* A "run collection" is a group of runs on a particular course by the user.
* An "obstacle" is a portion of a course. We track how long it takes to finish each portion of the course

For example, here are some times for an obstacle course with four obstacles:

Obstacles:    O1  O2  O3  O4
    Run 1:      3   4   5   6    (total: 18 seconds)
    Run 2:      4   4   4   5    (total: 17 seconds)
    Run 3:      4   5   4   6    (total: 19 seconds)
    Run 4:      5   5   3        (13 seconds, but run is incomplete)

All of these runs for one obstacle course (including the incomplete run) make up a run collection.

To begin with, we present you with two tasks:
1-1) Read through and understand the code below. Please take as much time as necessary, and feel free to run the code.
1-2) The test for RunCollection is not passing due to a bug in the code. Make the necessary changes to RunCollection to fix the bug.


2) We would like to implement a new function in RunCollection called "bestOfBests". This is a measure of how fast a run could be if everything went perfectly, and is determined by taking the fastest times for each obstacle across all runs (even incomplete ones) and summing them.

Implement this function, and add a test to verify that it works.
*/

 


import java.util.*;

class Course {
  /* Data about a particular course. */
  public String title;  // The name of the obstacle course
  public int obstacleCount;  // The number of obstacles in the course

 public Course(String courseTitle, int obstacles) {
    title = courseTitle;
    obstacleCount = obstacles;
  }

 @Override
  public boolean equals(Object o) {
    if(!(o instanceof Course)) { return false; }
    Course c = (Course) o;
    return c.title == this.title && c.obstacleCount == this.obstacleCount;
  }

 @Override
  public int hashCode() {
    return (title == null ? 0 : title.hashCode()) * obstacleCount; 
  }
}

class Run {
  /* Data and methods about a single run of the obstacle course */
  public Course course; // The Course object this run is for
  public boolean complete; // true if the run is a full run of the course
                            // false if the run is in progress or was aborted
  public List<Integer> obstacleTimes; // The times it took to complete each obstacle

 public Run(Course runCourse) {
    course = runCourse;
    complete = false;
    obstacleTimes = new ArrayList<>();
  }

 public void addObstacleTime(int obstacleTime) {
    // When an obstacle is completed, add the time to the current run.
    // Params:
    //   obstacleTime: the time in seconds it took to complete the obstacle
    if(complete) {
      throw new IllegalStateException("Cannot add obstacle to complete run");
    }
    obstacleTimes.add(obstacleTime);
    if(obstacleTimes.size() == course.obstacleCount) {
      complete = true;
    }
  }

 public int getRunTime() {
    // Returns the total time this run has taken.
    // If the run is not complete, it returns the time taken so far.
    return obstacleTimes.stream().mapToInt(Integer::intValue).sum();  
  }
}

class RunCollection {
  public Course course; // the Course this RunCollection is for
  public List<Run> runs;  // the Run objects for this particular course

 public RunCollection(Course collectionCourse) {
    course = collectionCourse;
    runs = new ArrayList<>();
  }

  public int getNumRuns() {
    // Returns the number of runs in this collection
    return runs.size();
  }

  public void addRun(Run run) {
    // Adds a run to this collection
    if(!run.course.equals(course)) {
      throw new IllegalArgumentException("run's Course is not the same as the RunCollection's");
    }
    runs.add(run);
  }
#######Bug in the below method: 
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

#######Above issue Bug Fix
 public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().filter(v->v.complete).mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

//New Functionality implemented code for the 2nd Question
public int bestOfBest() {
    int total = 0;
    for (int i = 0; i < course.obstacleCount; i++) {
        // to find the minimum time
        int minTime = Integer.MAX_VALUE;
        for (Run run : runs) {
            // run reached the obstacles
            if (run.obstacleTimes.size() > i) {
                minTime = Math.min(minTime, run.obstacleTimes.get(i));
            }
        }
        // condition that checks if no such run exist
        if (minTime == Integer.MAX_VALUE) {
            throw new IllegalStateException("No recorded time for obstacles: "+ i);
        }
        total = total + minTime;
    }
    System.out.println("Fastest run completed in time is :" +total+ " Seconds");
    return total;

}

 

}

public class Solution {
  public static void main(String[] argv) {
    testRun();
    testRunCollection();
  }

 // This is not a complete test suite, but tests some basic functionality of the above code, and
  // shows some examples of using the code.
  public static void testRun() {
    System.out.println("Running testRun");
    Course testCourse = new Course("Test course", 2);
    Run testRun = new Run(testCourse);
    testRun.addObstacleTime(3);
    assert !testRun.complete : "Test run should not be complete";
    testRun.addObstacleTime(5);
    assert testRun.complete : "Test run should be complete";
    assert testRun.obstacleTimes.equals(new ArrayList<Integer>(List.of(3, 5))) :
      "obstacleTimes should be [3, 5], was " + testRun.obstacleTimes;
    assert testRun.getRunTime() == 8 : "getRunTime should return 8, returned " + testRun.getRunTime();
    try {
      testRun.addObstacleTime(4);
      assert false : "adding obstacle time to complete run should throw";
    } catch(IllegalStateException e) {
      // expected
    }
  }

 public static RunCollection makeRunCollection(Course course, int[][] obstacleData) {
    // Create a new RunCollection for test purposes.
    // Params:
    //   course: the Course object this RunCollection is for
    //   obstacleData: an int[][]. Each int[] represents obstacle times for a single
    //                 run of the course.
    RunCollection runCollection = new RunCollection(course);
    for(int[] runData : obstacleData) {
      Run run = new Run(course);
      for(int obstacleTime : runData) {
        run.addObstacleTime(obstacleTime);
      }
      runCollection.addRun(run);
    }
    return runCollection;
  }

 public static void testRunCollection() {
    // Tests basic RunCollection functionality

   //    Obstacles: O1  O2  O3  O4
    //    Run 1:      3   4   5   6    (total: 18 seconds)
    //    Run 2:      4   4   4   5    (total: 17 seconds)
    //    Run 3:      4   5   4   6    (total: 19 seconds)
    //    Run 4:      5   5   3        (13 seconds, but run is incomplete)
    System.out.println("Running testRunCollection");
    int[][] obstacleData = new int[][] {{3, 4, 5, 6},
                                        {4, 4, 4, 5},
                                        {4, 5, 4, 6},
                                        {5, 5, 3}};
    Course testCourse = new Course("Test course", 4);
    RunCollection runCollection = makeRunCollection(testCourse, obstacleData);

    int numRuns = obstacleData.length;
    assert runCollection.getNumRuns() == numRuns : "number of runs should be " + numRuns + ", was " + runCollection.getNumRuns();
    assert runCollection.personalBest() == 17 : 
      "personalBest should be 17, was " + runCollection.personalBest();

 

 }
}

The RunCollection test expects personalBest() to return 17, which is the best completed run time. But the current implementation returns 13, because it’s incorrectly including an incomplete run

The fix is to consider only completed runs when computing personalBest().”

So we filter by run.complete == true:

Filter: runs.stream().filter(r -> r.complete)
Then min of getRunTime() among completed runs only

If no completed runs exist, return something safe like Integer.MAX_VALUE (or 0 / Optional depending on design).

The test fails because personalBest() computes the minimum time across all runs, including incomplete ones. In our data, run 4 is incomplete with a partial time of 13 seconds, which is less than any completed run, so personalBest() returns 13. But personal best should only be based on completed runs, and the best completed run is 17. The fix is to filter the stream to only complete runs before taking the min.”


Answer : update
  public int personalBest() {
    // Returns the best finish time achieved in this RunCollection
    return runs.stream().mapToInt(v -> v.getRunTime()).min().orElse(Integer.MAX_VALUE);
  }

to


public int personalBest() {
    // Returns the best *completed* finish time achieved in this RunCollection
    return runs.stream()
               .filter(r -> r.complete)
               .mapToInt(Run::getRunTime)
               .min()
               .orElse(Integer.MAX_VALUE);
  }


Task 2 : 
bestOfBests represents the fastest possible full run if everything went perfectly. To compute it, I take the minimum time for each obstacle index across all runs, including incomplete runs, and then sum those minima.”

The course has N = course.obstacleCount obstacles.
For each obstacle index i from 0 to N-1:

Look across all runs.
Consider only runs that actually have a recorded time for obstacle i (i.e., run.obstacleTimes.size() > i).
Find the minimum time for that obstacle.


Add those minimum times together to get the final “perfect run” time.

“Incomplete runs might still contain a fast time for obstacle 1, 2, or 3, so they should be included when taking the minimum per obstacle.”

If no run has a recorded time for some obstacle i, then we can’t compute a complete ‘best possible full run’. In that case, I’ll return Integer.MAX_VALUE (similar to how personalBest returns MAX_VALUE when nothing is found).”

If R is number of runs and N is obstacle count:

Time: O(R × N)
Space: O(1) extra (besides input)


public int bestOfBests() {
    // For each obstacle index, take the fastest recorded time across all runs (even incomplete),
    // then sum those fastest times.
    int total = 0;

   for (int i = 0; i < course.obstacleCount; i++) {
      int bestForObstacle = Integer.MAX_VALUE;

     for (Run r : runs) {
        if (r.obstacleTimes.size() > i) {
          bestForObstacle = Math.min(bestForObstacle, r.obstacleTimes.get(i));
        }
      }
     
     // If no run had this obstacle time recorded, we can't compute a full best-of-bests.
      if (bestForObstacle == Integer.MAX_VALUE) {
        return Integer.MAX_VALUE;
      }
     
     total += bestForObstacle;
    }

   return total;
  }

Test case: 2nd Question
//bestOfBests: 3+4+3+5 = 15
assert runCollection.bestOfBest() == 15 : "bestOfBests should be 15, was "+runCollection.bestOfBest();


We are writing software to analyze logs for toll booths on a highway. This highway is a divided highway with limited access; the only way on to or off of the highway is through a toll booth.
There are three types of toll booths:
* ENTRY (E in the diagram) toll booths, where a car goes through a booth as it enters the highway.
* EXIT (X in the diagram) toll booths, where a car goes through a booth as it exits the highway.
* MAINROAD (M in the diagram), which have sensors that record a license plate as a car drives through at full speed.

        Exit Booth                         Entry Booth
            |                                   |
            X                                   E
             \                                 /
---<------------<---------M---------<-----------<---------<----
                                         (West-bound side)
===============================================================
                                         (East-bound side)
------>--------->---------M--------->--------->--------->------
             /                                 \
            E                                   X
            |                                   |
        Entry Booth                         Exit Booth
For our first task:
1-1) Read through and understand the code and comments below. Feel free to run the code and tests.
1-2) The tests are not passing due to a bug in the code. Make the necessary changes to LogEntry to fix the bug.
*/
class LogEntry {
  /**
   * Represents an entry from a single log line. Log lines look like this in the file:
   *
   * 34400.409 SXY288 210E ENTRY
   *
   * Where:
   * * 34400.409 is the timestamp in seconds since the software was started.
   * * SXY288 is the license plate of the vehicle passing through the toll booth.
   * * 210E is the location and traffic direction of the toll booth. Here, the toll
   *     booth is at 210 kilometers from the start of the tollway, and the E indicates
   *     that the toll booth was on the east-bound traffic side. Tollbooths are placed
   *     every ten kilometers.
   * * ENTRY indicates which type of toll booth the vehicle went through. This is one of
   *     "ENTRY", "EXIT", or "MAINROAD".
   **/
  private final String timestamp;
  private final String licensePlate;
  private final String boothType;
  private final int location;
  private final String direction;
  public LogEntry(String logLine) {
    String[] tokens = logLine.split(" ");
    this.timestamp = tokens[0];
    this.licensePlate = tokens[1];
    this.boothType = tokens[3];
    this.location =
      Integer.parseInt(tokens[2].substring(0, tokens[2].length() - 1));
    String directionLetter = tokens[2].substring(tokens[2].length() - 1);
    if (directionLetter.equals("E")) {
      this.direction = "EAST";
    } else if (directionLetter.equals("W")) {
      this.direction = "WEST";
    } else {
      throw new IllegalArgumentException();
    }
  }
  public String getTimestamp() {
    return timestamp;
  }
  public String getLicensePlate() {
    return licensePlate;
  }
  public String getBoothType() {
    return boothType;
  }
  public int getLocation() {
    return location;
  }
  public String getDirection() {
    return direction;
  }
  @Override
  public String toString() {
    return String.format(
      "<LogEntry timestamp: %f  license: %s  location: %d  direction: %s  booth type: %s>",
      timestamp,
      licensePlate,
      location,
      direction,
      boothType
    );
  }
}
class LogFile {
  /*
   * Represents a file containing a number of log lines, converted to LogEntry
   * objects.
   */
   List<LogEntry> logEntries;
   public LogFile(BufferedReader reader) throws IOException {
     this.logEntries = new ArrayList<>();
     String line = reader.readLine();
     while (line != null) {
      LogEntry logEntry = new LogEntry(line.strip());
      this.logEntries.add(logEntry);
      line = reader.readLine();
     }
   }
   public LogEntry get(int index) {
     return this.logEntries.get(index);
   }
   public int size() {
     return this.logEntries.size();
   }
 }
 public class Solution {
   public static void main(String[] argv) throws IOException {
     testLogFile();
     testLogEntry();
   }
   public static void testLogFile() throws IOException {
     System.out.println("Running testLogFile");
     try (
      BufferedReader reader = new BufferedReader(
        new FileReader("/content/test/tollbooth_small.log")
      );
     ) {
      LogFile logFile = new LogFile(reader);
      assertEquals(13, logFile.size());
      for (LogEntry entry : logFile.logEntries) {
        assert (entry instanceof LogEntry);
      }
     }
   }
   public static void testLogEntry() {
     System.out.println("Running testLogEntry");
     String logLine = "44776.619 KTB918 310E MAINROAD";
     LogEntry logEntry = new LogEntry(logLine);
     assertEquals(44776.619f, logEntry.getTimestamp(), 0.0001);
     assertEquals("KTB918", logEntry.getLicensePlate());
     assertEquals(310, logEntry.getLocation());
     assertEquals("EAST", logEntry.getDirection());
     assertEquals("MAINROAD", logEntry.getBoothType());
     logLine = "52160.132 ABC123 400W ENTRY";
     logEntry = new LogEntry(logLine);
     assertEquals(52160.132f, logEntry.getTimestamp(), 0.0001);
     assertEquals("ABC123", logEntry.getLicensePlate());
     assertEquals(400, logEntry.getLocation());
     assertEquals("WEST", logEntry.getDirection());
     assertEquals("ENTRY", logEntry.getBoothType());
   }
 }

1-2) The tests are not passing due to a bug in the code. Make the necessary changes to LogEntry to fix the bug.

The bug is that timestamp is stored as a String, but the tests treat it as a float (assertEquals(44776.619f, logEntry.getTimestamp(), ...)).
So the test fails either due to type mismatch (won’t compile in real JUnit) or because the toString() uses %f which expects a numeric type, not a String.

Walkthrough

“The unit test expects getTimestamp() to return a numeric value because it compares it using floating point assert with a delta.”
assertEquals(44776.619f, logEntry.getTimestamp(), 0.0001);


In LogEntry, timestamp is declared as private final String timestamp; and assigned using tokens[0] directly. So we never parse it to a numeric type.”
String.format("<LogEntry timestamp: %f ...>", timestamp, ...)
%f expects a float/double → this is inconsistent with storing a String.


Because timestamp isn’t numeric, the getter doesn’t match how the rest of the program and tests use it. It breaks comparisons, sorting, and formatted output.”

Fix is to store timestamp as double (or float) and parse it in the constructor. Then getTimestamp() should return the numeric type, and toString() will work correctly with %f.”

String[] tokens = logLine.split(" "); ----> String[] tokens = logLine.split("\\s+");

convert private final String timestamp; ---> private final float timestamp;
convert this.timestamp = tokens[0]; -> this.timestamp = Double.parseDouble(tokens[0]);
convert public String getTimestamp() { ---> public float getTimestamp() {


“The tests are failing because timestamp is stored as a String in LogEntry, but the tests treat it as a numeric value and compare it using floating-point assert with a delta. Also toString() formats timestamp using %f, which expects a numeric type. The fix is to change timestamp to a double or float, parse it in the constructor using Double.parseDouble(tokens[0]), and return that numeric value from getTimestamp(). This aligns implementation with how hash-based comparisons and formatting are intended, and the tests pass.”


2-1)  Write a function to count number of journeys.   

Logs are processed in timestamp order (or the file already is).
A journey starts at ENTRY and ends at EXIT.
MAINROAD entries don’t affect journey count.
If an EXIT appears with no prior ENTRY for that plate+direction, we ignore it (incomplete journey).
A car cannot be on two journeys at once on the same direction; we track “active” journeys.


“I need to track which vehicles are currently on the highway—meaning they’ve entered but not yet exited. That’s a membership problem: is this vehicle currently active or not?”

When I see an ENTRY, I mark the vehicle as active.
When I see an EXIT, I check if it was active.

If yes → I count one completed journey and remove it from active.
If no → it’s an unmatched exit, so ignore or log it.

Why Set is perfect:

add, remove, contains are average O(1).
We don’t need ordering or counts per vehicle — just “active or not”.

A vehicle is identified by license plate, and I also include direction because the same plate could appear on both sides or direction matters in logs.”
"ABC123|EAST"
“I’ll keep an integer journeys = 0 to count completed journeys, and a Set<String> active to store currently active vehicles.”


journeys tracks the output.
active tracks cars that are currently inside the highway.

“I scan logs one by one in time order. Each entry is either ENTRY, EXIT, or MAINROA
For every entry:

Extract type = getBoothType()
Build key = plate + "|" + direction

If it’s an ENTRY

“ENTRY means the car has started a journey. I add it to the active set.”


active.add(key)

If entry duplicates happen, Set naturally avoids duplicates.

“Even if the same ENTRY appears twice, Set prevents duplicate state, and we still count only when it exits.”

“EXIT means the car is leaving the highway. I only count a journey if we had a matching active entry.”

So:

If active contains the key → remove it and increment journeys.
If not found → ignore it as invalid/incomplete logs.

In code, I use:

if (active.remove(key)) journeys++;

Explain why this is nice:

“remove() returns true only if the key existed, so I can combine the check and removal in one operation.”

“Time is O(n) because I scan the log once. Space is O(a) where a is the number of cars currently active on the highway.”


public int countJourneys() {
    Set<String> activeJourneys = new HashSet<>();
    int journeys = 0;

    for (LogEntry entry : logEntries) {
      String key = entry.getLicensePlate() + "|" + entry.getDirection();
      String type = entry.getBoothType();
     
      if ("ENTRY".equals(type)) {
        // Start journey (or keep it active if already active)
        activeJourneys.add(key);
     
      } else if ("EXIT".equals(type)) {
        // Count only if there was a previous unmatched ENTRY
        if (activeJourneys.remove(key)) {
          journeys++;
        }
      }
      // MAINROAD does not affect journey boundaries
    }
     
    return journeys;
  }

3-1) We would like to catch people who are driving at unsafe speeds on the highway. To help us do that, we would like to identify journeys where a driver does either of the following:
* Drive 130 km/h or greater in any individual 10km segment of tollway.
* Drive 120 km/h or greater in any two 10km segments of tollway.

For example, consider the following journey:
1000.000 TST002 270W ENTRY
1275.000 TST002 260W EXIT

In this case, the driver of TST002 drove 10 km in 275 seconds. We can calculate
that this driver drove an average speed of ~130.91km/hr over this segment:

10 km * 3600 sec/hr
------------------- = 130.91 km/hr
      275 sec

Note that:
* A license plate may have multiple journeys in one file, and if they drive at unsafe speeds in both journeys, both should be counted.
* We do not mark speeding if they are not on the highway (i.e. for any driving between an EXIT and ENTRY event).
* Speeding is only marked once per journey. For example, if there are 4 segments 120km/h or greater, or multiple segments 130km/h or greater, the journey is only counted once.

q. Write a function catchSpeeders in LogFile that returns a collection of license plates that drove at unsafe speeds during a journey in the LogFile.
     If the same license plate drives at unsafe speeds during two different journeys, the license plate should appear twice (once for each journey they drove at unsafe speeds).

Maintain journey state :


private static class JourneyState {
    LogEntry last;           // last log entry seen on-highway
    int segments120OrMore;   // count of 10km segments >= 120 km/h
    boolean flagged;         // whether speeding already detected for this journey

    JourneyState(LogEntry start) {
      this.last = start;
      this.segments120OrMore = 0;
      this.flagged = false;
    }
  }


public List<String> catchSpeeders() {
    Map<String, JourneyState> active = new HashMap<>();
    List<String> speeders = new ArrayList<>();

    for (LogEntry e : logEntries) {
      String type = e.getBoothType();
      String key = e.getLicensePlate() + "|" + e.getDirection();
     
      if ("ENTRY".equals(type)) {
        // Start or restart a journey for this plate+direction
        active.put(key, new JourneyState(e));
        continue;
      }
     
      JourneyState state = active.get(key);
      if (state == null) {
        // Not on the highway (or missing ENTRY); ignore this record.
        continue;
      }
     
      // We are on-highway: compute segment stats from state.last -> e
      float dt = e.getTimestamp() - state.last.getTimestamp(); // seconds
      int distanceKm = Math.abs(e.getLocation() - state.last.getLocation());
     
      // Update last regardless; but only compute speeds if we have a valid segment
      state.last = e;
     
      if (dt <= 0 || distanceKm <= 0) {
        // Non-increasing time or no movement: ignore segment
      } else {
        int segments = distanceKm / 10; // number of 10km segments
        if (segments > 0) {
          float speedKmh = (distanceKm * 3600.0f) / dt;
     
          if (speedKmh >= 130.0f) {
            state.flagged = true;
          }
          if (speedKmh >= 120.0f) {
            state.segments120OrMore += segments;
            if (state.segments120OrMore >= 2) {
              state.flagged = true;
            }
          }
        }
      }
     
      if ("EXIT".equals(type)) {
        // Journey ends here; count at most once for this journey
        if (state.flagged) {
          speeders.add(e.getLicensePlate());
        }
        active.remove(key);
      }
    }
     
    return speeders;
  }

We are building a program to manage a gym's membership. The gym has multiple members, each with a unique ID, name, and membership status. The program allows gym staff to add new members, update members status, and get membership statistics.

Definitions:
* A "member" is an object that represents a gym member. It has properties for the ID, name, and membership status.
* A "membership" is a class which is used for managing members in the gym.

To begin with, we present you with two tasks:
1-1) Read through and understand the code below. Please take as much time as necessary, and feel free to run the code.
1-2) The test for Membership is not passing due to a bug in the code. Make the necessary changes to Membership to fix the bug.
*/


/*
We are currently updating our system to include information about workouts for our members. As part of this update, we have introduced the Workout class, which represents a single workout session for a member. Each object of the Workout class has a unique ID, as well as a start time and end time that are represented in the number of minutes spent from the start of the day. You can assume that all the Workouts are from the same day.

To implement these changes, we need to add two functions to the Membership class:

2.1) The `addWorkout` function should be used to add a workout session for a member. If the given member does not exist while calling this function, the workout can be ignored.

2.2) The `getAverageWorkoutDurations` function should calculate the average duration of workouts for each member in minutes and return the results as a map.

To assist you in testing these new functions, we have provided the testGetAverageWorkoutDurations function.
*/

import java.util.*;
import org.junit.Test;
import static org.junit.Assert.*;


class Workout {
    /**
     * This class represents a single workout session for a member.
     * Each object of the Workout class has a unique ID, as well as
     * a start time and end time that are represented in the number
     * of minutes spent from the start of the day.
     */

    private int id;
    private int startTime;
    private int endTime;
    
    public Workout(int id, int startTime, int endTime) {
        this.id = id;
        this.startTime = startTime;
        this.endTime = endTime;
    }
    
    public int getId() {
        return id;
    }
    
    public int getStartTime() {
        return startTime;
    }
    
    public int getEndTime() {
        return endTime;
    }
    
    public int getDuration() {
        return endTime - startTime;
    }
}


enum MembershipStatus {
    /*
        Membership Status is of three types: BRONZE, SILVER and GOLD.
        BRONZE is the default membership a new member gets.
        SILVER and GOLD are paid memberships for the gym.
    */
    BRONZE,
    SILVER,
    GOLD
}

class Member {
    /* Data about a gym member.*/
    public int memberId;
    public String name;
    public MembershipStatus membershipStatus;
    public List<Workout> workout;

    public Member(int memberId, String name, MembershipStatus membershipStatus,Workout workout) {
        this.memberId = memberId;
        this.name = name;
        this.membershipStatus = membershipStatus;
        this.workout = workout;
    }
    
    @Override
    public String toString() {
        return "Member ID: " + memberId + ", Name: " + name + ", Membership Status: " + membershipStatus;
    }
}

class Membership {
    /*
        Data for managing a gym membership, and methods which staff can
        use to perform any queries or updates.
    */
    public List<Member> members;

    public Membership() {
        members = new ArrayList<>();
    }
    
    public void addMember(Member member) {
        members.add(member);
    }
    
    public void updateMembership(int memberId, MembershipStatus membershipStatus) {
        for (Member member : members) {
            if (member.memberId == memberId) {
                member.membershipStatus = membershipStatus;
                break;
            }
        }
    }
    public void addWorkout(int id,Workout workout){ // added this method to add workout time. Also explained how to calculate average workout time
      for(Member member : members){
        if(member.memberId == id){
            member.workout = workout;
          break;
        }
      }
    }
    public MembershipStatistics getMembershipStatistics() {
        int totalMembers = members.size();
        int totalPaidMembers = 0;
        for (Member member : members) {
            if (member.membershipStatus == MembershipStatus.GOLD || /*added this check to work failing test case */
                member.membershipStatus == MembershipStatus.SILVER) {
                totalPaidMembers++;
            }
        }
        double conversionRate = (totalPaidMembers / (double) totalMembers) * 100.0;
        return new MembershipStatistics(totalMembers, totalPaidMembers, conversionRate);
    }
}

class MembershipStatistics {
    /*
        Class for returning the getMembershipStatistics result
    */
    public int totalMembers;
    public int totalPaidMembers;
    public double conversionRate;

    public MembershipStatistics(int totalMembers, int totalPaidMembers, double conversionRate) {
        this.totalMembers = totalMembers;
        this.totalPaidMembers = totalPaidMembers;
        this.conversionRate = conversionRate;
    }
}

public class Solution {
    /*
        This is not a complete test suite, but tests some basic functionality of
        the code and shows how to use it.
    */
    public static void main(String[] args) {
        testMember();
        testMembership();
        testGetAverageWorkoutDurations();
    }

    public static void testMember() {
        System.out.println("Running testMember");
        Member testMember = new Member(1, "John Doe", MembershipStatus.BRONZE);
        assert testMember.memberId == 1 : 
            "member ID should be 1, was " + testMember.memberId;
        assert testMember.name.equals("John Doe") : 
            "member name should be \"John Doe\", was \"" + testMember.name + "\"";
        assert testMember.membershipStatus == MembershipStatus.BRONZE : 
            "membership status should be BRONZE, was " + testMember.membershipStatus;
    }
    
    public static void testMembership() {
        System.out.println("Running testMembership");
        Membership testMembership = new Membership();
        Member testMember = new Member(1, "John Doe", MembershipStatus.BRONZE);
        testMembership.addMember(testMember);
        assert testMembership.members.size() == 1 : 
            "members size should be 1, was " + testMembership.members.size();
        assert testMembership.members.get(0).equals(testMember) : 
            "first member should equal testMember";
    
        testMembership.updateMembership(1, MembershipStatus.SILVER);
        assert testMembership.members.get(0).membershipStatus == MembershipStatus.SILVER : 
            "membership status should be SILVER, was " + testMembership.members.get(0).membershipStatus;
    
        Member testMember2 = new Member(2, "Alex C", MembershipStatus.BRONZE);
        testMembership.addMember(testMember2);
    
        Member testMember3 = new Member(3, "Marie C", MembershipStatus.GOLD);
        testMembership.addMember(testMember3);
    
        Member testMember4 = new Member(4, "Joe D", MembershipStatus.SILVER);
        testMembership.addMember(testMember4);
    
        Member testMember5 = new Member(5, "June R", MembershipStatus.BRONZE);
        testMembership.addMember(testMember5);
    
        MembershipStatistics attendanceStats = testMembership.getMembershipStatistics();
        assert attendanceStats.totalMembers == 5 : 
            "total members should be 5, was " + attendanceStats.totalMembers;
        assert attendanceStats.totalPaidMembers == 3 : 
            "total paid members should be 3, was " + attendanceStats.totalPaidMembers;
        assert Math.abs(attendanceStats.conversionRate - 60.00) < 0.1 : 
            "conversion rate should be 60.00, was " + attendanceStats.conversionRate;
    }
      public static void testGetAverageWorkoutDurations() {
        System.out.println("Running testGetAverageWorkoutDurations");
        Membership testMembership = new Membership();
        Member testMember1 = new Member(12, "John Doe", MembershipStatus.SILVER);
        testMembership.addMember(testMember1);
    
        Member testMember2 = new Member(22, "Alex Cleeve", MembershipStatus.BRONZE);
        testMembership.addMember(testMember2);
    
        Member testMember3 = new Member(31, "Marie Cardiff", MembershipStatus.GOLD);
        testMembership.addMember(testMember3);
    
        Member testMember4 = new Member(37, "George Costanza", MembershipStatus.SILVER);
        testMembership.addMember(testMember4);
    
        Workout testWorkout1 = new Workout(11, 10, 20);
        Workout testWorkout2 = new Workout(24, 15, 35);
        Workout testWorkout3 = new Workout(32, 45, 90);
        Workout testWorkout4 = new Workout(47, 100, 155);
        Workout testWorkout5 = new Workout(56, 120, 200);
        Workout testWorkout6 = new Workout(62, 300, 400);
        Workout testWorkout7 = new Workout(78, 1000, 1010);
        Workout testWorkout8 = new Workout(80, 1010, 1045);
    
        testMembership.addWorkout(12, testWorkout1);
        testMembership.addWorkout(22, testWorkout2);
        testMembership.addWorkout(31, testWorkout3);
        testMembership.addWorkout(12, testWorkout4);
        testMembership.addWorkout(22, testWorkout5);
        testMembership.addWorkout(31, testWorkout6);
        testMembership.addWorkout(12, testWorkout7);
        testMembership.addWorkout(4, testWorkout8);
    
        Map<Integer, Double> averageDurations = testMembership.getAverageWorkoutDurations();
        assert Math.abs(averageDurations.get(12) - 25.0) < 0.1 : 
            "average duration for member 12 should be 25.0, was " + averageDurations.get(12);
        assert Math.abs(averageDurations.get(22) - 50.0) < 0.1 : 
            "average duration for member 22 should be 50.0, was " + averageDurations.get(22);
        assert Math.abs(averageDurations.get(31) - 72.5) < 0.1 : 
            "average duration for member 31 should be 72.5, was " + averageDurations.get(31);
        assertFalse(averageDurations.containsKey(4));
    }
}

Answer : update 
public void updateMembership(int memberId, MembershipStatus membershipStatus) {
        for (Member member : members) {
            if (member.memberId == memberId) {
                member.membershipStatus = membershipStatus;
                break;
            }
        }
to

public void updateMembership(int memberId, MembershipStatus membershipStatus) {
        for (Member member : members) {
            if (member.memberId == memberId) {
                member.membershipStatus = membershipStatus;
                return;
            }
        }


/**
     * 2.1) Add a workout for a member. If member doesn't exist, ignore.
     */
    public void addWorkout(int memberId, Workout workout) {
        for (Member member : members) {
            if (member.memberId == memberId) {
                member.workouts.add(workout);  // ✅ append, do not overwrite
                return;
            }
        }
        // ✅ ignore if member not found
    }

    /**
     * 2.2) Return average workout durations (minutes) per member.
     * Only members with at least 1 workout are included (common interpretation).
     */
    public Map<Integer, Double> getAverageWorkoutDurations() {
        Map<Integer, Double> avg = new HashMap<>();
     
        for (Member member : members) {
            if (member.workouts.isEmpty()) continue; // choose to omit members with no workouts
     
            int total = 0;
            for (Workout w : member.workouts) total += w.getDuration();
     
            avg.put(member.memberId, total / (double) member.workouts.size());
        }
        return avg;
    }

 An LRU Cache (Least Recently Used Cache) is a data structure that stores a limited number of items and automatically removes the item that has not been used for the longest time when the cache is full.

It’s commonly used to improve performance by keeping frequently accessed data quickly available.

Simple Example

Imagine a cache with capacity = 3.

Operations:

1. Add A → Cache: [A]


2. Add B → Cache: [A, B]


3. Add C → Cache: [A, B, C]


4. Access A → Cache becomes: [B, C, A]

A is now most recently used



5. Add D

Cache is full

Remove least recently used item (B)

Cache becomes: [C, A, D]




So:

Most recently used items stay

Least recently used items get evicted first



---

Where LRU Cache Is Used

Web browsers (cached pages)

Databases

Operating systems

APIs

CDN caching

Image/video loading apps



---

Time Complexity Goal

A good LRU cache supports:

get(key) → O(1)

put(key, value) → O(1)


To achieve this, it usually combines:

1. Hash Map → fast lookup


2. Doubly Linked List → track usage order




---

Basic Working

Hash Map

Stores:

key -> node

Doubly Linked List

Maintains order:

Head = most recently used

Tail = least recently used


When an item is accessed:

Move it to the front


When cache is full:

Remove from the tail



---

Example in Python

from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key):
        if key not in self.cache:
            return -1
        
        self.cache.move_to_end(key)
        return self.cache[key]
    
    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
    
        self.cache[key] = value
    
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)

# Example
lru = LRUCache(3)

lru.put(1, "A")
lru.put(2, "B")
lru.put(3, "C")

print(lru.get(1))  # A

lru.put(4, "D")    # Removes key 2

print(lru.cache)


---

Key Idea

An LRU cache is useful when:

memory/storage is limited

recently used data is more likely to be used again


This follows the principle of temporal locality.

