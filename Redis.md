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

### 📌 Spring Cache with Redis

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

### ⚠️ Common Redis Use Cases

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

---

# Redis Interview Questions & Answers (ELI10 + Interview Ready)

------

# 1. What is Redis?

## 🧠 ELI10

Imagine you have a huge library.

Every time someone asks for a book, you walk all the way to the shelf.

That's slow.

Now imagine you keep the **most popular books on your desk**.

Finding them takes only a second.

**Redis is that desk.**

It stores frequently used data in **RAM (memory)** so applications can access it extremely fast.

### 📌 Interview Answer

Redis is an **in-memory NoSQL key-value database** used for **caching, session storage, real-time analytics, messaging, and fast data retrieval**. Since it stores data in RAM instead of disk, it provides sub-millisecond response times.

------

# 2. Why is Redis faster than a relational database?

## 🧠 ELI10

Imagine finding a toy.

### Database

```
Go to basement

↓

Open box

↓

Find toy
```

Time = Slow

### Redis

```
Toy is already on your table

↓

Pick it
```

Time = Very Fast

### Why?

✅ Stores data in RAM

❌ Doesn't read from disk every time

✅ Single-threaded (no locking)

✅ Optimized data structures

### 📌 Interview Answer

Redis is faster because it stores data in **memory**, avoids disk I/O, uses efficient data structures, and processes commands using a single-threaded event loop.

------

# 3. What are Redis data types?

Redis isn't just key-value.

| Data Type   | Used For           |
| ----------- | ------------------ |
| String      | Text, numbers, OTP |
| Hash        | Java Object        |
| List        | Queue, Tasks       |
| Set         | Unique values      |
| Sorted Set  | Leaderboard        |
| Streams     | Event streaming    |
| Bitmap      | Attendance         |
| HyperLogLog | Count unique users |
| Geo         | Nearby locations   |

### 🧠 Easy Example

```
String

name = Narsing

----------------

Hash

User

name
age
city

----------------

List

Task1
Task2
Task3

----------------

Set

Java
Spring
Kafka

(No duplicates)

----------------

Sorted Set

John = 100

Alice = 200

Bob =150

----------------

Streams

Producer

↓

Consumer
```

------

# 4. What is TTL?

TTL means

> **Time To Live**

It tells Redis

> "Delete this data after some time."

Example

```
OTP = 456789

Expire after 60 seconds
```

After one minute

```
OTP disappears automatically.
```

### Why?

Perfect for

- OTP
- Session
- Temporary data

### 📌 Interview Answer

TTL is the expiration time of a Redis key. Once the specified time is over, Redis automatically removes the key.

------

# 5. Explain the Cache Aside Pattern.

This is the **most common caching strategy.**

Suppose user asks

```
Get User 101
```

Flow

```
Client

↓

Spring Boot

↓

Redis

↓

Found?

YES

↓

Return Data

------------------

NO

↓

Database

↓

Store in Redis

↓

Return Data
```

### Real Example

First request

```
Redis ❌

↓

Database ✅

↓

Redis Save

↓

Return
```

Second request

```
Redis ✅

↓

Return

(No database call)
```

### 📌 Interview Answer

In the Cache Aside pattern, the application first checks Redis. If the data exists, it is returned immediately. Otherwise, the application fetches it from the database, stores it in Redis, and then returns it.

------

# 6. What is cache eviction?

Suppose Redis memory becomes full.

It cannot keep everything.

So Redis removes some keys.

This is called

**Cache Eviction**

Example

Memory

```
User1

User2

User3

User4

Memory Full
```

Redis removes

```
Least Recently Used
```

to create space.

### Popular policies

```
LRU

LFU

Random

TTL
```

### 📌 Interview Answer

Cache eviction is the process of removing keys from Redis when memory is full based on configured eviction policies.

------

# 7. Difference between RDB and AOF?

## RDB

Imagine taking a photo.

```
Memory

↓

Photo

↓

Save
```

If crash happens

You lose data after last photo.

------

## AOF

