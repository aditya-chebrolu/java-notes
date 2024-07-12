# Method Local Inner Class (Important Points)

- The inner class is declared **inside a method**.
- You can instantiate the class only **inside the method** in which the class is present.
- Can access members outside of the inner class (i.e., of the method and outer class).

## Points to Remember

- **Local variables of the method:** The local inner class can access local variables of the method if they are marked as `final` or are effectively final.
- **Instantiation:** The class can only be instantiated within the method it is defined in.
- **Non-static:** The inner class cannot be static.
- **Accessing variables:** If the method has local variables with the same name as the instance variables of the outer class, the local variables will shadow the instance variables of the outer class.

### Example Explanation

1. **Local variable access:**
   - Local variables of the method can be accessed by the inner class.
   - Example diagram shows local variables and instantiation of the inner class within the method.

2. **Static Method Case:**
   - In case the method is static, the inner class can only access static members of the outer class.
   - The inner class in a static method is effectively static.

3. **Naming conflicts:**
   - If a local variable of the method has the same name as an instance variable of the outer class, use `Outer.this.var` to access the instance variable.
   - Directly using the variable name will refer to the local variable.

### Additional Clarifications:

- **Scope and Access:**
  - The inner class can access the enclosing method's local variables if they are final or effectively final.
  - Using `Outer.this.var` in the case of non-static variables allows access to the instance variable from the outer class, preventing naming conflicts.

These points should help clarify the usage and constraints of method local inner classes in Java.
