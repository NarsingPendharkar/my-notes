# SQL vs NoSQL

## SQL Database

**SQL (Structured Query Language)** databases are **relational databases** that store data in **tables with rows and columns**.

Examples

- MySQL
- PostgreSQL
- Oracle Database

### Characteristics

- Data stored in **tables**
- Fixed **schema**
- Supports **ACID properties**
- Uses **SQL queries**
- Strong relationships using **primary key and foreign key**

### Example Table

Employee table

| emp_id | name  | salary |
| ------ | ----- | ------ |
| 1      | Rahul | 50000  |
| 2      | Priya | 60000  |

### Example Query

```sql
SELECT name, salary
FROM employee
WHERE salary > 50000;
```

### When to Use SQL

- Banking systems
- Financial systems
- Systems requiring **strong consistency**
- Applications with **complex joins**

Example
Bank transaction system must maintain **accurate balances**, so SQL is preferred.

------

# NoSQL Database

**NoSQL (Not Only SQL)** databases are **non-relational databases** designed for **large-scale distributed data**.

Examples

- MongoDB
- Apache Cassandra
- Redis

### Characteristics

- Schema **flexible**
- Stores **unstructured or semi-structured data**
- High **horizontal scalability**
- Designed for **big data and high traffic**
- Usually follows **BASE model instead of ACID**

------

# Types of NoSQL Databases

### 1. Document Database

Stores data as JSON-like documents.

Example

```json
{
  "emp_id": 1,
  "name": "Rahul",
  "skills": ["Java", "Spring Boot"]
}
```

Example database
MongoDB

------

### 2. Key-Value Database

Data stored as **key-value pairs**

Example

```
key: user123
value: {name: "Rahul", age: 28}
```

Example database
Redis

------

### 3. Column-Based Database

Stores data in **columns instead of rows**.

Example database
Apache Cassandra

------

### 4. Graph Database

Used for relationship-heavy data.

Example database
Neo4j

Example use case

- Social networks
- Recommendation engines

------

# SQL vs NoSQL Comparison

| Feature        | SQL        | NoSQL                         |
| -------------- | ---------- | ----------------------------- |
| Database Type  | Relational | Non-Relational                |
| Schema         | Fixed      | Flexible                      |
| Data Structure | Tables     | Documents / Key-Value / Graph |
| Query Language | SQL        | Database specific             |
| Scalability    | Vertical   | Horizontal                    |
| Transactions   | ACID       | BASE                          |
| Joins          | Supported  | Usually avoided               |

------

# ACID vs BASE

### ACID (Used in SQL)

| Property    | Meaning                            |
| ----------- | ---------------------------------- |
| Atomicity   | All operations succeed or rollback |
| Consistency | Data always valid                  |
| Isolation   | Transactions independent           |
| Durability  | Data permanently stored            |

Example
Bank money transfer.

------

### BASE (Used in NoSQL)

| Property              | Meaning                    |
| --------------------- | -------------------------- |
| Basically Available   | System always available    |
| Soft State            | Data may change over time  |
| Eventually Consistent | Consistency achieved later |

Example
Social media likes count may update after few seconds.

------

# Real Project Example (Java Microservices)

### SQL Use Case

Banking application

Tables

```
Customer
Account
Transaction
```

Reason

- Need **ACID transactions**
- Data consistency critical

------

### NoSQL Use Case

Application logs or analytics.

Example document

```json
{
  "service": "payment-service",
  "status": "success",
  "time": "2026-03-10T10:20:00"
}
```

Reason

- Huge data
- Flexible structure

------

**When should you use SQL vs NoSQL?**

Good answer:

Use **SQL**

- When data relationships are complex
- When ACID transactions are required
- Example: banking, payments

Use **NoSQL**

- When handling large-scale distributed data
- Flexible schema required
- Example: logs, analytics, social media

---



# 1. DBMS vs RDBMS

## DBMS

**DBMS (Database Management System)** is software used to store and manage data.

Examples

- MySQL
- PostgreSQL
- Oracle Database

### Characteristics

- Data stored in files
- Limited relationships
- Less data integrity
- Less security

------

## RDBMS

**RDBMS (Relational Database Management System)** stores data in **tables with relationships**.

### Characteristics

- Tables connected via keys
- Supports ACID properties
- High data integrity
- Used in enterprise systems

------

## Example

```sql
CREATE TABLE employee (
    id INT,
    name VARCHAR(50),
    salary DECIMAL
);
```

------

# 2. Primary Key

A **Primary Key** uniquely identifies each row in a table.

### Rules

- Must be **unique**
- Cannot contain **NULL**
- Only **one primary key per table**

### Example

```sql
CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL
);
```

### Example Data

| emp_id | name  | salary |
| ------ | ----- | ------ |
| 1      | Rahul | 50000  |
| 2      | Priya | 60000  |

------

# 3. Foreign Key

A **Foreign Key** creates a relationship between two tables.

### Example

Employee belongs to a department.

```sql
CREATE TABLE department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES department(dept_id)
);
```

### Relationship

```
Department (Parent)
        |
        |
Employee (Child)
```

------

# 4. Composite Key

A **Composite Key** is a combination of multiple columns used as a primary key.

### Example

