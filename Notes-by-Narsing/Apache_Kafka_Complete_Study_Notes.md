# Apache Kafka 

------------------------------------------------------------------------

# What is Messaging System

## Introduction / Definition

A messaging system enables different applications or services to
communicate asynchronously by sending messages through a broker instead
of calling each other directly.

## Why it is needed

-   Loose coupling
-   Better scalability
-   Fault tolerance
-   Async processing

## Core Concepts

-   Producer
-   Consumer
-   Queue / Topic
-   Broker

## Architecture Explanation

``` mermaid
flowchart LR
    A[Producer] --> B[Message Broker]
    B --> C[Consumer]
```

## Real-Life Example

Ordering food online. You place order → system processes later →
delivery service picks it.

## Practical Example (Conceptual Java)

``` java
messageBroker.send("order-topic", orderObject);
```

## Use Cases

-   Microservices communication
-   Notifications
-   Order processing

## Interview Question with Answer

**Q: Why use messaging over REST?**\
A: Messaging supports async processing, decoupling, and better
scalability.

## Memory Trick

Messaging = Post office system.

------------------------------------------------------------------------

# What is Apache Kafka

## Introduction / Definition

Apache Kafka is a distributed event streaming platform used to publish,
store, and process streams of records in real time.

## Why it is needed

-   High throughput
-   Durable storage
-   Real-time streaming

## Core Concepts

Topic, Partition, Offset, Producer, Consumer, Broker

## Architecture Explanation

``` mermaid
flowchart LR
    P[Producer] --> K[Kafka Cluster]
    K --> C[Consumer]
```

## Real-Life Example

Order events stored and processed in real time.

## Practical Example (Java Producer)

``` java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

KafkaProducer<String, String> producer = new KafkaProducer<>(props);
producer.send(new ProducerRecord<>("orders", "order1"));
producer.close();
```

## Use Cases

-   Event sourcing
-   Log aggregation
-   Real-time analytics

## Interview Question with Answer

**Q: Why is Kafka fast?**\
A: Sequential disk writes + partitioning + zero-copy transfer.

## Memory Trick

Kafka = Distributed commit log.

------------------------------------------------------------------------

# Kafka Architecture

## Introduction / Definition

Kafka runs as a distributed cluster of brokers storing partitioned logs.

## Why it is needed

-   Scalability
-   High availability

## Core Concepts

Broker, Topic, Partition, Replication

## Architecture Explanation

``` mermaid
flowchart TB
    subgraph Cluster
        B1[Broker1]
        B2[Broker2]
        B3[Broker3]
    end
    P[Producer] --> B1
    C[Consumer] --> B2
```

## Real-Life Example

E-commerce system distributing orders across multiple servers.

## Practical Example

``` yaml
spring.kafka.bootstrap-servers=localhost:9092
```

## Use Cases

-   Streaming pipelines
-   Enterprise event backbone

## Interview Question with Answer

**Q: What happens if a broker fails?**\
A: Replica leader takes over.

## Memory Trick

Cluster = Multiple brokers + replication.

------------------------------------------------------------------------

# Broker

## Introduction / Definition

A broker is a Kafka server that stores data and serves clients.

## Why it is needed

-   Data storage
-   Client handling

## Core Concepts

Broker ID, Log storage

## Architecture Explanation

``` mermaid
flowchart LR
    P --> B[Broker]
    B --> C
```

## Real-Life Example

Warehouse storing packages.

## Practical Example

broker.id=1

## Use Cases

Cluster node in distributed system.

## Interview Question with Answer

**Q: Can Kafka run with single broker?**\
A: Yes, but no fault tolerance.

## Memory Trick

Broker = Storage server.

------------------------------------------------------------------------

# Topic

## Introduction / Definition

Logical category where messages are stored.

## Why it is needed

Data classification.

## Core Concepts

Partitions

## Architecture Explanation

``` mermaid
flowchart LR
    Topic --> P1
    Topic --> P2
```

## Real-Life Example

Different folders: orders, payments.

## Practical Example

``` bash
kafka-topics.sh --create --topic orders --partitions 3 --replication-factor 2
```

## Use Cases

Separate business domains.

## Interview Question with Answer

**Q: Is topic physically stored?**\
A: Yes, as partition logs.

## Memory Trick

Topic = Folder name.

------------------------------------------------------------------------

# Partition

## Introduction / Definition

A partition is a subset of topic data stored as ordered log.

## Why it is needed

Parallelism and scalability.

## Core Concepts

Offset ordering

## Architecture Explanation

``` mermaid
flowchart LR
    Topic --> Partition0
    Topic --> Partition1
```

## Real-Life Example

Book split into chapters.

## Practical Example

Key-based partitioning in producer.

## Use Cases

Parallel consumers.

## Interview Question with Answer

**Q: Ordering guaranteed?**\
A: Only within a partition.

## Memory Trick

Partition = Parallel lane.

------------------------------------------------------------------------

# Offset

## Introduction / Definition

Offset is unique position of message inside partition.

## Why it is needed

Track consumption progress.

## Core Concepts

Sequential number.

## Real-Life Example

Page number in book.

## Practical Example

``` java
consumer.commitSync();
```

## Use Cases

Message tracking.

## Interview Question with Answer

**Q: Who manages offsets?**\
A: Consumer group coordinator.

## Memory Trick

Offset = Index number.

------------------------------------------------------------------------

# Producer

## Introduction / Definition

Application that sends data to Kafka.

## Why it is needed

Data ingestion.

## Core Concepts

Key, Partitioning, Acks

## Architecture Explanation

``` mermaid
flowchart LR
    Producer --> Broker
```

## Practical Example

KafkaProducer API.

## Interview Question with Answer

**Q: What is idempotent producer?**\
A: Prevents duplicate messages.

