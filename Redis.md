# Redis

### 📌 What is Redis?

**Redis (Remote Dictionary Server)** is an **in-memory NoSQL data store** used as a **cache, database, message broker, and streaming engine**.

- Stores data in **RAM** (very fast).
- Supports **key-value** data model.
- Can persist data to disk.
- Open-source and single-threaded (core command execution).

> **Think of Redis as a super-fast HashMap stored on a server.**

------

### 🧠 Why Redis?

Without Redis:

```
Client
   |
   v
Spring Boot
   |
   v
Database (Slow)
```

Every request goes to the database.

------

With Redis:

```
Client
   |
   v
Spring Boot
   |
   +------> Redis (Fast Cache)
   |           |
   |      Found? Return
   |
   v
Database
```

Most requests never reach the database.

------

### 📌 Why is Redis So Fast?

Because:

- Stores data in RAM
- No disk I/O for reads
- Efficient data structures
- Single-threaded event loop (no thread locking)
- Uses non-blocking I/O

Average read/write:

```
< 1 millisecond
```

------

### 📌 Redis Characteristics

| Feature      | Description    |
| ------------ | -------------- |
| Database     | NoSQL          |
| Storage      | Memory (RAM)   |
| Persistence  | Optional       |
| Speed        | Extremely Fast |
| Thread Model | Single Thread  |
| Data Model   | Key-Value      |

------

### 🧠 Redis Data Types

Redis is much more than key-value.

------

#### 1. String

Most common.

```
Key -> Value
```

Example:

```
name -> Narsing
age -> 24
```

Commands

```bash
SET name Narsing

GET name

DEL name

INCR counter

DECR counter
```

------

#### 2. Hash

Like Java Object.

Example

```
User

id=1
name=John
city=Pune
```

Redis

```
user:1

name -> John
city -> Pune
```

Commands

```bash
HSET user:1 name John

HSET user:1 city Pune

HGET user:1 name

HGETALL user:1
```

------

#### 3. List

Ordered collection.

```
Tasks

Task1
Task2
Task3
```

Commands

```bash
LPUSH tasks Task1

LPUSH tasks Task2

RPUSH tasks Task3

LRANGE tasks 0 -1
```

------

#### 4. Set

Unique values only.

```
Java
Spring
Kafka
Java
```

Stored:

```
Java
Spring
Kafka
```

Commands

```bash
SADD skills Java

SADD skills Spring

SMEMBERS skills
```

------

#### 5. Sorted Set

Stores values with score.

Example

```
John -> 100

Alice -> 200

Bob -> 150
```

Commands

```bash
ZADD leaderboard 100 John

ZADD leaderboard 150 Bob

ZRANGE leaderboard 0 -1 WITHSCORES
```

Used for:

- Leaderboards
- Rankings
- Gaming

------

#### 6. Streams

Used for event streaming.

```
Producer

↓

Redis Stream

↓

Consumers
```

Similar to Kafka but lightweight.

------

#### 7. Bitmap

Stores bits efficiently.

Used for:

- Daily login
- Attendance
- Boolean flags

------

#### 8. HyperLogLog

Counts unique users with very little memory.

Example

```
Unique Website Visitors
```

------

#### 9. Geospatial

Stores latitude and longitude.

Example

```
Restaurants

Hospitals

Drivers
```

Can search nearby locations.

------

### 📌 Redis Persistence

Redis stores data in memory, but you can save it to disk.

Two methods:

------

#### 1. RDB Snapshot

```
Memory

↓

Snapshot.rdb
```

- Saves periodically
- Faster restart
- May lose recent writes

------

#### 2. AOF (Append Only File)

```
SET name John

SET age 24

DEL age
```

Every operation is logged.

Advantages

- Better durability
- Less data loss

Disadvantages

- Larger files
- Slightly slower writes

------

### 📌 Cache Aside Pattern (Most Common)

Flow

```
Client

↓

Spring Boot

↓

Redis

↓

Found?

YES → Return

NO

↓

Database

↓

Redis

↓

Return
```

Steps

1. Check Redis.
2. If present → Return.
3. Otherwise query database.
4. Store result in Redis.
5. Return response.

------

### 📌 TTL (Time To Live)

Redis keys can expire automatically.

Example

```bash
SET otp 123456

EXPIRE otp 60
```

OTP disappears after 60 seconds.

Check remaining time:

```bash
TTL otp
```

------

### 📌 Eviction Policies

When memory is full.

Redis removes keys.

Common policies:

| Policy          | Description                    |
| --------------- | ------------------------------ |
| noeviction      | Reject new writes              |
| allkeys-lru     | Remove least recently used key |
| volatile-lru    | Remove LRU keys with TTL       |
| allkeys-random  | Remove random key              |
| volatile-random | Random TTL key                 |

------

### 📌 Pub/Sub

Real-time messaging.

