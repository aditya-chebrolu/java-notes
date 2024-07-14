Sure, here are the notes formatted in Markdown:

# Java Streams

Java Streams are a powerful feature introduced in Java 8 as part of the java.util.stream package. They allow you to perform bulk operations on collections of data in a declarative manner. Streams can be used for both sequential and parallel operations.

## Key Concepts

- **Stream**: A sequence of elements supporting sequential and parallel aggregate operations.
- **Intermediate Operations**: Transformations on a stream that return another stream. These operations are lazy, meaning they are not executed until a terminal operation is invoked.
- **Terminal Operations**: Operations that produce a result or a side-effect and mark the end of the stream processing.

## Stream Creation

Streams can be created from various sources:

```java
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();

Stream<String> streamOfArray = Stream.of("a", "b", "c");

IntStream intStream = IntStream.range(1, 10);

Stream<String> streamGenerated = Stream.generate(() -> "element").limit(10);
```

## Intermediate Operations

These operations are lazy and are not executed until a terminal operation is invoked.

1. **filter(Predicate<? super T> predicate)**
   ```java
   List<String> result = list.stream()
                             .filter(s -> s.startsWith("a"))
                             .collect(Collectors.toList());
   ```

2. **map(Function<? super T, ? extends R> mapper)**
   ```java
   List<Integer> lengths = list.stream()
                               .map(String::length)
                               .collect(Collectors.toList());
   ```

3. **flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)**
   ```java
   List<String> flatMapped = listOfLists.stream()
                                        .flatMap(Collection::stream)
                                        .collect(Collectors.toList());
   ```

4. **distinct()**
   ```java
   List<String> distinct = list.stream()
                               .distinct()
                               .collect(Collectors.toList());
   ```

5. **sorted()**
   ```java
   List<String> sorted = list.stream()
                             .sorted()
                             .collect(Collectors.toList());
   ```

6. **sorted(Comparator<? super T> comparator)**
   ```java
   List<String> sortedByLength = list.stream()
                                     .sorted(Comparator.comparing(String::length))
                                     .collect(Collectors.toList());
   ```

7. **peek(Consumer<? super T> action)**
   ```java
   List<String> peeked = list.stream()
                             .peek(System.out::println)
                             .collect(Collectors.toList());
   ```

8. **limit(long maxSize)**
   ```java
   List<String> limited = list.stream()
                              .limit(2)
                              .collect(Collectors.toList());
   ```

9. **skip(long n)**
   ```java
   List<String> skipped = list.stream()
                              .skip(2)
                              .collect(Collectors.toList());
   ```

## Terminal Operations

These operations produce a result or a side-effect.

1. **forEach(Consumer<? super T> action)**
   ```java
   list.stream().forEach(System.out::println);
   ```

2. **collect(Collector<? super T, A, R> collector)**
   ```java
   List<String> collected = list.stream()
                                .collect(Collectors.toList());
   ```

3. **toArray()**
   ```java
   String[] array = list.stream()
                        .toArray(String[]::new);
   ```

4. **reduce(BinaryOperator<T> accumulator)**
   ```java
   Optional<String> reduced = list.stream()
                                  .reduce((s1, s2) -> s1 + s2);
   ```

5. **reduce(T identity, BinaryOperator<T> accumulator)**
   ```java
   String concatenated = list.stream()
                             .reduce("", (s1, s2) -> s1 + s2);
   ```

6. **reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)**
   ```java
   int sum = numbers.stream()
                    .reduce(0, Integer::sum, Integer::sum);
   ```

7. **findFirst()**
   ```java
   Optional<String> first = list.stream()
                                .findFirst();
   ```

8. **findAny()**
   ```java
   Optional<String> any = list.stream()
                              .findAny();
   ```

9. **count()**
   ```java
   long count = list.stream()
                    .count();
   ```

10. **anyMatch(Predicate<? super T> predicate)**
    ```java
    boolean anyMatch = list.stream()
                           .anyMatch(s -> s.startsWith("a"));
    ```

11. **allMatch(Predicate<? super T> predicate)**
    ```java
    boolean allMatch = list.stream()
                           .allMatch(s -> s.startsWith("a"));
    ```

12. **noneMatch(Predicate<? super T> predicate)**
    ```java
    boolean noneMatch = list.stream()
                            .noneMatch(s -> s.startsWith("z"));
    ```

## Specialized Streams

Java also provides specialized streams for primitive types:
- **IntStream**
- **LongStream**
- **DoubleStream**

These streams have additional methods such as:
- `sum()`
- `average()`
- `max()`
- `min()`

## Example Usage

Here's a comprehensive example using various stream operations:

```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "date", "elderberry", "fig", "grape");

List<String> result = words.stream()
    .filter(word -> word.length() > 4)
    .map(String::toUpperCase)
    .sorted()
    .peek(System.out::println)
    .collect(Collectors.toList());
```

In this example:
- `filter` filters words with length greater than 4.
- `map` converts each word to uppercase.
- `sorted` sorts the words.
- `peek` prints each word.
- `collect` collects the result into a list.

## Lazy Evaluation

Lazy evaluation means that the operations are not performed when they are encountered. Instead, they are deferred until a result is actually needed. This allows for optimization, as the system can batch and streamline the operations to be more efficient.

### Intermediate Operations

Intermediate operations, such as `filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`, `limit`, and `skip`, are all lazy. This means when you call these methods, you are defining a pipeline of operations to be performed on the stream, but no actual data processing occurs at that point.

### Terminal Operations

Terminal operations, such as `forEach`, `collect`, `reduce`, `toArray`, `count`, `findFirst`, `findAny`, `anyMatch`, `allMatch`, and `noneMatch`, trigger the actual data processing. When a terminal operation is invoked, the entire pipeline of intermediate operations is executed.

### Example

Consider the following example:

```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "date", "elderberry", "fig", "grape");

Stream<String> stream = words.stream()
    .filter(word -> {
        System.out.println("filter: " + word);
        return word.length() > 4;
    })
    .map(word -> {
        System.out.println("map: " + word);
        return word.toUpperCase();
    });

System.out.println("Stream defined, but nothing executed yet.");

List<String> result = stream.collect(Collectors.toList());

System.out.println("Result: " + result);
```

### Explanation

1. **Stream Definition**: 
   - When the stream is defined with `filter` and `map`, no operations are executed. The `filter` and `map` methods only set up the processing pipeline.
   - You will see the message "Stream defined, but nothing executed yet." printed, indicating that the stream operations have not been executed.

2. **Terminal Operation (`collect`)**:
   - When `collect` is called, the entire stream pipeline is executed.
   - The `filter` and `map` methods are applied to each element in the list, and their corresponding print statements will be executed.
   - Finally, the resulting list is collected.

### Output

```
Stream defined, but nothing executed yet.
filter: apple
map: apple
filter: banana
map: banana
filter: cherry
map: cherry
filter: elderberry
map: elderberry
filter: grape
map: grape
Result: [APPLE, BANANA, CHERRY, ELDERBERRY, GRAPE]
```

### Summary

- **Intermediate Operations**: Set up the pipeline but do not execute.
- **Terminal Operation**: Triggers the execution of the pipeline, causing all the intermediate operations to process the data.

Lazy evaluation ensures efficiency by avoiding unnecessary operations and allows for optimizations like short-circuiting and merging steps, which can significantly improve performance, especially with large datasets.
