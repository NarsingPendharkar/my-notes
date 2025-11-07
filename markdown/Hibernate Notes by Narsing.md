**Hibernate**

## What is Hibernate? Why is it used?

**Answer:** Hibernate is a object relational mapping framework which maps the java classes to the database tables and java data types to SQL data types automatically and generates the queries automatically.

**Advantages of Hibernate over JDBC:**

* Reduces boilerplate code
* Manages database connections and transactions
* Provided primary key auto increment feature
* Reduces developers’ effort , time and cost
* Supports caching for better performance
* Provides HQL (Hibernate Query Language) for database operations

**Disadvantages of Hibernate over JDBC:**

* Can’t perform multiple insertion at a time
* Debugging is difficult as compare to JDBC
* Contains lots of boiler plate code
* Can’t be used for small type of applications.

**Hibernate Mapping (XML and Annotations):**

1. XML Mapping: Define mappings in .hbm.xml files.
2. Annotations: Use Java annotations for mapping.

## What is ORM?

**Answer:** ORM stands for object relational mapping and it is a technic for converting object-oriented programming data to relational database. It is a programming technique that maps the object to the data stored in the database.

## What are the advantages of Hibernate over JDBC?

|  |  |  |
| --- | --- | --- |
| Feature | JDBC | Hibernate |
| Query Writing | Requires SQL queries | Uses HQL (Hibernate Query Language) |
| Object Mapping | Manual mapping | Automatic ORM mapping |
| Caching | No built-in caching | Supports first-level and second-level caching |
| Database Independence | Database-specific SQL | Works with multiple databases |

**Hibernate Example :**

1. **First create new maven project and use quick-start arch type.**
2. **Then Add required dependencies in pom.xml**

<!-- MS SQL -->

<dependency>

<groupId>com.microsoft.sqlserver</groupId>

<artifactId>mssql-jdbc</artifactId>

<version>12.9.0.jre11-preview</version>

</dependency>

<!-- Hibernate Core -->

<dependency>

<groupId>org.hibernate</groupId>

<artifactId>hibernate-core</artifactId>

<version>6.3.1.Final</version>

</dependency>

<!-- JPA API -->

<dependency>

<groupId>jakarta.persistence</groupId>

<artifactId>jakarta.persistence-api</artifactId>

<version>3.1.0</version>

</dependency>

1. **Create the hibernate configuration file in resource folder i.e hibernate.cfg.xml**

<?xml version='1.0' encoding='UTF-8'?>

<!DOCTYPE hibernate-configuration PUBLIC

"-//Hibernate/Hibernate Configuration DTD 3.0//EN"

"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

<session-factory>

<!-- Hibernate DDL Auto (Update DB Schema) -->

<property name="hibernate.hbm2ddl.auto">update</property>

<!-- SQL Server Dialect -->

<property name="hibernate.dialect">org.hibernate.dialect.SQLServer2012Dialect</property>

<!-- Database Connection Settings -->

<property name="hibernate.connection.driver\_class">com.microsoft.sqlserver.jdbc.SQLServerDriver</property>

<property name="hibernate.connection.url">jdbc:sqlserver://DESKTOP-G774017:1433;databaseName=testdb;encrypt=false</property>

<property name="hibernate.connection.username">Narsing</property>

<property name="hibernate.connection.password">root</property>

<!-- Show SQL Queries in Console -->

<property name="hibernate.show\_sql">true</property>

<property name="hibernate.format\_sql">true</property>

</session-factory>

</hibernate-configuration>

1. **Create class for table mapping**

@Entity

@Table(name = "Emp")

**public** **class** Employee {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

**private** **int** id;

**private** String name;

**private** **int** age;

**private** String address;

}

1. **Now write a code to connect database and perform operation**

**public** **static** **void** main(String[] args) {

**try** {

// 1. Load Hibernate Configuration

Configuration cfg = **new** Configuration();

cfg.configure("hibernate.cfg.xml");

cfg.addAnnotatedClass(Employee.**class**);

System.***out***.println("Loaded Hibernate configuration");

// 2. Build SessionFactory

SessionFactory sessionFactory = cfg.buildSessionFactory();

// 3. Open Session

Session session = sessionFactory.openSession();

// 4. Start Transaction

Transaction txn = session.beginTransaction();

// 5. Create Employee Object

Employee emp = **new** Employee();

emp.setName("nikita");

emp.setAddress("kolnoor");

emp.setAge(24);

// 6. Save Employee Object

session.save(emp);

// 7. Commit Transaction

txn.commit();

System.***out***.println("Employee created successfully: " + emp);

// 8. Close Session & SessionFactory

session.close();

sessionFactory.close();

} **catch** (Exception e) {

e.printStackTrace(); // Print the actual error

}

}

## Steps to Create a **SessionFactory** Object in Hibernate and Perform an Operation

### **Step 1: Load Hibernate Configuration**

