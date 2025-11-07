1. **Why JAVA 8 ? Main agenda behind JAVA 8 ?**

* The reason for introducing java 8 was to introduce Conciseness in the code.
* JAVA 8 brings in functional programming which is enabled by Lamda Expression ( a powerful tool to create concise code base ).

1. **What are the features of JAVA 8 ?**

* Java 8 Features :
  + Lamda Expression
  + Stream API
  + Default methods in Interface
  + Static methods in Interface
  + Functional Interface
  + Optional Class
  + Method References
  + Date API
  + String Joiner
  + Nashron, JavaScript Engine

1. **What are the main advantages of JAVA 8 ?**

* Compact code ( Less Boiler Plate Code ).
* More Readable & Reusable Code.
* More Testable Code.
* Parallel Operations.

1. **What is Functional Interfaces ?**

* Functional interfaces are those interfaces which can have only one abstract method.
* It can have any number of static methods & default methods. No restriction on that.
* There are many functional interfaces already present in java such as :
  + Comparable : compareTo();
  + Runnable : run();
  + Callable : call();
  + Comparator : compare();
* Functional interfaces is also known as Single Abstract Method Interfaces or SAM interfaces.

1. **What is Lamda Expression ?**

* Lamda Expression is an anonymous function ( without name, return type and access modifier and having one lamda -> symbol.
* Example :
  + Normal Programming Language

public void add ( int a, int b ) {

System.out.println( a + b );

}

* Equivalent Lamda Expression

( a, b ) -> System.out.println( a + b );

1. **What is Predicate, Consumer & Supplier ?**

* **Predicate :**
  + This interface is used for conditional check.
  + We can use it where the return type should be boolean.
  + It has boolean test(T t); method.
* **Consumer** :
  + Consumer<T> is an in-built functional interface.
  + We can use it when we have to take input and perform some operations without returning any result.
  + It has void accept(T t); method.
* **Supplier :**
  + Supplier can be used in all contexts where there is no input but an output is expected.
  + It has get(); method.

1. **Default methods in Interface ?**

* Java provides a facility to create default methods inside the interface.
* Methods which are defined inside the interface and tagged with default are known as default methods.
* The methods are non-abstract methods.
* **Need of default methods :**
  + Suppose one interface has one or multiple implementation classes, if one or more methods are added to the interface, all the implementation classes will be forced to implement them too. Otherwise, the design will just break down.
  + Default methods are an efficient way to deal with this issue.
  + They allow us to add new methods to an interface that are automatically available in the all implementation classes. Therefore, we don't need to modify the implementing classes.
* Default methods can be override.

1. **Static methods in Interface ?**

* Java provides a facility to create static methods inside the interface.
* It provides the common functionality.

1. **Explain forEach() ?**

* The Java forEach() method is a utility function to iterate over a collection such as(list, set or map) and stream.
* It is used to perform a given action on each the element of the collection.

1. **What is Optional Class ?**

* Optional class is introduced in java 8.
* **Need of Optional Class :**
  + There are scenarios where the value is present or not present it can be null, in this case it’s tricky to write lot of checks, and those checks are not readable so that is the reason the optional was introduced.
* Optional can handle the scenario if the value is present or not present.

1. **We have to print default value if the value is null using optional ?**

* So in this case we can use orElse method and we can pass the value and assign it to a string variable and print it.

1. **Explain String Joiner ?**

* Java added a new final class StringJoiner in java.util package.
* To construct an instance of StringJoiner, we need to mention the delimiter. Optionally, we can also specify the prefix and suffix that should be present in the result:

1. **What is Method Reference ?**

Java added a new final cl

1. **What is Stream API ?**

* Stream API concept is present inside the java util package.
* It is used for processing the collection objects.
* There are some predefine methods present in the stream api.

filter(), map(), forEach(),

collect(), count(), distinct(),

sorted(), toArray(), flatMap(),

reduce()

1. **Methods ofStream API ?**

* **Methods of Stream :**
  + **sorted() :**
    - Sorts according to the natural order.
  + **anyMatch() :**
    - It returns true if any element matches the predicate.
    - If the stream is empty then returns false & predicate not evaluated.
  + **allMatch() :**
    - It returns true if all element matches the predicate.
    - If the stream is empty then returns true & predicate not evaluated.
  + **findFirst() :**
    - It returns the optional describing the first element.
    - Returns empty Optional if the stream is empty.
  + **distinct() :**
    - It means that the element occurring first will be present in the distinct elements stream.
  + **count() :**
    - It returns the count of elements in the stream.
    - Return type is long.
  + **limit() :**
    - Sets the limit for elements.
  + **min() :**
    - It returns the minimum element of this stream according to the provided Comparator.
  + **max() :**
    - It returns the maximum element of this stream according to the provided Comparator.
  + **reduce() :**
    - Reducing is the repeated process of combining all elements.
  + **toArray() :**
    - It returns an array containing the elements of this stream.
  + **filter() :**
    - Using filter we can filter the data based on condition.
  + **map() :**
    - Using map we can perform operations on each element.
  + **flatMap() :**
    - If we have complex data in our collection then we can go for flatmap.
  + **parallelStream() :**
    - Parallel streams used a multiple thread to process their pipeline.

1. **Sequential Stream & Parallel Stream difference ?**

|  |  |
| --- | --- |
| **Sequential Stream** | **Parallel Stream** |
| Sequential streams used a single thread to process their pipeline. | Parallel streams used a multiple thread to process their pipeline. |
| It runs on the single core of the computer | It utilizes multiple core of the computer |
| The performance is faster / high. | The performance is slower / low. |
| Order is maintained | Order is not maintained |

1. **map() & Parallel faltMap() difference ?**

|  |  |
| --- | --- |
| **map()** | **flatMap()** |
| It does only mapping. | It performs mapping as well as flattening |
| It is one-to-one mapping. | It is one-to-many mapping. |
| Produces a stream of value. | Produces a stream of stream value. |
| Use this method when map is producing single value for each input value. | Use this method when map is producing multiple values for each input value. |
| Using map() we are adding 2 lists, so the output will be list containing lists.  [1, 2], [3, 4] -> [ [1, 2], [3, 4] ] | Using flatMap() we are adding 2 lists, so the output will be list containing elements.  [1, 2], [3, 4] -> [ 1, 2, 3, 4 ] |