Imagine writing every action in a notebook.

```
SET name John

SET age 24

DELETE age
```

Nothing is missed.

------

| RDB          | AOF             |
| ------------ | --------------- |
| Snapshot     | Every command   |
| Faster       | Slightly slower |
| Small file   | Large file      |
| Less durable | More durable    |

### 📌 Interview Answer

RDB stores periodic snapshots, while AOF logs every write command. RDB is faster and smaller; AOF offers better durability with minimal data loss.

------

# 8. What is Redis Pub/Sub?

Imagine

Teacher speaks.

```
Teacher

↓

Students
```

Students only hear messages while sitting in class.

If absent

Message is gone.

Redis Pub/Sub works exactly like this.

Publisher

```
Publish

↓

Channel

↓

Subscribers
```

No message storage.

### 📌 Interview Answer

Redis Pub/Sub is a messaging mechanism where publishers send messages to channels and subscribers receive them in real time. Messages are not stored.

------

# 9. What are Redis Streams?

Streams are like WhatsApp.

```
Friend sends message.

↓

Stored.

↓

You read later.
```

Unlike Pub/Sub

Messages remain.

```
Producer

↓

Redis Stream

↓

Consumers
```

Supports

- Replay
- Acknowledgement
- Consumer Groups

### 📌 Interview Answer

Redis Streams are a persistent messaging feature that stores events, allowing multiple consumers to process messages reliably.

------

# 10. Difference between Pub/Sub and Streams?

| Pub/Sub           | Streams         |
| ----------------- | --------------- |
| Live only         | Stored          |
| Lost if offline   | Read later      |
| No history        | Has history     |
| No acknowledgment | Acknowledgment  |
| Broadcast         | Consumer groups |

### Easy Example

Pub/Sub

```
TV Live

Missed?

Gone forever.
```

Streams

```
Netflix

Watch later.
```

------

# 11. What is Redis Sentinel?

Suppose

```
Master

↓

Crash
```

Who creates new master?

Sentinel.

It watches Redis all the time.

If master fails

```
Replica

↓

New Master
```

Automatically.

### 📌 Interview Answer

Redis Sentinel monitors Redis servers, detects failures, and automatically promotes a replica to master during failover.

------

# 12. What is Redis Cluster?

Suppose one Redis server becomes full.

Instead of buying a huge computer,

Split data.

```
Node1

Node2

Node3

Node4
```

Each stores some keys.

Benefits

- High Availability
- Scalability
- Fault Tolerance

### 📌 Interview Answer

Redis Cluster distributes data across multiple Redis nodes using sharding, providing scalability and high availability.

------

# 13. Difference between Redis and Kafka?

| Redis        | Kafka             |
| ------------ | ----------------- |
| Cache        | Event Streaming   |
| RAM          | Disk              |
| Super Fast   | Highly Durable    |
| Small events | Huge events       |
| Temporary    | Long-term storage |

### Easy Example

Redis

```
Notebook on Desk
```

Kafka

```
Library Archive
```

### 📌 Interview Answer

Redis is mainly used for caching and lightweight messaging, whereas Kafka is designed for large-scale, durable event streaming.

------

# 14. How do you integrate Redis with Spring Boot?

### Step 1

Dependency

```xml
spring-boot-starter-data-redis
```

Step 2

application.properties

```properties
spring.data.redis.host=localhost
spring.data.redis.port=6379
```

Step 3

Use

```java
RedisTemplate
```

or

```java
@Cacheable
```

### 📌 Interview Answer

Spring Boot integrates Redis using `spring-boot-starter-data-redis`, Redis configuration, and APIs like `RedisTemplate` or Spring Cache annotations.

------

# 15. What is RedisTemplate?

Think of it as

```
Java

↓

Translator

↓

Redis
```

Instead of writing Redis commands,

You call Java methods.

Example

```java
redisTemplate.opsForValue().set("name","Narsing");
```

Read

```java
redisTemplate.opsForValue().get("name");
```

### 📌 Interview Answer