* The Configuration class is used to **load and configure** Hibernate settings from hibernate.cfg.xml.
* This takes hibernate-configuration file name and location as input value . also take hibernate maping files names.
* Use:

Configuration cfg = **new** Configuration();

cfg.configure("hibernate.cfg.xml");

* **Explanation**:
  + **new** Configuration() initializes the Hibernate configuration.
  + cfg.configure("hibernate.cfg.xml") loads database connection details and Hibernate properties.’

### **Step 2: Add Annotated Entity Class (Optional)**

* If you're using **annotations** instead of hbm.xml mapping files, register the entity class:
* cfg.addAnnotatedClass(Employee.**class**);
* **Explanation**:
  + This tells Hibernate to recognize the @Entity annotated Employee class.

### **Step 3: Build the** SessionFactory **Object**

* The SessionFactory is the main Hibernate factory for creating sessions:
* It is the interface used to create session factory object and which turn configure hibernate for the application using configuration file and allows for a session object to be intiate.

SessionFactory sessionFactory = cfg.buildSessionFactory();

* **Explanation**:
  + buildSessionFactory reads the configuration and creates a **single instance** of SessionFactory.
  + This object **must be created once** (Singleton Pattern).

### **Step 4: Open a Session**

* A Session represents a **database connection**.

Session session = sessionFactory.openSession();

* **Explanation**:
  + openSession() creates a **new session** for database operations.
  + Sessions are **not thread-safe**; use a new one for each transaction.

### **Step 5: Begin a Transaction**

* Transactions ensure **ACID compliance**:

Transaction txn = session.beginTransaction();

* **Explanation**:
  + beginTransaction() starts a database transaction.
  + All DB changes must be committed or rolled back within a transaction.

### **Step 6: Perform a Database Operation**

* **Example: Saving an Employee object**

session.save(emp);

* **Explanation**:
  + save(emp) inserts a new row if the primary key does not exist; otherwise, it updates.

### **Step 7: Commit the Transaction**

* Save the changes to the database:

txn.commit();

* **Explanation**:
  + commit() makes the changes permanent.

#### **Step 8: Close the Session and SessionFactory**

* Always **release resources** after use:

session.close();

sessionFactory.close();

* **Explanation**:
  + session.close(); closes the current session.
  + sessionFactory.close(); shuts down Hibernate completely.

### **✅ Summary of Steps**

|  |  |  |
| --- | --- | --- |
| **Step** | **Operation** | **Method Used** |
| 1️ | Load Hibernate Config | cfg.configure("hibernate.cfg.xml") |
| 2️ | Add Entity Class (Optional) | cfg.addAnnotatedClass(Employee.class) |
| 3️ | Build SessionFactory | cfg.buildSessionFactory() |
| 4️ | Open a Session | sessionFactory.openSession() |
| 5️ | Begin Transaction | session.beginTransaction() |
| 6️ | Perform Operation | session.saveOrUpdate(emp) |
| 7️ | Commit Transaction | txn.commit() |
| 8️ | Close Resources | session.close(); sessionFactory.close(); |

## Explain Hibernate Architecture.

**Answer:** Hibernate consists of several components:

1. **Configuration (hibernate.cfg.xml)** – Stores database and Hibernate configurations.
2. **SessionFactory** – A factory for Session objects (one per database).
3. **Session** – Provides methods for performing CRUD operations.
4. **Transaction** – Manages database transactions.
5. **Query API** – HQL (Hibernate Query Language) and Criteria API.

## What is SessionFactory in Hibernate?

**Answer:** SessionFactory is a heavyweight object that creates and manages Session objects. It is created **once per database** and is thread-safe.

## What is Session in Hibernate?

**Answer:** A Session is a lightweight, non-thread-safe object that acts as a bridge between Java code and the database. It is used to perform CRUD operations.

## What are the different states of an entity in Hibernate?

* **Transient:** The object is created but not associated with a Hibernate session.
* **Persistent:** The object is associated with a session and mapped to a database.
* **Detached:** The object was persistent but is now out of the session scope.
* **Removed:** The object is marked for deletion.

## What is HQL (Hibernate Query Language)? How is it different from SQL?

**Answer:** HQL is an object-oriented query language that uses entity names instead of table names. It is database-independent.
Example:

String hql = "FROM Student WHERE name = :name";

Query query = session.~~createQuery~~(hql);

query.setParameter("name", "Nirav");

List<Student> students = query.list();

## What are Fetch Types in Hibernate?

* **Lazy Loading (FetchType.LAZY)** – Data is loaded only when requested.
* **Eager Loading (FetchType.EAGER)** – Data is loaded immediately.

Example:

@OneToMany(fetch = FetchType.LAZY)

**private** List<Course> courses;

## What is the difference between save(), persist(), and saveOrUpdate()?

|  |  |  |
| --- | --- | --- |
| Method | When to Use | Returns |
| save() | Inserts new record | Generated primary key |
| persist() | Inserts new record, but doesn’t return ID | void |
| saveOrUpdate() | Inserts if new, updates if existing | void |

