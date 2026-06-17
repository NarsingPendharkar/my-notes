# 🧠 Linked List Data Structure (DSA)

---

### What is a Linked List?

- A **linked list** is a way to store data in a series of connected nodes.
- Each **node** contains:
  - **Data**: The value or information it holds.
  - A **pointer** (or link) to the **next node** in the list.
- Unlike arrays, linked lists do **not** store data in continuous memory locations.

### Types of Linked Lists

1. **Singly Linked List**

  - Each node points to the **next** node only.
  - The last node points to **null** (no next node).
  - You can only move forward through the list.

2. **Doubly Linked List**

  - Each node has **two pointers**:
    - One to the **next** node.
    - One to the **previous** node.
  - You can move both forward and backward.

3. **Circular Linked List**

  - The last node points back to the **first** node.
  - Can be singly or doubly linked.  

### Why Use Linked Lists?

- **Dynamic size**: You don't need to know the number of items before creating the list.
- **Easy insertion and deletion**: Adding or removing nodes doesn’t require shifting other elements (like in arrays).
- Useful when you want to frequently add or remove data.

### How Does a Linked List Work?

- Start with a **head** pointer that points to the first node in the list.
- Each node stores data and the address of the next node.
- To access any node, you start from the head and follow the pointers one by one.

---

**Structure of a Node**

Each node has two parts:

1. **Data** – Stores the actual value.
2. **Next Pointer/Reference** – Stores the address of the next node.

```mermaid
flowchart LR
    A[Head Pointer] --> B[Node 1<br/>Data + Next]
    B --> C[Node 2<br/>Data + Next]
    C --> D[Node 3<br/>Data + NULL]
```

---

**🔗 Linked List Representation**

```mermaid
flowchart LR
    Head --> N1["Node 1<br>Data: 10<br>Next"]
    N1 --> N2["Node 2<br>Data: 20<br>Next"]
    N2 --> N3["Node 3<br>Data: 30<br>Next: NULL"]
```

---

### 📌 Why Linked List?

Arrays have some limitations:

| Array | Linked List |
|---|---|
| Fixed size | Dynamic size |
| Continuous memory required | Non-continuous memory |
| Fast random access | Sequential access |
| Insertion/deletion costly | Easy insertion/deletion |
| Wastes memory when size is unknown | Grows as needed |

---

### Types of Linked Lists

#### 1. Singly Linked List

Each node points only to the next node.

```text
10 → 20 → 30 → NULL
```

---

#### 2. Doubly Linked List

Each node has two references:

- Previous node
- Next node

```text
NULL ← 10 ⇄ 20 ⇄ 30 → NULL
```

---

#### 3. Circular Linked List

The last node points back to the first node.

```text
       +----------------+
       |                |
       v                |
10 → 20 → 30 → 40 ------+
```

---

##### Node Implementation in Java

```java
class Node {

    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

---

### Singly Linked List Operations

#### 1. Traversal

Visit every node from head until `NULL`.

```mermaid
flowchart LR

A[Start at Head]
--> B{Current Node Exists?}

B -->|Yes| C[Process Data]
C --> D[Move to Next Node]
D --> B

B -->|No| E[Stop]
```

```java
public void display() {

    Node temp = head;

    while(temp != null) {
        System.out.print(temp.data + " -> ");
        temp = temp.next;
    }

    System.out.println("NULL");
}
```

---

#### 2. Insert at Beginning

Before:

```text
10 → 20 → 30 → NULL
```

Insert `5`

After:

```text
5 → 10 → 20 → 30 → NULL
```

**Algorithm**

1. Create a new node.
2. Make new node point to current head.
3. Update head to new node.



```mermaid
flowchart TD

A[Create New Node]
--> B[NewNode.next = Head]
--> C[Head = NewNode]
--> D[Insertion Complete]
```



```java
public void insertFirst(int data) {

    Node node = new Node(data);

    node.next = head;

    head = node;
}
```

---

#### 3. Insert at End

```mermaid
flowchart TD

A[Create New Node]
--> B{Is Head NULL?}

B -->|Yes| C[Head = New Node]

B -->|No| D[Traverse Until Last Node]
D --> E[Last.next = New Node]
```



```java
public void insertLast(int data) {

    Node node = new Node(data);

    if(head == null) {
        head = node;
        return;
    }

    Node temp = head;

    while(temp.next != null) {
        temp = temp.next;
    }

    temp.next = node;
}
```

---

#### 4. Delete First Node

Logic : Simply move the head to the next node.

```text
Before:
10 → 20 → 30

Head = head.next

After:
20 → 30
```

```java
public void deleteFirst() {

    if(head == null)
        return;

    head = head.next;
}
```

---

#### 5. Delete Last Node



```mermaid
flowchart TD