`RedisTemplate` is the main Spring Data Redis class that provides convenient methods for performing Redis operations from Java code.

------

# 16. What are `@Cacheable`, `@CachePut`, and `@CacheEvict`?

## @Cacheable

```
Already cached?

YES

↓

Don't call database.
```

------

## @CachePut

```
Database Updated

↓

Cache Updated
```

------

## @CacheEvict

```
Delete User

↓

Delete Cache
```

### Summary

| Annotation  | Purpose                      |
| ----------- | ---------------------------- |
| @Cacheable  | Read from cache if available |
| @CachePut   | Update cache                 |
| @CacheEvict | Remove cache                 |

------

# 17. How do you handle cache invalidation?

Imagine

Database

```
Name

↓

John
```

Redis

```
John
```

Database updated

```
John

↓

David
```

Redis still has

```
John
```

Wrong!

Solutions

✅ TTL

✅ @CacheEvict

✅ @CachePut

### 📌 Interview Answer

Cache invalidation ensures cached data remains consistent with the database. Common approaches include using TTL, evicting stale entries, or updating the cache after database changes.

------

# 18. What happens if Redis goes down?

Application

```
↓

Redis ❌

↓

Database ✅

↓

Return
```

Application becomes slower

but should still work.

Good systems

```
Redis Down

↓

Fallback

↓

Database
```

### 📌 Interview Answer

If Redis is unavailable, the application should fall back to the database. Performance decreases, but functionality should continue if proper error handling is implemented.

------

# 19. What is pipelining in Redis?

Without Pipeline

```
SET A

(wait)

SET B

(wait)

SET C
```

Three network trips.

With Pipeline

```
SET A

SET B

SET C

↓

Send together
```

Only one trip.

Much faster.

### 📌 Interview Answer

Pipelining sends multiple Redis commands together in one network request, reducing latency and improving performance.

------

# 20. Explain replication and failover in Redis.

Replication

```
Master

↓

Replica1

↓

Replica2
```

Master

- Write

Replica

- Read

If Master crashes

```
Replica1

↓

New Master
```

This automatic switching is called

**Failover**

Usually handled by

**Redis Sentinel**

### 📌 Interview Answer

Replication creates copies of data from the master to one or more replicas for improved read scalability and redundancy. During a master failure, Redis Sentinel automatically promotes a replica to become the new master, ensuring high availability.

------

# 🎯 One-Line Revision (Interview)

| Question                | One-Line Answer                                              |
| ----------------------- | ------------------------------------------------------------ |
| Redis                   | In-memory NoSQL key-value store for ultra-fast access.       |
| Why Fast?               | Stores data in RAM with efficient data structures.           |
| Data Types              | String, Hash, List, Set, Sorted Set, Streams, Bitmap, HyperLogLog, Geo. |
| TTL                     | Automatic expiration time for a key.                         |
| Cache Aside             | Check cache → DB on miss → Save back to cache.               |
| Cache Eviction          | Removing keys when memory is full.                           |
| RDB vs AOF              | Snapshot vs command logging.                                 |
| Pub/Sub                 | Live messaging without persistence.                          |
| Streams                 | Persistent messaging with replay support.                    |
| Sentinel                | Monitors Redis and performs automatic failover.              |
| Cluster                 | Distributes data across multiple nodes.                      |
| Redis vs Kafka          | Cache/lightweight messaging vs durable event streaming.      |
| Spring Boot Integration | Use `spring-boot-starter-data-redis` with `RedisTemplate` or cache annotations. |
| RedisTemplate           | Spring class for interacting with Redis.                     |
| Cache Annotations       | `@Cacheable` reads, `@CachePut` updates, `@CacheEvict` removes cache. |
| Cache Invalidation      | Keep cache in sync using TTL or cache updates/evictions.     |
| Redis Down              | Fall back to the database; performance decreases.            |
| Pipelining              | Send multiple commands in one network request.               |
| Replication & Failover  | Replicas copy data; Sentinel promotes a replica if the master fails. |

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