## What are @OneToOne, @OneToMany, and @ManyToMany relationships in Hibernate?

**Answer:**

* **One-to-One:** A person has one passport.
* **One-to-Many:** A department has many employees.
* **Many-to-Many:** A student can enrol in multiple courses.

Example:

@OneToMany(mappedBy = "department", cascade = CascadeType.ALL)

**private** List<Employee> employees;

## What is the difference between First-Level and Second-Level Cache?

|  |  |  |
| --- | --- | --- |
| Cache Type | Scope | Default? |
| First-Level Cache | Per Session | Yes |
| Second-Level Cache | Across Sessions | No |

## What is the difference between HQL and Criteria API?

|  |  |  |
| --- | --- | --- |
| Feature | HQL | Criteria API |
| Query Type | String-based | Object-oriented |
| Readability | Hard to read for complex queries | Easy to read |

Example of Criteria API:

CriteriaBuilder cb = session.getCriteriaBuilder();

CriteriaQuery<Student> cq = cb.createQuery(Student.**class**);

Root<Student> root = cq.from(Student.**class**);

cq.select(root).where(cb.equal(root.get("name"), "Nirav"));

Query<Student> query = session.~~createQuery~~(cq);

List<Student> students = query.getResultList();

## What are the different caching strategies in Hibernate?

1. **Read-Only:** Best for static data.
2. **Non-Strict Read-Write:** Allows reads, but updates are not guaranteed.
3. **Read-Write:** Uses timestamps to maintain consistency.
4. **Transactional:** Works with JTA transactions.

## How does Hibernate handle transactions?

**Answer:** Transactions in Hibernate are managed using beginTransaction() and commit().

Example:

SessionFactory sf= HibernateUtil.getSessionFactory() ;

Session session=sf.openSession();

Transaction txn=**null**;

**try** {

txn=session.beginTransaction();

Question q=session.~~load~~(Question.**class**, 2);

System.***out***.println(q.toString());

txn.commit();

session.close();

HibernateUtil.shutdown();

} **catch** (Exception e) {

**if**(txn!=**null**) {

txn.rollback();

}

e.printStackTrace();

}

## How would you optimize performance in Hibernate?

* Use **lazy loading** (FetchType.LAZY).
* Enable **second-level caching** (EhCache, Infinispan).
* Optimize **batch processing** using batch\_size.
* Use **pagination** in queries.

## What will happen if you don't close a Hibernate Session?

**Answer:** Memory leaks can occur because the session holds database connections and cached objects.

## How do you integrate Hibernate with Spring Boot?

By using spring-boot-starter-data-jpa:

spring.datasource.url=jdbc:mysql://localhost:3306/hibernate\_db

spring.jpa.hibernate.ddl-auto=update

## **Hibernate Mappings Explained with Example**

### **One-to-One Mapping**

**Definition:**

In **One-to-One mapping**, one entity is related to exactly one other entity.
Example: A **Person** has only **one Passport**, and a Passport belongs to only one Person.

### **🛠 Implementation:**

* **Use @OneToOne annotation.**
* **Use @JoinColumn to specify the foreign key.**

### **📌 Example**

**public** **class** Person {

@Id

@GeneratedValue(strategy = GenerationType.***IDENTITY***)

**private** **int** id;

@Column

@NotBlank

**private** String name;

@OneToOne(cascade = CascadeType.***ALL***)

@JoinColumn(name="passport\_id")

**private** Passport passport;

}

**public** **class** Passport {

@Id

@GeneratedValue(strategy = GenerationType.***IDENTITY***)

**private** **int** id;

**private** String passportNumber;

@OneToOne

**private** Person person;

}

🔹 **Database Example:**

|  |  |  |
| --- | --- | --- |
| person\_id | name | passport\_id |
| 1 | Nirav | 101 |

|  |  |
| --- | --- |
| passport\_id | passportNumber |
| 101 | A123456 |

### One-to-Many Mapping

**Definition:**

In **One-to-Many mapping**, one entity can be related to multiple other entities.
Example: A **Department** has multiple **Employees**, but an Employee belongs to only one Department.

### **Implementation:**

* **Use @OneToMany on the parent (Department)**
* **Use @ManyToOne on the child (Employee)**
* **Use mappedBy to establish bidirectional mapping**

### **📌 Example**

**public** **class** Department {

@Id

@GeneratedValue(strategy = GenerationType.***IDENTITY***)

**private** **int** id;

**private** String department;

@OneToMany(mappedBy = "department", cascade = CascadeType.***ALL***)

**private** List<Employee> employees;

}

@Entity

**public** **class** Employee {

@Id

@GeneratedValue(strategy = GenerationType.***AUTO***)

**private** **int** id;

**private** String name;

**private** **double** salary;

@ManyToOne

@JoinColumn(name = "department\_id")

**private** Department department;

}

🔹 **Database Example:**

|  |  |
| --- | --- |
| department\_id | name |
| 1 | IT |
|  |  |
|  |  |