Order can contain multiple products.

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY(order_id, product_id)
);
```

### Example Data

| order_id | product_id | quantity |
| -------- | ---------- | -------- |
| 101      | 1          | 2        |
| 101      | 2          | 1        |

------

# 5. Index

An **Index** improves database query performance.

### Without Index

Database scans entire table (**Full Table Scan**).

### With Index

Database directly finds data.

### Example

```sql
CREATE INDEX idx_employee_name
ON employee(name);
```

### Benefits

- Faster SELECT queries
- Improves search performance

### Drawback

- Slightly slower INSERT / UPDATE

------

# 6. WHERE vs HAVING

| Feature             | WHERE           | HAVING          |
| ------------------- | --------------- | --------------- |
| Used for            | Row filtering   | Group filtering |
| Used with aggregate | No              | Yes             |
| Executed            | Before GROUP BY | After GROUP BY  |

### Example

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id
HAVING SUM(salary) > 50000;
```

------

# 7. ACID Properties

ACID ensures **reliable database transactions**.

### Atomicity

Transaction happens completely or not at all.

Example
Money transfer fails → rollback.

### Consistency

Database remains in valid state.

Example
Balance cannot become negative.

### Isolation

Multiple transactions do not interfere.

### Durability

Once committed → data is permanently stored.

------

# 8. Joins

Join is used to combine data from multiple tables.

### Types of Joins

| Join       | Description                  |
| ---------- | ---------------------------- |
| INNER JOIN | Returns matching records     |
| LEFT JOIN  | All records from left table  |
| RIGHT JOIN | All records from right table |
| FULL JOIN  | All records from both tables |

------

## Example Tables

### Employee

| id   | name  | dept_id |
| ---- | ----- | ------- |
| 1    | Rahul | 10      |
| 2    | Priya | 20      |

### Department

| dept_id | dept_name |
| ------- | --------- |
| 10      | IT        |
| 20      | HR        |

------

## INNER JOIN Example

```sql
SELECT e.name, d.dept_name
FROM employee e
INNER JOIN department d
ON e.dept_id = d.dept_id;
```

Result

| name  | dept_name |
| ----- | --------- |
| Rahul | IT        |
| Priya | HR        |

------

# 9. DELETE vs TRUNCATE vs DROP

| Command  | Description              | Rollback |
| -------- | ------------------------ | -------- |
| DELETE   | Removes rows             | Yes      |
| TRUNCATE | Removes all rows quickly | No       |
| DROP     | Deletes table structure  | No       |

### Examples

Delete specific row

```sql
DELETE FROM employee
WHERE emp_id = 10;
```

Remove all rows

```sql
TRUNCATE TABLE employee;
```

Delete table

```sql
DROP TABLE employee;
```

------

# 10. Normalization

Normalization removes **data redundancy** and improves **data consistency**.

------

## 1NF (First Normal Form)

- No repeating columns
- Atomic values

Bad Example

| id   | phones  |
| ---- | ------- |
| 1    | 123,456 |

Good Example

| id   | phone |
| ---- | ----- |
| 1    | 123   |
| 1    | 456   |

------

## 2NF (Second Normal Form)

Remove **partial dependency**.

------

## 3NF (Third Normal Form)

Remove **transitive dependency**.

Example

Bad design

| emp_id | dept_id | dept_name |

Better design

Employee Table

| emp_id | dept_id |

Department Table

| dept_id | dept_name |

------

# 11. Third Highest Salary Query

### Method 1 – Using LIMIT

(PostgreSQL)

```sql
SELECT salary
FROM employee
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
```

------

### Method 2 – Using DENSE_RANK

Handles duplicate salaries.

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) r
    FROM employee
) t
WHERE r = 3;
```

------

# 12. Transactions

Transaction = group of operations executed together.

### Example

Bank Transfer

```sql
BEGIN;

UPDATE account
SET balance = balance - 1000
WHERE id = 1;

UPDATE account
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

If error occurs

```
ROLLBACK;
```

------

# 13. View

A **View** is a virtual table created from a query.

### Example

```sql
CREATE VIEW employee_view AS
SELECT name, salary
FROM employee;
```

### Use Case

- Security
- Simplify complex queries

------

# 14. Stored Procedure

Stored Procedure = precompiled SQL stored in database.

### Example

```sql
CREATE PROCEDURE getEmployees()
BEGIN
    SELECT * FROM employee;
END;
```

Execute

```sql
CALL getEmployees();
```

------

# 15. Pagination

Pagination is used when dataset is very large.

### Example

Get page 3 with 10 records per page.

```sql
SELECT *
FROM employee
LIMIT 10 OFFSET 20;
```

Explanation

```
OFFSET = (page_number - 1) * page_size
```

------

# 16. Query Optimization

Improving query performance.

### Techniques

- Use **indexes**
- Avoid `SELECT *`
- Use **JOIN instead of subqueries when possible**
- Use **EXPLAIN plan**

Example

```sql
EXPLAIN
SELECT *
FROM employee
WHERE dept_id = 10;
```

------

# 17. N+1 Query Problem (Hibernate)

Occurs when ORM executes multiple queries.

Example

1 query for orders

```
SELECT * FROM orders;
```

Then for each order

```
SELECT * FROM items WHERE order_id=1;
SELECT * FROM items WHERE order_id=2;
SELECT * FROM items WHERE order_id=3;
```

### Solution

Use **JOIN FETCH**

```java
SELECT o FROM Order o
JOIN FETCH o.items
```

------

# 18. Optimistic Locking

Used to prevent concurrent update issues.

### Example

```java
@Version
private int version;
```

If two users update same record → second update fails.

------

# 19. Pessimistic Locking

Database locks row immediately.

Example

```sql
SELECT * FROM account
FOR UPDATE;
```

