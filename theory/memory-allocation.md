# Java Heap Space vs Stack - Memory Allocation in Java

## Heap

- Java heap space is used by Java runtime to allocate memory to objects and JRE classes (Java Runtime Environment).
- **Whenever we create an object, it is always created on Heap space.**
- Garbage collection runs on heap memory to free up the space used by objects without any reference.
- Any object created on heap space has global access and can be referenced from anywhere in the application.

## Stack

- Used for execution of threads.
- Contains method-specific values that are short-lived and references to other objects on the heap that is getting referenced from the method.
- **Whenever a method is invoked, a new block is created on stack memory to hold local primitive values and references to other objects in the method.**