|  |  |  |
| --- | --- | --- |
| employee\_id | name | department\_id |
| 101 | Nirav | 1 |
| 102 | Raj | 1 |

### **Many-to-Many Mapping**

### **Definition:**

In **Many-to-Many mapping**, multiple entities can be associated with multiple other entities.
Example: A **Student** can enroll in multiple **Courses**, and a Course can have multiple Students.

### **Implementation:**

* **Use @ManyToMany on both entities.**
* **Use @JoinTable to create a join table between them.**

### **Example**

@Entity

@Table(name = "student")

**public** **class** Student {

@Id

@GeneratedValue(strategy = GenerationType.***IDENTITY***)

**private** **int** id;

**private** String name;

@ManyToMany

@JoinTable(

name = "student\_course",

joinColumns = @JoinColumn(name = "student\_id"),

inverseJoinColumns = @JoinColumn(name = "course\_id")

)

**private** List<Course> courses;

// Getters, Setters, Constructors

}

@Entity

@Table(name = "course")

**public** **class** Course {

@Id

@GeneratedValue(strategy = GenerationType.***IDENTITY***)

**private** **int** id;

**private** String title;

@ManyToMany(mappedBy = "courses")

**private** List<Student> students;

// Getters, Setters, Constructors

}

🔹 **Database Example (Join Table):**

|  |  |
| --- | --- |
| student\_id | course\_id |
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

👆 **Student 1 is enrolled in Course 101 and 102, while Student 2 is only in Course 101.**

### **Summary Table of Hibernate Mappings**

|  |  |  |
| --- | --- | --- |
| Mapping Type | Example | Hibernate Annotation |
| One-to-One | Person ↔ Passport | @OneToOne |
| One-to-Many | Department ↔ Employees | @OneToMany, @ManyToOne |
| Many-to-Many | Student ↔ Course | @ManyToMany |

✔ **One-to-One**: One entity maps to exactly one other entity.
✔ **One-to-Many**: One entity maps to multiple child entities.
✔ **Many-to-Many**: Entities have multiple relationships with each other via a join table.

### **Hibernate Mapping Annotations Summary Table**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @Entity | Marks a class as a JPA entity (mapped to a table) | @Entity public class Student {} |
| @Table(name = "table\_name") | Specifies the table name in the database | @Table(name = "students") |
| @Id | Marks a field as the primary key | @Id private Long id; |
| @GeneratedValue(strategy = GenerationType.IDENTITY) | Specifies how the primary key is generated | @GeneratedValue(strategy = GenerationType.IDENTITY) |
| @Column(name = "column\_name") | Maps a field to a specific database column | @Column(name = "student\_name") private String name; |
| @Transient | Excludes a field from persistence (not stored in the database) | @Transient private int age; |
| @Basic(fetch = FetchType.LAZY) | Marks a field for lazy loading | @Basic(fetch = FetchType.LAZY) private String description; |
| @Temporal(TemporalType.DATE) | Specifies how Date/Time fields should be stored | @Temporal(TemporalType.DATE) private Date dob; |
| @Lob | Maps a field to a large object (BLOB or CLOB) | @Lob private byte[] image; |

### **Primary Key and ID Generation**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @GeneratedValue(strategy = GenerationType.IDENTITY) | Uses auto-increment (database-generated) | @GeneratedValue(strategy = GenerationType.IDENTITY) |
| @GeneratedValue(strategy = GenerationType.SEQUENCE) | Uses a database sequence for ID generation | @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "seq") |
| @SequenceGenerator(name = "seq", sequenceName = "my\_sequence", allocationSize = 1) | Defines a sequence generator | @SequenceGenerator(name = "seq", sequenceName = "student\_seq") |
| @GeneratedValue(strategy = GenerationType.TABLE) | Uses a table-based strategy for ID generation | @GeneratedValue(strategy = GenerationType.TABLE) |

### **One-to-One Mapping**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @OneToOne | Defines a one-to-one relationship | @OneToOne private Profile profile; |
| @JoinColumn(name = "profile\_id") | Specifies the foreign key column | @JoinColumn(name = "profile\_id") |
| @MapsId | Uses the primary key of the parent entity as the foreign key | @MapsId private Long id; |

### **One-to-Many and Many-to-One Mapping**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @OneToMany(mappedBy = "department") | One-to-many bidirectional mapping | @OneToMany(mappedBy = "department") private List<Employee> employees; |
| @ManyToOne | Many-to-one relationship (child to parent) | @ManyToOne @JoinColumn(name = "department\_id") |
| @JoinColumn(name = "foreign\_key\_column") | Defines the foreign key column | @JoinColumn(name = "dept\_id") |
| @Cascade(CascadeType.ALL) | Defines cascading operations | @Cascade(CascadeType.ALL) |

### **Many-to-Many Mapping**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @ManyToMany | Defines a many-to-many relationship | @ManyToMany private List<Course> courses; |
| @JoinTable(name = "student\_course", joinColumns = @JoinColumn(name = "student\_id"), inverseJoinColumns = @JoinColumn(name = "course\_id")) | Defines a join table for many-to-many relationships | @JoinTable(name = "student\_course") |