## Memory Trick

Producer = Sender.

------------------------------------------------------------------------

# Consumer

## Introduction / Definition

Reads messages from Kafka.

## Why it is needed

Process events.

## Core Concepts

Polling, Offset commit

## Architecture Explanation

``` mermaid
flowchart LR
    Broker --> Consumer
```

## Practical Example

``` java
consumer.poll(Duration.ofMillis(100));
```

## Interview Question with Answer

**Q: Push or Pull?**\
A: Pull-based.

## Memory Trick

Consumer = Reader.

------------------------------------------------------------------------

# Consumer Group

## Introduction / Definition

Group of consumers sharing same group ID.

## Why it is needed

Load balancing.

## Architecture Explanation

``` mermaid
flowchart LR
    P0 --> C1
    P1 --> C2
```

## Interview Question with Answer

**Q: Can two consumers read same partition?**\
A: Not in same group.

## Memory Trick

Group = Team dividing work.

------------------------------------------------------------------------

# Zookeeper (Basic)

## Introduction / Definition

Service used earlier for metadata and coordination.

## Why it is needed

Leader election, cluster metadata.

## Interview Question with Answer

**Q: Is Zookeeper required now?**\
A: No in newer versions (KRaft).

## Memory Trick

Zookeeper = Cluster manager.

------------------------------------------------------------------------

# Kafka without Zookeeper (KRaft)

## Introduction / Definition

Kafka Raft mode replacing Zookeeper using internal consensus.

## Why it is needed

Simpler architecture.

## Interview Question with Answer

**Q: What protocol used?**\
A: Raft consensus.

## Memory Trick

KRaft = Kafka + Raft.

------------------------------------------------------------------------

# Replication & ISR

## Introduction / Definition

Replication duplicates partitions across brokers. ISR = In-Sync
Replicas.

## Why it is needed

Fault tolerance.

## Interview Question with Answer

**Q: What if ISR shrinks?**\
A: Risk of data loss if leader fails.

## Memory Trick

ISR = Healthy replicas.

------------------------------------------------------------------------

# Leader & Follower

## Introduction / Definition

Leader handles reads/writes. Followers replicate.

## Why it is needed

Consistency control.

## Interview Question with Answer

**Q: Who serves client requests?**\
A: Leader.

## Memory Trick

Leader = Boss partition.

------------------------------------------------------------------------

# Acknowledgment (acks)

## Introduction / Definition

Controls durability guarantee.

## Values

-   0
-   1
-   all

## Interview Question with Answer

**Q: Safest ack?**\
A: all

## Memory Trick

acks=all = safest.

------------------------------------------------------------------------

# Retention Policy

## Introduction / Definition

Defines how long Kafka keeps data.

## Types

-   Time-based
-   Size-based

## Interview Question with Answer

**Q: Does consumption delete message?**\
A: No.

## Memory Trick

Kafka = Log, not queue.

------------------------------------------------------------------------

# Log Compaction

## Introduction / Definition

Keeps latest record per key.

## Why it is needed

Maintain state.

## Interview Question with Answer

**Q: When use compaction?**\
A: State topics.

## Memory Trick

Compaction = Keep latest.

------------------------------------------------------------------------

# Kafka Delivery Semantics

## Types

-   At most once
-   At least once
-   Exactly once

## Interview Question with Answer

**Q: How achieve exactly once?**\
A: Idempotent producer + transactions.

## Memory Trick

0, 1+, 1 exactly.

------------------------------------------------------------------------

# Kafka Configuration Important Properties

-   bootstrap.servers
-   acks
-   retries
-   replication.factor
-   min.insync.replicas
-   enable.auto.commit

## Interview Question with Answer

**Q: What ensures durability?**\
A: replication.factor + acks=all.

## Memory Trick

Durability = Replication + acks.

------------------------------------------------------------------------

# Kafka with Spring Boot

## Introduction

Spring Kafka simplifies integration.

## Practical Example

``` java
@KafkaListener(topics="orders")
public void listen(String message){
    System.out.println(message);
}
```

## Interview Question with Answer

**Q: Annotation for consumer?**\
A: @KafkaListener

## Memory Trick

Spring + @KafkaListener.

------------------------------------------------------------------------

# Kafka Performance Tuning

-   Increase partitions
-   Batch size tuning
-   Compression
-   Proper replication

## Interview Question with Answer

**Q: How increase throughput?**\
A: More partitions + batching.

## Memory Trick

Performance = Partitions + Batching.

------------------------------------------------------------------------

# Kafka Security (SSL, SASL)

## Introduction

Secures communication and authentication.

## Types

-   SSL (encryption)
-   SASL (authentication)

## Interview Question with Answer

**Q: Difference?**\
A: SSL encrypts, SASL authenticates.

## Memory Trick

SSL = Lock, SASL = Identity check.

------------------------------------------------------------------------

# Kafka Transactions

## Introduction

Ensures atomic writes across partitions.

## Interview Question with Answer

**Q: When needed?**\
A: Exactly-once pipelines.

## Memory Trick

Transaction = All or nothing.

------------------------------------------------------------------------

# Kafka Streams

## Introduction

Library for stream processing.

## Architecture

``` mermaid
flowchart LR
    InputTopic --> StreamApp --> OutputTopic
```

## Interview Question with Answer

**Q: Is it separate cluster?**\
A: No, library.

## Memory Trick

Streams = Processing layer.

------------------------------------------------------------------------

# Common Production Issues

-   Consumer lag
-   Rebalancing
-   Disk full
-   ISR shrink
-   Misconfigured acks

## Interview Question with Answer

**Q: What is consumer lag?**\
A: Delay between produced and consumed offset.

## Memory Trick

Lag = Behind in reading.

------------------------------------------------------------------------

End of Notes.
