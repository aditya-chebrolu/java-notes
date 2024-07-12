# Java Heap Space vs Stack - Memory Allocation in Java

## Heap

- Java heap space is used by the Java runtime to allocate memory to objects and JRE classes (Java Runtime Environment).
- **Whenever we create an object, it is always created on heap space.**
- Garbage collection runs on heap memory to free up the space used by objects without any references.
- Any object created on heap space has global access and can be referenced from anywhere in the application.

## Stack

- Used for execution of threads.
- Contains method-specific values that are short-lived, such as primitive data types, method calls, and references to objects on the heap that are accessed by the method.
- **Whenever a method is invoked, a new block (called a stack frame) is created on stack memory to hold local primitive values and references to other objects in the method.**