### **Cascade and Fetch Strategies**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @Cascade(CascadeType.ALL) | Propagates all operations (SAVE, DELETE, etc.) | @Cascade(CascadeType.ALL) |
| @Cascade(CascadeType.MERGE) | Propagates merge operation | @Cascade(CascadeType.MERGE) |
| @Cascade(CascadeType.REMOVE) | Propagates remove operation | @Cascade(CascadeType.REMOVE) |
| @Cascade(CascadeType.REFRESH) | Refreshes entity when the transaction is committed | @Cascade(CascadeType.REFRESH) |
| @Fetch(FetchMode.JOIN) | Fetches related entities using joins | @Fetch(FetchMode.JOIN) |
| @Fetch(FetchMode.SELECT) | Fetches related entities with separate queries | @Fetch(FetchMode.SELECT) |

### **Named Queries (JPQL and Native SQL)**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @Query("SELECT s FROM Student s WHERE s.name = ?1") | Defines a JPQL query | @Query("SELECT s FROM Student s WHERE s.name = ?1") |
| @Query(value = "SELECT \* FROM students WHERE email = ?1", nativeQuery = true) | Defines a native SQL query | @Query(value = "SELECT \* FROM students WHERE email = ?1", nativeQuery = true) |
| @NamedQuery(name = "Student.findByName", query = "SELECT s FROM Student s WHERE s.name = :name") | Defines a named JPQL query | @NamedQuery(name = "Student.findByName", query = "SELECT s FROM Student s WHERE s.name = :name") |

### **Transactional and Locking Annotations**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @Transactional | Marks a method as transactional | @Transactional public void saveStudent(Student s) {} |
| @Modifying | Used with @Query for update/delete operations | @Modifying @Query("UPDATE Student s SET s.name = ?1 WHERE s.id = ?2") |
| @Version | Enables optimistic locking (prevents concurrent updates) | @Version private int version; |

### **Logging and Debugging**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @EnableJpaRepositories | Enables JPA repositories | @EnableJpaRepositories("com.example.repository") |
| spring.jpa.show-sql=true | Logs generated SQL queries | In application.properties |
| spring.jpa.properties.hibernate.format\_sql=true | Formats SQL queries in logs | In application.properties |

### **Special Field Annotations**

|  |  |  |
| --- | --- | --- |
| **Annotation** | **Description** | **Example Usage** |
| @CreationTimestamp | Automatically sets the timestamp when a record is created | @CreationTimestamp private LocalDateTime createdAt; |
| @UpdateTimestamp | Automatically updates the timestamp when a record is modified | @UpdateTimestamp private LocalDateTime updatedAt; |
| @Enumerated(EnumType.STRING) | Maps an enum to a database column as a string | @Enumerated(EnumType.STRING) private Status status; |
| @Lob | Maps a large object (BLOB or CLOB) | @Lob private byte[] image; |

## Difference between get( ) & load( )?

|  |  |
| --- | --- |
| get ( ) | load ( ) |
| Eager Loading | Lazy Loading |
| If value is absent in database then it returns null. | If value is absent in database then hibernate exception (ObjectNotFoundException) occurs. |
| It always hit database. | It may or may not be hit to database. |

Difference between save( ) & persist( **)?**

|  |  |
| --- | --- |
| Save ( ) | Persist ( ) |
| Its return type is Serializable object. | Its return type is void. |
| It can save object within transaction boundaries and outside boundaries. | It can only save object within the transaction boundaries. |
| It is only supported by Hibernate. | It is supported by Hibernate and also by JPA (Java Persistence API). |
| It will create a new row in the table for detached object. | It will throw persistence exception for detached object. |

## What is cache? What is 1st level cache?

* First level cache is associated with session and its by default enabled.
* When we fire query first time we will get data from database and then data is stored in session object.
* Then next time when you fire same query to get same data then it will not hit query on database it gets data from session object.

## What is 2nd level cache?

* It is enabled with session factory and its need to be enabled.
* It is available globally for all session.
* It stores data from first level cache then to second level cached also then if we try to get same record then first it see withing 1 level cache if data present or not.
* If data is not present in 1 level cache it will check in 2 level cache
* If these also data not found then it goes to fire query from database.

## How to remove particular object from cache?

**Answer :** Session has Evict( ) method used for removing particular cache.

## How to clean cache?

**Answer :** Session has **Clear( )** method to clear all cache.

## Which version of Hibernate, Spring, Spring boot you have used?

**Answer :** Hibernate-4, Spring-4, Springboot-2.

## In One-to-Many & Many-to-One, how many tables are created by-default and if mapped by is used?

**Answer :** By-default it will create 3 tables.

For mapped by it will create 2 tables.

## In Many-to-Many, how many tables are created by-default and if mapped by is used?

