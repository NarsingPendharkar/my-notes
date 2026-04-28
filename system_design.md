## System Design Notes

System Design is the process of designing the architecture, components, and interfaces for a system so that it meets the end-user requirements.

- **Key Concepts**:
  - **Architecture**: The overall structure of the system, including how different parts interact.
  - **Components**: Individual parts of a system that work together to perform specific functions.
  - **Modules**: Smaller sections of a system that can be developed independently but work together as a whole.
  - **Interfaces**: Points of interaction between components or systems, allowing them to communicate.
- **Importance of System Design**:
  - Ensures that systems are efficient, scalable, and maintainable.
  - Helps in understanding user requirements and translating them into technical specifications.
- **Steps in System Design**:
  1. **Requirements Gathering**: Collecting information about what users need from the system.
  2. **System Specification**: Documenting the requirements in detail.
  3. **Design**: Creating models and diagrams to represent the system structure and behavior.
  4. **Implementation**: Actual building of the system based on the design.
  5. **Testing**: Checking the system for errors and ensuring it meets requirements.
  6. **Deployment**: Releasing the system for use.
  7. **Maintenance**: Ongoing support and updates to keep the system functioning well.
- **Types of System Design**:
  - **High-Level Design (HLD)**: Focuses on the system architecture and how components interact.
  - **Low-Level Design (LLD)**: Details how each component will be implemented, including algorithms and data structures.
- **Challenges in System Design**:
  - Balancing functionality with performance and cost.
  - Adapting to changing user needs and technology advancements.
  - Ensuring security and data protection.

---

### 🗺️ High-Level Design (HLD)

**HLD** focuses on the "Big Picture." It describes the overall architecture and how major services interact.

- **Goal:** Define the system structure, data flow, and major components.
- **Target Audience:** Architects, stakeholders, and senior developers.
- **Key Components:**
  - **Architecture:** Microservices vs. Monoliths.
  - **Databases:** Choosing between SQL and NoSQL.
  - **Communication:** Protocols (HTTP, WebSockets) and Message Queues (Kafka, RabbitMQ).
  - **Scalability:** Load balancers, Caching (Redis/CDN), and Rate Limiting.
- **Artifacts:** Architecture diagrams, data flow diagrams, and deployment diagrams.

------

### 🔍 Low-Level Design (LLD)

**LLD** focuses on the "Internal Logic." It provides a detailed blueprint for developers to start coding.

- **Goal:** Convert the HLD into a detailed implementation plan for individual modules.
- **Target Audience:** Senior developers and programmers.
- **Key Components:**
  - **OOP Concepts:** Encapsulation, Inheritance, and Polymorphism.
  - **Design Patterns:** Implementation of SOLID principles and specific patterns (e.g., Singleton, Strategy).
  - **Data Structures:** Selecting appropriate structures for logic.
  - **API Specs:** Precise request/response formats and error handling.
  - **Database Schema:** Detailed table structures, indexes, and relationships.
- **Artifacts:** UML Class diagrams, sequence diagrams, and pseudocode.

------

### 🚀 Steps to Approach a Design Problem

1. **Clarify Requirements:** Understand functional (what it does) and non-functional (performance, latency) requirements.
2. **Define Architecture:** Sketch the high-level flow (HLD).
3. **Choose Tech Stack:** Select languages, frameworks, and databases based on needs.
4. **Design Modules:** Break the system into smaller, manageable components (LLD).
5. **Plan for Scalability:** Identify bottlenecks and add load balancing or sharding.
6. **Ensure Security:** Implement authentication, encryption, and privacy measures.

---







##### **SCALABILITY**

Scalability is the ability of a system to handle increasing load by adding resources.

##### **AVAILABILITY**
Availability = Uptime / (Uptime + Downtime)

##### **LATENCY VS THROUGHPUT**
Latency: Time per request  
Throughput: Requests per second

##### **CAP THEOREM**
Consistency, Availability, Partition Tolerance (choose 2)

##### **LOAD BALANCERS**
Round Robin, Least Connections, IP Hash

##### **DATABASES**
Relational, NoSQL, In-Memory, Graph

##### **CDN**
Delivers content from nearest server

##### **MESSAGE QUEUES**
Async communication between services

##### **RATE LIMITING**
Token Bucket, Leaky Bucket

##### **DATABASE INDEXES**
Improve query performance

##### **CACHING**
Read-Through, Write-Through, LRU, TTL

##### **CONSISTENT HASHING**
Efficient distribution across nodes

##### **DATABASE SHARDING**
Horizontal partitioning

##### **CONSENSUS ALGORITHMS**
Paxos, Raft

##### **PROXY SERVERS**
Forward, Reverse proxy

##### **HEARTBEATS**
Health check signals

##### **CHECKSUMS**
Data integrity verification

##### **SERVICE DISCOVERY**
Dynamic service communication

##### **BLOOM FILTERS**
Probabilistic existence check

##### **GOSSIP PROTOCOL**
Decentralized data sharing

##### **SCALING**
Vertical vs Horizontal

##### **CONSISTENCY**
Strong vs Eventual

##### **STATE**
Stateful vs Stateless

##### **CACHE TYPES**
Read-Through vs Write-Through

##### **SQL VS NOSQL**
Structured vs Flexible

##### **REST VS RPC**
Resource vs Action based

##### **SYNC VS ASYNC**
Sequential vs Concurrent

##### **BATCH VS STREAM**
Bulk vs Real-time

##### **LONG POLLING VS WEBSOCKETS**
Polling vs Persistent connection

##### **NORMALIZATION VS DENORMALIZATION**
Integrity vs Performance

##### **TCP VS UDP**
Reliable vs Fast

##### **ARCHITECTURES**
Client-Server, Microservices, Serverless, Event-Driven, P2P

##### **SYSTEM DESIGN STEPS**
Requirements → Capacity → Design → DB → API → Deep Dive → Scale

##### **TIPS**
Design scalable, fault-tolerant systems

##### **COMMON QUESTIONS**
URL Shortener, Chat App, E-commerce, Streaming, Logging System
