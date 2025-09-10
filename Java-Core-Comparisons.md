# 📘 Java Core Concepts & Comparisons Cheat Sheet

This document contains **all important Core Java comparisons** — a one-stop resource for **interview prep & quick revision**.

---

## 🔹 OOPs Core Concepts

| Feature               | Encapsulation                     | Abstraction                        | Inheritance                                         | Polymorphism                                     |
| --------------------- | --------------------------------- | ---------------------------------- | --------------------------------------------------- | ------------------------------------------------ |
| **Focus**             | Hides **data** (variables)        | Hides **implementation** (methods) | Reuse code by deriving new class from existing      | Same method/behavior but in **different forms**  |
| **Achieved by**       | Access modifiers, getters/setters | Abstract classes & Interfaces      | `extends` (class) / `implements` (interface)        | Method Overloading & Method Overriding           |
| **Purpose**           | Data hiding & protection          | Show only essential features       | Promote reusability and hierarchical relationships  | Flexibility & dynamic behavior at runtime        |
| **Access**            | Restricts direct access to fields | Restricts knowledge of "how"       | Child class inherits parent's fields & methods      | One interface, many implementations              |
| **Code Impact**       | Secure and controlled access      | Defines contracts (what to do)     | Reduces redundancy, improves maintainability        | Increases extensibility, promotes loose coupling |
| **Real-life analogy** | Capsule hides medicine            | Car hides engine complexity        | Child inherits traits from parent (e.g., eye color) | A person acts as **student, employee, customer** |
| **Type**              | Implementation detail             | Design/Blueprint detail            | Structural relationship                             | Behavioral relationship                          |

---

## 🔹 Abstract Class vs Interface

| Feature                  | Abstract Class                                                                       | Interface                                                                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Purpose**              | Provides a **partial abstraction** → can have both abstract and concrete methods     | Provides a **full abstraction contract**                                                                                               |
| **Keywords**             | Declared using `abstract` keyword                                                    | Declared using `interface` keyword                                                                                                     |
| **Method Types**         | Abstract + Concrete + Static + Final                                                 | Java 7 → Abstract only <br> Java 8 → Default + Static <br> Java 9 → Private methods also                                                |
| **Variables**            | Instance variables allowed                                                           | Only `public static final` (constants)                                                                                                |
| **Access Modifiers**     | `public`, `protected`, `private`                                                     | Always `public`                                                                                                                       |
| **Multiple Inheritance** | Only **one** abstract class                                                          | Multiple interfaces supported                                                                                                         |
| **Constructor**          | Allowed                                                                              | Not allowed                                                                                                                           |
| **When to use**          | Common code + enforce contracts                                                      | 100% abstraction or multiple inheritance                                                                                              |
| **Analogy**              | *Vehicle* class with partial implementation                                          | *Drivable*, *Flyable* → pure contracts                                                                                                |

---

## 🔹 Access Modifiers

| Modifier                 | Same Class | Same Package | Subclass (Diff Package) | Other Package | Example Usage                                     |
| ------------------------ | ---------- | ------------ | ----------------------- | ------------- | ------------------------------------------------ |
| **public**               | ✅         | ✅           | ✅                      | ✅            | APIs, utilities                                   |
| **protected**            | ✅         | ✅           | ✅                      | ❌            | Subclass access                                   |
| **default (no keyword)** | ✅         | ✅           | ❌                      | ❌            | Package-private utilities                         |
| **private**              | ✅         | ❌           | ❌                      | ❌            | Encapsulation (sensitive data, helper methods)    |

---

## 🔹 throw vs throws vs Exception vs Error

| Feature        | `throw`                               | `throws`                                | Checked Exception                   | Error                                |
| -------------- | ------------------------------------- | --------------------------------------- | ----------------------------------- | ------------------------------------ |
| **Type**       | Keyword                               | Keyword                                 | Class (recoverable issue)           | Class (serious JVM issue)            |
| **Usage**      | Explicitly throw exception            | Declare exception in method signature   | Must be caught/declared             | Not recommended to catch             |
| **Checked?**   | Can throw checked/unchecked           | Declares only checked                   | Compile-time check                  | Runtime only                         |
| **Example**    | `throw new IOException();`            | `void read() throws IOException {}`     | `IOException`, `SQLException`       | `OutOfMemoryError`, `StackOverflow`  |

---

## 🔹 final vs finally vs finalize

| Feature       | `final`                                                | `finally`                                  | `finalize`                                    |
| ------------- | ------------------------------------------------------ | ------------------------------------------ | --------------------------------------------- |
| **Type**      | Keyword                                                | Block                                      | Method (`protected void finalize()`)          |
| **Usage**     | Const variables, prevent inheritance, prevent override | Cleanup code after try-catch                | Called by GC before object destruction        |
| **Execution** | Compile-time restriction                               | Always executes (except `System.exit(0)`)   | Not guaranteed (GC dependent, deprecated)     |
| **Example**   | `final int x=10;` <br> `final class A{}`               | `try{} finally{}`                          | `@Override protected void finalize(){}`       |