**Answer :** By-default it will create 4 tables.

For mapped by it will create 3 tables.

## What is Dirty Checking?

**Answer :** If we get record & we set again then it is updated without calling update method, its because of dirty checking. This can be avoided by using @Immutable annotation.

## What is process for Automatic ID generation from any random number?

@SequenceGenerator(name = "mySeqGen", sequenceName = "mySeq", initialValue = 500, allocationSize=1)

@GeneratedValue(generator = "mySeqGen")

## How to show SQL queries at run time?

**Answer :** While specifying hibernate properties, add Show\_SQL property as a true,

e.g. <property name="show\_sql">true</property>

## What does hbm2ddl does?

**Answer :** It validates number of column.

## How to disable 1st level cache?

**Answer :** We can’t disable cache but we can clear all cache using clear( ) method of session, then it works as disabled.

## How to enable 2nd level cache?

* Add 3 rd party jar files. (ehcache)
* Add Annotation below to Entity class.

@Cache(usage=CacheConcurrencyStrategy.READ\_WRITE)

* Include two extra lines in settings in ‘HibernateUtil.class’

settings.put(Environment.USE\_SECOND\_LEVEL\_CACHE, "true");

settings.put(Environment.CACHE\_REGION\_FACTORY, "org.hibernate.cache.ehcache.EhCach-eRegionFactory");

## How you have used Hibernate (XML, Annotations, Java Based)?

(Always Answer as) Annotation Based.

## Native Queries-Definition, syntax, advantages?

* It allows developers to write **pure SQL queries** and execute them within Hibernate.
* Your application will create a native SQL query from the session with the createSQLQuery() method.
* You need to pass a string containing the SQL query to the createSQLQuery() method.
* List<Object[]> results = session.createNativeQuery("SELECT id, name, age FROM Employee").list();

**Spring Data JPA![Database with solid fill](data:image/png;base64...)**

## What is Spring Data JPA?

Answer :

* It is a part of spring framework that reduces the boiler plate code of database connection and transection management and take care of everything. We have to implement only repository interface and it will handle every thing
* It has inbuild methods to perform database operations like findbyId, findall() etc.
* It is built on top of JPA and provide the repository interface that handles all the database operations.

## What are the advantages of Spring Data JPA?

**Answer:**

* Reduces boiler plate code
* Provide built in CRUD operations.
* Support pagination and sorting
* Support Native Query, Criteria API,JPQL

## **What is the purpose of the** @Entity **annotation in JPA?**

**Answer :** The @Entity annotation marks a Java class as a **JPA entity**, meaning it maps to a table in the database.

### **What is the** @Repository **annotation?**

It is used in Spring Data JPA to indicate that a class is a **DAO (Data Access Object)**. It also enables **exception translation** for database-related exceptions.

## **What is the difference between** JpaRepository**,** CrudRepository**, and** PagingAndSortingRepository**?**

|  |  |
| --- | --- |
| Interface | Description |
| CrudRepository | Provides basic CRUD operations (save(), findById(), delete()). |
| PagingAndSortingRepository | Extends CrudRepository with pagination and sorting features. |
| JpaRepository | Extends PagingAndSortingRepository and provides **flush, batch processing, and custom queries**. |

![](data:image/png;base64...)

## **What are Derived Queries in Spring Data JPA?**

Spring Data JPA generates queries **automatically** based on method names.

Example:

List<Employee> findByDepartment(String department);

## How do you write a custom query using @Query annotation?

@Query( value="SELECT count(task\_id) FROM tasks ",nativeQuery=**true**)

**public** Integer getcount();

@Query(value="SELECT count(task\_id) FROM tasks where status=",nativeQuery=**true**)

**public** Integer getCompletedtasks();

@Query(value="SELECT count(task\_id) FROM tasks where deadline<?1", nativeQuery=**true**)

**public** Integer getOverduetasks( String date);

## **How do you enable pagination in Spring Data JPA?**.

Answer:

* Pagination is used to print small amount of data instead of all data at a time from the database
* This will help us to improve the performance
* For that we will use Pageable interface object sent as a parameter in findAll method.
* **Page**: this is used to hold the current page data, total number of elements and weather there are more pages .

Page<Tasks> alltasks(Pageable pageable);

* **PageRequest**: The request object can be used to specify which page to fetch and how many records should be included in that page. It takes page Size and page number as parameter

PageRequest.of(page, size))

Example:

**Service Method :**

Page<Tasks> alltasks(Pageable pageable);

**Service Implementation :**

**public** Page<Tasks> alltasks(Pageable pageable) {

**return** taskRepository.findAll(pageable);

}

**Controller code :**

@GetMapping("/tasks-list")

**public** String listTasks(@RequestParam(name = "page", defaultValue = "0") **int** page,

@RequestParam(name = "size", defaultValue = "6") **int** size,

Model model) {

Page<Tasks> tasksPage = taskserviceImpl.alltasks(PageRequest.of(page, size));

model.addAttribute("tasks", tasksPage.getContent());

model.addAttribute("currentPage", page);

model.addAttribute("totalPages", tasksPage.getTotalPages());

**return** "task-list"; // Return the JSP page

}

