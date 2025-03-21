## 1. Why we need to use OOP? Some major OOP languages?

OOP improves code reusability, maintainability, and scalability. It enables structured and secure coding through principles like encapsulation, inheritance, and polymorphism.
- **Major OOP Languages**: Java, C++, Python, C#

## 2. Interface vs Abstract Class?

- **Interface**:  
  - **Before Java 8**, it could only contain method signatures (no body).  
  - **Since Java 8**, it can include `default` and `static` methods with a body.  
  - Supports **multiple inheritance**, allowing a class to implement multiple interfaces.  
  - All variables are automatically **`public static final` (constants).**  

- **Abstract Class**:  
  - Can have both **abstract methods (without a body) and concrete methods (with a body).**  
  - Supports **single inheritance**, meaning a class can extend only one abstract class.  
  - Can have **constructors and define common behavior** for subclasses.
 
- **When to Use Which?**  
  - Use an **Interface** when you only need to define method signatures.  
  - Use an **Abstract Class** when you need to share common behavior among subclasses. 

## 3. Why we need equals and hashcode? When to override?

### equals:
- The `equals()` method is used to check if two objects are logically **equivalent** based on their **content** rather than their memory locations.
- It should be overridden when you want to define custom logic for comparing objects, especially when working with custom classes.

### hashCode:
- The `hashCode()` method generates a **numeric hash value** for an object based on its content.
- This method is crucial for efficient object retrieval in hash-based collections like `HashMap`, `HashSet`, and `Hashtable`.

### When to Override:
- **Override both `equals()` and `hashCode()`** when you're working with custom objects that will be used in collections like `HashMap` or `HashSet`.
- Always override `hashCode()` if you override `equals()`, as they must be consistent with each other for the correct behavior in collections.

## 4. Diamond problem in Java? How to fix it?
Occurs when a class inherits the same method from multiple classes, which can lead to ambiguity.

- **Example:** Imagine an abstract `Animal` class with a method `makeSound()`. If two subclasses (`Dog` and `Cat`) override `makeSound()` differently, and a third class tries to inherit both `Dog` and `Cat`, it wouldn't know which version of `makeSound()` to call, leading to a conflict.
- **Solution:** Java prevents this issue by **disallowing multiple inheritance** in classes. Instead, interfaces can be used to achieve a similar effect, as a class can implement multiple interfaces without encountering method conflicts.

## 5. Why do we need a Garbage Collector? How does it run?

The **Garbage Collector** is responsible for automatically managing memory in Java. It identifies and removes objects that are no longer needed, helping to prevent memory leaks and ensuring efficient memory usage.

- **Why do we need it?**  
  Without garbage collection, developers would need to manually manage memory, which can be error-prone and lead to memory leaks (unused memory that is not properly released). The Garbage Collector helps automate this process, ensuring that memory is freed when objects are no longer in use.

- **How does it run?**  
  The Garbage Collector runs in the background as part of the Java Virtual Machine (JVM). It performs periodic checks to identify objects that are no longer reachable or referenced by the application and marks them for removal.  
  While the GC can be manually triggered using `System.gc()`, its actual execution is not guaranteed and depends on the JVM’s decision on when it is appropriate to run the garbage collection.

## 6. Java `static` Keyword Usage ?

The `static` keyword in Java is used to indicate that a member (variable, method, or block) belongs to the class itself, rather than to instances of the class. Here's how it is used:

- **Variable**: A static variable is shared among all instances of a class. It is **common** to all objects, and any changes made to it will be reflected across all instances.
  - **Example**: `static int count;`  
  This means `count` will be shared by all instances of the class.

- **Method**: A static method can be called **without creating an instance** of the class. It can only access static members (variables and methods) of the class and cannot refer to instance-specific data.
  - **Example**: `public static void printCount() { System.out.println(count); }`

- **Block**: A static block is executed when the class is **loaded** into memory. It is often used for class-level initialization that needs to occur only once.
  - **Example**:  
    ```java
    static {
        System.out.println("Class loaded!");
    }
    ```

In short, the `static` keyword allows for class-level members and initialization, improving memory management and offering behavior that is shared across all instances of the class.

## 7. Immutability means? Where, How and Why to use it?

**Immutability** means that once an object is created, its state cannot be modified. Any attempt to change the object's fields will result in a new object being created.

- **Where to use?**  
  - **Thread safety**: Immutable objects are naturally thread-safe because they cannot be altered once created.
  - When the object should not change during its lifetime, ensuring consistency and predictability.

- **How to use?**  
  - Make the class `final` to prevent subclassing.
  - Mark fields as `final` so they cannot be reassigned.
  - Do not provide setter methods to alter the fields.
  - If the class contains references to other objects, ensure those objects are also immutable or make defensive copies.