```
Publisher

↓

Redis Channel

↓

Subscriber1

Subscriber2

Subscriber3
```

Commands

```bash
SUBSCRIBE news

PUBLISH news Hello
```

------

### 📌 Redis Streams

Better than Pub/Sub because messages are stored.

```
Producer

↓

Redis Stream

↓

Consumer Group

↓

Consumers
```

Features

- Persistent messages
- Replay
- Acknowledgement
- Multiple consumers

------

### 📌 Redis Transactions

Commands

```bash
MULTI

SET name John

SET age 25

EXEC
```

Everything executes together.

------

### 📌 Pipeline

Without Pipeline

```
SET A

(wait)

SET B

(wait)

SET C
```

Many network calls.

------

With Pipeline

```
SET A

SET B

SET C

↓

Send together
```

Faster.

------

### 📌 Replication

```
Master

↓

Replica1

↓

Replica2
```

Master handles writes.

Replicas handle reads.

------

### 📌 Redis Sentinel

Problem

```
Master crashes.
```

Sentinel:

- Detects failure
- Elects a new master
- Performs automatic failover

------

### 📌 Redis Cluster

Distributes data across multiple nodes.

```
Node1

Node2

Node3

Node4
```

Benefits:

- High availability
- Horizontal scaling
- Automatic sharding

------

### 📌 Redis vs Database

| Redis          | Database                |
| -------------- | ----------------------- |
| RAM            | Disk                    |
| Very Fast      | Slower                  |
| Temporary data | Permanent data          |
| Cache          | Source of truth         |
| Milliseconds   | Milliseconds to seconds |

------

### 📌 Redis vs Kafka

| Redis Streams                    | Kafka                                |
| -------------------------------- | ------------------------------------ |
| In-memory                        | Disk-based                           |
| Lightweight                      | Distributed platform                 |
| Fast                             | Highly scalable                      |
| Good for smaller event workloads | Best for large-scale event streaming |

------

### 📌 Spring Boot Integration

Dependency

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Configuration

```properties
spring.data.redis.host=localhost
spring.data.redis.port=6379
```

Configuration Bean

```java
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(
            RedisConnectionFactory connectionFactory) {

        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(connectionFactory);

        return template;
    }
}
```

Save Data

```java
@Autowired
private RedisTemplate<String, Object> redisTemplate;

public void saveUser() {
    redisTemplate.opsForValue().set("name", "Narsing");
}
```

Read Data

```java
String name = (String) redisTemplate.opsForValue().get("name");
```

------

# 📌 Spring Cache with Redis

Enable Caching

```java
@SpringBootApplication
@EnableCaching
public class Application {
}
```

Cache Result

```java
@Cacheable("users")
public User getUser(Long id) {
    return repository.findById(id).orElse(null);
}
```

Evict Cache

```java
@CacheEvict(value = "users", key = "#id")
public void deleteUser(Long id) {
    repository.deleteById(id);
}
```

Update Cache

```java
@CachePut(value = "users", key = "#user.id")
public User update(User user) {
    return repository.save(user);
}
```

------

# ⚠️ Common Redis Use Cases

- ✅ API response caching
- ✅ Session storage
- ✅ OTP storage (TTL)
- ✅ Rate limiting
- ✅ Shopping carts
- ✅ Leaderboards
- ✅ Real-time analytics
- ✅ Pub/Sub messaging
- ✅ Event streaming
- ✅ Distributed locking
- ✅ Feature flags

------

# 💡 Redis Interview Questions

1. What is Redis?
2. Why is Redis faster than a relational database?
3. What are Redis data types?
4. What is TTL?
5. Explain the Cache Aside pattern.
6. What is cache eviction?
7. Difference between RDB and AOF?
8. What is Redis Pub/Sub?
9. What are Redis Streams?
10. Difference between Pub/Sub and Streams?
11. What is Redis Sentinel?
12. What is Redis Cluster?
13. Difference between Redis and Kafka?
14. How do you integrate Redis with Spring Boot?
15. What is `RedisTemplate`?
16. What are `@Cacheable`, `@CachePut`, and `@CacheEvict`?
17. How do you handle cache invalidation?
18. What happens if Redis goes down?
19. What is pipelining in Redis?
20. Explain replication and failover in Redis.

------

# 📝 Quick Revision

- 📌 Redis = In-memory NoSQL key-value store.
- 📌 Extremely fast because data is stored in RAM.
- 📌 Common data types: String, Hash, List, Set, Sorted Set, Streams.
- 📌 Persistence options: RDB (snapshots) and AOF (command log).
- 📌 TTL enables automatic key expiration.
- 📌 Cache Aside is the most common caching strategy.
- 📌 Pub/Sub is for transient messaging; Streams provide durable event storage.
- 📌 Sentinel offers automatic failover; Cluster provides horizontal scaling.
- 📌 Spring Boot integrates via `RedisTemplate` or Spring Cache annotations.