**Jsp page code :**

<!-- Pagination -->

<div class="d-flex justify-content-between">

<c:if test="${currentPage > 0}">

<a href="tasks-list?page=${currentPage - 1}&size=6" class="btn btn-secondary btn-sm">Previous</a>

</c:if>

<span>Page ${currentPage + 1} of ${totalPages}</span>

<c:if test="${currentPage + 1 < totalPages}">

<a href="tasks-list?page=${currentPage + 1}&size=6" class="btn btn-secondary btn-sm">Next</a>

</c:if>

</div>

## **What is Lazy and Eager loading?**

|  |  |
| --- | --- |
| Type | Description |
| **Lazy Loading** | Loads data **only when needed** (default for @OneToMany, @ManyToOne).  @OneToMany(fetch = FetchType.LAZY) |
| **Eager Loading** | Loads data **immediately** along with parent entity.  @OneToMany(fetch = FetchType.EAGER) |

### **What is the purpose of** @Modifying **in Spring Data JPA?**

Used for **update or delete queries** in native SQL.

@Modifying

@Query("UPDATE Employee e SET e.salary = :salary WHERE e.id = :id")

void updateSalary(@Param("salary") Double salary, @Param("id") Long id);

### **How do you handle transactions in Spring Data JPA?**

Use @Transactional.

@Transactional

public void updateEmployee(Long id, String name) {

Employee emp = repository.findById(id).orElseThrow();

emp.setName(name);

repository.save(emp);

}

## **What is the difference between** @Transactional **at method vs class level?**

* **At Method Level**: Affects only that method.
* **At Class Level**: Affects all methods inside the class.

@Service

@Transactional // Applied to all methods

public class EmployeeService {

public void updateEmployee() { } // Runs inside a transaction

}

### **How does Spring Data JPA handle caching?**

Spring Data JPA integrates with **Hibernate's First-Level and Second-Level cache**.

* **First-Level Cache:** Default and enabled per session.
* **Second-Level Cache:** Enabled using **EhCache, Hazelcast, Redis**.

### **What happens if you don't annotate a JPA entity with** @Id**?**

Hibernate **throws an exception** because every entity requires a primary key.

How to roll back a transaction in Spring Data JPA?

@Transactional(rollbackFor = Exception.class)

## **Pagination in Spring Data JPA**

## **What is Pagination?**

Pagination allows you to **fetch data in smaller chunks (pages)** instead of retrieving all records at once, improving performance.

### **Steps for Pagination in Spring Data JPA**

1. Use **Spring’s Pageable interface** to request specific pages.
2. Use **Spring’s Page or Slice interface** to receive paginated results.
3. Call a repository method that **returns Page<T>**.

## **🔹 Example: Implementing Pagination**

### **Entity Class (**Product**)**

**public** **class** Product {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

**private** Long id;

**private** String title;

**private** Double price;}

### **Repository Interface (**ProductRepository **)**

**public** **interface** ProductRepository **extends** JpaRepository<Product, Integer>

### **Service Layer: Using Pagination**

**public** Page<Product> getAllProducts(**int** pageNo, **int** pageSize) {

Pageable pageable = PageRequest.of(pageNo, pageSize);

Page<Product> pageList = productRepository.findAll(pageable);

**return** pageList;

}

**Explanation of PageRequest.of(page, size):**

|  |  |
| --- | --- |
| Parameter | Description |
| page | Zero-based index of the page to retrieve. |
| size | Number of records per page. |

### **Controller Layer: Handling Pagination Requests**

@GetMapping("/products")

**public** Page<Product> getMethodName(@RequestParam(defaultValue = "0") **int** pageNo,

@RequestParam(defaultValue = "3") **int** pageSize) {

**return** productService.getAllProducts(pageNo, pageSize);

}

### **Example Request and Response**

**Request URL:**

http://localhost:8485/products?pageNo=2&pageSize=2

**Response (PageNumber-2 , 2 products per page):**

{

    "content": [

        {

            "id": 5,

            "title": "Chanel Coco Noir Eau De",

            "price": 129.99

        },

        {

            "id": 6,

            "title": "Dior J'adore",

            "price": 89.99

        }

    ],

    "pageable": {

        "pageNumber": 2,

        "pageSize": 2,

        "sort": {

            "empty": **true**,

            "sorted": **false**,

            "unsorted": **true**

        },

        "offset": 4,

        "paged": **true**,

        "unpaged": **false**

    },

    "last": **false**,

    "totalPages": 50,

    "totalElements": 100,

    "size": 2,

    "number": 2,

    "sort": {

        "empty": **true**,

        "sorted": **false**,

        "unsorted": **true**

    },

    "first": **false**,

    "numberOfElements": 2,

    "empty": **false**

}

## **Pagination Methods in** Page **Interface**

