# Java `Optional` Methods

## `get` Method
Returns the value if present, otherwise throws `NoSuchElementException`.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
String value = optional.get(); // Hello
```

## `orElse` Method
Returns the value if present, otherwise returns the provided default value.

**Example:**
```java
Optional<String> optional = Optional.ofNullable(null);
String value = optional.orElse("Default Value"); // Default Value
```

## `orElseThrow` Method
Returns the value if present, otherwise throws an exception.

**Example:**
```java
Optional<String> optional = Optional.ofNullable(null);
String value = optional.orElseThrow(() -> new IllegalArgumentException("Value not present"));
```

## `orElseGet` Method
Returns the value if present, otherwise invokes the provided `Supplier`.

**Example:**
```java
Optional<String> optional = Optional.ofNullable(null);
String value = optional.orElseGet(() -> "Computed Default Value"); // Computed Default Value
```

## `isPresent` Method
Returns `true` if a value is present, otherwise `false`.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
if (optional.isPresent()) {
    System.out.println(optional.get()); // Hello
}
```

## `ifPresent` Method
Performs the given action if a value is present.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
optional.ifPresent(value -> System.out.println(value)); // Hello
```

## `filter` Method
Returns an `Optional` describing the value if it matches the given predicate, otherwise returns an empty `Optional`.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
Optional<String> filtered = optional.filter(value -> value.startsWith("H"));
System.out.println(filtered.isPresent()); // true
```

## `map` Method
Applies the given `Function` to the value if present and returns an `Optional` describing the result.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
Optional<Integer> mapped = optional.map(String::length);
System.out.println(mapped.get()); // 5
```

## `flatMap` Method
Similar to `map`, but the function must return an `Optional`.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
Optional<Integer> flatMapped = optional.flatMap(value -> Optional.of(value.length()));
System.out.println(flatMapped.get()); // 5
```

## `empty` Method
Returns an empty `Optional`.

**Example:**
```java
Optional<String> emptyOptional = Optional.empty();
System.out.println(emptyOptional.isPresent()); // false
```

## `of` Method
Returns an `Optional` with the specified present non-null value.

**Example:**
```java
Optional<String> optional = Optional.of("Hello");
System.out.println(optional.isPresent()); // true
```

## `ofNullable` Method
Returns an `Optional` describing the specified value, if non-null, otherwise returns an empty `Optional`.

**Example:**
```java
Optional<String> optional = Optional.ofNullable(null);
System.out.println(optional.isPresent()); // false
```
