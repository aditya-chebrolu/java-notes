# Method Local Inner Class (Important Points)

- The inner class is declared **inside a method**.
- You can instantiate the class only **inside the method** in which the class is present.
- Can access members outside of the inner class (i.e., of the method and outer class).

## Points to Remember

- **Local variables of the method:** The local inner class can access local variables of the method if they are marked as `final` or are effectively final.
- **Instantiation:** The class can only be instantiated within the method it is defined in.
- **Non-static:** The inner class cannot be static.
- **Accessing variables:** If the method has local variables with the same name as the instance variables of the outer class, the local variables will shadow the instance variables of the outer class.

### Code Examples

#### Example 1: Basic Method Local Inner Class

```java
public class OuterClass {
    public void outerMethod() {
        final int localVar = 10; // Must be final or effectively final

        // Method local inner class
        class InnerClass {
            public void display() {
                System.out.println("Local variable: " + localVar);
            }
        }

        // Instantiating the inner class inside the method
        InnerClass inner = new InnerClass();
        inner.display();
    }

    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```

#### Example 2: Accessing Outer Class Members

```java
public class OuterClass {
    private int instanceVar = 20;

    public void outerMethod() {
        final int localVar = 10; // Must be final or effectively final

        // Method local inner class
        class InnerClass {
            public void display() {
                System.out.println("Local variable: " + localVar);
                System.out.println("Instance variable: " + instanceVar);
            }
        }

        // Instantiating the inner class inside the method
        InnerClass inner = new InnerClass();
        inner.display();
    }

    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```

#### Example 3: Static Method Case

```java
public class OuterClass {
    private static int staticVar = 30;

    public static void outerStaticMethod() {
        final int localVar = 10; // Must be final or effectively final

        // Method local inner class
        class InnerClass {
            public void display() {
                System.out.println("Local variable: " + localVar);
                System.out.println("Static variable: " + staticVar);
            }
        }

        // Instantiating the inner class inside the static method
        InnerClass inner = new InnerClass();
        inner.display();
    }

    public static void main(String[] args) {
        OuterClass.outerStaticMethod();
    }
}
```

#### Example 4: Naming Conflicts

```java
public class OuterClass {
    private int var = 40;

    public void outerMethod() {
        final int var = 10; // Local variable with the same name

        // Method local inner class
        class InnerClass {
            public void display() {
                System.out.println("Local variable: " + var);
                System.out.println("Instance variable: " + OuterClass.this.var);
            }
        }

        // Instantiating the inner class inside the method
        InnerClass inner = new InnerClass();
        inner.display();
    }

    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```

### Additional Clarifications:

- **Scope and Access:**
  - The inner class can access the enclosing method's local variables if they are final or effectively final.
  - Using `Outer.this.var` in the case of non-static variables allows access to the instance variable from the outer class, preventing naming conflicts.