A[Start from Head]
--> B[Move until second last node]
--> C[SecondLast.next = NULL]
```



```java
public void deleteLast() {

    if(head == null || head.next == null) {
        head = null;
        return;
    }

    Node temp = head;

    while(temp.next.next != null) {
        temp = temp.next;
    }

    temp.next = null;
}
```

---

#### 6. Searching

**Linear Search :** Linked List does not support binary search because random access is not possible.

```java
public boolean search(int value) {

    Node temp = head;

    while(temp != null) {

        if(temp.data == value) {
            return true;
        }

        temp = temp.next;
    }

    return false;
}
```

---

#### 7. Find Size of Linked List

```java
public int size() {

    int count = 0;

    Node temp = head;

    while(temp != null) {

        count++;
        temp = temp.next;
    }

    return count;
}
```

---

---

### Time Complexity Table

| Operation | Complexity |
|---|---|
| Access nth element | O(n) |
| Search | O(n) |
| Insert at beginning | O(1) |
| Insert at end | O(n) |
| Delete beginning | O(1) |
| Delete end | O(n) |
| Reverse | O(n) |
| Find middle | O(n) |
| Detect cycle | O(n) |

---

### Array vs Linked List

| Feature | Array | Linked List |
|---|---|---|
| Memory | Continuous | Non-continuous |
| Size | Fixed | Dynamic |
| Access | O(1) | O(n) |
| Insert/Delete at beginning | O(n) | O(1) |
| Cache Performance | Better | Lower |
| Extra Memory | No | Pointer required |

---

# Stack Data Structure in Java

A **Stack** is a simple linear data structure that works on the **LIFO (Last In, First Out)** principle. This means the last item you add is the first one you get out. Imagine a stack of plates: you place new plates on top and take plates from the top.

---

### 1. Core Stack Operations & Performance

All stack implementations support a set of basic operations that usually run very fast, in constant time — that is, **O(1)** time complexity.


| Operation      | What it Does                                                | Time Complexity | Space Complexity |
| -------------- | ----------------------------------------------------------- | --------------- | ---------------- |
| `push(E item)` | Adds an item to the top of the stack                        | O(1)            | O(1)             |
| `pop()`        | Removes and returns the top item. Throws exception if empty | O(1)            | O(1)             |
| `peek()`       | Shows the top item without removing it                      | O(1)            | O(1)             |
| `isEmpty()`    | Checks if the stack is empty                                | O(1)            | O(1)             |
| `size()`       | Returns the number of items in the stack                    | O(1)            | O(1)             |


**Key points:**

- These operations are very fast and don’t depend on how big the stack is.
- `pop()` throws an error if you try to remove an item from an empty stack.  
- `peek()` lets you see the top element without changing the stack.

---

### 2. Java Stack Implementations: Modern vs Legacy

Java provides different classes to use stacks. It’s important to pick the right one:

##### Legacy: `java.util.Stack`

- Extends the `Vector` class.
- **Synchronized**: This means it is thread-safe but slower because of performance overhead.
- Not recommended for new code, especially if your program is single-threaded.
- It’s considered **legacy code** and best avoided in modern applications.

##### Modern: Using `Deque` with `ArrayDeque`

- `Deque` stands for Double-Ended Queue.
- `ArrayDeque` implements `Deque` with a resizable array.
- It is **not synchronized** and much faster than `Stack`.
- Recommended for use as a stack in modern Java code.

##### Example: Modern vs Legacy Stack Usage

```java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Stack;

public class JavaStackDemo {
    public static void main(String[] args) {
        // Modern recommended stack using ArrayDeque
        Deque<Integer> modernStack = new ArrayDeque<>();
        modernStack.push(10);
        modernStack.push(20);
        System.out.println("Modern Top: " + modernStack.peek()); // Prints 20
        System.out.println("Modern Pop: " + modernStack.pop());  // Removes and prints 20

        // Legacy stack (not recommended)
        Stack<Integer> legacyStack = new Stack<>();
        legacyStack.push(100);
        legacyStack.push(200);
        System.out.println("Legacy Top: " + legacyStack.peek()); // Prints 200
    }
}
```

**Summary:**

- Use `ArrayDeque` when you want a fast and simple stack.
- Avoid `Stack` unless working with legacy code or synchronization is needed.

---

#### 3. Custom Stack Implementation (Good for Interviews)

Many interviews ask you to build your own stack to show understanding of data structures and memory.

##### Option A: Fixed-Size Array Stack

This implementation uses a simple array and a variable (`top`) that keeps track of the stack’s top index.

##### Important Points:

- `top` starts at -1 to show the stack is empty.
- `push` adds an element on top and increments `top`.
- `pop` removes the element at `top` and decrements `top`.
- You must handle:
  - **Stack Overflow:** Trying to push when the stack is full.
  - **Stack Underflow:** Trying to pop when the stack is empty.

##### Partial Example Code:

```java
class ArrayStack {
    private int maxSize;
    private int[] stackArray;
    private int top;

    public ArrayStack(int size) {
        this.maxSize = size;
        this.stackArray = new int[maxSize];
        this.top = -1; // Stack is empty initially
    }

    public void push(int value) {
        if (top == maxSize - 1) {
            System.out.println("Stack Overflow! Cannot push " + value);
            return;
        }
        stackArray[++top] = value; // Add item and increase top
    }

    public int pop() {
        if (top == -1) {
            System.out.println("Stack Underflow! Cannot pop.");
            return -1; // or throw exception
        }
        return stackArray[top--]; // Return item and decrease top
    }

    public int peek() {
        if (top == -1) {
            System.out.println("Stack is empty.");
            return -1;
        }
        return stackArray[top]; // Show top item without removing
    }

    public boolean isEmpty() {
        return (top == -1);
    }

    public int size() {
        return top + 1;
    }
}
```

##### Why This Matters:

- Shows clear understanding of pointer/index management.
- Demonstrates handling edge cases like overflow and underflow.
- Builds foundational knowledge for linked list-based stacks or dynamic stacks.

---

## Summary of Key Learnings

- **Stack is LIFO:** last in, first out.
- All common stack operations (`push/pop/peek`) work in **O(1)** time.
- Use `**ArrayDeque**` with `Deque` interface for stacks in modern Java code — faster and not synchronized.
- Avoid old `Stack` class unless working with legacy or need synchronization.
- Practice building your own stack using arrays for interview success — understand boundaries and errors.
- Stack concepts apply widely in algorithms and applications like undo mechanisms, parsing, backtracking, and more.

---