- **Why to use?**  
  - Immutable objects are easier to reason about, as their state is constant throughout their lifetime.
  - They help prevent issues in multi-threaded environments by eliminating the risk of shared mutable state.
  - They improve security and consistency by ensuring that objects can't be inadvertently changed after creation.

## 8. Composition and Aggregation means and differences?

- **Composition**: Represents a **strong "Has-A"** relationship where the child object **cannot exist independently** of the parent. If the parent object is deleted, the child objects are also deleted.  
  - **Example**: A `Car` **has-a** `Engine`. If the `Car` is destroyed, the `Engine` is also destroyed.

- **Aggregation**: Represents a **weaker "Has-A"** relationship where the child object **can exist independently** of the parent. The child can continue to exist even if the parent is destroyed.  
  - **Example**: A `University` **has-a** `Student`. A `Student` can exist without the `University` (after graduation).

- **Differences**:
  - **Lifecycle dependency**: In **Composition**, the child object depends on the parent for its existence. In **Aggregation**, the child object can exist independently of the parent.
  - **Example of Composition**: A `House` **has-a** `Room`. The room cannot exist without the house.
  - **Example of Aggregation**: A `Library` **has-a** `Book`. The book can exist without the library.

## 9. Cohesion and Coupling means and differences?

- **Cohesion**: Refers to how closely related the methods and responsibilities are within a single class. **High cohesion** means that the class has a well-defined responsibility and its methods are strongly related to that responsibility.  
  - **Good Example**: A `UserManager` class that only manages user-related tasks (authentication, registration).

- **Coupling**: Refers to the degree of dependency between classes. **Low coupling** is preferred, meaning classes should have minimal knowledge of and dependencies on each other.  
  - **Good Example**: A `Customer` class that doesn’t depend heavily on a `Order` class but communicates through interfaces or methods.

- **Differences**:
  - **Cohesion** focuses on how well a class's methods are related to its purpose.
  - **Coupling** focuses on how much a class depends on other classes.

## 10. Heap and Stack means and differences?

- **Stack**: 
  - Stores local variables and method calls. It's a region of memory where function calls and local variables are pushed and popped in a **Last In, First Out (LIFO)** order. 
  - **Scope**: Memory is automatically allocated and deallocated as functions are called and return.
  - **Size**: Generally, stack memory is limited in size, making it faster but smaller.

- **Heap**:
  - Stores objects and dynamic memory allocations made during runtime. Memory in the heap is managed by the **Garbage Collector**.
  - **Scope**: Objects in the heap remain in memory until they are no longer referenced and are garbage collected.
  - **Size**: Heap memory is generally much larger than the stack but slower in access.

- **Differences**:
  - **Memory Management**: Stack memory is automatically managed, while heap memory is manually managed by the Garbage Collector.
  - **Storage**: Stack is for method calls and local variables, while heap is for objects created dynamically.
  - **Access Speed**: Stack access is faster than heap access due to its organized, last-in-first-out nature.
  - **Lifetime**: Stack variables live only within the scope of a method, while heap objects live until they are no longer referenced.

## 11. Exception means? Type of Exceptions?

- **Exceptions** are unexpected errors that occur during the execution of a program, causing it to behave abnormally.

- **Checked Exceptions**: 
  - These exceptions **must** be handled at compile time, either through a `try-catch` block or by declaring the exception with the `throws` keyword.
  - **Example**: `IOException`, `SQLException`. These are typically recoverable errors that the programmer is expected to handle.

- **Unchecked Exceptions**: 
  - These exceptions occur during runtime and are **not required to be handled** at compile time.
  - **Example**: `NullPointerException`, `ArrayIndexOutOfBoundsException`. These typically represent programming errors.

## 12. How to summarize ‘clean code’ as short as possible?

**Simple, readable, maintainable, reusable.**

## 13. What is the method of hiding in Java?

- **Method Hiding** occurs when a **child class** defines a `static` method with the same signature as a `static` method in the parent class.
- The parent class’s method is hidden, not overridden.
- **Static methods** are resolved at compile time based on the reference type, not the object type.

## 14. What is the difference between abstraction and polymorphism in Java?

- **Abstraction**: Hides the implementation details and shows only the essential features of an object. It allows you to focus on what an object does rather than how it does it.
  *Example*: A `Car` class may expose methods like `start()` and `stop()`, but hides the internal details of how the engine works.

- **Polymorphism**: Allows one method to behave differently based on the object calling it. This can happen through method overriding (runtime polymorphism) or method overloading (compile-time polymorphism).
  *Example*: Both `Dog` and `Cat` can have a `makeSound()` method, but each will produce a different sound (`Dog` barks, `Cat` meows).
