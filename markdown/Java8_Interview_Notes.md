# ☕ Java 8 Interview Notes

---

## 🧠 1. Why Java 8? What is the Main Agenda Behind Java 8?

- The main reason for introducing **Java 8** was to bring **conciseness** in code.
- It introduced **Functional Programming** through **Lambda Expressions**, enabling shorter and more expressive code.

---

## 🚀 2. Features of Java 8

- Lambda Expressions  
- Stream API  
- Default Methods in Interfaces  
- Static Methods in Interfaces  
- Functional Interfaces  
- Optional Class  
- Method References  
- New Date & Time API  
- StringJoiner  
- Nashorn JavaScript Engine  

---

## ⚙️ 3. Advantages of Java 8

- Compact code (less boilerplate)  
- More readable and reusable code  
- Easier testing  
- Supports **parallel operations**

---

## 🧩 4. Functional Interfaces

- An interface with **only one abstract method**.
- Can contain **any number of static or default methods**.
- Also known as **SAM Interfaces (Single Abstract Method)**.

**Examples:**
- `Comparable` → `compareTo()`
- `Runnable` → `run()`
- `Callable` → `call()`
- `Comparator` → `compare()`

---

## 🔹 5. Lambda Expression

- A **lambda expression** is an **anonymous function** (no name, return type, or access modifier) using the `->` symbol.

**Example:**

**Normal method:**
```java
public void add(int a, int b) {
    System.out.println(a + b);
}
```

**Equivalent Lambda Expression:**
```java
(a, b) -> System.out.println(a + b);
```

---

## 🎯 6. Predicate, Consumer & Supplier

| Interface | Purpose | Method | Description |
|:-----------|:---------|:--------|:-------------|
| **Predicate<T>** | Used for conditional checks | `boolean test(T t)` | Returns true/false |
| **Consumer<T>** | Takes input, performs operation, no result | `void accept(T t)` | Performs side-effect action |
| **Supplier<T>** | No input, returns output | `T get()` | Produces a value |

---

## 🧱 7. Default Methods in Interface

- Declared with the `default` keyword.
- Provides **method implementation** inside an interface.
- **Use case:** When adding new methods to interfaces without breaking existing implementations.

**Can be overridden** by implementing classes.

---

## ⚡ 8. Static Methods in Interface

- Declared with the `static` keyword.
- Provides **common functionality**.
- Can be accessed using `InterfaceName.methodName()`.

---

## 🔁 9. forEach()

- Used to **iterate collections (List, Set, Map)** or **Streams**.
- Performs an action on each element.

**Example:**
```java
list.forEach(item -> System.out.println(item));
```

---

## 🎁 10. Optional Class

- Introduced to **avoid null pointer exceptions**.
- Used when a value **might or might not be present**.

**Example:**
```java
Optional<String> name = Optional.ofNullable(null);
System.out.println(name.orElse("Default Value"));
```

---

## 🧵 11. StringJoiner

- A new utility class in `java.util` package to join strings with **delimiter**, **prefix**, and **suffix**.

**Example:**
```java
StringJoiner joiner = new StringJoiner(", ", "[", "]");
joiner.add("Java").add("Spring").add("Hibernate");
System.out.println(joiner); // [Java, Spring, Hibernate]
```

---

## 🔗 12. Method Reference

- Provides a way to refer to a method without executing it.
- Uses `::` operator.

**Example:**
```java
list.forEach(System.out::println);
```

---

## 🌊 13. Stream API

- Introduced in `java.util.stream` package.
- Used for **processing collections** efficiently using functional style.

**Common Stream Methods:**
`filter()`, `map()`, `flatMap()`, `collect()`, `count()`, `distinct()`, `sorted()`,  
`toArray()`, `reduce()`, `forEach()`, `limit()`, `min()`, `max()`, `anyMatch()`, `allMatch()`,  
`findFirst()`, `parallelStream()`

---

## ⚒️ 14. Important Stream Methods

| Method | Description |
|:--------|:-------------|
| **sorted()** | Sorts elements in natural order |
| **anyMatch()** | Returns true if any element matches the predicate |
| **allMatch()** | Returns true if all elements match the predicate |
| **findFirst()** | Returns the first element as Optional |
| **distinct()** | Removes duplicate elements |
| **count()** | Returns the total count of elements |
| **limit(n)** | Limits the number of elements in the stream |
| **min()/max()** | Returns min/max element based on comparator |
| **reduce()** | Combines elements repeatedly |
| **toArray()** | Converts stream to array |
| **filter()** | Filters data based on condition |
| **map()** | Performs operation on each element |
| **flatMap()** | Flattens nested collections |
| **parallelStream()** | Executes stream using multiple threads |

---

## ⚖️ 15. Sequential Stream vs Parallel Stream

| Feature | **Sequential Stream** | **Parallel Stream** |
|:----------|:----------------------|:---------------------|
| **Execution** | Single thread | Multiple threads |
| **Core usage** | Single core | Multiple cores |
| **Performance** | Slower for large data | Faster for large data |
| **Order** | Maintains order | Order not guaranteed |

---

## 🧩 16. map() vs flatMap()

| Feature | **map()** | **flatMap()** |
|:----------|:-----------|:---------------|
| **Operation** | Only mapping | Mapping + Flattening |
| **Mapping Type** | One-to-One | One-to-Many |
| **Output** | Stream of values | Stream of flattened values |
| **Use Case** | When each input → single output | When each input → multiple outputs |
| **Example** | `[ [1, 2], [3, 4] ] → [ [1, 2], [3, 4] ]` | `[ [1, 2], [3, 4] ] → [1, 2, 3, 4]` |

---

✅ **Summary:**
- **Java 8 = Functional + Concise + Streamlined**
- Focuses on **clean**, **parallel**, and **efficient** code.