|  |  |
| --- | --- |
| Method | Description |
| getContent() | Retrieves the current page content as a List<T>. |
| getTotalPages() | Returns the total number of pages available. |
| getTotalElements() | Returns the total number of records. |
| getSize() | Returns the number of elements per page. |
| getNumber() | Returns the **current** page index. |
| hasNext() | Returns true if the next page exists. |
| hasPrevious() | Returns true if a previous page exists. |

# **Sorting in Spring Data JPA**

## **What is Sorting?**

Sorting allows us to **order database records based on specific fields**.

### **Sorting Methods in Spring Data JPA**

There are **three ways** to perform sorting:

1. **Using Sort Parameter in Repository Method**
2. **Using PageRequest for Sorting & Pagination**
3. **Using @Query Annotation for Custom Sorting**

## **Sorting using** Sort **Parameter**

**Service Method**

// sort product using sort method

**public** List<Product> sortedProducts(){

**return** productRepository.findAll(Sort.by("price").descending());

}

**Controller Method**

// sort by sort method

@GetMapping("sortbyprice")

**public** ResponseEntity<List<Product>> getsortedProductByPrice(){

List<Product>listsorted=productService.sortedProducts();

**return** ResponseEntity.ok(listsorted);

}

**Example Request:**

http://localhost:8483/sortbyprice

## **Sorting with Pagination (**PageRequest**)**

**Controller Method:**

@GetMapping("productedsortedandpagination")

**public** ResponseEntity<Page<Product>> getPaginatedAndSortedProducts(@RequestParam(defaultValue = "0") **int** pageNumber,

@RequestParam(defaultValue = "3") **int** pageSize, @RequestParam(defaultValue = "price") String sortBy,

@RequestParam(defaultValue = "asc") String sortDirection) {

// Validate Page Number and Size

**if** (pageNumber < 0) {

**return** ResponseEntity.badRequest().body(**null**);

}

**if** (pageSize <= 0) {

**return** ResponseEntity.badRequest().body(**null**);

}

Page<Product> productPage = productService.pageAndSortProducts(pageNumber, pageSize, sortBy, sortDirection);

logger.info("Returning {} products for page {} with sorting by {} ({})", productPage.getNumberOfElements(),

pageNumber, sortBy, sortDirection);

**return** ResponseEntity.ok(productPage);

}

Service Method :

**public** Page<Product> pageAndSortProducts(**int** pageNumber, **int** pageSize, String sortBy, String sortDirection) {

Sort sort = sortDirection.equalsIgnoreCase("asc") ? Sort.by(sortBy).ascending() : Sort.by(sortBy).descending();

Pageable pageable = PageRequest.of(pageNumber, pageSize, sort);

**return** productRepository.findAll(pageable);

}

Here, **sorting and pagination are combined**.

url : http://localhost:8483/productedsortedandpagination?pageNumber=0&pageSize=10&sortBy=title&sortDirection=asc

## **Custom Sorting with** @Query **Annotation**

@Query("SELECT e FROM Employee e WHERE e.department = :department ORDER BY e.name DESC")

List<Employee> findEmployeesSorted(@Param("department") String department);

## **🔹 Sorting Methods in** Sort **Interface**

|  |  |
| --- | --- |
| Method | Description |
| Sort.by("name").ascending() | Sorts by name in **ascending** order. |
| Sort.by("salary").descending() | Sorts by salary in **descending** order. |
| Sort.by("name", "salary") | Sorts by name first, then salary. |

# **Combining Pagination & Sorting**

You can combine both as shown below:

### **📌 Example Service Method**

public Page<Employee> getEmployees(String department, int page, int size, String sortBy, String sortDir) {

Sort sort = sortDir.equalsIgnoreCase("asc") ? Sort.by(sortBy).ascending() : Sort.by(sortBy).descending();

Pageable pageable = PageRequest.of(page, size, sort);

return employeeRepository.findByDepartment(department, pageable);

}

### **📌 Example Controller**

@GetMapping("/employees")

public Page<Employee> getEmployees(

@RequestParam String department,

@RequestParam(defaultValue = "0") int page,

@RequestParam(defaultValue = "5") int size,

@RequestParam(defaultValue = "name") String sortBy,

@RequestParam(defaultValue = "asc") String sortDir) {

return employeeService.getEmployees(department, page, size, sortBy, sortDir);

}

### **📌 Example Request**

GET http://localhost:8080/employees?department=IT&page=0&size=3&sortBy=name&sortDir=desc

# **🔹 Summary**

|  |  |  |
| --- | --- | --- |
| Feature | Pagination | Sorting |
| Purpose | Fetch limited records per page | Order records in ascending/descending order |
| Interface | Pageable, Page<T> | Sort |
| Repository Support | Page<T> findAll(Pageable p) | List<T> findAll(Sort s) |
| Methods Used | PageRequest.of(page, size) | Sort.by("column").ascending() |
| Query Type | JPQL, Native, Derived | JPQL, Native, Derived |