---

## 🔹 == vs equals()

| Feature     | `==` (operator)                     | `.equals()` (method)                     |
| ----------- | ----------------------------------- | ---------------------------------------- |
| **Checks**  | Reference (memory address)          | Value/content equality (can override)    |
| **Default** | Works for primitives & references   | From `Object` → same as `==` unless overridden |
| **Example** | `s1 == s2` → false (different refs) | `s1.equals(s2)` → true (same content)    |

---

## 🔹 String vs StringBuilder vs StringBuffer

| Feature           | `String`             | `StringBuilder`        | `StringBuffer`             |
| ----------------- | ------------------- | ---------------------- | --------------------------- |
| **Mutability**    | Immutable            | Mutable                | Mutable                     |
| **Thread Safety** | Immutable = safe     | Not thread-safe        | Thread-safe (synchronized)  |
| **Performance**   | Slower for changes   | Fastest for single-thread | Slower than Builder         |

---

## 🔹 Checked vs Unchecked Exception

| Feature        | Checked Exception              | Unchecked Exception                |
| -------------- | ------------------------------ | ---------------------------------- |
| **Type**       | Compile-time                   | Runtime                            |
| **Examples**   | `IOException`, `SQLException`  | `NullPointerException`, `ArithmeticException` |
| **Handling**   | Must declare/handle            | No declaration needed              |

---

## 🔹 Overloading vs Overriding

| Feature        | Overloading (Compile-time)         | Overriding (Runtime)             |
| -------------- | --------------------------------- | -------------------------------- |
| **Params**     | Must differ (type/number/order)    | Must be same                     |
| **Return type**| Can differ (covariant allowed)     | Must be same or covariant        |
| **Polymorphism**| Compile-time                     | Runtime                          |

---

## 🔹 Comparable vs Comparator

| Feature        | Comparable                     | Comparator                        |
| -------------- | ------------------------------ | --------------------------------- |
| **Package**    | `java.lang`                   | `java.util`                       |
| **Method**     | `compareTo(Object o)`         | `compare(Object o1, Object o2)`   |
| **Sorting**    | Natural ordering              | Custom ordering                   |

---

## 🔹 this vs super

| Feature        | `this`                         | `super`                          |
| -------------- | ------------------------------ | -------------------------------- |
| **Refers to**  | Current object                 | Parent class object              |
| **Usage**      | Call current fields/methods    | Call parent fields/methods/ctor  |

---

## 🔹 Heap vs Stack Memory

| Feature        | Stack Memory                    | Heap Memory                      |
| -------------- | ------------------------------- | -------------------------------- |
| **Stores**     | Method calls, local vars        | Objects, instance vars           |
| **Access**     | LIFO, very fast                 | Slower, managed by GC            |
| **Life**       | Until method ends               | Until GC collects                |

---

## 🔹 String Pool vs Heap String

| Feature        | String Pool (interned)          | Heap String                      |
| -------------- | ------------------------------- | -------------------------------- |
| **Creation**   | `"abc"`                         | `new String("abc")`              |
| **Memory**     | Shared in SCP                   | New object in Heap                |
| **Equality**   | Same ref for same value         | Always new reference              |

---

## 🔹 Process vs Thread

| Feature        | Process                         | Thread                           |
| -------------- | ------------------------------- | -------------------------------- |
| **Definition** | Independent program in execution| Lightweight unit inside process   |
| **Memory**     | Own memory space                | Shared memory with process        |
| **Switching**  | Expensive (context switch)      | Cheaper switching                 |

---

## 🔹 Synchronized Method vs Synchronized Block

| Feature        | Synchronized Method             | Synchronized Block               |
| -------------- | ------------------------------- | -------------------------------- |
| **Scope**      | Locks entire method             | Locks only specific block/object |
| **Performance**| Less efficient                  | More efficient                   |
| **Granularity**| Coarse-grained                  | Fine-grained                     |

---

## 🔹 Enumeration vs Iterator vs ListIterator

| Feature        | Enumeration (Legacy)            | Iterator                         | ListIterator                     |
| -------------- | ------------------------------- | -------------------------------- | -------------------------------- |
| **Direction**  | Forward only                    | Forward only                     | Forward + Backward               |
| **Modification**| Cannot remove                  | Can remove                       | Can add/remove/update            |
| **Use-case**   | Legacy collections              | All collections                  | Lists only                       |

---

## 🔹 WeakReference vs SoftReference vs StrongReference

| Feature        | Strong Reference                 | Soft Reference                   | Weak Reference                   |
| -------------- | -------------------------------- | -------------------------------- | -------------------------------- |
| **GC Behavior**| Never collected until unreachable| Collected if memory needed       | Collected at next GC cycle       |
| **Use-case**   | Normal objects                   | Caching                          | WeakHashMap, listeners           |

---
